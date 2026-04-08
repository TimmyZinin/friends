# API Reference

## Endpoints

```mermaid
flowchart LR
    subgraph api["REST API v1"]
        R["POST /v1 register"]
        M["POST /v1 match"]
        U["PUT /v1 profile"]
        D["DELETE /v1 profile"]
        G["GET /v1 graph"]
        F["POST /v1 feedback"]
        S["GET /v1 stats"]
    end

    CLIENT["Клиент<br/>(скилл)"] --> R
    CLIENT --> M
    CLIENT --> U
    CLIENT --> D
    CLIENT --> G
    CLIENT --> F
    CLIENT --> S

    style api fill:#0a0d14,color:#e8eaf0,stroke:#00D4FF
```

## Обзор

| Метод | Эндпоинт | Описание | Auth | Rate Limit |
|-------|----------|---------|------|-----------|
| POST | /v1 register | Регистрация профиля | Ed25519 sig | 1 per hour per IP |
| POST | /v1 match | Запрос матчей | Ed25519 sig | 10 per min per pubkey |
| PUT | /v1 profile | Обновление профиля | Ed25519 sig | 5 per min per pubkey |
| DELETE | /v1 profile | Удаление (GDPR) | Ed25519 sig | 1 per day per pubkey |
| GET | /v1 graph | Граф для визуализации | pubkey param | 30 per min per pubkey |
| POST | /v1 feedback | Оценка матча (Phase 2) | Ed25519 sig | 20 per min |
| GET | /v1 stats | Публичная статистика | нет | 60 per min per IP |

## Аутентификация

```mermaid
sequenceDiagram
    participant C as Клиент
    participant S as Сервер

    C->>C: Создаёт JSON payload
    C->>C: Подписывает Ed25519(payload)
    C->>S: POST {payload, pubkey, signature, timestamp}
    S->>S: Проверяет timestamp (<5 мин)
    S->>S: Verify(pubkey, payload, signature)
    alt Подпись валидна
        S-->>C: 200 OK + результат
    else Подпись невалидна
        S-->>C: 401 Unauthorized
    end
```

## Полная спецификация

Детальные схемы запросов и ответов — в [docs/API_SPEC.md](../blob/main/docs/API_SPEC.md)
