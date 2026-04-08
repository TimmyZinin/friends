# Friends — System Design Document (SDD)

> Status: DRAFT v0.2 — post Expert Panel + Codex Adversarial
> Version: 0.2
> Date: 2026-04-09

## 1. Vision

A knowledge networking protocol that connects people based on their intellectual fingerprint — not photos or bios. Distributed as a Claude Code skill, with privacy-by-design architecture.

## 2. Problem Statement

Current networking apps:
- Rely on photos → discrimination, catfishing, superficiality
- Store all personal data centrally → privacy nightmare
- Use manual questionnaires → people lie
- No way to match on "how you think" or "what you know"

## 3. Solution

### 3.1 User Flow
```
User installs /friends skill
    → Skill scans local markdown files (with explicit permission)
    → Extracts topic tags locally (keyword extraction + TF-IDF)
    → Encodes tags into a weighted Bloom filter (on device)
    → Sends ONLY the Bloom filter to matching server
    → Server computes Jaccard similarity against other Bloom filters
    → Top-K matches returned
    → Opens browser with interactive 2D graph
    → User clicks node → sees info the other person chose to share → connects via TG
```

### 3.2 Data Sources — MVP (Phase 1-2)

| Source | What we extract | What crosses the wire |
|--------|----------------|----------------------|
| Markdown files (*.md) | Topic tags, keywords | Bloom filter (not invertible) |
| Claude session history | Conversation themes | Bloom filter (not invertible) |
| Location (opt-in) | City-level only | City name string |

**Explicitly NOT in MVP scope:**
- ~~DNA tests~~ — removed (legal: GDPR Art.9, GINA; market: Pheramor failure; PR risk)
- ~~Wearables / health data~~ — removed (medical data regulations, HIPAA)
- ~~Income inference~~ — removed permanently (ethically toxic, technically unproven, GDPR Art.22)
- ~~Blockchain~~ — not in public-facing architecture or messaging

> **Future data sources (Phase 3+ only, requires legal review):**
> Wearables integration could be explored after product-market fit is proven and a dedicated legal review ($5-10K) is completed. DNA matching is indefinitely deferred.

### 3.3 Matching Engine

**What the server receives:** Weighted Bloom filter (fixed-size bit array, not invertible to original text).

**What the server stores:** Bloom filter + Ed25519 public key + optional display name + optional Telegram handle.

**What the server does NOT store:** Raw text, topic names, file contents, embeddings, location history.

**Matching algorithm (MVP):**
1. Client extracts topic tags from markdown files (TF-IDF or keyword extraction)
2. Tags encoded into weighted Bloom filter on device
3. Bloom filter sent to server via REST API (signed with Ed25519 private key)
4. Server computes Jaccard similarity on Bloom filters
5. Top-K matches returned with similarity scores
6. Feedback (thumbs up/down) adjusts weight in future queries (Phase 2)

**Privacy claim (precise):** Topic extraction and encoding happen entirely on the user's device. The matching server receives only a Bloom filter — a fixed-size bit array that cannot be reversed to recover original topics. The server does not see, store, or process the user's files, text, or embeddings.

### 3.4 Privacy Architecture
```
[Client Side]                         [Server Side]
                                      
Markdown files ─┐                     
Claude sessions ─┤→ Topic extraction   
                 │   (local, on device)
                 ↓                     
              TF-IDF / keywords        
                 ↓                     
           Bloom filter encoding       
                 ↓                     
           Ed25519 signature           
                 ↓                     
        ─── REST API ──────────→  Matching Engine
                                  (Bloom filter store)
                                  (Jaccard similarity)
                                       ↓
                                  Top-K results
        ←── REST API ──────────       
                 ↓                     
           Graph visualization         
           (browser, D3.js)            

Private key: ~/.friends/keypair.json (never transmitted)
Bloom filter: fixed-size, not invertible
Server: stateless matching, no raw data
```

## 4. Architecture Phases

### Phase 1: MVP (current)
- Landing page with interactive graph visualization (timzinin.com/friends/)
- Concept documentation (SDD, expert panel, launch strategy)
- Demo graph with synthetic data (clearly labeled, NOT from real users)

### Phase 2: Centralized Alpha
- FastAPI matching server on Contabo VPS 30
- Claude Code skill (TypeScript) for local tag extraction
- Bloom filter transmission via REST API
- Ed25519 keypair for identity and consent
- Telegram as communication channel after match
- Basic feedback loop (thumbs up/down)

### Phase 3: Protocol & Scale
- Open-source "Friends Protocol" specification
- Multi-agent support (Cursor, Windsurf, any MCP-compatible)
- Event matching for conferences (Telegram group analysis)
- Evaluate decentralization IF >10K users AND proven demand

## 5. Tech Stack (planned)

| Component | Technology |
|-----------|-----------|
| Skill | Claude Code skill (TypeScript) |
| Client encoding | TF-IDF keyword extraction → Bloom filter |
| Matching engine | FastAPI (Python) on Contabo VPS 30 |
| Database | SQLite (upgrade to Postgres at >10K users) |
| Visualization | D3.js force-directed graph |
| Landing page | Static HTML/JS on GitHub Pages |
| Identity | Ed25519 keypair (local) |
| Communication | REST API (skill → server) |

## 6. Monetization

### MVP: Free (no monetization)
Goal is network effect and validation.

### Phase 2-3 options (pick one):
1. **Event matching ($2/participant)** — conference organizers pay for attendee matching. Solves cold start.
2. **Verified profiles ($5/mo)** — identity verification badge, priority in matching.
3. **Team matching (B2B, $20/seat/mo)** — companies match employees for projects/mentoring.

**Explicitly removed:** Token economics, DNA test commissions, blockchain-native monetization.

## 7. Open Questions

- [ ] Bloom filter parameters: optimal size and hash count for topic matching?
- [ ] Minimum viable topic count per user for meaningful matching?
- [ ] How to handle users with very few markdown files?
- [ ] Sybil attack prevention without centralized identity?
- [ ] GDPR data processing agreement template
- [ ] Event matching: technical approach for Telegram group analysis?

## 8. References

- [Origin Transcript](origin-transcript.md) — brainstorm recording (Tim + Denis)
- [Expert Panel Results](expert-panel-results.md) — 7-expert analysis, 35 ideas reviewed
- [Launch Strategy](launch-strategy.md) — 5-phase plan, ORB channels, $0 budget
- Codex Adversarial Review — 2026-04-09 (3 findings addressed in v0.2)
