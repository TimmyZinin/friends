# Friends

**Find the friend you didn't know existed.**

Friends is a knowledge networking protocol that connects people based on their intellectual fingerprint — extracted from markdown files and AI conversations. Not by photos, not by bios, not by swiping.

## How it works

1. **Install the `/friends` skill** in Claude Code
2. The skill **extracts topic tags** from your local markdown files (on your device)
3. Tags are encoded into a **Bloom filter** (a compact, non-reversible representation)
4. Only the Bloom filter is sent to the matching server — your files stay on your device
5. You see a **live graph** of compatible people
6. Click a node → see what they chose to share → connect via Telegram

## Privacy

Topic extraction and encoding happen entirely on your device. The matching server receives only a Bloom filter — a fixed-size bit array that cannot be reversed to recover your original topics. The server does not see, store, or process your files, text, or raw data.

See [docs/SDD.md](docs/SDD.md) for the full technical privacy architecture.

## Data Sources (MVP)

- Markdown files (`*.md`) — topics, interests, thinking patterns
- Claude session history — conversation themes
- Location (opt-in, city-level only)

## Architecture

See [docs/SDD.md](docs/SDD.md) for the System Design Document.

## Status

🔬 Concept phase — MVP landing page in development.

## Docs

- [System Design Document](docs/SDD.md)
- [Expert Panel Results](docs/expert-panel-results.md) — 35 ideas from brainstorm analyzed by 7-expert panel
- [Launch Strategy](docs/launch-strategy.md) — 5-phase go-to-market plan

## Authors

- [Tim Zinin](https://github.com/TimmyZinin)
- Denis Govorunov
