# /research-ideation — Generate research questions

Interactive brainstorming to move from a vague topic to a sharp, identifiable research question.

## Arguments

- `<topic>` — the rough area of interest
- *(none)* — ask

## Instructions

### Step 1: Map the area

Briefly: what is known, what is contested, what is unknown? Two paragraphs, drawing on what you know or a quick search. Honest about uncertainty.

### Step 2: Generate 5–8 candidate questions

Each candidate must be:
- **Sharp** — answerable in one sentence
- **Feasible** — plausible identification + plausible data
- **Novel** — not a direct restatement of an existing paper
- **Important** — would the answer change someone's prior?

Present as:

```
[1] Question
Identification: [DiD on …, IV using …, etc.]
Data: [dataset, period, unit]
Why it matters: [one sentence]
Closest existing paper: [author, year — what they did, what this would add]
```

### Step 3: Rank by tractability × interest

Score each on:
- **Tractability** — can this actually be done? (data exists, identification is plausible, scope is bounded)
- **Interest** — would a referee at a target journal care?

Place the candidates on a 2×2. The top-right cell is where to push.

### Step 4: Pressure-test the top 1–2

For each, walk through:
- What is the strongest threat to identification? How would the paper address it?
- What is the most likely null result, and is the null itself interesting?
- What is the smallest viable version of the study? (One outcome, one specification, one robustness check)

### Step 5: Recommend next step

One of:
- A short scoping doc (data check, key citations, draft empirical strategy)
- A `/lit-review` on the area to confirm novelty
- A `/preregister` if the design is already clear

## Notes

- Resist the urge to converge too fast. The value is in surfacing options the user hasn't considered, not in picking one.
- "Important" beats "novel" — a well-answered version of a known question is often a better paper than a poorly-answered novel one.
