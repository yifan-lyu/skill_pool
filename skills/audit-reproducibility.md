# /audit-reproducibility — Paper ↔ code consistency check

Verify that the numbers in a paper actually match what the code produces. Catches the most common pre-submission failure: stale tables, hand-edited LaTeX numbers, code that diverged from the version that produced the reported results.

## Arguments

- `<paper>` — path to the `.tex` (or `.md`) paper
- *(none)* — auto-detect main `.tex` in `writing/`

## Instructions

### Step 1: Identify claims with numbers

Read the paper. Extract every quantitative claim:
- Regression coefficients and standard errors stated in the text
- Numbers in inline text that come from tables ("the effect is 0.23 log points")
- N, R², specifications described in table notes
- Numbers in figures' captions or annotations

For each, record the source: which table cell, which figure, which appendix.

### Step 2: Locate the producing code

For each number, locate the script in `code/` that produced it. Common patterns:
- Stata: `outreg2`, `estout`, `esttab` calls write directly to `output/tables/*.tex`
- Python: a regression result written via `to_latex()` or a custom writer

If the LaTeX paper `\input{}`s the output file directly, the link is mechanical — confirm timestamps line up (table file newer than the most recent edit to the relevant code).

If the LaTeX paper has hardcoded numbers (typed by hand), flag this as a reproducibility risk regardless of correctness.

### Step 3: Re-run and compare

If feasible, run `code/<lang>/00_run_all.{py,do}` to regenerate `output/`. Then for each claim:

- **Exact match** — paper number = regenerated number to all reported significant figures → PASS
- **Match within tolerance** — agrees to first 2 significant figures but differs in the last (e.g. rounding, RNG seed, version drift) → WARN
- **Mismatch** — disagrees beyond rounding → FAIL

If re-running is not feasible (restricted data, long runtime), compare the paper's claim against the existing `output/` and the most recent log file, and report the staleness window (time between log timestamp and current commit).

### Step 4: Report

```
## Reproducibility Audit
Date: [YYYY-MM-DD]
Paper: [path]

### Summary
- Claims checked: N
- PASS: X
- WARN: Y
- FAIL: Z
- Hardcoded numbers found: K (flagged as risk)

### Failures
**[1] Table 3, column 2 coefficient**
> Paper: "0.142 (0.031)"
> Code (output/tables/main_did.tex, generated 2026-04-12): "0.128 (0.034)"
> Likely cause: ...

### Warnings
...

### Hardcoded numbers
...
```

### Step 5: Offer next steps

- "Want me to update the paper to match the latest code output?"
- "Want me to investigate the most likely cause of mismatch [X]?"
- "Want me to add `\input{}` patterns to remove hardcoded numbers?"

## Notes

- This is **not** a substitute for running the analysis from clean state on a fresh machine. It catches in-place drift only.
- Never silently "fix" the paper to match the code without telling the user. Mismatches may indicate that the *code* is wrong, not the paper.
