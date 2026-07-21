# Product Strategy & MVP Planning

**Project:** OTT Comparison & Discovery Platform
**Phase:** Epic 2 — Product Strategy & MVP Planning
**Builds on:** `03-product-discovery-report.md`

---

## 1. Product Vision

> **To make "what should I watch tonight" a 30-second decision, not a 20-minute research project — by bringing ratings, platform availability, and content details together in one place.**

The vision is deliberately scoped around *decision speed*, not catalog size or recommendation intelligence. This product isn't trying to out-recommend Netflix's algorithm — it's trying to remove the manual cross-referencing work that currently sits between a user's curiosity and their remote control.

## 2. Value Proposition

**For** people who subscribe to one or more OTT platforms and want to quickly find a genuinely good movie or series,
**who are currently** forced to check ratings and availability across multiple disconnected sites,
**this product is** a genre-based comparison tool
**that** shows ranked, rated, and platform-tagged titles in a single table,
**unlike** existing tools that either focus on ratings only (IMDb, Rotten Tomatoes) or availability only (JustWatch) without regional platform depth,
**our product** combines both in one glance, with first-class treatment of Disney+ Hotstar's regional catalog.

### Why this is valuable (tied back to discovery findings)
- Removes the single most time-costly step identified in the journey map: checking platform availability *after* already investing time in rating research
- Aggregates trust rather than forcing users to pick one rating source
- Respects the user's existing subscriptions instead of nudging them toward new ones — a subtle but important trust signal

## 3. MVP Definition

The MVP is scoped to prove one thing: **that a unified comparison table meaningfully reduces decision time.** Everything not in service of that gets deferred.

### In Scope for MVP
- Genre-based search/filter
- Movies vs. Series segmentation
- Comparison table showing, per title:
  - Availability across Netflix, Amazon Prime, Disney+ Hotstar
  - Ratings from IMDb and Rotten Tomatoes
  - Content origin/language
- Default sort: rating, high to low

### Explicitly Out of Scope for MVP (Post-Launch / Backlog)
- Personalized recommendations or watch history
- User accounts/profiles
- Additional OTT platforms beyond the initial three
- Additional rating sources beyond IMDb/Rotten Tomatoes
- Social features (reviews, sharing, watchlists)
- Mobile app (web-first for MVP)

### MVP Success Definition
A user can select a genre, see a sorted comparison table, and identify a title available on their subscribed platform(s) faster than they currently can using manual cross-referencing.

## 4. Product Success Metrics

### North Star Metric
**Median time from genre search to title selection.**
This directly measures the core value proposition — decision speed — and ties straight back to the discovery report's central finding.

### Leading Metrics (early signals, measurable soon after launch)
- Number of genre searches per session
- Table sort/filter interaction rate
- Bounce rate on the comparison table page (low bounce = table is doing its job)

### Lagging Metrics (measured over weeks/months)
- Return usage rate (users coming back for a new search)
- Session-to-selection completion rate (did they land on a title, or leave empty-handed)
- Qualitative: user feedback theme frequency (e.g., "saved me time" mentions)

### Guardrail Metrics
- Data accuracy rate (ratings/availability must stay current — stale data undermines the entire value proposition)
- Page load time for the comparison table (speed is part of the promise, so a slow table defeats its own purpose)

## 5. Product Roadmap

| Phase | Epic | Focus | Target Outcome |
|---|---|---|---|
| **Now** | Epic 1 | Product Discovery | Problem validated, personas & journey mapped |
| **Now** | Epic 2 | Strategy & MVP Planning | Vision, MVP scope, metrics defined *(this document)* |
| **Next** | Epic 3 | Product Requirements Document (PRD) | Detailed functional/non-functional requirements |
| **Next** | Epic 4 | Product Experience Design | IA, user flows, sitemap, wireframes |
| **Later** | Epic 5 | Backend Development & Data Infrastructure | Data sourcing (ratings/availability), APIs |
| **Later** | Epic 6 | Frontend Development & UI | Comparison table build, genre filters |
| **Later** | Epic 7 | QA, Testing & Validation | Functional + data-accuracy testing |
| **Launch** | Epic 8 | Launch, Analytics & Continuous Improvement | Deploy, measure North Star Metric, iterate |

### Post-MVP Roadmap (V2 candidates, informed by MVP learnings)
- Expand rating sources or additional OTT platforms based on user feedback themes
- User accounts + saved searches/watchlists
- Personalization layer (only after core comparison-table value is validated)

## 6. Risks, Assumptions & Constraints

### Risks
| Risk | Impact | Mitigation Direction |
|---|---|---|
| Rating/availability data goes stale or requires paid APIs | Undermines core value prop | Identify reliable data sources early in Epic 5; plan for scheduled refresh |
| Platforms' availability data isn't reliably scrapeable/accessible via API | Blocks the hero feature entirely | Validate data source feasibility *before* committing to full MVP build (spike recommended at start of Epic 3/5) |
| Competitive tools (JustWatch) already solve this at scale | Reduces perceived differentiation | Lean into regional (Hotstar) depth and dual-rating aggregation as the differentiator, not raw platform count |
| Solo/small team bandwidth vs. scope | Delayed timeline | Keep MVP scope strictly limited to the 3-platform, 2-rating-source table; resist scope creep |

### Assumptions
- Users are willing to select a genre before seeing results (not open browsing) — validated conceptually via journey map, should be confirmed with early user testing
- IMDb and Rotten Tomatoes are the two rating sources users trust most — based on persona interviews/founding use case, worth validating further
- Netflix, Amazon Prime, and Disney+ Hotstar represent the majority of the target market's subscriptions — reasonable for Indian market context, should be sized/confirmed

### Constraints
- Three-platform, two-rating-source scope for MVP (deliberate, not a limitation to solve immediately)
- Web-first delivery (no native mobile app for MVP)
- No user accounts/personalization in MVP — table must be valuable to an anonymous, first-time user
- Team size/timeline typical of a portfolio/internship-prep project — favors a lean MVP over a feature-rich build

---

*Next: Epic 3 — Product Requirements Document (PRD), which will translate this MVP scope into detailed functional requirements.*
