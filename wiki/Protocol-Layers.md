# Слои протокола

## Friends Protocol Stack

```mermaid
graph TB
    subgraph stack["Friends Protocol"]
        L5["<b>Presentation</b><br/>D3.js граф | Мобильное приложение | TG бот"]
        L4["<b>Matching</b><br/>Jaccard similarity | Top-K | Feedback loop"]
        L3["<b>Encoding</b><br/>Bloom filter (MVP) → PSI → FHE → ZK-proofs"]
        L2["<b>Identity</b><br/>Ed25519 keypair | Подпись | Consent"]
        L1["<b>Transport</b><br/>REST API (MVP) | WebSocket | Blockchain RPC"]
    end

    L5 --> L4
    L4 --> L3
    L3 --> L2
    L2 --> L1

    style L5 fill:#00D4FF,color:#000
    style L4 fill:#e6a817,color:#000
    style L3 fill:#c5380e,color:#fff
    style L2 fill:#6b5ce7,color:#fff
    style L1 fill:#333,color:#fff
```

## Детализация каждого слоя

### L1: Transport
Отвечает за передачу данных между клиентом и сервером.

| Фаза | Транспорт | Описание |
|------|-----------|---------|
| MVP | REST API (HTTPS) | Простой, проверенный |
| Phase 2 | + WebSocket | Real-time уведомления |
| Phase 4 | + Blockchain RPC | On-chain операции |

### L2: Identity
Управляет идентичностью пользователя.

```mermaid
sequenceDiagram
    participant Client
    participant KeyStore as ~/.friends/keypair.json

    Note over Client: Первый запуск
    Client->>KeyStore: Генерация Ed25519 keypair
    KeyStore-->>Client: {publicKey, privateKey}

    Note over Client: Каждый запрос
    Client->>Client: Создаёт payload
    Client->>KeyStore: Подписать payload
    KeyStore-->>Client: signature
    Client->>Client: Отправляет {payload, pubkey, sig}
```

### L3: Encoding
Преобразует данные пользователя в privacy-preserving представление.

| Подход | Фаза | Что передаётся | Обратимость |
|--------|------|----------------|-------------|
| Bloom filter | MVP | 128 байт bit array | Нет (heuristic) |
| PSI | Phase 2 | Зашифрованные множества | Нет (crypto) |
| FHE | Phase 3 | Fully encrypted data | Нет (math) |
| ZK-proofs | Phase 4 | Zero-knowledge proof | Нет (proven) |

### L4: Matching
Вычисляет сходство между профилями.

```mermaid
flowchart LR
    IN["Bloom filter<br/>пользователя"] --> SCAN["Сравнить с N<br/>Bloom filters"]
    SCAN --> JACCARD["Jaccard<br/>similarity"]
    JACCARD --> FILTER["Score > 0.15"]
    FILTER --> SORT["Сортировка<br/>по score"]
    SORT --> TOP["Top-20"]
    TOP --> OUT["Результат"]
```

### L5: Presentation
Визуализация результатов.

- **MVP:** D3.js force-directed граф в браузере
- **Phase 2:** + push-уведомления о новых матчах
- **Phase 3:** + мобильное приложение (React Native)
- **Phase 4:** + Telegram бот для быстрого доступа

## Extensibility

```mermaid
flowchart TD
    subgraph core["Friends Protocol Core"]
        PROTO["Protocol Spec v0.1"]
    end

    subgraph plugins["Data Source Plugins"]
        P1["Markdown Plugin"]
        P2["Telegram Plugin"]
        P3["Discord Plugin"]
        P4["Notion Plugin"]
        P5["Custom Plugin X<br/>(third-party)"]
    end

    subgraph clients["Клиенты (third-party)"]
        C1["Claude Code скилл"]
        C2["Cursor Extension"]
        C3["Mobile App"]
        C4["Telegram Bot"]
        C5["Web App"]
    end

    plugins --> core
    core --> clients
```

Любой разработчик может создать:
1. **Data Source Plugin** — новый источник данных (реализует интерфейс `FriendsDataPlugin`)
2. **Client** — новый клиент поверх Friends Protocol (использует REST API)
3. **Matching Node** — свой node для децентрализованного матчинга (Phase 4)
