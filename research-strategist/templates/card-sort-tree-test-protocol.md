# Card Sort and Tree Test Protocol Template

For information architecture studies. Use card sort to discover how users group concepts; tree test to validate a proposed hierarchy.

---

## Protocol — [Study name]

**Format:** [Open card sort / Closed card sort / Hybrid card sort / Tree test]
**Mode:** [Unmoderated online (Optimal Workshop / Maze / similar) / Moderated]
**Sample size:** [15–30 unmoderated for stat confidence; 8–12 moderated for depth]
**Session length:** 20–30 min unmoderated; 45 min moderated

---

## When To Use Which Method

| Method | Use when | Sample size |
|---|---|---|
| **Open card sort** | You want to discover users' natural mental groupings before designing the IA | 15–20 |
| **Closed card sort** | You have category names and want to test which items users put where | 20–30 |
| **Hybrid card sort** | You want both — fixed categories with option to create new ones | 20–30 |
| **Tree test** | You have a proposed nav/IA and want to test if users can find things | 30–50 |

---

## Card Sort Setup

### Card list

[List the items being sorted. Rules:
- Use the user's vocabulary, not internal product names
- Each card = one concept, one phrase
- 30–60 cards is the practical range; beyond 60, fatigue dominates
- Pre-test cards on 2–3 colleagues to catch ambiguous wording]

| Card # | Card text | Source / rationale |
|---|---|---|
| 1 | [Concept in user words] | [Why this is in the deck] |
| 2 | […] | […] |

### Categories (closed/hybrid only)

| Category | Definition (for moderator only — don't show participant) |
|---|---|
| [Category A] | [What belongs here] |
| [Category B] | [What belongs here] |

### Pre-test instructions to participant

> "I'm going to show you a list of items. Please group them in any way that makes sense to you. There are no right or wrong groupings — we want to see how you naturally think about these. Take your time. When you're done, give each group a name in your own words."

For closed: "Please put each item into one of the categories shown."

---

## Tree Test Setup

### Tree structure

Define the proposed IA. Use indentation to show hierarchy.

```
Home
├── Browse
│   ├── Categories
│   │   ├── Electronics
│   │   ├── Fashion
│   │   └── …
│   └── Search
├── Sell
│   ├── List an item
│   ├── My listings
│   └── …
└── Inbox
    ├── Chats
    └── Notifications
```

### Tasks

[List 5–10 findability tasks. Each task = "Where would you go to [action]?" Tasks should:
- Use the user's words, not the system's
- Cover the most important paths in the tree
- Be unambiguous about what success looks like]

| Task # | Task statement | Correct path(s) |
|---|---|---|
| 1 | "You want to find an iPhone for sale near you. Where would you go?" | Browse → Search OR Browse → Categories → Electronics |
| 2 | "You want to check if anyone has replied to your listing. Where would you go?" | Inbox → Chats |
| 3 | […] | […] |

---

## Recruitment Criteria

- Filter on **past behaviour** relevant to the IA. (Buyer / seller mix; recency in app; category exposure.)
- Avoid power-user-only sample — IA tests need representative users.
- Quota by market and primary language if studying multi-market IA.

---

## Analysis

### Card sort

- **Similarity matrix** — for each pair of cards, how often did participants put them together? Visualise as a heatmap.
- **Dendrogram** — cluster cards by co-occurrence to see natural groupings emerge.
- **Category labels (open/hybrid)** — what names did participants use? What vocabulary cluster emerges? This becomes the IA labelling.
- **Standardisation grid (optional)** — % of times each card landed in each category, useful for closed sorts.

### Tree test

- **Success rate per task** — % of participants who reached the correct destination.
- **Directness** — % who got there without backtracking.
- **First-click analysis** — where did they go first? First-click accuracy is a strong predictor of overall success.
- **Path analysis** — common wrong paths reveal model mismatches.

Threshold: tasks with <70% success rate need IA revision. Tasks with <50% are critical failures.

---

## Reporting

In the synthesis doc, report:

- **What clusters emerged** (card sort) — describe in user vocabulary
- **What labels users used** (open/hybrid) — feed into IA naming
- **Where the tree failed** (tree test) — task-by-task with first-click + success rate
- **Mental model implications** — what does this say about how users conceptually navigate the space?
- **Recommended IA changes** — concrete, with rationale tied to data

---

## Common Pitfalls

- **Too many cards (>60)** — fatigue collapses the data quality
- **Using internal product jargon on cards** — primes participants and tests vocabulary, not structure
- **Mixing card sort with concept testing** — keep IA work separate from "do you like this idea?"
- **Sample too small (<10)** — stat noise; need at least 15 for any directional reading
- **Single-market sample for multi-market IA** — vocabulary varies by language; recruit across markets
