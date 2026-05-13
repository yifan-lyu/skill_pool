# /preregister — Draft a preregistration document

Produce a preregistration document for an empirical study. Supports OSF, AsPredicted, and AEA RCT Registry formats.

## Arguments

- `--style osf` — long-form OSF preregistration template (default)
- `--style aspredicted` — short 9-question AsPredicted template
- `--style aea-rct` — AEA RCT Registry template (for experiments)

## Instructions

### Step 1: Gather inputs

Ask in one batch (do not interview one question at a time):

1. **Question** — one-sentence research question
2. **Hypothesis** — directional prediction, with sign
3. **Data** — dataset, period, unit of observation, sample size
4. **Treatment / predictor** — variable, variation exploited
5. **Outcome(s)** — primary + secondary, with definitions
6. **Identification** — DiD, IV, RDD, RCT, etc.
7. **Specification** — main estimating equation, controls, FE, SE clustering
8. **Power / MDE** — if computed
9. **Robustness** — pre-specified checks
10. **Analysis plan** — exclusion rules, multiple-testing adjustment, subgroup analyses

Anything not provided: mark `[TO BE FILLED]` in the draft rather than guessing.

### Step 2: Draft to the chosen template

#### OSF (long-form)

Sections: Title; Authors; Research question; Hypotheses; Data description; Sample; Variables; Identification; Estimating equation; Inference; Robustness; Subgroups; Heterogeneity; Multiple testing; Deviations protocol.

#### AsPredicted

Nine numbered questions, ≤2 sentences each. Do not exceed. The discipline of brevity is the point.

#### AEA RCT

Fields: Trial title; Status; Country; PIs; Sponsor; Sample size; Treatment arms; Outcomes (primary, secondary, exploratory); Experimental design; Randomisation; IRB; Analysis plan.

### Step 3: Cross-check internal consistency

Before saving, verify:
- Every hypothesis maps to a specific outcome
- Every outcome is defined and measurable
- The estimating equation produces a coefficient that tests the hypothesis
- Subgroup analyses are pre-specified, not data-driven

If anything is inconsistent, flag it before writing the file.

### Step 4: Save

Write to `writing/preregistration-[YYYY-MM-DD].md`.

### Step 5: Submission instructions

Print:
- OSF: paste into a new OSF preregistration, attach the markdown as a PDF
- AsPredicted: aspredicted.org → New Pre-Registration → paste each question
- AEA RCT: socialscienceregistry.org → New Trial Registration

## Notes

- Preregistration locks the analysis plan. Anything not specified can still be done later as exploratory — but must be labelled as such in the paper.
- Power calculations: if the user has not done one, offer to compute MDE for the main specification given N and clustering.
