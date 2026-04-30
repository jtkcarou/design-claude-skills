# Synthesis Framework — For `/synthesize` Mode

The user pastes raw research artifacts (interview transcripts, UT notes, survey exports, card-sort results, free-text responses). The skill produces a synthesis document with a built-in stakeholder summary brief.

## Inputs This Skill Expects

Acceptable raw materials:
- Interview transcripts (text)
- UT session notes / observation logs
- Survey CSV / numeric tables / open-ended response dumps
- Card sort / tree test result tables
- Diary entries (less common — flag as out of priority scope)

If the input is missing structure (e.g. a wall of unattributed text), ask the user to clarify:
- Whose voice is this? (Single participant or many?)
- What method generated it?
- What was the original research question?

Don't synthesise without those three — the output will be unreliable.

## Synthesis Pipeline

### Step 1 — Atomise
Break raw data into atomic units. One unit = one verbatim quote, one observed behaviour, or one survey response. Each unit is tagged with:
- Participant ID (P01, P02…)
- Method context (interview / UT / survey)
- Original timestamp or section if available
- Segment tags (buyer/seller, casual/pro, market, category)

Output of this step: a flat, tagged list. No interpretation yet.

### Step 2 — Code (open coding)
For each atomic unit, attach a short code (1–3 words) capturing what it's *about*. Codes emerge from the data — not from a pre-existing framework.

Examples (for a Carousell listing-flow study):
- `photo-anxiety`
- `price-uncertainty`
- `category-confusion`
- `keyboard-friction`
- `abandoned-mid-flow`

Track code frequency and which participants raised it.

### Step 3 — Cluster (affinity diagramming)
Group codes into emergent themes. Themes should:
- Come from the data (not from your hypotheses)
- Cut across participants (≥3 participants in qual; meaningful % in quant)
- Have a name that uses the user's vocabulary, not the team's

For each theme, capture:
- Theme name
- Participant count + IDs
- 2–3 representative verbatim quotes (anonymised)
- Observed behaviours that support it
- Counter-evidence (where it didn't appear)

### Step 4 — Build mental models
For 2–3 of the strongest themes, articulate the user's underlying mental model. A mental model is a one-sentence statement of how the user thinks the system / problem / workflow operates, in their own words.

Example: *"Users believe the listing's first photo determines whether the algorithm shows it to anyone, so they obsess over it and abandon if they can't get a good shot."*

Mental models are the bridge between observation and design implication.

### Step 5 — Translate to design implications
For each strong theme, name:
- **What this means for the product** (concrete implication, not hand-wavy)
- **Recommended action** (testable, actionable, not "consider improving")
- **Confidence level** (high / medium / low based on participant count, method strength, triangulation)

Avoid: marketing-style personas, fictional demographics, "users are X" generalisations beyond what the data supports.

### Step 6 — Surface the unknowns
What couldn't this study answer? What would the next study need to test? Be explicit. The doc treats unstated limitations as a deliverable defect.

## The Synthesis Document Output

Produce a single document with this structure (the synthesis-doc-template.md in /templates is the skeleton):

```
1. Stakeholder Summary Brief (top of doc, 1 page max)
   - One-paragraph TL;DR
   - 3–5 headline findings as bullet points
   - Top 2–3 recommended actions
   - What this study did NOT answer

2. Method recap (½ page)
   - Research question, method, sample, fielding window, limitations

3. Findings (bulk of doc)
   - Each theme as a section
   - Theme name → one-sentence summary → verbatim quotes → behavioural evidence → counter-evidence → mental model → design implication

4. Unanswered questions and next-study recommendations

5. Appendix (optional)
   - Raw atomic units / coded list / participant summary
```

## Quality Bar (Final Deliverable)

The doc reference is opinionated. Apply it:
- **Cohesive** — all findings refer to the same problem space
- **Consistent** — findings don't contradict each other (or contradictions are explicitly named as tensions)
- **Complete** — no secret findings floating in the team's heads
- **Unambiguous** — stripped of jargon, acronyms, internal slang
- **Feasible** — recommendations within technological + capital reach
- **Concise** — the stakeholder summary fits on one page; the full doc fits in 3–5 pages plus appendix

Verbatim quotes throughout. Anonymise but preserve voice. Quotes are the anti-corporate-projection device — they force stakeholders to confront the user's actual words.

## What NOT To Do

- Don't generate findings that aren't in the atomic data. Hallucinated insights are the worst possible output.
- Don't paper over contradictions — call them tensions and explore them.
- Don't write personas. If the user asks for personas, push back: archetype based on behaviour, not demographics, and only if the data supports it.
- Don't write recommendations softer than the data warrants. "Consider improving X" is meaningless. "Move the price field above the photo because P01, P03, P07 abandoned trying to find it" is useful.
- Don't synthesise quant from qual or vice versa. If sample is 6 participants, don't say "30% of users…"; say "P01, P03, P07 (3 of 6) did X".

## Confidence Calibration

Use these phrases consistently:
- **High confidence** — observed in ≥75% of participants, multiple methods, behavioural data
- **Medium confidence** — observed in ≥50%, single method, mix of attitudinal and behavioural
- **Low confidence / signal** — observed in <50%, single method, attitudinal only

Stakeholders trust calibrated language. Avoid "users want…" as a blanket claim.
