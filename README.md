# Friends

**Find people who truly match you — not by photos, but by what you think about.**

Friends is a knowledge-graph-based matching protocol that connects people through their actual interests, thinking patterns, and life context — extracted from markdown files, AI conversations, and personal data sources.

## How it works

1. **Install the Claude Code skill** → `/friends`
2. Your local data gets **encoded on your device** (zero-knowledge)
3. Encrypted embeddings are sent to the **matching engine**
4. You see a **live graph** of compatible people near you
5. Click a node → see what they chose to share → connect via Telegram

## Core Principles

- **Privacy-first**: All encoding happens client-side. The matching engine never sees raw data.
- **No photos, no fake profiles**: Matching is based on knowledge graphs, not selfies.
- **Opt-in depth**: Share as much or as little as you want. More data = better matches.
- **Decentralization-ready**: Start centralized, migrate to blockchain when scale demands it.

## Data Sources (opt-in)

- Markdown files (Claude sessions, notes, docs)
- Wearables (Oura, Apple Health)
- DNA tests (23andMe, etc.)
- Blood work / health data
- Location (proximity matching)

## Architecture

See [docs/SDD.md](docs/SDD.md) for the full System Design Document.

## Status

🔬 Concept phase — Expert panel review in progress.

## Authors

- [Tim Zinin](https://github.com/TimmyZinin)
- Denis Govorunov
