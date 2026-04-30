# Bias Library — What To Flag and How To Mitigate

This is the catalogue used in `/critique` and stress-tests in `/plan` and `/act`. When reviewing any research artifact, scan against every entry.

## Researcher-Side Biases (in question writing and method design)

### 1. Confirmation bias
- **Pattern:** Plan or script designed to confirm what the team already believes.
- **Tells:** "We want to validate that…", "users love X" as a starting hypothesis, only positive scales offered.
- **Fix:** Force a falsifiable question. Ask "what would have to be true for us to be wrong?"

### 2. Sponsor bias / leading questions
- **Pattern:** Question or framing telegraphs the desired answer.
- **Tells:** "How much do you like…", "Would you agree that…", company name in the prompt, value-laden adjectives.
- **Fix:** Strip evaluative adjectives. Replace "satisfaction" with "your experience". Anonymise sponsor.

### 3. Validation trap
- **Pattern:** Asking users about a future product/feature concept and treating their reaction as predictive.
- **Tells:** "Would you use…", "Would you pay for…", "Do you like this idea?"
- **Fix:** Replace with past behaviour. "When did you last face this problem? Walk me through what you did." See Mom Test rules.

### 4. Methodological monoculture
- **Pattern:** Defaulting to one method (focus group, survey) regardless of question.
- **Tells:** Survey to diagnose usability friction. Interviews to size a market. Focus groups for sensitive topics.
- **Fix:** Use the methodology matrix. Match method to question shape.

### 5. Solution embedded in research question
- **Pattern:** The "research question" is actually a feature spec.
- **Tells:** "Should the button be blue or red?", "Where should the filter live in the nav?"
- **Fix:** Move design decisions to A/B tests or preference tests. If research, reframe to "what mental model do users hold?"

### 6. Vague screener
- **Pattern:** Recruitment criteria are demographic-only with no behavioural filter.
- **Tells:** "Carousell user, age 25–45". No filter on activity, category, recency.
- **Fix:** Filter on past behaviour relevant to the topic. "Has listed an item in last 30 days", "Has bought from a Pro Seller in last 90 days."

### 7. Over-explicit screener (gives away the study topic)
- **Pattern:** Screener telegraphs what the study is about, letting fraudsters self-select.
- **Tells:** "We're studying [feature]. Have you used [feature]?"
- **Fix:** Hide the topic behind general behaviour questions. Screen on behaviour, not awareness.

## Participant-Side Biases (in how they answer)

### 8. Social desirability bias
- **Pattern:** Participant answers to look good (greener, more responsible, less stigmatised behaviour).
- **Especially strong for:** Voting, eco choices, money habits, screen time, scam victimisation.
- **Fix:** Self-administered modes (online survey > phone). Provide psychological cover ("many people have…"). Anchor in past behaviour.

### 9. Hospitality bias (SEA-specific overlay)
- **Pattern:** Participants over-praise to be polite, especially in SG/MY/PH/ID interviews.
- **Tells:** "It's nice", "I like it lah", smiles + agreement without specifics.
- **Fix:** Ask "what's the *first* thing you'd change?" Push for concrete past examples. Look for behavioural commitment, not verbal compliment.

### 10. Hawthorne effect
- **Pattern:** Behaviour changes because participant knows they're being observed.
- **Tells:** Slower, more deliberate task execution; over-narration; "showing off" workflow.
- **Fix:** Contextual inquiry over lab studies. Longer warm-up. Diary studies for habitual behaviour.

### 11. Acquiescence bias
- **Pattern:** Participants tend to agree with statements rather than disagree, especially when uncertain.
- **Tells:** Agree/Disagree scales. "Do you agree that X?"
- **Fix:** Replace with forced choice between two balanced statements. Or ask "to what extent" with a balanced bipolar scale.

### 12. Demand characteristics
- **Pattern:** Participant guesses what the researcher wants and delivers it.
- **Tells:** Participant asks "is this what you wanted?" Performs visibly for the camera.
- **Fix:** Hide hypotheses. Don't react visibly to answers. Don't pitch the product.

## Question Construction Faults

### 13. Double-barrelled question
- **Pattern:** Two questions in one. Forces a single answer to two distinct things.
- **Tells:** "fast and reliable", "easy and intuitive", any "and" between two evaluable concepts.
- **Fix:** Split into two atomic questions.

### 14. Loaded language
- **Pattern:** Emotive or politically charged term distorts response.
- **Tells:** "welfare" vs "assistance", "tax burden" vs "tax contribution", "cheap" vs "affordable".
- **Fix:** Use neutral, descriptive language. Test wording on a small sample for connotation.

### 15. Hypothetical question
- **Pattern:** Asks the user to predict their future behaviour or imagine reactions.
- **Tells:** "Would you…", "Imagine if…", "How often would you…"
- **Fix:** Replace with past tense. "When was the last time…", "Walk me through what you did."

### 16. Cognitive overload
- **Pattern:** Question requires too much working memory, parsing, or context.
- **Tells:** Long sentence, nested clauses, jargon, internal acronyms, more than 7 response options on a list.
- **Fix:** Split. Define terms inline. Cap categorical lists at 5–7 options.

### 17. Overlapping or non-exhaustive options
- **Pattern:** Response options overlap (18–25, 25–30) or miss valid states.
- **Fix:** Mutually exclusive and collectively exhaustive (MECE). Always include "Other" or "Not applicable" where relevant.

## Order Effects (whole-survey faults)

### 18. Assimilation effect
- Early questions prime mood and depress later answers (or vice versa).
- **Fix:** Randomise sections where logical. Buffer related questions apart.

### 19. Primacy effect (visual)
- First options in a list get over-selected in self-administered surveys.
- **Fix:** Randomise nominal categorical options per respondent. Never randomise ordinal scales.

### 20. Recency effect (auditory)
- Last options heard get over-selected in phone/voice surveys.
- **Fix:** Randomise; keep lists short.

### 21. Open-ended placement
- Open-ended at the start tanks completion rates and primes later answers.
- **Fix:** Place open-ended near the end. Mandatory screeners at the very start.

### 22. Sensitive-question placement
- Income/political/health asked early erodes trust and inflates dropout.
- **Fix:** End of survey, after rapport.

## Sampling Biases

### 23. Self-selection bias
- Highly engaged or highly aggrieved users over-respond to open recruitment.
- **Fix:** Stratified sampling. Quota by behaviour segment. Weight if needed.

### 24. Survivorship bias
- Only currently active users sampled. Churned/lapsed users invisible.
- **Fix:** Recruit lapsed users explicitly when relevant. Source from CRM, not in-app.

### 25. Convenience sampling (Slack, internal panel)
- Internal users or convenience samples over-represent power users.
- **Fix:** Use external panel for production research. Slack call-outs only for internal-tooling research.

## Stress-Test Application

When reviewing any artifact, walk through this list once. For each hit, surface:
1. Which bias it is (named)
2. Where in the artifact (quote it)
3. Why it matters (what it will skew)
4. Concrete rewrite (not just "fix this")
