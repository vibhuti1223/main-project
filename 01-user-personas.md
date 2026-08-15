# User Personas: CineCompass

| | |
|---|---|
| **Project** | CineCompass (OTT Comparison & Discovery Platform) |
| **Phase** | Epic 1: Product Discovery |
| **Prepared By** | Vibhuti Gupta |
| **Status** | v2.1, Live |
| **Last Updated** | 2026-08-06 |
| **Related Docs** | `02-user-journey-map.md`, `03-product-discovery-report.md` |

---

## Table of Contents

1. [Purpose of This Document](#1-purpose-of-this-document)
2. [Persona 1: The Budget Juggler](#2-persona-1-the-budget-juggler-primary-persona)
3. [Persona 2: The Time-Starved Professional](#3-persona-2-the-time-starved-professional-secondary-persona)
4. [Persona 3: The Regional Content Seeker](#4-persona-3-the-regional-content-seeker-secondary-persona)
5. [Cross-Persona Needs Matrix](#5-cross-persona-needs-matrix)
6. [Cross-Persona Insight](#6-cross-persona-insight)
7. [Open Gaps by Persona](#7-open-gaps-by-persona)

---

## 1. Purpose of This Document

These personas represent the primary user types CineCompass is designed for. They're built from the core pain point driving the project: **fragmented decision-making across genre search, ratings, and platform availability.** Each persona below is followed by a section grounding it in what's actually live at cinecompass-app.vercel.app, so this document functions as a real reference for design and roadmap decisions, not just an artifact from the discovery phase.

---

## 2. Persona 1: "The Budget Juggler" (Primary Persona)

| Attribute | Detail |
|---|---|
| **Name** | Ananya Sharma |
| **Age** | 22 |
| **Occupation** | College student |
| **OTT Subscriptions** | 1 to 2 at a time (rotates based on what's "worth it" that month) |
| **Persona Priority** | Primary |

### Background
Ananya doesn't have unlimited subscriptions. She shares a Netflix account with roommates and has Amazon Prime mainly for the shopping benefits. She's price-conscious and hates the feeling of "wasting" a subscription month scrolling without finding anything good.

### Goals
- Find a highly-rated movie/series quickly, without opening five tabs
- Know before she commits to watching whether it's on a platform she already has
- Avoid subscribing to a new platform just for one title

### Frustrations
- Rating sites (IMDb, Rotten Tomatoes) don't tell her platform availability
- Platform apps don't show trusted external ratings, just their own algorithm
- She's been burned before: finished reading about a movie, opened the app, and it wasn't there

### Behaviors
- Checks IMDb/Rotten Tomatoes before watching
- Switches between OTT apps to verify availability
- Often abandons a title after discovering it's unavailable

### Tech Comfort
High. Comfortable navigating multiple apps and websites, but wants friction removed, not more steps.

### Needs
One screen where genre, rating, and platform availability show up together, sorted so the best option surfaces first without her having to think about it.

### How the Shipped Product Serves Her

| Need | Shipped Behavior |
|---|---|
| Platform-first filtering | One-tap pills for Netflix, Prime, Hotstar, Apple TV+, and Max (5 platforms, up from the 3 originally planned) |
| Trusted, aggregated ratings | IMDb, Rotten Tomatoes, and Metacritic shown per title |
| Best-option-first by default | **Now resolved.** Comparison view defaults to IMDb rating, high to low. This was a known gap as of the previous revision of this document and has since been fixed |
| Not losing a good option she can't watch right now | A watchlist (Want to Watch / Watching / Watched, plus optional personal star rating). Not in the original MVP scope, added because it directly serves this exact goal |

**Net assessment:** this persona's needs are now the most fully served of the three. Every goal listed above maps to a shipped, working feature.

---

## 3. Persona 2: "The Time-Starved Professional" (Secondary Persona)

| Attribute | Detail |
|---|---|
| **Name** | Rohan Mehta |
| **Age** | 31 |
| **Occupation** | Working professional, long hours |
| **OTT Subscriptions** | Netflix + Disney+ Hotstar (through a family plan) |
| **Persona Priority** | Secondary |

### Background
Rohan has maybe 45 minutes to an hour some evenings before he's too tired to care. He doesn't want to "browse"; browsing itself feels like a chore. He wants a shortlist, not an infinite scroll.

### Goals
- Get a short, ranked list of genuinely good options fast
- Trust the ratings shown (has been misled by platform-native "recommended for you" rows before)
- Not waste his limited free time on research instead of watching

### Frustrations
- Platform algorithms push new/sponsored content over genuinely well-rated content
- Doesn't have time to cross-check IMDb and Rotten Tomatoes manually every time
- Series vs. movie mixed together in most apps makes browsing slower when he only has time for a movie

### Behaviors
- Glances at the aggregate rating rather than reading full reviews
- Picks from a platform's "recommended for you" row when short on time, despite not trusting it
- Rewatches a familiar title if deciding what's new takes too long

### Tech Comfort
Moderate. Wants simplicity over customization.

### Needs
Fast genre-to-sorted-by-rating table, clearly split into Movies vs. Series, so he can decide in under two minutes.

### How the Shipped Product Serves Him

| Need | Shipped Behavior |
|---|---|
| Movies/Series split | Top-level type toggle (All / Movies / TV Series), one tap, exactly as scoped |
| Ranked-by-rating by default | **Now resolved.** Previously the table defaulted to popularity, requiring Rohan to manually change the sort dropdown, the exact extra step he doesn't have time for. This has been fixed so IMDb-rating-descending is now the default on every fresh load |
| Fast decision under time pressure | Genre filter, platform pills, and default rating sort now combine so his entire path is: land, pick genre, pick platform, done, with no manual re-sorting required |

**Net assessment:** this was the persona most directly hurt by the previous default-sort gap. With that fixed, his core workflow now matches what was designed for him from the start.

---

## 4. Persona 3: "The Regional Content Seeker" (Secondary Persona)

| Attribute | Detail |
|---|---|
| **Name** | Priya Nair |
| **Age** | 27 |
| **Occupation** | Marketing executive |
| **OTT Subscriptions** | Disney+ Hotstar (primary), occasionally Prime |
| **Persona Priority** | Secondary |

### Background
Priya enjoys a mix of regional-language content and international titles. Origin of content matters to her; she often specifically wants to know if something is Korean, Indian regional cinema, or Hollywood before deciding.

### Goals
- Filter/see content origin alongside ratings and platform info
- Discover well-rated regional content that doesn't always surface in Western-focused recommendation tools
- Compare a title's popularity across trusted rating sources, since regional titles are sometimes under-rated on one platform and not another

### Frustrations
- Most comparison tools (like existing platform-availability tools) are built around Western content and under-serve regional platforms
- Hard to find one place that respects both Hotstar's regional catalog and global rating credibility

### Behaviors
- Searches separately for a title's country/language of origin before deciding whether it interests her
- Checks Hotstar's catalog on its own, since regional titles are often missing from broader comparison tools
- Cross-references a regional title's rating across sources more carefully, since it's more likely to be under-rated on one platform than a Hollywood title

### Tech Comfort
High.

### Needs
Origin/language visibility built into the same table, not treated as an afterthought.

### How the Shipped Product Serves Her (and Where It Still Falls Short)

| Need | Status |
|---|---|
| Hotstar's regional catalog treated as first-class | **Shipped.** Hotstar is one of five platforms with full live availability data, not a secondary integration |
| Region-aware availability | **Shipped, narrow.** A region selector exists in the filter bar and streaming data is fetched per-region rather than hardcoded, but only India is live today; the control is built to extend, not yet exercised |
| Genuine origin/language filter (e.g., filter by "Korean" or "Tamil cinema") | **Not shipped.** A content-rating/"International" label is shown per title (and a real bug, where a language code was mislabeled as a country, has been fixed), but there is no way to actually filter results by origin. This is the one core need from this persona that remains unmet. |

**Net assessment:** this persona's needs are the least served of the three. The region selector is real progress, but the specific ask, filtering by content origin, hasn't been built. This should be the top candidate for the next feature cycle if user validation confirms it matters.

---

## 5. Cross-Persona Needs Matrix

| Need | Budget Juggler | Time-Starved Professional | Regional Content Seeker | Shipped? |
|---|:---:|:---:|:---:|---|
| Platform availability visible inline | Primary need | Supporting need | Supporting need | **Yes** (5 platforms) |
| Aggregated, trusted ratings | Primary need | Primary need | Supporting need | **Yes** (IMDb + RT + Metacritic) |
| Default sort surfaces best option first | Supporting need | Primary need | N/A | **Yes** (fixed to IMDb, descending) |
| Movies/Series segmentation | N/A | Primary need | N/A | **Yes** |
| Save-for-later without deciding now | Primary need | N/A | N/A | **Yes** (watchlist) |
| Origin/language filter | N/A | N/A | Primary need | **No** (open gap) |
| Region-specific availability | N/A | N/A | Supporting need | **Partial** (India only) |

---

## 6. Cross-Persona Insight

All three personas hit the same wall despite different contexts: **the research is scattered across genre, rating, and platform-availability sources, and the cost of that scatter is time.** This is the shared problem the comparison view is designed to solve. It's not a "nice to have" feature, it's the direct answer to the friction every persona independently describes.

What's changed since the personas were first written: the product now sources live data (Watchmode for discovery/availability, OMDb for ratings, TVMaze for TV search) instead of a fixed catalog, which means the "well, is this data even current" skepticism baked into all three personas' frustrations is now actually addressed at the architecture level, not just promised in the vision doc.

---

## 7. Open Gaps by Persona

| Persona | Gap | Priority for Next Cycle |
|---|---|---|
| Regional Content Seeker | No real origin/language filter | High. This is her one unmet primary need |
| Regional Content Seeker | Region selector only supports India | Medium. Expected to grow, not urgent while the target market is India-first |
| All personas | North Star Metric (search-to-selection time) not yet measured. Can't confirm any persona's experience is actually faster in practice, only that the features exist | High. This affects confidence in every claim above |
