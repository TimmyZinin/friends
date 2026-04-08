# Friends — Launch Strategy

> Date: 2026-04-09
> Product: Friends — knowledge networking protocol
> Team: Tim Zinin + Denis Govorunov
> Budget: $0 (bootstrap)
> MVP: Landing page + interactive graph on timzinin.com/friends/

---

## Executive Summary

Friends launches as an **open-source Claude Code skill** distributed through GitHub. The MVP is a stunning interactive graph visualization that demonstrates the concept and captures early adopters. Zero marketing budget — growth comes from the skill ecosystem, developer Twitter, and borrowed channels (podcasts, newsletters, Hacker News).

**Core hook:** *"Find the friend you didn't know existed."*

**Distribution moat:** Claude Code skill install = zero-friction onboarding. GitHub repo = the app store.

---

## ORB Channel Strategy

### Owned Channels

| Channel | Asset | Purpose |
|---------|-------|---------|
| **GitHub repo** | TimmyZinin/friends | Source of truth, discovery, stars = social proof |
| **Landing page** | timzinin.com/friends/ | Demo the graph, capture emails, explain the concept |
| **Email list** | Collected from landing page | Launch announcements, updates, community building |
| **README.md** | GitHub repo | First touchpoint for developers — this IS the marketing copy |

**Priority:** GitHub repo + landing page. These are the two owned assets that matter. Email list builds passively from landing page signups.

### Rented Channels

| Channel | Why | Tactic |
|---------|-----|--------|
| **Twitter/X** | AI/dev community lives here | Thread: "I built a skill that matches people by how they think, not how they look" + graph screenshot + GH link |
| **LinkedIn** | Professional networking angle | Post: "What if your next co-founder was hiding in your markdown files?" |
| **Reddit** | ClaudeAI subreddit, singularity subreddit, programming subreddit | "Show HN"-style post with technical depth |
| **Hacker News** | Developer early adopters | "Show HN: Friends – find people who think like you (Claude Code skill)" |
| **Product Hunt** | Tech early adopters | Phase 4 launch — after 100+ users |

**Rule:** Every rented channel post links to **GitHub repo** (not landing page). Developers trust GitHub, not marketing sites.

### Borrowed Channels

| Channel | Target | Pitch |
|---------|--------|-------|
| **AI newsletters** | Ben's Bites, The Neuron, TLDR AI | "First Claude Code skill that connects people — matching by knowledge graph" |
| **Dev podcasts** | Changelog, DevTools FM, Latent Space | "Privacy-first social networking through AI conversations" |
| **Claude Partner Network** | Tim's 10 certified partners | Direct DM: "I built this, try it, give feedback" |
| **Denis's network** | Co-founder's contacts | Personal invites to test + share |
| **Anthropic community** | Claude Code Discord/forum | Skill showcase post |

---

## Five-Phase Launch Plan

### Phase 1: Internal Launch (Days 1-3) ← CURRENT

**Goal:** Validate that the graph visualization is compelling enough to share.

