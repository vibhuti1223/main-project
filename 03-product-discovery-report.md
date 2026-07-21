# Product Discovery Report

**Project:** OTT Comparison & Discovery Platform
**Phase:** Epic 1 — Product Discovery
**Prepared by:** Product Team

---

## 1. Problem Statement

Users looking to watch a movie or series must currently piece together their decision from multiple disconnected sources: genre-based "best of" lists, trusted rating sites (IMDb, Rotten Tomatoes), and individual platform searches to confirm availability. This fragmented process costs users significant time and frequently ends in disappointment when a well-rated title turns out not to be available on the platform they've already subscribed to.

## 2. Background & Context

Streaming subscriptions have multiplied, but discovery tools haven't kept pace with cross-platform fragmentation. Most users don't subscribe to every platform — they typically hold 1–3 subscriptions and must decide, title by title, whether something is worth watching *and* whether it's accessible to them at all. The result is a two-part decision problem (quality + availability) that no single existing tool answers well for the Indian market specifically, where Disney+ Hotstar's regional catalog is often under-represented in Western-built comparison tools.

## 3. Research Approach

This discovery phase drew on:
- Direct problem articulation from the founding use case (personal frustration with cross-referencing ratings and platform availability)
- Persona construction across three representative user types (budget-conscious student, time-starved professional, regional-content seeker)
- A journey mapping exercise tracing the current, broken discovery flow end-to-end

*Note: If formal user interviews or surveys are conducted in a later iteration, they should be appended here with direct findings — this strengthens the case study's credibility for a PM portfolio.*

## 4. Key Findings

1. **The core inefficiency is fragmentation, not lack of content.** Users aren't struggling to find things to watch — streaming catalogs are large. They're struggling to evaluate quality and access in one place.
2. **Rating trust is split across sources.** No persona relies on a single rating source; IMDb and Rotten Tomatoes are both referenced, meaning any solution needs to aggregate rather than pick one.
3. **Platform availability is the final, most time-costly step.** Every persona described checking availability *last*, after already investing time in genre and rating research — meaning it's currently the single biggest point of wasted effort and drop-off.
4. **Regional content is underserved by existing tools.** Competitor tools (e.g., JustWatch) are built around Western platform ecosystems and don't give Hotstar's regional catalog equal visibility — this is a specific, defensible gap for this product to fill in the Indian market.
5. **Movies and series need separate treatment.** Time-starved users in particular want to filter by format early, not sort through a mixed list.

## 5. Target Users

See `01-user-personas.md` for full detail. Summary:

| Persona | Core Need |
|---|---|
| Budget Juggler (primary) | One-glance rating + availability match against limited subscriptions |
| Time-Starved Professional | Fast, trustworthy shortlist — no browsing required |
| Regional Content Seeker | Origin/language visibility alongside credible ratings |

## 6. Opportunity Statement

There is an opportunity to build a genre-based discovery tool whose hero feature — a single comparison table showing rating (aggregated from trusted sources), OTT platform availability (Netflix, Prime, Hotstar), format (movie/series), and origin — directly collapses the three-step research process users currently perform manually. This is not a recommendation engine; it is a **decision-support tool** that respects the user's existing subscriptions rather than pushing new ones.

## 7. Competitive Landscape (Brief)

Tools like JustWatch already address platform-availability comparison at a broad, global scale. This product's differentiation is narrower and more defensible for a portfolio project:
- Aggregated trust-scoring (IMDb + Rotten Tomatoes shown together, not one or the other)
- Deliberate focus on the three most-used platforms in the target market rather than exhaustive global coverage
- First-class treatment of Disney+ Hotstar's regional catalog, rather than treating it as a secondary/Western-platform afterthought

## 8. Success Metrics (Preliminary — to formalize in Epic 2 Strategy phase)

- **North Star Metric (candidate):** Time from search to selection (target: reduce vs. baseline manual cross-checking time)
- **Leading indicators:** Genre searches per session, table sort/filter interactions
- **Lagging indicators:** Return usage rate, session-to-selection completion rate

## 9. Recommendation & Next Steps

Proceed to **Epic 2 — Product Strategy & MVP Planning**, using these findings to:
- Finalize the MVP scope around the comparison table as the hero feature
- Formalize success metrics and North Star Metric
- Begin translating personas and journey map pain points into PRD requirements (Epic 3)

---

*Supporting documents: `01-user-personas.md`, `02-user-journey-map.md`*
