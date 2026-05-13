# /data-analysis — End-to-end empirical analysis

Run a complete analysis pipeline from raw data to clean tables and figures. Python and Stata supported.

## Arguments

- `<dataset>` — path to a raw data file (in `data/raw/`) or a description of the question
- *(none)* — ask the user to point at the dataset

## Folder conventions (this template)

- `data/raw/` — never modified, never overwritten
- `data/clean/` — analysis-ready datasets, produced by cleaning scripts
- `code/python/` or `code/stata/` — numbered scripts: `00_run_all`, `01_load`, `02_clean`, `03_analyse`, `04_tables`, `05_figures`
- `output/tables/` — `.tex`, `.csv` regression outputs
- `output/figures/` — `.pdf` figures used in the paper
- `output/logs/` — `.log` files from Stata or stdout dumps from Python

## Instructions

### Step 1: Understand the question

Before touching data, write down (in conversation, or to `HANDOFF.md` if substantial):
- **Question** — one sentence
- **Outcome** — variable, measurement, level
- **Treatment / predictor** — variable, variation exploited
- **Identification** — DiD, IV, RDD, descriptive, etc.
- **Sample** — population, period, restrictions

Confirm with the user before writing code.

### Step 2: Inspect the raw data

Read a sample (head, dtypes, summary). Note:
- N rows, N columns
- Missing data pattern per column
- Outliers in key variables
- Encoding (UTF-8 for Swedish characters; check)

Do NOT modify anything in `data/raw/`.

### Step 3: Clean

Write `code/<lang>/02_clean.{py,do}`. Output one or more files to `data/clean/`. Document every drop and recode with a comment giving the *reason*. Report the row count at each step so attrition is visible.

### Step 4: Analyse

Write `code/<lang>/03_analyse.{py,do}`. Prefer:
- **Python**: `pandas` for manipulation, `statsmodels` or `linearmodels` for econometrics
- **Stata**: `reghdfe` for FE models, `csdid` or `did_multiplegt` for staggered DiD, `rdrobust` for RDD, `ivreg2` for IV. See `skills/stata/` for the full reference.

For causal claims, follow the lab's identification hierarchy: DiD → event study → IV → RDD → matching.

### Step 5: Output tables and figures

- `04_tables.{py,do}` → `output/tables/*.tex` (use `estout`/`outreg2` in Stata, custom LaTeX writer or `stargazer`/`pyfixest`-style in Python)
- `05_figures.{py,do}` → `output/figures/*.pdf` (matplotlib in Python; `graph export` + `graph_schemes.md` in Stata)

Figures: publication-ready by default — labelled axes, units in labels, no titles (the LaTeX caption is the title), legible at 50% scale.

### Step 6: Reproduce end-to-end

Write `00_run_all.{py,do}` that calls 01–05 in order. Run it once cleanly. Confirm all outputs in `output/` are regenerated and that nothing in `data/raw/` was touched.

### Step 7: Report

Summarise:
- Final N and sample
- Headline result with magnitude, SE, clustering level
- Files created
- Any open issue or assumption the user should confirm

## Notes

- Variable names in English; comments in English.
- UTF-8 throughout. In Stata, use `unicode encoding set utf-8` if reading non-ASCII files.
- Never commit anything in `data/` or `output/` to git.
- For restricted-data environments (e.g. MONA, register data on secure servers): scripts only, no data ever leaves; print statements ASCII-only; minimum cell-size rules apply per environment policy. Flag and ask if relevant.
