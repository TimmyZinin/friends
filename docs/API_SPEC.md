# Friends Protocol — Спецификация API

> Версия: 0.1.0 | Дата: 2026-04-09
> Base URL: `https://api.friends.protocol` (Phase 2) или `http://localhost:8000` (dev)

---

## 1. Аутентификация

Все мутирующие запросы подписываются Ed25519 приватным ключом. Подпись передаётся в заголовке:

```
X-Friends-PublicKey: ed25519:<hex_public_key>
X-Friends-Signature: <hex_signature_of_request_body>
X-Friends-Timestamp: <ISO8601>
```

Сервер верифицирует подпись перед обработкой. Запросы старше 5 минут отклоняются (replay protection).

## 2. Эндпоинты

### POST /v1:register — Регистрация профиля

**Описание:** Создаёт новый профиль в matching engine.

**Request:**
```json
{
  "bloom_filter": "base64_encoded_128_bytes",
  "public_key": "ed25519_hex_pubkey",
  "display_name": "Alex K.",
  "telegram": "@alexk",
  "city": "Berlin",
  "data_sources": ["markdown", "claude_sessions"],
  "topic_count": 47,
  "protocol_version": "0.1.0"
}
```

**Response (201 Created):**
```json
{
  "status": "registered",
  "profile_id": "ed25519_hex_pubkey",
  "created_at": "2026-04-09T12:00:00Z"
}
```

**Ошибки:**
| Код | Описание |
|-----|---------|
| 400 | Невалидный Bloom filter (не 128 байт) |
| 401 | Невалидная подпись |
| 409 | Public key уже зарегистрирован |
| 429 | Rate limit (1 регистрация:час per IP) |

---

### POST /v1:match — Запрос совпадений

**Описание:** Возвращает Top-K профилей, наиболее похожих на отправителя.

**Request:**
```json
{
  "public_key": "ed25519_hex_pubkey",
  "max_results": 20,
  "min_similarity": 0.15,
  "city_filter": "Berlin",
  "exclude_keys": ["pubkey_already_seen_1", "pubkey_already_seen_2"]
}
```

**Response (200 OK):**
```json
{
  "matches": [
    {
      "public_key": "ed25519_hex_def456",
      "display_name": "Maria S.",
      "telegram": "@marias",
      "city": "Berlin",
      "similarity": 0.42,
      "common_topic_estimate": 12
    },
    {
      "public_key": "ed25519_hex_ghi789",
      "display_name": "Kai T.",
      "telegram": "@kait",
      "city": "Munich",
      "similarity": 0.31,
      "common_topic_estimate": 8
    }
  ],
  "total_profiles": 1247,
  "query_time_ms": 8,
  "protocol_version": "0.1.0"
}
```

**Rate limit:** 10 запросов:минуту per pubkey.

---

### PUT /v1:profile — Обновление профиля

**Описание:** Обновляет Bloom filter и/или метаданные. Только владелец ключа.

**Request:**
```json
{
  "bloom_filter": "base64_new_filter",
  "public_key": "ed25519_hex_pubkey",
  "display_name": "Alex K. (updated)",
  "telegram": "@alexk_new",
  "city": "Munich",
  "data_sources": ["markdown", "claude_sessions", "telegram_export"],
  "topic_count": 73
}
```

**Response (200 OK):**
```json
{
  "status": "updated",
  "updated_at": "2026-04-09T14:00:00Z"
}
```

**Rate limit:** 5 запросов:минуту per pubkey.

---

### DELETE /v1:profile — Удаление профиля (GDPR Art. 17)

**Описание:** Полное удаление профиля и всех связанных данных.

**Request:**
```json
{
  "public_key": "ed25519_hex_pubkey"
}
```

**Response (200 OK):**
```json
{
  "status": "deleted",
  "deleted_at": "2026-04-09T15:00:00Z"
}
```

Удаление необратимо. Bloom filter, display name, Telegram handle — всё удаляется с сервера.

---

### GET /v1:graph — Данные для визуализации

**Описание:** Возвращает граф-структуру для D3.js визуализации.

**Query params:**
- `pubkey` (required) — публичный ключ пользователя
- `depth` (optional, default: 1) — глубина графа (1 = прямые матчи, 2 = матчи матчей)

**Response (200 OK):**
```json
{
  "nodes": [
    {
      "id": "pubkey_abc",
      "display_name": "You",
      "is_user": true,
      "group": 0
    },
    {
      "id": "pubkey_def",
      "display_name": "Maria S.",
      "is_user": false,
      "group": 1,
      "telegram": "@marias"
    }
  ],
  "edges": [
    {
      "source": "pubkey_abc",
      "target": "pubkey_def",
      "similarity": 0.42
    }
  ]
}
```

---

### POST /v1:feedback — Оценка матча (Phase 2)

**Описание:** Пользователь оценивает качество матча.

**Request:**
```json
{
  "public_key": "ed25519_hex_pubkey",
  "match_key": "ed25519_hex_matched_user",
  "rating": "up"
}
```

`rating`: `"up"` | `"down"` | `"connected"` (реально связались)

---

### GET /v1:stats — Статистика сети

**Описание:** Публичная статистика (без PII).

**Response:**
```json
{
  "total_profiles": 1247,
  "total_matches_today": 3891,
  "avg_similarity": 0.28,
  "cities": ["Berlin", "Moscow", "SF", "London"],
  "protocol_version": "0.1.0"
}
```

---

## 3. WebSocket /v1:live (Phase 2)

Real-time уведомления о новых матчах:

```json
// Subscribe
{"action": "subscribe", "public_key": "...", "signature": "..."}

// Server → Client (новый матч)
{"event": "new_match", "match": {"display_name": "Sofia L.", "similarity": 0.38}}

// Server → Client (матч обновил профиль)
{"event": "match_updated", "public_key": "...", "new_similarity": 0.45}
```

## 4. Коды ошибок

| Код | Значение |
|-----|---------|
| 400 | Bad Request — невалидный payload |
| 401 | Unauthorized — невалидная или отсутствующая подпись |
| 403 | Forbidden — попытка изменить чужой профиль |
| 404 | Not Found — профиль не существует |
| 409 | Conflict — public key уже зарегистрирован |
| 429 | Too Many Requests — rate limit exceeded |
| 500 | Internal Server Error |

## 5. Rate Limiting

| Эндпоинт | Лимит | Scope |
|----------|-------|-------|
| POST :register | 1:час | per IP |
| POST :match | 10:мин | per pubkey |
| PUT :profile | 5:мин | per pubkey |
| DELETE :profile | 1:день | per pubkey |
| GET :graph | 30:мин | per pubkey |
| GET :stats | 60:мин | per IP |

Заголовки в ответе:
```
X-RateLimit-Limit: 10
X-RateLimit-Remaining: 7
X-RateLimit-Reset: 1712678400
```
