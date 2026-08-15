# Product Strategy & MVP Planning: CineCompass

| | |
|---|---|
| **Project** | CineCompass (OTT Comparison & Discovery Platform) |
| **Phase** | Epic 2: Product Strategy & MVP Planning |
| **Prepared By** | Vibhuti Gupta |
| **Builds On** | `03-product-discovery-report.md` |
| **Status** | v2.2, Live, Post-Build |
| **Last Updated** | 2026-08-06 |

---

## Table of Contents

1. [Product Vision](#1-product-vision)
2. [Product Goals](#2-product-goals)
3. [Value Proposition](#3-value-proposition)
4. [MVP Definition: Planned vs. Shipped](#4-mvp-definition-planned-vs-shipped)
5. [Product Success Metrics](#5-product-success-metrics)
6. [Product Roadmap: Status](#6-product-roadmap-status)
7. [Risks, Assumptions and Constraints](#7-risks-assumptions-and-constraints)
8. [Prioritized Next Steps](#8-prioritized-next-steps)

---

## 1. Product Vision

> **To make "what should I watch tonight" a 30-second decision, not a 20-minute research project, by bringing ratings, platform availability, and content details together in one place.**

The vision is deliberately scoped around *decision speed*, not catalog size or recommendation intelligence. This product isn't trying to out-recommend Netflix's algorithm. It's trying to remove the manual cross-referencing work that currently sits between a user's curiosity and their remote control. **Unchanged since v1.0.** This still holds as the product's reason for existing.

## 2. Product Goals

- Reduce the time required to find a watchable title
- Help users match ratings with the OTT subscriptions they already have
- Validate whether a unified comparison view actually improves decision-making

These goals are the explicit bridge between the vision above and the MVP scope below: the vision states the outcome CineCompass wants for users, these goals state what the product itself has to do to get there, and Section 4 defines the smallest version that tests them.

## 3. Value Proposition

**For** people who subscribe to one or more OTT platforms and want to quickly find a genuinely good movie or series,
**who are currently** forced to check ratings and availability across multiple disconnected sites,
**this product is** a genre-based comparison tool
**that** shows ranked, rated, and platform-tagged titles in a single view,
**unlike** tools primarily focused on ratings or platform availability alone,
**our product** combines both in one glance, with first-class treatment of Disney+ Hotstar's catalog.

### Why This Is Valuable
- Removes the single most time-costly step identified in discovery: checking platform availability after already investing time in rating research
- Aggregates trust rather than forcing users to pick one rating source
- Respects the user's existing subscriptions instead of nudging them toward new ones, a subtle but important trust signal

## 4. MVP Definition: Planned vs. Shipped

The MVP was scoped to prove one thing: **that a unified comparison view meaningfully reduces decision time.** That hypothesis still hasn't been formally measured (see Section 5), but the build itself went further than the original MVP line in most areas.

### 4.1 MVP User, Problem, and Hypothesis

- **Primary user:** budget-conscious OTT subscriber
- **Core problem:** fragmented rating and availability research
- **Core hypothesis:** a unified comparison view reduces time-to-selection

### 4.2 Scope Comparison Table

| Requirement | Originally Planned | Shipped | Status |
|---|---|---|---|
| Genre-based search/filter | Yes | 13 genres + "All Genres" | As planned |
| Movies vs. Series segmentation | Yes | Top-level type toggle | As planned |
| Platform coverage | Netflix, Amazon Prime, Disney+ Hotstar (3) | Plus Apple TV+ and Max (5 total) | Exceeded |
| Rating sources | IMDb, Rotten Tomatoes (2) | Plus Metacritic (3 total) | Exceeded |
| Default sort | Rating, high to low | **IMDb rating, high to low** | Resolved. This briefly shipped as popularity-first, was flagged as a gap, and has since been fixed |
| Content origin/language | Full visibility | Content-rating label plus "International" tag; no true origin filter | Fell short |
| User accounts / watchlist | Explicitly out of scope | Watchlist shipped anyway (no-account, localStorage-based, 3 statuses plus personal rating) | Beyond scope, added deliberately |
| Region-aware availability | Not planned | Region selector (India live, extensible) | Beyond scope |
| Offline resilience | Not planned | Fallback dataset plus visible banner when live sources fail | Beyond scope |

### 4.3 Explicitly Out of Scope (Still True Post-Launch)
- User accounts/login/authentication in the traditional sense (the watchlist works without one, by design)
- Personalized recommendations
- Social features (reviews, sharing)
- Native mobile applications (the app is a responsive web SPA)
- Additional rating/platform sources beyond what's listed above, a soft boundary since it already moved once during build

### 4.4 MVP Success Definition: Status

> *"A user can select a genre, see a sorted comparison table, and identify a title available on their subscribed platform(s) faster than they currently can using manual cross-referencing."*

This has **not been formally measured.** The product is live and functionally does this. Every piece of the mechanism described is built and working, including the default-sort fix that makes "sorted comparison table" true without a manual step. But no baseline/comparison timing study has been run, and analytics to measure it in the wild isn't switched on yet. **This remains the single most important next step, ahead of any new feature.**

## 5. Product Success Metrics

**Revision note (2026-08-06):** these metrics were carried forward from v1.0 without being re-examined, and a review surfaced real definitional problems, not just missing instrumentation. Two fixes below: (1) "selection" is now a defined event, not a vague phrase, and (2) analytics events have been implemented, so the leading metrics are now capturable. The North Star metric itself still requires a manual calculation from raw event data; the analytics dashboard shows event counts, not the time delta between two named events.

### 5.1 Defining "selection"
Previously undefined, which made the North Star metric unmeasurable in practice. **Selection is now explicitly either of two tracked events:** the user clicking through to actually watch on a platform (the primary conversion), or the user saving the title to the watchlist for later (a secondary but still valid conversion, per the journey map's "Save for Later" branch). A session that produces neither event within a reasonable window did not result in a selection.

### 5.2 Metric Hierarchy

```
North Star Metric (candidate)
        ↓
  Leading Metrics
        ↓
Lagging / Outcome Metrics
        ↓
  Guardrail Metrics
```

The North Star is deliberately still labeled a *candidate*: it hasn't been validated against real production data yet, and this document is honest about that rather than presenting it as a settled definitive metric.

| Metric Tier | Metric | Purpose | Production Status |
|---|---|---|---|
| North Star (candidate) | Median time from genre selection to a selection event | Directly measures the core value proposition | Analytics events implemented; production data collection pending. The time-delta calculation itself is not automatic and needs to be pulled from raw analytics data, not read off the dashboard |
| Leading | Genre searches per session | Early usage signal | Instrumented |
| Leading | Sort/filter interaction rate | Are users engaging with the mechanism designed to help them? | Instrumented |
| Leading | Bounce rate on the comparison view | Low bounce means the view is doing its job | Not instrumented, and flagged as a weak metric on its own: a fast exit can mean "found it immediately" or "found nothing and gave up," the same signal for opposite outcomes. Should always be read alongside the completion rate below, never alone |
| Lagging/Outcome | Return usage rate | Habit formation | Not instrumented |
| Lagging/Outcome | Session-to-selection completion rate | Did they land on a title or leave empty-handed | Analytics events implemented; completion rate itself still needs to be computed from raw data |
| Guardrail | API proxy error rate | Concrete, checkable substitute for the original "data accuracy rate," which had no defined measurement method | Not instrumented, but genuinely measurable once added, unlike its predecessor |
| Guardrail | Page load time | Speed is part of the promise | Not formally benchmarked |

## 6. Product Roadmap: Status

| Phase | Epic | Focus | Status |
|---|---|---|---|
| Done | Epic 1 | Product Discovery | Complete |
| Done | Epic 2 | Strategy & MVP Planning | Complete (this document) |
| Done | Epic 3 | Product Requirements Document (PRD) | Complete, updated post-build; see `05-prd.md` |
| Skipped/Informal | Epic 4 | Product Experience Design | No separate wireframe/IA phase was run as a distinct step; design decisions were made directly during build. Named honestly here rather than claiming a phase that didn't happen. |
| Done | Epic 5 | Backend Development & Data Infrastructure | Complete. Live discovery, ratings, and availability data now power the app, fronted by a server-side proxy layer so API keys never reach the browser |
| Done | Epic 6 | Frontend Development & UI | Complete. Comparison view, filters (including the now-fixed default sort), watchlist, routing, responsive layout |
| Partial | Epic 7 | QA, Testing & Validation | An informal but substantial bug-fix pass happened (16 distinct bugs fixed across the build, including the default-sort issue, a real streaming-availability data bug, broken images, search race conditions, and accessibility gaps). No formal automated test suite or structured QA plan exists. |
| Partial | Epic 8 | Launch, Analytics & Continuous Improvement | Deployed to production. Analytics events implemented; production data collection pending, so "measure the North Star Metric" hasn't actually started. |

### 6.1 Post-MVP Roadmap: Revisited

| Original "V2 Candidate" | Actual Outcome |
|---|---|
| Expand rating sources or additional OTT platforms based on user feedback themes | **Already happened, ahead of user feedback.** Opportunistic during build, not feedback-driven. Worth validating retroactively that these were the right additions. |
| User accounts + saved searches/watchlists | **Watchlist shipped without accounts.** A leaner version of what was planned |
| Personalization layer | **Still correctly deferred.** No change, and this remains the right call until the core comparison-table value is validated with real usage data |

## 7. Risks, Assumptions and Constraints

### 7.1 Risk Status

| Risk | Original Concern | Status |
|---|---|---|
| Rating/availability data goes stale or requires paid APIs | Undermines core value prop | **Resolved.** Live data sources confirmed working, with a visible offline-fallback mode if any go down |
| Platform availability isn't reliably accessible via API | Blocks the hero feature entirely | **Resolved, with a lesson learned.** A real production bug briefly showed everything as unavailable everywhere before it was caught and fixed |
| Competitive tools (JustWatch) already solve this at scale | Reduces perceived differentiation | **Unchanged.** Differentiation still rests on rating aggregation and regional depth, neither of which has been market-tested |
| Solo/small team bandwidth vs. scope | Delayed timeline | **Materialized in a notable way.** Scope grew (more platforms, more rating sources, a watchlist) rather than shrank. Worth watching going forward, since the discipline this risk called for hasn't really been tested yet. |

### 7.2 Assumptions: Still Open
- Users are willing to select a genre before seeing results (not open browsing)
- IMDb, Rotten Tomatoes, and now Metacritic are the rating sources users trust most
- Netflix, Amazon Prime, Disney+ Hotstar, Apple TV+, and Max represent the majority of the target market's subscriptions. The platform list grew during build without re-validating this assumption against the wider set

None of these have been tested with real users. They remain reasonable defaults, not confirmed facts.

### 7.3 Constraints
- **No version control has been used for this project.** Every deploy has been a manual command-line push. Not a functional blocker, but worth fixing soon, both for maintainability and because commit history has independent value for a portfolio project.
- Web-first delivery (no native mobile app), unchanged
- No formal user accounts, unchanged; the watchlist proves the current feature set doesn't need them

## 8. Prioritized Next Steps

1. **Enable production analytics collection.** Analytics events are implemented as of 2026-08-06, but they don't collect anything until data collection is switched on.
2. **Pull raw event data periodically and compute the North Star Metric and completion rate by hand.** The analytics dashboard shows event counts, not the time delta between genre selection and a selection event, so this calculation has to be done outside the dashboard, at least until it's worth building a proper pipeline for it.
3. **Build a real origin/language filter.** The one persona need (Regional Content Seeker) still meaningfully unmet.
4. **Add basic rate limiting to the API proxy layer**, and instrument its error rate while doing so, since that's now the guardrail metric standing in for the old, unmeasurable "data accuracy rate."
5. **Initialize version control.** A maintainability gap independent of feature scope.
6. Everything else (additional platforms, accounts, personalization) stays deferred until 1 through 3 above produce real signal.

---

*Next: `05-prd.md`, updated to reflect the same shipped-vs-planned reality documented here. Implementation-level detail (file names, code identifiers, API endpoint paths) intentionally lives there and in the codebase, not in this strategy document.*
