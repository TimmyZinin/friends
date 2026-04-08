# Фазы децентрализации

## State Diagram

```mermaid
stateDiagram-v2
    [*] --> Phase1

    Phase1: Phase 1 — Centralized MVP
    Phase1: FastAPI + SQLite на Contabo
    Phase1: <1K users
    Phase1: Gate: 20+ installs, 3+ positive reviews

    Phase2: Phase 2 — Hybrid Alpha  
    Phase2: Postgres + API, feedback loop
    Phase2: 1K-10K users
    Phase2: Gate: 500+ users, первый revenue

    Phase3: Phase 3 — Protocol
    Phase3: Open-source spec, PSI privacy
    Phase3: 10K-50K users
    Phase3: Gate: 5K+ users, $5K MRR, legal review

    Phase4: Phase 4 — Decentralized
    Phase4: Smart contracts, token, DAO
    Phase4: 50K+ users

    Phase1 --> Phase2: Gates пройдены
    Phase2 --> Phase3: Gates пройдены
    Phase3 --> Phase4: Gates пройдены + юр. ревью
```

## Что когда переходит на блокчейн

```mermaid
flowchart TB
    subgraph phase1["Phase 1: Всё centralized"]
        C1_ID["Identity: Ed25519 (local)"]
        C1_BF["Bloom filters: SQLite"]
        C1_MATCH["Matching: FastAPI"]
    end

    subgraph phase2["Phase 2: Hybrid"]
        C2_ID["Identity: Ed25519 + optional TG verify"]
        C2_BF["Bloom filters: PostgreSQL"]
        C2_MATCH["Matching: FastAPI + feedback"]
    end

    subgraph phase3["Phase 3: Protocol"]
        C3_ID["Identity: Ed25519 + PSI"]
        C3_BF["Bloom filters: distributed store"]
        C3_MATCH["Matching: open protocol spec"]
    end

    subgraph phase4["Phase 4: On-chain"]
        C4_ID["Identity: Smart contract (on-chain)"]
        C4_BF["Bloom filters: off-chain (IPFS or local)"]
        C4_MATCH["Matching: decentralized nodes"]
        C4_TOKEN["Fees: FRND token"]
    end

    phase1 --> phase2
    phase2 --> phase3
    phase3 --> phase4

    style phase1 fill:#1a1d24,color:#e8eaf0,stroke:#7a8299
    style phase2 fill:#1a1d24,color:#e8eaf0,stroke:#e6a817
    style phase3 fill:#1a1d24,color:#e8eaf0,stroke:#00D4FF
    style phase4 fill:#1a1d24,color:#e8eaf0,stroke:#c5380e
```

## Сравнение блокчейнов

| Критерий | Solana | Base (Ethereum L2) | Sui |
|----------|--------|-------------------|-----|
| TPS | ~65,000 | ~2,000 | ~120,000 |
| Стоимость tx | $0.00025 | $0.001-0.01 | $0.001 |
| Язык контрактов | Rust (Anchor) | Solidity | Move |
| Экосистема DeFi | Большая | Растущая (Coinbase) | Средняя |
| Время финализации | ~400ms | ~2s | ~400ms |
| **Наш выбор** | **Рекомендован** | Альтернатива | Запасной |

## Smart Contract архитектура (Phase 4)

```mermaid
flowchart TB
    subgraph contracts["Smart Contracts"]
        REG["ProfileRegistry<br/>register, update, delete"]
        MATCH["MatchingOracle<br/>submit results, verify"]
        TOKEN["FRNDToken<br/>ERC-20 / SPL"]
        GOV["Governance<br/>proposals, voting"]
    end

    subgraph offchain["Off-chain"]
        NODE["Matching Nodes<br/>(run Jaccard engine)"]
        IPFS["IPFS / Arweave<br/>(Bloom filter storage)"]
    end

    USER["Пользователь"] -->|register| REG
    REG -->|emit event| NODE
    NODE -->|compute matches| MATCH
    MATCH -->|verify + distribute fees| TOKEN
    TOKEN --> GOV
    USER -->|upload bloom| IPFS
    IPFS -->|CID| REG

    style contracts fill:#c5380e,color:#fff
    style offchain fill:#1a1d24,color:#e8eaf0
```

## Токеномика FRND (если будет)

| Аллокация | % |
|-----------|---|
| Community и airdrops | 40% |
| Team (Тим + Денис) | 20% |
| Node operators | 20% |
| Treasury | 15% |
| Early contributors | 5% |
