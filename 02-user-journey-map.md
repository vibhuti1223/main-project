# User Journey Map: CineCompass

| | |
|---|---|
| **Project** | CineCompass (OTT Comparison & Discovery Platform) |
| **Phase** | Epic 1: Product Discovery |
| **Prepared By** | Vibhuti Gupta |
| **Primary Persona Mapped** | Ananya Sharma ("The Budget Juggler"), see `01-user-personas.md` |
| **Scenario** | Ananya has a free evening and wants to watch a highly-rated thriller series, but isn't sure it'll be on a platform she already subscribes to |
| **User Goal** | Find a highly-rated thriller series available on an existing OTT subscription with minimal search effort |
| **Status** | v2.1, Live |
| **Last Updated** | 2026-08-06 |

---

## Table of Contents

1. [Journey Overview](#1-journey-overview)
2. [Stage-by-Stage Detail](#2-stage-by-stage-detail)
3. [Emotional Arc: Current (Broken) Experience](#3-emotional-arc-current-broken-experience)
4. [Emotional Arc: With CineCompass](#4-emotional-arc-with-cinecompass)
5. [Key Takeaways for Product Design](#5-key-takeaways-for-product-design)
6. [What Changed From the Original Map](#6-what-changed-from-the-original-map)

---

## 1. Journey Overview

| Stage | Stage 1: Trigger | Stage 2: Search | Stage 3: Cross-Check | Stage 4: Platform Reality Check | Stage 5: Decision | Stage 6A: Watch (Current) | Stage 6B: Watch (With CineCompass) |
|---|---|---|---|---|---|---|---|
| **Actions** | Wants to watch something tonight | Googles "best thriller series 2026" | Opens IMDb / Rotten Tomatoes to verify ratings on shortlisted titles | Searches "[Title] Netflix" or "[Title] available on" for each title | Has spent 15 to 20 min, still hasn't picked | Either gives up and rewatches something old, or finally finds one, often not on her platform | Opens the app, filters by Thriller and her platform; the table is already sorted by IMDb rating on load, so the best option is first, not something she has to dig for |
| **Thoughts** | "I want something good, not another mediocre pick" | "There are too many 'best of' lists, which one is even reliable?" | "Okay this one's rated well, but is it on something I have?" | "Ugh, not on Netflix. Let me check the next one." | "Why does this take so long just to start watching?" | "Fine, I'll just watch something I've already seen." | "The top result is already on Prime and rated well, and I saved two others for later instead of losing track of them." |
| **Emotions** | Curious, hopeful | Mildly optimistic | Slightly annoyed, this is the 3rd tab now | Frustrated, repetitive fatigue setting in | Tired, deflated | Disappointed / resigned | Relieved, in control, with no anxiety about "losing" a good option she doesn't have time for tonight |
| **Pain Points** | N/A | Generic "best of" lists aren't personalized by genre in one place | Ratings live on separate sites from availability info | No single source cross-references rating and platform | Decision fatigue is entirely avoidable; it's a data-fragmentation problem, not a taste problem | Time lost, mild subscription regret ("why do I even pay for this if I can't find anything") | N/A |
| **Opportunities** | Prompt genre selection immediately | Centralize genre-based discovery | Pull IMDb and Rotten Tomatoes (plus now Metacritic) into the same view | Show OTT availability inline, not as a separate search | Sort by rating automatically so the "best" option is visually first, not buried; let the user act on a decision later without losing it | N/A | This is the target end-state the product now delivers |

---

## 2. Stage-by-Stage Detail

### Stage 1: Trigger
Ananya has free time and the intent to watch something, but no title in mind yet. Nothing about this stage is a product problem; it's the starting condition every downstream stage either compounds or resolves.

### Stage 2: Search
She turns to generic "best of" lists because there's no single, personalized starting point. **Shipped resolution:** landing directly on a genre-filterable, platform-filterable comparison view replaces the "best of" list search entirely, so she never needs to leave the app to start this stage.

### Stage 3: Cross-Check
Historically the most tab-heavy stage: opening IMDb, then Rotten Tomatoes, per shortlisted title. **Shipped resolution:** all three rating sources (IMDb, Rotten Tomatoes, Metacritic) render in the same row as the title, with no click-through required to see them.

### Stage 4: Platform Reality Check
Previously the single most time-costly step, per the discovery report's key findings, checked last, after time was already sunk into stages 2 and 3. **Shipped resolution:** platform availability is fetched and displayed inline per title, in the same row as its rating and genre.

### Stage 5: Decision
The compounding cost of stages 2 through 4 run manually. **Shipped resolution:** by collapsing stages 2 through 4 into one filtered, pre-sorted view, this stage is designed to not exist in the new flow. Whether it actually doesn't, meaning whether real users reach a decision meaningfully faster, is the one claim in this document that hasn't been measured yet (see Section 6 and the PRD's success metrics).

### Stage 6A: Watch (Current)
The failure mode: give up and rewatch something old, or land on a title that isn't accessible after all.

### Stage 6B: Watch (With CineCompass)
The intended resolution is reaching a confident pick fast. **Extended beyond the original map:** a second valid resolution now exists, saving a strong option to the watchlist instead of committing tonight. The original map only had one "success" ending; the shipped product has two.

---

## 3. Emotional Arc: Current (Broken) Experience

```
Curious → Optimistic → Annoyed → Frustrated → Fatigued → Deflated
   ▲                                                          │
   └──────────────── (repeats next time) ────────────────────┘
```

This is still the accurate "before" state for anyone not using the product, unchanged from the original mapping exercise.

## 4. Emotional Arc: With CineCompass

```
Curious → Genre/Platform Filter → Pre-Sorted Comparison View → Relieved / Confident Decision → Watch (or Save for Later) → Watching
```

The "Save for Later" branch is the one structural addition to this arc since the original exercise; see Section 6.

---

## 5. Key Takeaways for Product Design

| # | Takeaway | Status |
|---|---|---|
| 1 | The comparison view needs to be reachable in one filter action, not buried after browsing | **Held up.** Platform and genre filters are both one click/tap from any browse page |
| 2 | Platform availability and rating must appear in the same row, not adjacent screens | **Held up.** Both appear together in the comparison view |
| 3 | Sorting by rating (high to low) by default removes the "which one is even good" decision cost | **Now fully held up.** This was flagged as an open deviation in the prior revision of this document (the shipped default was popularity, not rating). That gap has since been resolved, and the default sort is now IMDb rating, descending |
| 4 | Movies/Series segmentation should happen at the genre-selection step | **Held up as designed.** Implemented as a top-level toggle |

---

## 6. What Changed From the Original Map

1. **New failure/success mode discovered during build:** the original map assumed "found a good option" always resolves to "watching." In practice there's a valid middle state, found something good, not in the mood tonight, that the original journey didn't account for. The watchlist (Want to Watch / Watching / Watched, with an optional personal rating) exists specifically to give that middle state a real home instead of forcing a false choice between "watch now" and "lose it."
2. **A gap between plan and build was found and closed.** The default sort briefly shipped as popularity instead of rating, which directly undercut takeaway #3 above for exactly the persona (Rohan, the Time-Starved Professional) it mattered most for. This is now fixed.
3. **Not yet validated:** everything in the "With CineCompass" column describes intended behavior confirmed by manual testing, not measured user behavior. The North Star Metric this journey map exists to support, time from search to selection, is not yet instrumented in production (see `03-product-discovery-report.md`, Section 8). Treat the emotional arc above as a design hypothesis that's been built, not yet as a proven outcome.
