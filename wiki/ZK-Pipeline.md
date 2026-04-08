# ZK Pipeline — Обработка данных

## Полный pipeline от файлов до матча

```mermaid
sequenceDiagram
    participant U as Пользователь
    participant S as /friends скилл
    participant N as NLP Pipeline
    participant B as Bloom Encoder
    participant K as Ed25519 Key
    participant API as Matching Server
    participant G as Граф (браузер)

    U->>S: Запускает /friends
    S->>S: Сканирует ~/docs/**/*.md
    S->>S: Парсит Telegram export (JSON)
    S->>S: Парсит Discord export
    S->>N: Объединённый текст
    N->>N: Токенизация + стоп-слова
    N->>N: TF-IDF scoring
    N->>N: Top-50 тегов тем
    N->>B: ["distributed systems", "Rust", ...]
    B->>B: MurmurHash3 x 5 seeds
    B->>B: 1024-bit array
    B->>K: Bloom filter (128 байт)
    K->>K: Ed25519 подпись
    K->>API: POST register {bloom, pubkey, sig, name, tg}
    API->>API: Верификация подписи
    API->>API: Сохранение Bloom filter
    API-->>K: 201 Created

    U->>S: Запрашивает матчи
    S->>K: Подписать запрос
    K->>API: POST match {pubkey, sig}
    API->>API: Jaccard similarity vs ALL Bloom filters
    API->>API: Sort by score, Top-20
    API-->>G: [{name, tg, score}, ...]
    G->>U: Интерактивный граф
    U->>U: Кликает узел → видит профиль
    U->>U: Связывается в Telegram
```

## Источники данных и парсинг

```mermaid
flowchart TD
    subgraph sources["Источники (всё на устройстве)"]
        MD["*.md файлы"]
        CL["Claude sessions (.jsonl)"]
        TG["Telegram export (JSON)"]
        DC["Discord export (JSON)"]
        SL["Slack export (JSON)"]
        BK["Браузер закладки (HTML)"]
        NT["Notion export (MD)"]
        TXT["Произвольный текст"]
    end

    subgraph parse["Unified Parser"]
        P["→ plain text"]
    end

    subgraph nlp["NLP (на устройстве)"]
        TOK["Токенизация"]
        STOP["Удаление стоп-слов (EN+RU)"]
        TFIDF["TF-IDF scoring"]
        TOP["Top-50 тегов"]
    end

    subgraph encode["Encoding (на устройстве)"]
        BF["Bloom filter<br/>1024 бит, MurmurHash3 x 5"]
        SIG["Ed25519 подпись"]
    end

    MD --> P
    CL --> P
    TG --> P
    DC --> P
    SL --> P
    BK --> P
    NT --> P
    TXT --> P
    P --> TOK
    TOK --> STOP
    STOP --> TFIDF
    TFIDF --> TOP
    TOP --> BF
    BF --> SIG

    style sources fill:#1a1d24,color:#e8eaf0
    style parse fill:#00D4FF,color:#000
    style nlp fill:#e6a817,color:#000
    style encode fill:#c5380e,color:#fff
```

## Bloom Filter: визуализация

```
Тег "distributed systems" → hash(seed=0) = 142, hash(seed=1) = 587, ...

Bit array (1024 бит):
[0 0 0 ... 1 ... 0 0 0 ... 1 ... 0 0 0 ...]
              ↑ bit 142        ↑ bit 587

50 тегов × 5 hash функций = ~250 бит установлены из 1024
False positive rate: ~3.5%
```

## Эволюция приватности

```mermaid
stateDiagram-v2
    [*] --> BloomFilter: MVP
    BloomFilter --> PSI: Phase 2 (>1K users)
    PSI --> FHE: Phase 3 (>10K users)
    FHE --> ZKProofs: Phase 4 (blockchain)
    ZKProofs --> [*]

    BloomFilter: Bloom Filter + Ed25519
    BloomFilter: Practical privacy
    BloomFilter: 0 overhead

    PSI: Private Set Intersection
    PSI: Cryptographic privacy
    PSI: ~100ms overhead

    FHE: Homomorphic Encryption
    FHE: Full privacy
    FHE: 100-1000x overhead

    ZKProofs: ZK-SNARKs on-chain
    ZKProofs: Verifiable privacy
    ZKProofs: ~1s proof generation
```
