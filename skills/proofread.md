# /proofread — Grammar, typos, and prose polish

Light proofreading pass on a LaTeX paper, slides, or markdown document. Catches typos, grammar, awkward phrasing, and style inconsistencies. Does not restructure arguments — use `/paper-review` for that.

## Arguments

- `<file>` — path to a `.tex`, `.md`, or `.txt` file
- *(none)* — auto-detect the most recently edited document in `writing/` or `slides/`

## Instructions

### Step 1: Read the file

Read the whole file. For LaTeX, ignore preamble commands but read everything inside `\begin{document}`.

### Step 2: Identify issues

Pass over the text looking for, in order:

1. **Typos and spelling** — including British/American mixing (the lab convention is British English: labour, behaviour, analyse, organisation, colour)
2. **Grammar** — subject-verb agreement, dangling modifiers, comma splices
3. **Punctuation** — minimise em-dashes (prefer commas, colons, parentheses); fix spacing around units, percentages, currency
4. **Word repetition** — same content word twice in adjacent sentences without rhetorical reason
5. **Hedging soup** — "may potentially possibly suggest" — flag and tighten
6. **Inconsistent terminology** — same concept named two different ways (e.g. "exposure measure" vs. "AI exposure index" — pick one)
7. **Number formatting** — consistent thousands separator, decimals, significant figures
8. **Citation form** — `\citet{}` vs `\citep{}` used appropriately (text-flow vs. parenthetical)

### Step 3: Present findings

For each issue:

```
[line N] type: typo | grammar | style | consistency
> "exact quote"
fix: "proposed correction"
```

Group by type. Do not propose fixes that change meaning — those are review-level concerns, flag them but do not "fix" them.

### Step 4: Offer to apply

Ask: "Apply all fixes? Apply selectively? Or leave for manual review?"

If applying, edit the file directly. Do not touch anything beyond the flagged spans.

## Notes

- Test for any sentence: would a careful empirical economist write this? If it sounds like marketing prose ("our novel framework", "transformative implications"), flag and tighten.
- Never invent statistics, citations, or factual claims while "fixing" prose.
