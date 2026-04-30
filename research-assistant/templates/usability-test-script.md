# Moderated Usability Test Script Template

For moderated UT on a prototype or live product. Embed inside Section 6 of the research plan. 60–90 min sessions, 5–8 participants per segment.

---

## UT Script — [Study name]

**Format:** Moderated usability test · [60/75/90] min · [Remote (Zoom/Meet) / In-person]
**Test artifact:** [Figma prototype link / Live URL / Test build]
**Device:** [Mobile (Android default) / Desktop / Tablet — match production]
**Moderation style:** Think-aloud protocol throughout core tasks; moderator silent during task execution.

---

### Pre-session checklist

- [ ] Prototype / build tested end-to-end, all paths working
- [ ] Recording consent (verbal + written)
- [ ] Participant on correct device + screen-share working
- [ ] Notetaker capturing observations in real time
- [ ] Reset script ready (cookies / app state) between participants if testing live

---

### Section 1 — Welcome and orientation (5 min)

- "Thanks for joining. We're testing the [product / prototype], not you. There are no right or wrong answers — anything that's confusing tells us we need to fix the design."
- "I'm going to ask you to do a few tasks. While you're doing them, please **think aloud** — say what you're looking at, what you're trying to do, what you expect to happen. Even small reactions help."
- "If something doesn't work, that's our problem, not yours. Just describe what you'd want to do."
- "I might ask follow-up questions but I'll mostly stay quiet so I can see how you naturally use it."

**Confirm:** Recording on. Screen share on. Participant comfortable.

---

### Section 2 — Context-setting questions (5 min)

Quick warm-up to anchor the session in their real context. **Past behaviour only — do not pitch the test artifact yet.**

- "How often do you use [Carousell / category]?"
- "Tell me about the last time you [target task in real life]. What did you do?"
- "What apps do you usually use for this?"

This frames the participant as a buyer/seller/etc. and sets a behavioural baseline.

---

### Section 3 — Core tasks (40–60 min)

For each task, follow this structure:

#### Task setup
- **Scenario:** [Realistic scenario in plain language. e.g. "Imagine you've just finished cleaning out your closet and want to sell a jacket. Open the app and post the listing."]
- **Success criteria** (don't tell the participant): [What completion looks like — e.g. "User reaches the 'Listed!' confirmation screen with all required fields filled."]
- **Failure modes to watch for:** [Common stumbles — e.g. "Can't find category", "abandons photo upload", "uses wrong navigation."]

#### Task execution
- **Read the scenario, then stop talking.**
- Let the participant attempt. Don't help. Don't react to errors. Don't confirm correct moves.
- Take observation notes: where do they hover/scroll, what do they say aloud, where do they hesitate, what do they tap that doesn't work.
- If completely stuck for >2 min: "What would you try next? If nothing else worked, what would you do?"
- If they ask "is this right?": deflect — "What do you think?"

#### Post-task probes (after each task)
- "What was that experience like?"
- "What was confusing?"
- "What did you expect to happen at [specific moment] that didn't?"
- On a scale of 1–7, how easy was that task? (Single-Ease Question — captures perceived ease without leading.)

[List 3–5 tasks here. Order them so success builds confidence — start easier, escalate. Reset between tasks if state carries over.]

**Example task list (placeholder):**

**Task 1 — Find a specific item**
Scenario: "You want to buy a used iPhone 14 in good condition under $600 in your area. Find one you might consider buying."
Success: User reaches a listing detail page that meets criteria.
Watch: Search vs browse choice, filter use, price/condition awareness.

**Task 2 — Make an offer via chat**
Scenario: "You found a listing you like but the price is a bit high. Try to negotiate."
Success: User sends a message with an offer.
Watch: Where they look for chat entry, how they phrase the message, hesitation around offer amount.

**Task 3 — [study-specific]**
[…]

---

### Section 4 — Post-test reflection (10 min)

After all tasks complete:

- "Overall, what stood out — good or bad?"
- "If you had to describe this app/feature to a friend in one sentence, what would you say?"
- "What would you change first?"
- (If applicable) "Compared to [Shopee / current Carousell / competitor], how does this feel different?"

**Avoid:** "Did you like it?", "Would you use this?", "Is this better than X?" — leading and hypothetical.

---

### Section 5 — Wrap (5 min)

- Any final questions from the participant?
- Confirm incentive logistics
- Thank, close, stop recording

---

## Observation Capture Template (for the notetaker)

Per task, log:

| Task | Time on task | Completed? | Errors observed | Verbatim quotes | Critical incidents | Notes |
|---|---|---|---|---|---|---|
| 1 | mm:ss | Y/N/Partial | [count + type] | "Quote 1" / "Quote 2" | [What broke] | [Behavioural observations] |

Critical incidents are the gold — moments where the user said or did something that revealed a model mismatch. Capture verbatim and timestamp.

---

## Moderator Reminders

- **Treat user errors as design faults.** The doc is explicit: errors are systemic, not personal. Never imply the participant is at fault.
- **Stay silent during tasks.** Every word from the moderator skews behaviour.
- **Don't react.** No "great", no "exactly", no "yeah good question". Neutral face, neutral voice.
- **Use the think-aloud only when it's running natural** — if the participant goes silent and is mid-task, let them. Re-prompt only if they go silent for >30 sec.
- **After session, debrief with notetaker for 10 min.** Top 3 surprises, top 3 quotes, top 3 friction points.
