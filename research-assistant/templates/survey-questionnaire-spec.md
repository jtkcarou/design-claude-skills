# Survey Questionnaire Spec — Google Sheet Structure

For surveys, the deliverable is **two files**:
1. The research plan Google Doc (uses research-plan-doc-template.md)
2. The questionnaire spec **Google Sheet** (this template) — linked from Section 6 of the Doc

The Sheet is the source of truth for the survey. The Google Form is built from the Sheet, row by row.

---

## How To Hand Off The Spec

When generating the survey artifact, produce:
- A markdown table representing the Google Sheet (user pastes into Sheets)
- OR an .xlsx file using the xlsx skill (if user wants direct file)
- OR a CSV the user imports

Tell the user:
> "Paste this table into a new Google Sheet, then build the Google Form from the Sheet row by row. Each row = one question. Branching logic, options, and required flags are all here."

---

## Sheet Schema (Columns)

| Column | Required | Format | Notes |
|---|---|---|---|
| `Q#` | Y | Q1, Q2… | Stable IDs; never reuse if a question is removed |
| `Section` | Y | String | Logical group: "Screener", "Behaviour", "Attitudes", "Demographics", "Open-ended" |
| `Question text` | Y | String | The exact wording as participant sees it |
| `Question type` | Y | Enum | See type list below |
| `Options` | Conditional | Semicolon-separated | Required for any closed-ended type |
| `Randomise options?` | Y | Y/N | Y for nominal lists; N for ordinal scales |
| `Required?` | Y | Y/N | Default Y for screeners and core; N for optional/sensitive |
| `Branching logic` | Conditional | Free text | "If Q3 = 'No', skip to Q7" |
| `Maps to objective` | Y | RQ ID | Which research question this serves (RQ1, RQ2…). If blank, cut the question. |
| `Notes for build` | N | Free text | For the Form-builder — placement, formatting, validation rules |

### Question types

- `Single select` — one choice from a list
- `Multi select` — multiple choices, optional cap (e.g. "Pick up to 3")
- `Likert 5` — 5-point agreement / frequency / satisfaction (use bipolar adjectives, not Agree/Disagree)
- `Likert 7` — 7-point semantic differential
- `Numeric 0-10` — NPS-style or single numeric
- `Slider` — continuous (use sparingly on mobile)
- `Open-ended short` — single line, mobile-friendly
- `Open-ended long` — paragraph; place near end
- `Yes/No` — binary; consider whether forced choice is right
- `Ranking` — order N items by preference
- `Date` — calendar input
- `Email` (only if recontacting; flag privacy)

---

## Example Sheet Rows

| Q# | Section | Question text | Question type | Options | Randomise options? | Required? | Branching logic | Maps to objective | Notes |
|---|---|---|---|---|---|---|---|---|---|
| Q1 | Screener | In the last 30 days, have you sold something on Carousell? | Single select | Yes; No | N | Y | If "No", end survey | RQ1 (target audience filter) | Place at very start |
| Q2 | Screener | What category did you most recently list in? | Single select | Electronics; Fashion; Home; Cars; Other; Don't remember | Y (except "Other"/"Don't remember" pinned to end) | Y | If "Don't remember", skip to Q5 | Quota check | |
| Q3 | Behaviour | Thinking about your most recent listing, how many photos did you upload? | Single select | 1; 2-3; 4-5; 6-9; 10+ | N (ordinal) | Y | | RQ2 | |
| Q4 | Behaviour | When you set the price for that listing, what did you do to decide? Select all that apply. | Multi select | Searched similar listings; Asked someone; Used my gut; Looked up retail price; Checked a price guide; Other | Y | Y | | RQ2 | Cap visible options at 7 |
| Q5 | Attitudes | Rate the speed of the listing flow on your most recent listing. | Likert 5 | Very slow; Slow; Neither; Fast; Very fast | N (ordinal) | Y | | RQ3 | Avoid "satisfied" framing — neutral "speed" |
| Q6 | Attitudes | Rate the clarity of the listing flow on your most recent listing. | Likert 5 | Very unclear; Unclear; Neither; Clear; Very clear | N | Y | | RQ3 | Split from Q5 — never combine "fast and clear" |
| Q7 | Open | What's the **first** thing you'd change about the listing flow? | Open-ended short | | | N | | RQ4 | Open-ended at end; "first" reduces over-elaborate answers |
| Q8 | Demographics | Which market do you mostly use Carousell in? | Single select | SG; MY; PH; ID; HK; TW; Other | Y (except "Other") | Y | | Quota cut | |
| Q9 | Demographics | (Optional) What's your monthly household income range? | Single select | <S$3k; S$3k-6k; S$6k-10k; S$10k+; Prefer not to say | N (ordinal) | N | | Sub-group analysis | Sensitive — placed at end |

---

## Length Discipline

- **In-app intercept:** 5–8 questions max
- **Email survey:** 10–15 questions max
- **Brand tracker / longitudinal:** length capped by historical instrument; never extend without ending the trend

If the Sheet has more than the cap, the skill should refuse to generate the Form and force the user to cut. Every additional question drops completion ~10%.

---

## Pre-Field Stress Test (run on the full Sheet)

Walk every row through the bias library. For each row:

- [ ] Single concept (not double-barrelled)?
- [ ] Past or present tense, not hypothetical?
- [ ] Neutral language, no leading framing?
- [ ] Options MECE (mutually exclusive, collectively exhaustive)?
- [ ] Randomisation correct (nominal Y, ordinal N)?
- [ ] Maps to a stated RQ?
- [ ] Placement correct (screeners early, sensitive late, open-ended last)?
- [ ] Mobile-friendly (no long open-ended in middle of survey)?

Mark issues in a "Stress test notes" column or a separate review tab.

---

## Localisation

If fielding in multiple markets, add columns:
- `Question text (Bahasa)`
- `Question text (Filipino)`
- `Question text (Chinese — Traditional)`
- `Question text (Chinese — Simplified)`

Cognitively pre-test each language with 2–3 native speakers before fielding. Loaded terms shift across languages — always re-test for connotation, not just translation.

---

## Building the Google Form from the Sheet

1. Create new Google Form
2. For each row in the Sheet, add a Form question matching the type
3. Apply branching logic via "Go to section based on answer"
4. Apply randomisation via "Shuffle option order" (only for nominal lists)
5. Mark required where indicated
6. Test the full flow end-to-end with a colleague before fielding
7. Pilot with 5–10 real users; check completion time, dropout points, open-ended quality
8. Adjust, then field
