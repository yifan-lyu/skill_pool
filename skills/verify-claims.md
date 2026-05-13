# /verify-claims — Chain-of-verification fact check

Independent fact-check of factual claims in a draft. Catches hallucinated citations, wrong dataset fields, and misattributed findings. Adapted from Dhuliawala et al. 2023 (arXiv:2309.11495).

## Arguments

- `<file>` — path to a `.tex` or `.md` document
- *(none)* — auto-detect

## Instructions

### Step 1: Extract verifiable claims

Read the document and extract every claim that can be checked against an external source:
- Attributed findings ("Acemoglu and Restrepo (2020) find that…")
- Numerical facts ("Sweden has 1,400 firms with…")
- Dataset descriptions ("the LISA register covers all individuals aged 16+ since 1990")
- Methodology references ("we use the Callaway and Sant'Anna estimator")

Skip claims that are this paper's own results (those belong in `/audit-reproducibility`).

### Step 2: Build a verification question per claim

For each claim, write a verification question that does NOT presuppose the answer.

```
Claim: "Acemoglu and Restrepo (2020) find that one more robot per thousand workers reduces employment by 0.2 percentage points."
Question: "What is the employment effect of robots reported in Acemoglu and Restrepo (2020)?"
```

### Step 3: Answer from primary sources only

For each question, find the answer using the cited source — not the draft itself.

- Citations: open the actual paper (DOI, journal page, or working paper).
- Data: open the official codebook or dataset documentation.
- Methods: open the methods paper that introduced the technique.

If you cannot access the primary source, mark UNVERIFIED — do not guess.

### Step 4: Compare and flag

For each claim, classify:
- **CONFIRMED** — claim matches source
- **PARTIALLY CONFIRMED** — direction right, magnitude or qualifier off
- **CONTRADICTED** — source says something different
- **UNVERIFIED** — primary source not accessible

### Step 5: Report

```
## Claim Verification
Date: [YYYY-MM-DD]
Claims checked: N
- CONFIRMED: X
- PARTIALLY CONFIRMED: Y
- CONTRADICTED: Z
- UNVERIFIED: W

### Contradicted
**[1] [Section, line N]**
> Claim: "..."
> Source says: "..."
> Suggested revision: "..."

### Partially confirmed
...

### Unverified (manual follow-up needed)
...
```

## Notes

- Independence matters: do not let the draft's framing prime the verification. Read the source first, then compare.
- This complements `/cite-audit` (bibliographic accuracy) and `/estimate-audit` (this paper's own results). All three together cover the surface of pre-submission fact-checking.