**Actions:**
- [x] Create GitHub repo with SDD and expert panel
- [ ] Build MVP landing page with interactive force-directed graph
- [ ] Seed graph with 10-15 synthetic demo profiles (fictional personas, clearly labeled, NOT from real users' repos)
- [ ] Tim + Denis test with their own markdown files
- [ ] Collect 3-5 screenshots of the graph for marketing

**Success metric:** Tim and Denis both say "this looks cool enough to share."

**Landing page must have:**
1. Hero: animated graph visualization (full-screen, interactive)
2. One-liner: "Find the friend you didn't know existed."
3. 3-step "How it works": Install skill → Scan your files → See your graph
4. Email capture: "Get early access"
5. GitHub link: "Star the repo"
6. Privacy section: "Your files stay on your device. Only a Bloom filter (non-reversible) reaches the server."

### Phase 2: Alpha Launch (Days 4-7)

**Goal:** Get 20-30 real developers to install and try the skill.

**Actions:**
- Share with Claude Partner Network (10 people) via personal DM
- Share with Denis's developer contacts (10-15 people)
- Post in 2-3 developer Telegram groups
- Ask each alpha user for one piece of feedback

**Messaging for alpha:**
> "I'm building a skill that matches developers based on their knowledge graph — extracted from markdown files and Claude conversations. Privacy-first: everything stays on your device. Would you try it and tell me if the matches make sense?"

**Success metric:** 20+ installs, 5+ people say "the matching surprised me."

### Phase 3: Beta Launch (Days 8-14)

**Goal:** Generate first wave of organic buzz.

**Actions:**
- Twitter thread (Tim's account): Build-in-public story
  - Tweet 1: The problem ("I spent 3 years in tech and the most interesting people I met were through random Slack conversations, not LinkedIn")
  - Tweet 2: The insight ("What if an AI could read your notes and find people who think like you?")
  - Tweet 3: The demo (graph screenshot/GIF)
  - Tweet 4: The privacy angle ("Your files stay on your device. The server sees only a Bloom filter — a compact bit array it can't reverse into your content.")
  - Tweet 5: CTA ("Install the skill: /friends. Star the repo: github.com/TimmyZinin/friends")
- LinkedIn post (professional angle): "What if your next co-founder was hiding in your Claude conversations?"
- Reddit ClaudeAI subreddit: Technical deep-dive post

**Content assets to prepare:**
- 15-second screen recording: install skill → run `/friends` → graph appears
- 3 graph screenshots (different node layouts)
- Architecture diagram (client-side encoding flow)

**Success metric:** 100+ GitHub stars, 50+ email signups.

### Phase 4: Early Access Launch (Days 15-30)

**Goal:** Reach 500+ aware, 100+ active users.

**Actions:**
- Product Hunt launch (aim for weekday, Tuesday-Thursday)
  - Tagline: "Find the friend you didn't know existed"
  - Subtitle: "Knowledge networking powered by your AI conversations"
  - Maker comment: Technical deep-dive + privacy explanation
  - Assets: Graph demo GIF, architecture diagram, 3 screenshots
- Hacker News "Show HN" post
- Submit to AI newsletter features (Ben's Bites, The Neuron, TLDR AI)
- Pitch 2-3 dev podcasts

**Product Hunt preparation (start Day 8):**
- [ ] Create PH listing (draft)
- [ ] Prepare 5 screenshots + 1 demo video (30 sec)
- [ ] Write maker comment (500 words: problem, solution, privacy, tech)
- [ ] Brief 20 supporters to engage on launch day
- [ ] Schedule social posts for launch morning

**Success metric:** Top 5 Product of the Day, 500+ GitHub stars, 200+ email signups.

### Phase 5: Full Launch (Day 30+)

**Goal:** Sustainable organic growth.

**Actions:**
- Open skill for self-serve install (already open via GitHub)
- Weekly "interesting matches" newsletter to email list
- Monthly "state of the graph" blog post (how many nodes, clusters, interesting patterns)
- Explore event matching pilot (first conference partnership)
- MCP-compatible versions for Cursor/Windsurf

**Success metric:** 50+ new users/week organic, first event matching pilot.

---

## Messaging Framework

### Positioning Statement

> Friends is a knowledge networking protocol that connects people based on how they think — not how they look. Install a Claude Code skill, and it builds a knowledge graph from your local files. Then it finds other minds that resonate with yours. Privacy-first: your files stay on your device, the server sees only non-reversible Bloom filters.

### Key Messages

| Audience | Message | Channel |
|----------|---------|---------|
| Developers | "Match by knowledge graph, not selfies. Install `/friends` and see who thinks like you." | Twitter, GitHub, HN |
| AI enthusiasts | "The first Claude Code skill that connects people. Your AI conversations reveal more about you than any dating profile." | Reddit, AI newsletters |
| Privacy advocates | "Zero-knowledge matching. Client-side encoding. The matching engine never sees your data." | HN, privacy communities |
| Professionals | "Find your next co-founder in your markdown files." | LinkedIn |

### Hooks (ranked by predicted engagement)

1. **"Find the friend you didn't know existed."** — curiosity + serendipity
2. **"Your AI conversations say more about you than your LinkedIn profile."** — provocative truth
3. **"No photos. No bios. No swiping. Just minds."** — anti-pattern positioning
4. **"What if your next co-founder was hiding in your Claude sessions?"** — professional FOMO
5. **"Install a skill. See your mind. Find minds like yours."** — product clarity

### What NOT to say

- ❌ "Decentralized" / "Blockchain" / "Web3" — repels mainstream
- ❌ "Dating app" — wrong category, wrong expectations
- ❌ "AI-powered matching" — generic, means nothing in 2026
- ❌ "Zero-knowledge proofs" — technically inaccurate for MVP, confuses non-crypto audience
- ❌ "DNA matching" / "Genetic compatibility" — not in MVP, PR risk

---

## Growth Loops

### Loop 1: Graph Shareability (Primary)
```
User installs /friends
    → Sees their knowledge graph
    → Screenshots it (it's beautiful)
    → Posts on Twitter: "look at my mind map"
    → Followers ask "what is this?"
    → Link to repo
    → New user installs
```
**Key insight:** The graph visualization IS the marketing. If it's beautiful enough, people share it unprompted.

### Loop 2: Match Notification (Phase 2)
```
User gets matched
    → "Someone who thinks like you just joined"
    → User returns to check
    → Tells friend about the match
    → Friend installs
```

### Loop 3: Event Matching (Phase 3+)
```
Conference organizer integrates Friends
    → Attendees install to see "who should I meet"
    → After event, attendees keep the skill
    → Become permanent network nodes
```

---

## Competitive Positioning

### What we're NOT competing with

| Product | Why not a competitor |
|---------|---------------------|
| Tinder/Bumble/Hinge | Photo-first dating. Completely different UX, audience, and value prop. |
| LinkedIn | Professional networking by credentials. We match by thinking patterns. |
| Meetup | Event-based. We're serendipity-based. |
| Discord communities | Interest-group-based. We're individual-matching-based. |

### What we ARE

**Category:** Knowledge Networking Protocol
**Closest analogies:**
- "Shazam, but for people" — discovers who resonates with you
- "GitHub social graph, but for your mind" — connections based on what you build/think
- "Obsidian graph view, but the nodes are people" — visual, interconnected, organic

### Unique advantages

1. **Distribution moat:** Claude Code skill ecosystem (85K+ skills, growing 10%/mo)
2. **Privacy moat:** Client-side encoding. Competitors can't copy this easily without rearchitecting.
3. **Data moat:** Once users contribute data, matching quality improves for everyone. Network effect.
4. **Cultural timing:** "AI-native" identity is forming. This product serves that identity.

---

## Metrics & KPIs

### Phase 1-2 (Validation)
| Metric | Target |
|--------|--------|
| GitHub stars | 50+ |
| Skill installs | 20+ |
| "Would you use this weekly?" (survey) | >40% yes |

### Phase 3-4 (Growth)
| Metric | Target |
|--------|--------|
| GitHub stars | 500+ |
| Email signups | 200+ |
| Weekly active users | 50+ |
| Product Hunt ranking | Top 5 of the Day |
| Twitter impressions from launch thread | 50K+ |

### Phase 5 (Sustainability)
| Metric | Target |
|--------|--------|
| New users/week (organic) | 50+ |
| Retention (30-day) | >30% |
| First revenue | Event matching pilot |

---

## Launch Timeline

```
Week 1 (Apr 9-15):   MVP landing page + graph visualization
                      Internal testing (Tim + Denis)
                      Seed demo profiles

Week 2 (Apr 16-22):  Alpha launch (30 people)
                      Claude Partner Network
                      Denis's contacts

Week 3 (Apr 23-29):  Beta launch
                      Twitter thread
                      LinkedIn post
                      Reddit ClaudeAI subreddit

Week 4 (Apr 30-May 6): Product Hunt prep
                        HN "Show HN" post
                        Newsletter pitches

Week 5 (May 7-13):   Product Hunt launch
                      Podcast pitches
                      Email to waitlist
```

---

## Budget: $0

| Item | Cost | Alternative |
|------|------|-------------|
| Hosting | $0 | GitHub Pages (landing) + Contabo VPS 30 (matching server, already paid) |
| Domain | $0 | timzinin.com/friends/ (existing) |
| Design | $0 | Claude Code frontend-design skill |
| Video | $0 | Screen recording + ffmpeg |
| Email | $0 | GitHub repo as primary, free tier of any email tool for waitlist |
| Product Hunt | $0 | Free to list |
| Social media | $0 | Organic only |

---

## Risk Mitigation

| Risk | Mitigation |
|------|------------|
| Graph looks ugly/boring | 60% of MVP effort on visualization. Test 3+ D3.js layouts. |
| Nobody installs the skill | Alpha test with warm network first. If 0/10 friends install → pivot. |
| Product Hunt flop | HN as backup. Newsletter features as backup. Don't bet everything on PH. |
| "Just another AI tool" perception | Lead with the graph visual, not the tech. Show, don't tell. |
| Privacy concerns despite architecture | Publish detailed privacy docs. Open-source everything. |
| Cold start (empty graph) | Demo profiles from public repos. Launch at specific community first. |

---

## Appendix: Content Calendar (Weeks 1-5)

| Day | Channel | Content |
|-----|---------|---------|
| D1 | GitHub | README + SDD pushed |
| D3 | — | MVP landing page live |
| D5 | TG (private) | Alpha invites to 10 Claude Partners |
| D7 | TG (private) | Alpha invites to Denis's contacts |
| D10 | Twitter | Teaser: graph screenshot + "something cooking" |
| D14 | Twitter | Launch thread (5 tweets) |
| D14 | LinkedIn | Professional angle post |
| D15 | Reddit | ClaudeAI subreddit technical post |
| D17 | Email | Newsletter pitch to Ben's Bites |
| D21 | Product Hunt | Listing goes live |
| D21 | Hacker News | "Show HN" post |
| D28 | Email | First newsletter to waitlist |
| D35 | Blog | "State of the Graph" — first month stats |
