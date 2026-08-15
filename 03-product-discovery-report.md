# Product Discovery Report: CineCompass

| | |
|---|---|
| **Project** | CineCompass (OTT Comparison & Discovery Platform) |
| **Phase** | Epic 1: Product Discovery |
| **Prepared By** | Vibhuti Gupta |
| **Status** | v2.2, Live |
| **Last Updated** | 2026-08-06 |
| **Related Docs** | `01-user-personas.md`, `02-user-journey-map.md`, `04-product-strategy-mvp.md` |

---

## Table of Contents

1. [Problem Statement](#1-problem-statement)
2. [Background and Context](#2-background-and-context)
3. [Research and Validation](#3-research-and-validation)
4. [Key Findings and Build Validation](#4-key-findings-and-build-validation)
5. [Target Users](#5-target-users)
6. [Opportunity Statement](#6-opportunity-statement)
7. [Competitive Landscape](#7-competitive-landscape)
8. [Success Metrics and Measurement Plan](#8-success-metrics-and-measurement-plan)
9. [Recommendation and Next Steps](#9-recommendation-and-next-steps)

---

## 1. Problem Statement

Users looking to watch a movie or series must currently piece together their decision from multiple disconnected sources: genre-based "best of" lists, trusted rating sites (IMDb, Rotten Tomatoes), and individual platform searches to confirm availability. This fragmented process costs users significant time and frequently ends in disappointment when a well-rated title turns out not to be available on the platform they've already subscribed to.

## 2. Background and Context

Streaming subscriptions have multiplied, but discovery tools haven't kept pace with cross-platform fragmentation. Most users don't subscribe to every platform; they typically hold 1 to 3 subscriptions and must decide, title by title, whether something is worth watching and whether it's accessible to them at all. The result is a two-part decision problem (quality plus availability) that no single existing tool answers well for the Indian market specifically, where Disney+ Hotstar's regional catalog is often under-represented in Western-built comparison tools.

## 3. Research and Validation

This discovery phase drew on:
- Direct problem articulation from the founding use case (personal frustration with cross-referencing ratings and platform availability)
- Persona construction across three representative user types (budget-conscious student, time-starved professional, regional-content seeker)
- A journey mapping exercise tracing the current, broken discovery flow end-to-end

**Limitation, stated plainly:** no formal user interviews or surveys were conducted before or during build. This remains a solo/founder-led case study grounded in direct personal experience of the problem, not field-validated research. That's an honest constraint of this project as a portfolio piece, and it directly informs why "measure real usage" (Section 8) is now the top priority rather than adding more features on an unvalidated foundation.

## 4. Key Findings and Build Validation

| # | Original Finding | Held Up? | Build-Time Outcome |
|---|---|---|---|
| 1 | The core inefficiency is fragmentation, not lack of content. Users struggle to evaluate quality and access in one place, not to find things to watch | Held up | Still the core thesis; nothing in build changed this |
| 2 | Rating trust is split across sources; no persona relies on a single one, so any solution needs to aggregate | Held up, extended | A third source, Metacritic, was added beyond the original two (IMDb, Rotten Tomatoes) once OMDb's response was found to already include it at no extra integration cost |
| 3 | Platform availability is the final, most time-costly step, checked last, after research is already sunk | Held up | Confirmed technically the hardest part to get right: Watchmode splits availability into a separate API endpoint from title details, which caused a real bug (all titles briefly showing as unavailable everywhere) before it was caught and fixed |
| 4 | Regional content is underserved by existing tools; Hotstar's catalog is a defensible gap to fill | Partially held up | Hotstar is a first-class platform and a region-selector infrastructure now exists, but a genuine origin/language filter, what this finding is really asking for, is still not built (see `01-user-personas.md`, Persona 3) |
| 5 | Movies and series need separate treatment; time-starved users want to filter by format early | Held up | Implemented as a top-level toggle, exactly as the finding predicted |

## 5. Target Users

See `01-user-personas.md` for full detail, including a needs matrix and per-persona shipped-status breakdown. Summary:

| Persona | Core Need | Shipped Status |
|---|---|---|
| Budget Juggler (primary) | One-glance rating and availability match against limited subscriptions | Fully served |
| Time-Starved Professional | Fast, trustworthy shortlist, no browsing required | Fully served (was blocked by a default-sort gap, now fixed) |
| Regional Content Seeker | Origin/language visibility alongside credible ratings | Partially served; biggest remaining gap |

## 6. Opportunity Statement

There is an opportunity to build a genre-based discovery tool whose hero feature, a single comparison view showing rating (aggregated from trusted sources), OTT platform availability, and format (movie/series), with origin/language as a future opportunity, directly collapses the three-step research process users currently perform manually. This is not a recommendation engine; it is a **decision-support tool** that respects the user's existing subscriptions rather than pushing new ones. This framing has not changed since the original discovery phase and remains the product's core identity.

## 7. Competitive Landscape

Tools like JustWatch already address platform-availability comparison at a broad, global scale. This product's differentiation is narrower and more defensible for a portfolio project:

| Product | Strength | Gap CineCompass Targets |
|---|---|---|
| JustWatch | Availability | Less focused on the ratings-plus-availability decision moment; not built around regional (Hotstar) depth |
| IMDb | Ratings and discovery | Doesn't combine availability with ratings; no platform-filtering workflow |
| CineCompass | Combined decision support | N/A |

| Differentiator | Original Plan | Shipped |
|---|---|---|
| Rating aggregation | IMDb + Rotten Tomatoes | IMDb + Rotten Tomatoes + Metacritic |
| Platform coverage | Netflix, Prime, Hotstar (3) | Netflix, Prime, Hotstar, Apple TV+, Max (5) |
| Regional depth | Hotstar treated as first-class, not an afterthought | Hotstar first-class; region-selector infrastructure added; origin/language filter still open |

## 8. Success Metrics and Measurement Plan

| Metric Type | Metric | Instrumented in Production? |
|---|---|---|
| North Star (candidate) | Time from `genre_selected` to a defined selection event (`watch_link_clicked` or `added_to_watchlist`) | Events fire in code as of 2026-08-06; not yet collected in production |
| Leading | Genre searches per session | Events fire in code; not yet collected in production |
| Leading | Table sort/filter interactions | Events fire in code; not yet collected in production |
| Lagging | Return usage rate | No |
| Lagging | Session-to-selection completion rate | Events fire in code; not yet collected in production |

**Status, stated directly:** the metrics in this report originally had a deeper problem than missing instrumentation. "Selection" was never actually defined, so even with analytics switched on, there would have been no way to know what to measure. That's now fixed: selection means one of two named events (see `04-product-strategy-mvp.md`, Section 4, and `05-prd.md`, Section 6 for full detail), and the underlying `track()` calls exist in code. What's still missing is enabling Vercel Web Analytics in the dashboard, so nothing is actually being collected in production yet. The product has shipped and functionally works, but the discovery report's own success criteria remain unproven by data. This is still the single most important open item across the entire document suite, ranked above any unbuilt feature.

## 9. Recommendation and Next Steps

At the time this report was originally written, the recommendation was to proceed through Epic 2 (Strategy & MVP) and Epic 3 (PRD). Both happened, and the product has since gone further, through Epics 5 to 7 (build and an informal QA/bug-fix pass) and a soft Epic 8 (deployed to production, analytics wired but inactive).

**Revised recommendation:** the next step isn't a new phase or a new feature. It's closing the loop this report opened. Specifically, in priority order:

1. Enable Vercel Web Analytics and start collecting real usage data against the North Star Metric this report proposed.
2. Once baseline data exists, decide whether the origin/language filter gap (Section 4, Finding 4) is worth building based on actual usage patterns rather than assumption.
3. Only after 1 and 2 are underway, consider expanding platform/rating-source coverage further. The current set already exceeded the original plan once without user-feedback validation driving that decision.

---

*Supporting documents: `01-user-personas.md`, `02-user-journey-map.md`*
