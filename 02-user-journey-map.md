# User Journey Map — OTT Comparison & Discovery Platform

**Primary Persona Mapped:** Ananya Sharma ("The Budget Juggler")
**Scenario:** Ananya has a free evening and wants to watch a highly-rated thriller series, but isn't sure it'll be on a platform she already subscribes to.

---

## Journey Overview

| Stage | 1. Trigger | 2. Search | 3. Cross-Check | 4. Platform Reality Check | 5. Decision Fatigue | 6. Watch (Current, Broken) | 6. Watch (With This Product) |
|---|---|---|---|---|---|---|---|
| **What she's doing** | Wants to watch something tonight | Googles "best thriller series 2026" | Opens IMDb / Rotten Tomatoes to verify ratings on shortlisted titles | Searches "[Title] Netflix" or "[Title] available on" for each title | Has spent 15–20 min, still hasn't picked | Either gives up and rewatches something old, or finally finds one — often not on her platform | Opens the app, selects "Thriller," sees ranked table with ratings + platform column already visible |
| **Thinks** | "I want something good, not another mediocre pick" | "There are too many 'best of' lists, which one is even reliable?" | "Okay this one's rated well, but is it on something I have?" | "Ugh, not on Netflix. Let me check the next one." | "Why does this take so long just to start watching?" | "Fine, I'll just watch something I've already seen." | "Oh, these three are all rated 8+ AND on Netflix. Done." |
| **Feels** | Curious, hopeful | Mildly optimistic | Slightly annoyed — this is the 3rd tab now | Frustrated, repetitive fatigue setting in | Tired, deflated | Disappointed / resigned | Relieved, satisfied, in control |
| **Pain Points** | — | Generic "best of" lists aren't personalized by genre in one place | Ratings live on separate sites from availability info | No single source cross-references rating + platform | Decision fatigue is entirely avoidable — it's a data-fragmentation problem, not a taste problem | Time lost, mild subscription regret ("why do I even pay for this if I can't find anything") | — |
| **Opportunity** | Prompt genre selection immediately | Centralize genre-based discovery | Pull IMDb + Rotten Tomatoes into the same view | Show OTT availability inline, not as a separate search | Sort by rating automatically so the "best" option is visually first, not buried | — | This is the target end-state the product delivers |

---

## Emotional Arc (Current Experience)

```
Curious → Optimistic → Annoyed → Frustrated → Fatigued → Deflated
   ▲                                                          │
   └──────────────── (repeats next time) ────────────────────┘
```

## Emotional Arc (With Product)

```
Curious → Genre Search → Instant Ranked Comparison → Relieved / Confident Decision → Watching
```

The gap between these two arcs *is* the product's value proposition. Every stage removed between "curious" and "watching" is time given back to the user — this is the number worth measuring post-launch (see Product Discovery Report → Success Metrics).

---

## Key Takeaways for Product Design

1. **The table needs to be the first thing shown after genre selection** — not a secondary feature buried after browsing, since the journey map shows the fatigue builds progressively across separate lookup stages.
2. **Platform availability and rating must appear in the same row**, not adjacent screens — this directly collapses stages 3 and 4 of the current journey into one glance.
3. **Sorting by rating (high→low) by default** removes the "which one is even good" decision cost identified at the Search stage.
4. **Movies/Series segmentation** should happen at the genre-selection step, before the table loads, so Rohan-type users (time-starved) aren't shown irrelevant format results.
