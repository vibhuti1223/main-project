# Product Requirements Document (PRD): CineCompass

| | |
|---|---|
| **Project** | CineCompass (OTT Comparison & Discovery Platform) |
| **Phase** | Epic 3: Product Requirements Document |
| **Prepared By** | Vibhuti Gupta |
| **Builds On** | `03-product-discovery-report.md`, `04-product-strategy-mvp.md` |
| **Status** | v2.3, Live, Post-Build |
| **Last Updated** | 2026-08-06 |
| **Live URL** | cinecompass-app.vercel.app |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Product Scope](#2-product-scope)
3. [User Stories](#3-user-stories)
4. [Functional Requirements](#4-functional-requirements)
5. [Acceptance Criteria: Key Requirements](#5-acceptance-criteria-key-requirements)
6. [Non-Functional Requirements](#6-non-functional-requirements)
7. [Success Metrics](#7-success-metrics)
8. [Open Questions: Status](#8-open-questions-status)
9. [Change Log Summary](#9-change-log-summary)

---

## 1. Executive Summary

Users currently spend excessive time deciding what to watch because the information they need is split across three disconnected sources: genre-based discovery, trusted rating sites (IMDb, Rotten Tomatoes), and individual OTT platform searches to confirm availability. CineCompass solves this by presenting a genre-filtered comparison view showing ratings, live platform availability, format (movie/series), and content details, for every title, in one place, sorted so the best option is visible without any manual step.

**What changed since v1.0:** the build shipped with a wider scope than originally planned in most areas: five platforms instead of three, three rating sources instead of two, and a watchlist that wasn't originally in MVP scope. One requirement (FR-04, default sort by rating) briefly fell short, shipping with a default of popularity, but this has now been corrected, and the requirement is fully met as of this revision.

The core hypothesis, that collapsing multi-source research into a single, pre-sorted view meaningfully reduces decision time, **has not yet been measured, though the path to measuring it is now built.** Analytics events for genre selection, sort/filter changes, and both conversion paths (clicking through to watch, or saving to the watchlist) were added on 2026-08-06 (FR-17). What's still open: production data collection needs to be switched on before any of it is actually collected, and the North Star Metric itself (a time delta between two named events) has to be computed from raw data rather than read directly off a dashboard. This remains the most important open item in this document, ahead of any unbuilt feature.

---

## 2. Product Scope

### 2.1 In Scope (Live)

| Area | Detail |
|---|---|
| Discovery | Genre-based search and filtering across 13 genres plus "All" |
| Format | Movies and Series as separate, explicitly segmented sections |
| Comparison view | Per title: title, genre, format, content rating, IMDb, Rotten Tomatoes, and Metacritic ratings, availability across Netflix, Amazon Prime, Disney+ Hotstar, Apple TV+, and Max |
| Sorting | Manual sort dropdown (rating sources, release year); **default is IMDb rating, descending** |
| Filtering | One-click platform pills, minimum-rating slider, release-year slider |
| Region | Region selector (India live today, built to extend) |
| Watchlist | Want to Watch / Watching / Watched statuses, optional personal 1 to 5 star rating; not originally in MVP scope |
| Responsiveness | Desktop and mobile browser, not a native app |
| Resilience | Offline-fallback mode with a visible banner when live data sources are unreachable |

### 2.2 Out of Scope (Still True)
- User accounts, login, or authentication
- Personalized recommendations or watch history beyond the self-managed watchlist
- Social/sharing features
- Additional OTT platforms/rating sources beyond what's listed above, a soft boundary since it already moved once
- Native mobile applications
- Multi-language UI (interface is English-only; content origin/language is metadata, not a UI localization feature, and there's still no dedicated origin/language filter, see FR-07)

### 2.3 Scope Boundary Rationale
Every in-scope item maps directly to collapsing the three-step research process identified in discovery (genre, then rating, then availability). The watchlist is the one addition that doesn't map directly to that original workflow. It was added because build-time testing surfaced a related but distinct need: sometimes the right outcome isn't "decide now," it's "don't lose this option." Worth validating with real users rather than assuming it was the right call.

---

## 3. User Stories

Core user stories the product is built to satisfy. Kept short and central rather than exhaustive.

- **US-01:** As an OTT subscriber, I want to filter titles by genre so that I can quickly narrow down what to watch.
- **US-02:** As an OTT subscriber, I want to compare ratings and platform availability in one view so that I don't have to cross-check multiple websites.
- **US-03:** As a user, I want to filter by my subscribed platform so that I only see titles I can actually watch.
- **US-04:** As a user, I want results sorted by rating by default so that the best option is easy to spot without an extra step.
- **US-05:** As a user, I want to save a title for later so that I don't lose track of something good I don't have time for right now.

### 3.1 User Story to Requirement Mapping

| ID | User Story | Requirement |
|---|---|---|
| US-01 | Filter by genre | FR-01 |
| US-02 | Compare ratings & availability in one view | FR-03 |
| US-03 | Filter by subscribed platform | FR-12 |
| US-04 | Default sort by rating | FR-04 |
| US-05 | Save title for later | FR-14 |

---

## 4. Functional Requirements

| ID | Requirement | Priority | Status |
|---|---|---|---|
| FR-01 | Genre-based search | P0 | Shipped |
| FR-02 | Format segmentation (Movies/Series toggle) | P0 | Shipped |
| FR-03 | Comparison view display (title, ratings, availability) | P0 | Shipped, exceeded scope |
| FR-04 | Default sort by rating, high to low | P0 | **Shipped.** Corrected 2026-08-06; default is now IMDb rating, descending |
| FR-05 | Manual sort controls | P1 | Shipped |
| FR-06 | Platform filter (dropdown/selection) | P1 | Shipped, as one-click pills rather than a dropdown (superseded by FR-12) |
| FR-07 | Origin/language display | P1 | Partially shipped |
| FR-08 | No-results handling | P1 | Shipped |
| FR-09 | Title detail view | P1 | Shipped |
| FR-10 | Data freshness indicator | P2 | Not shipped |
| FR-11 | Timeline/release-year filter | P1 | Shipped |
| FR-12 | One-click platform icon filter | P1 | Shipped |
| FR-13 | Inline trailer preview | P1 | Shipped, with a caveat |
| FR-14 (new) | Watchlist | N/A | Shipped, not in original PRD |
| FR-15 (new) | Region selector | N/A | Shipped, not in original PRD |
| FR-16 (new) | Offline-fallback banner | N/A | Shipped, not in original PRD |
| FR-17 (new) | Analytics event tracking | N/A | Shipped 2026-08-06. Events implemented for genre selection, sort/filter changes, and both conversion paths (watch-through, save-for-later), giving the North Star and leading metrics in Section 7 something to actually measure. Production data collection still needs to be switched on; see Section 7 |

**Summary:** 13 of 16 requirements fully shipped, 1 partially shipped (FR-07), 1 not shipped (FR-10, low priority), and 3 shipped beyond original scope.

---

## 5. Acceptance Criteria: Key Requirements

Detailed acceptance criteria below cover the P0 requirements and the P1 requirements with the most significant plan-vs-build gaps. Not every FR has a detailed entry here; the rest are covered by the status column in Section 4.

### FR-01: Genre-based search
- **Given** a user lands on the homepage
- **When** they select a genre
- **Then** the system returns only titles matching that genre, split by Movies/Series
- **Status:** Met

### FR-03: Comparison view display
- **Given** genre results are returned
- **When** the view renders
- **Then** every row shows rating (IMDb, Rotten Tomatoes, and Metacritic), platform availability across 5 platforms, and content details
- **Status:** Met, exceeded scope (2 extra platforms, 1 extra rating source vs. plan)

### FR-04: Default sort by rating
- **Given** the comparison view has loaded
- **When** no manual sort has been applied
- **Then** titles appear ordered from highest IMDb rating to lowest
- **Status:** Met as of 2026-08-06. Prior to this fix, the default was popularity, flagged as the clearest gap in the previous revision of this PRD. Default sorting was corrected to IMDb rating, descending.

### FR-07: Origin/language display
- **Given** a title is shown in the comparison view or detail modal
- **When** a user looks for its origin/language
- **Then** a content-rating/"International" label is visible
- **Status:** Partially met. Display exists; a true origin/language filter (the actual requirement, and the specific need described by the Regional Content Seeker persona) does not. Worth noting precisely: the "International" label is not a per-title lookup, it's a fixed placeholder applied to every title, so there's no real origin data behind it yet.

### FR-11: Timeline/release-year filter
- **Given** a user has selected a genre
- **When** they set a release-year filter
- **Then** the view shows only titles matching both genre and year, with the default rating sort still applied within those results
- **Status:** Met, implemented as a single "released after year X" slider rather than a two-sided range

### FR-12: One-click platform icon filter
- **Given** the comparison view is displayed with platform icons visible
- **When** a user clicks a specific platform's icon
- **Then** the view instantly filters to that platform, combining with existing genre/year filters rather than resetting them
- **Status:** Met

### FR-13: Inline trailer preview
- **Given** a user clicks a title
- **When** the detail view opens and a trailer exists
- **Then** it plays within the same view, with filters preserved on close
- **Status:** Met for titles with an available trailer; honest empty state for titles without one (previously this silently played the wrong movie's trailer as a fallback, fixed earlier in the build)

---

## 6. Non-Functional Requirements

| ID | Category | Requirement | Status |
|---|---|---|---|
| NFR-01 | Performance | Comparison view loads within 2 to 3 seconds under typical conditions | Not formally benchmarked |
| NFR-02 | Data Accuracy | Availability/rating data refreshed on a defined schedule | Exceeded. Fetched live per-request with a visibly flagged fallback dataset |
| NFR-03 | Responsiveness | Usable on desktop and mobile browser widths | Shipped, including a dedicated mobile-responsive redesign of the comparison table |
| NFR-04 | Scalability | Data layer allows additional platforms/sources without a full rebuild | Validated in practice. Platforms went from 3 to 5, rating sources from 2 to 3, with no architecture change |
| NFR-05 | Availability/Uptime | Reasonable uptime for a portfolio-stage MVP | Shipped. Live in production, no known prolonged outages, no formal monitoring |
| NFR-06 | Privacy/Compliance | Analytics must avoid collecting PII without disclosure | Not yet applicable. Analytics integrated but not enabled, so no data collection either way |
| NFR-07 | Maintainability | Codebase/schema documented for a small team to extend | Weak. No formal docs beyond this suite, and the project is not under version control |
| NFR-08 | Accessibility (baseline) | Readable contrast, semantic markup | Exceeded baseline. Aria-labels, consistent modal keyboard handling, skip-to-content link. Full focus-trapping inside modals is a known, named gap. |

---

## 7. Success Metrics

*(Carried forward from Epic 2, see `04-product-strategy-mvp.md` for full detail and the definitional critique behind these changes)*

"Title selection" is no longer a vague phrase. It's defined as either of two tracked events: clicking through to actually watch, or saving the title to the watchlist for later. A session with neither event did not result in a selection.

### 7.1 Metric Hierarchy

```
North Star
    ↓
Leading Metrics
    ↓
Lagging Metrics
    ↓
Guardrails
```

### 7.2 Metrics and Instrumentation Status

| Metric | Instrumented? |
|---|---|
| North Star: Median time from genre selection to a selection event | Events fire (FR-17); the time-delta calculation itself still needs to be pulled from raw data, not read off a dashboard |
| Leading: Genre searches per session, sort/filter interaction rate | Events fire (FR-17) |
| Leading: Bounce rate on the comparison view | Not instrumented. Flagged as unreliable read alone: a fast exit can mean "found it immediately" or "found nothing," the same number for opposite outcomes. Must be read alongside completion rate, never by itself |
| Lagging: Return usage rate | No |
| Lagging: Session-to-selection completion rate | Events fire; the rate calculation is manual |
| Guardrail: API proxy error rate | No. Replaces the original "data accuracy rate," which had no defined way to actually be measured |
| Guardrail: Page load time | Not benchmarked |

The honest state of this section: the events needed to compute the North Star Metric and the leading/lagging metrics now exist. What's still missing is (1) switching on production data collection so the events are actually gathered, and (2) a process for turning raw event counts into the actual rates and time deltas these metrics describe, since neither of those happens automatically. Shipping further requirements without closing this gap still risks optimizing blind.

---

## 8. Open Questions: Status

| Question | Status |
|---|---|
| What data source(s) will supply platform availability reliably? | Resolved. Three live data providers, proxied through a server-side layer so API keys stay out of the browser |
| Should "availability" be binary or include rental vs. subscription-included info? | Open, correctly deferred |
| Can IMDb/Rotten Tomatoes data be sourced within budget/legal constraints? | Resolved. The ratings provider's free tier covers IMDb, Rotten Tomatoes, and Metacritic |
| Should FR-06 (dropdown) and FR-12 (icon filter) both ship? | Resolved. FR-12 alone shipped |
| What's a reliable trailer source? | Resolved, with a caveat. Sourced per title from the discovery provider or the bundled dataset; no dedicated trailer-search fallback, so coverage is inconsistent by design |
| Should the default sort be rating or popularity? | Resolved 2026-08-06. Rating (IMDb, descending), matching FR-04 as originally written |
| Is the API proxy layer rate-limited? | Open. No rate limiting exists yet; low risk at current traffic, worth fixing before wider distribution |
| Is the project under version control? | Open. No repository exists yet; recommended before further iteration |

---

## 9. Change Log Summary

Two things shipped in this revision cycle:

1. **FR-04 (default sort) moved from "Not Met" to "Met."** Default sorting was corrected to IMDb rating, descending.
2. **FR-17 (analytics event tracking) added.** Events were implemented for genre selection, sort/filter changes, and both conversion paths (clicking through to watch, or saving to the watchlist), which together now define "selection" for the North Star Metric (Section 7).

Both changes close gaps identified in prior revisions: FR-04 was the clearest plan-vs-build mismatch, and FR-17 responds to a critique that the original success metrics were carried forward from v1.0 without being re-examined and had real definitional problems (an undefined "selection" event, a bounce-rate metric that can't distinguish success from failure, and a "data accuracy rate" guardrail with no way to actually compute it).

File names, function names, and other implementation-level detail behind these two changes are intentionally not repeated here; that documentation lives in the project's engineering notes and codebase, not in this PRD.

---

*This PRD is a living status document. Recommended next revision trigger: after production data collection is enabled and the North Star Metric has real data behind it for the first time.*
