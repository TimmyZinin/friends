# Friends — System Design Document (SDD)

> Status: DRAFT — pending Expert Panel review
> Version: 0.1
> Date: 2026-04-09

## 1. Vision

A matching protocol that connects people based on their knowledge graph — not photos or bios. Distributed as a Claude Code skill, with privacy-by-design architecture.

## 2. Problem Statement

Current dating/networking apps:
- Rely on photos → discrimination, catfishing, superficiality
- Store all personal data centrally → privacy nightmare
- Use manual questionnaires → people lie
- No way to match on "how you think" or "what you know"

## 3. Solution

### 3.1 User Flow
```
User installs /friends skill
    → Skill scans local markdown files (with permission)
    → Builds knowledge graph locally
    → Encodes into privacy-preserving embeddings
    → Sends embeddings to matching engine (MCP protocol)
    → Receives match results
    → Opens browser with interactive 2D/3D graph
    → User clicks node → sees shared info → connects via TG
```

### 3.2 Data Sources (all opt-in)
| Source | What we extract | Privacy level |
|--------|----------------|---------------|
| Markdown files | Topics, interests, expertise, thinking patterns | Encoded locally |
| Claude sessions | Conversation themes, question patterns | Encoded locally |
| Wearables (Oura etc.) | Stress, sleep, activity level | Encoded locally |
| DNA test | Genetic compatibility | Encoded locally |
| Location | Proximity for real-world meetups | Approximate only |
| Income signals | Auto-calculated from context, never asked directly | Encoded locally |

### 3.3 Matching Engine
- Receives ONLY encoded embeddings (zero-knowledge)
- Cosine similarity + weighted preference learning
- Feedback loop: user reactions adjust weights dynamically
- No personal data stored on server

### 3.4 Privacy Architecture
```
[Client Side]                    [Server Side]
Markdown files ─┐                
Claude sessions ─┤                
Wearables data ──┤→ Local encoder → Hash/Embeddings → Matching Engine
DNA data ────────┤                                     (no raw data)
Location ────────┘                
                                  
Private key stays on client       Only embeddings cross the wire
```

## 4. Architecture Phases

### Phase 1: MVP (current)
- Landing page with interactive graph visualization
- Concept documentation
- Claude Code skill prototype

### Phase 2: Centralized Alpha
- Central matching server on Contabo
- MCP-based data transmission
- Basic encoding on client side
- Telegram as communication channel

### Phase 3: Decentralized Beta
- Smart contracts per user profile
- Blockchain-based matching
- P2P data exchange
- Token economics (if applicable)

## 5. Tech Stack (planned)

| Component | Technology |
|-----------|-----------|
| Skill | Claude Code skill (Python/TypeScript) |
| Client encoding | Local LLM embeddings + hashing |
| Matching engine | Python (FastAPI) on Contabo |
| Visualization | D3.js / Three.js force-directed graph |
| Communication | MCP protocol |
| Landing page | Static HTML/JS on GitHub Pages |
| Future: Blockchain | TBD (Solana / Ethereum L2) |

## 6. Monetization (TBD)

Options discussed:
- Freemium (basic matching free, premium depth)
- Token/blockchain native
- DNA test ordering commission
- Enterprise (team matching for companies)

## 7. Open Questions

- [ ] Which embedding model for local encoding?
- [ ] Zero-knowledge proof vs homomorphic encryption vs simple hashing?
- [ ] Which blockchain for Phase 3?
- [ ] How to prevent Sybil attacks?
- [ ] Legal: GDPR, DNA data regulations
- [ ] How to bootstrap network effect?

## 8. References

- [Origin Transcript](origin-transcript.md) — brainstorm recording
- Expert Panel results — TBD
- Launch Strategy — TBD
