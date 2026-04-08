# Архитектура системы

## Общая архитектура

```mermaid
flowchart TB
    subgraph client["Устройство пользователя"]
        SKILL["🔧 /friends скилл<br/>(TypeScript, MCP)"]
        FILES["📁 Markdown, чаты,<br/>закладки, заметки"]
        NLP["🧠 NLP Pipeline<br/>(TF-IDF extraction)"]
        BLOOM["🔐 Bloom Filter<br/>Encoder (1024 бит)"]
        KEY["🔑 Ed25519 Keypair<br/>(~/.friends/)"]
    end

    subgraph server["Matching Server (Contabo VPS 30)"]
        API["⚡ FastAPI<br/>(Python, async)"]
        DB["💾 SQLite → PostgreSQL"]
        ENGINE["🎯 Matching Engine<br/>(Jaccard similarity)"]
    end

    subgraph viz["Визуализация"]
        GRAPH["📊 D3.js<br/>Force-directed граф"]
        TG["💬 Telegram<br/>Connect"]
    end

    FILES --> SKILL
    SKILL --> NLP
    NLP --> BLOOM
    BLOOM --> KEY
    KEY -->|"signed bloom filter<br/>(128 байт)"| API
    API --> DB
    API --> ENGINE
    ENGINE --> API
    API -->|"Top-K матчи"| GRAPH
    GRAPH --> TG

    style client fill:#0a0d14,color:#e8eaf0,stroke:#00D4FF
    style server fill:#0a0d14,color:#e8eaf0,stroke:#c5380e
    style viz fill:#0a0d14,color:#e8eaf0,stroke:#e6a817
```

## Что где хранится

```mermaid
pie title Распределение данных
    "На устройстве (файлы, ключи, теги)" : 95
    "На сервере (Bloom filter, имя, TG)" : 5
```

## Технологический стек

| Компонент | Технология | Фаза |
|-----------|-----------|------|
| Скилл | TypeScript + MCP | MVP |
| NLP | TF-IDF (MVP), Ollama + Llama 3 (Phase 2) | MVP |
| Encoding | Bloom filter 1024 бит, MurmurHash3 x 5 | MVP |
| Identity | Ed25519 (tweetnacl-js) | MVP |
| Сервер | FastAPI (Python) | MVP |
| БД | SQLite → PostgreSQL | MVP → Phase 2 |
| Визуализация | D3.js v7 force-directed | MVP |
| Лендинг | Static HTML на GitHub Pages | MVP |
| Блокчейн | Solana или Base (L2) | Phase 4 |

## Deployment

```mermaid
flowchart LR
    GH[GitHub<br/>Source of Truth] -->|push| GHA[GitHub Actions<br/>CI/CD]
    GHA -->|deploy landing| GP[GitHub Pages<br/>timzinin.com/friends]
    GHA -->|deploy server| CB[Contabo VPS 30<br/>Docker Compose]
    CB --> FAST[FastAPI :8000]
    CB --> SQL[SQLite/Postgres]
```
