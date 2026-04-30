# Survey Design Rules — In-App Surveys, Google Forms, Quant Instruments

For Carousell, the default survey channel is **Google Forms**, distributed in-app or via email. These rules govern question writing, response options, and instrument flow.

## Pre-Survey Audit

Before writing a single question, answer:
1. **What decision will this data drive?** If you can't name it, don't field it.
2. **Could the data be sourced elsewhere?** (CRM, app analytics, past research.) If yes, don't ask.
3. **Is the question attitudinal or behavioural?** Surveys are reliable for attitudes; weak for behaviour. If behavioural, route to UT or analytics.
4. **What's the minimum sample size?** Rule of thumb: 200+ for stat sig, 400+ if cutting by sub-group. Get data-science partner involved for power calc on key metrics.
5. **What's the maximum length?** Cap at 10 questions / 5 min. Every additional minute drops completion ~10%.

## Question Construction

### Linguistic neutrality
- Strip evaluative adjectives. "Rate your experience" beats "rate your satisfaction".
- No corporate framing. Don't preface with "Carousell strives for excellence…"
- No jargon. No internal acronyms. Define terms inline if unavoidable.
- **Cognitive pre-test in target language** for SEA markets — Bahasa, Filipino, Chinese variants matter.

### One question, one concept (no double-barrelled)
- ❌ "Was the listing flow fast and clear?"
- ✅ "How would you rate the speed of the listing flow?" + "How would you rate the clarity of the listing flow?"

### Past behaviour > hypotheticals
- ❌ "Would you use a saved-search feature?"
- ✅ "In the last 7 days, how many times did you re-search for the same item?"

### Sensitive topics need cover
- For stigma-laden behaviours (got scammed, abandoned a flow, regret a purchase), provide social cover.
- "Many sellers find it hard to estimate the right price. Did you change your asking price after listing? (Yes / No)"

## Response Options

### Scale rules
| Scale type | When to use | Pitfalls |
|---|---|---|
| 5-point Likert | Attitudes, satisfaction-style ratings | Acquiescence on Agree/Disagree formats — prefer bipolar adjective scales |
| 7-point semantic differential | Brand attributes, polarised concepts | Pre-test that endpoints make sense in target language |
| 0–10 NPS / numeric | Loyalty, recommendation, pricing buckets | Can be culturally inconsistent; SG ≠ ID baseline |
| Forced choice | Reduce acquiescence | Lose nuance; only use when reducing bias is critical |
| Multiple select | Behaviours, multi-feature use | Cap visible options at 7; randomise nominal lists |
| Single select | Mutually exclusive states | Always include "Other" or "None" if non-exhaustive |
| Open-ended | Surface unknown themes | Place at end; cap at 1–2 per survey |

### Mutually exclusive, collectively exhaustive (MECE)
- Age brackets must not overlap. (18–24, 25–34, 35–44 — never 18–25, 25–35.)
- Always include "Other (please specify)" or "Not applicable" if any respondent wouldn't fit.

### Randomisation rules
- **Nominal lists** (brand names, feature names, categories) — randomise per respondent. Defeats primacy/recency.
- **Ordinal scales** (Excellent → Poor) — never randomise. Inverting endpoints for 50% of sample is acceptable to balance directional bias.
- **Sections** — randomise where logical to defeat assimilation.

## Instrument Flow

### Funnel structure
```
1. Mandatory screeners (very start) — disqualify out of scope
2. Easy warm-up questions — build momentum
3. Core targeted questions — group by topic, randomise within group
4. Sensitive demographics (income, region, identity) — near end
5. Open-ended (max 1–2) — at the very end
6. Thank-you + incentive instructions
```

### Branching logic
- Use skip logic to keep length down. If the user says "I never list", don't ask listing-flow questions.
- Document branches in the spec sheet so the build is reproducible.

### Length discipline
- 10 questions max for in-app intercept.
- 15 questions max for email panel.
- Beyond that, abandonment dominates.

## In-App Survey-Specific Considerations

- **Trigger logic** — when does the user see it? After what action? Avoid mid-flow interruption.
- **Frequency capping** — don't show same user same survey twice. Don't show during transactional moments.
- **Mobile keyboard friction** — minimise typing. Open-ended fields tank completion on mobile.
- **Progress indicator** — yes for >5 questions; otherwise no (it primes abandonment).
- **Skip button** — required for trust. Make it visible.

## Google Forms Specific

When the deliverable is a Google Form:
1. Build the questionnaire in a **Google Sheet first** (the spec). Each row = one question.
2. The Sheet is the source of truth; the Form is built from it.
3. Spec sheet columns: `Q#`, `Section`, `Question text`, `Question type`, `Options (semicolon-separated)`, `Required (Y/N)`, `Branching logic`, `Maps to objective`.
4. The research plan Doc links to the Sheet.

## Longitudinal Surveys (Brand Trackers, NPS Trends)

- **Never change wording, options, or order** of tracked questions. Breaks the trend.
- If you must change, run both old and new versions in parallel for one wave to bridge.
- Flag mode changes (phone → online) explicitly — they shift baselines.

## Final Stress Test

Before fielding, walk every question through the bias library. For every question:
- [ ] Maps to a stated research objective?
- [ ] Single concept (not double-barrelled)?
- [ ] Past or present tense (not hypothetical), or stated-preference instrument with disclosed validity caveat?
- [ ] Neutral language (no leading framing)?
- [ ] Response options MECE?
- [ ] Order pollutes nothing?
- [ ] Pre-tested in target language(s)?

Survey is ready when every question passes every check.
