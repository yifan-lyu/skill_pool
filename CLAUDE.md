# Project context — Claude Code + Codex

<!-- This file is read by Claude Code (CLAUDE.md) and Codex (via AGENTS.md, which mirrors this file).
     Replace [BRACKETED] placeholders with your project info when you copy this template into a new project. -->

**Project:** [PROJECT NAME]
**Status:** [Draft / In progress / Under review / R&R / Submitted]
**Co-authors:** [Names]
**Target journal:** [Journal]

---

## What this project is

[One paragraph: the question, the identification strategy, the data, why it matters.]

---

## Folder structure

```
[project-root]/
├── CLAUDE.md            # this file
├── AGENTS.md            # mirror for Codex
├── README.md            # human-readable overview
├── MEMORY.md            # cross-session [LEARN] entries
├── HANDOFF.md           # last-session state (/done writes, /start reads)
├── data/
│   ├── raw/             # never modified, never committed
│   └── clean/           # analysis-ready, produced by code/, not committed
├── code/
│   ├── python/          # .py scripts, numbered 00_run_all, 01_load, 02_clean…
│   └── stata/           # .do scripts, same numbering
├── writing/             # LaTeX paper(s), .bib, paper figures
├── slides/              # Beamer .tex decks, slide figures
├── output/
│   ├── tables/          # .tex tables produced by code, \input{} into writing/
│   ├── figures/         # .pdf figures produced by code
│   └── logs/            # run logs
└── skills/              # skill files invokable as /<name> in Claude Code; read as docs by Codex
```

---

## Tooling conventions

### Python
- Python 3.10+
- `pandas` for data manipulation
- `statsmodels` or `linearmodels` for econometrics (not sklearn for causal inference)
- `matplotlib` for figures
- `pathlib` for paths (not `os.path`)
- UTF-8 throughout
- Variable names and comments in English

### Stata
- Use `reghdfe` for fixed-effects regressions
- `estout` / `outreg2` for publication-quality tables → `output/tables/`
- `csdid`, `did_multiplegt` for staggered DiD
- `rdrobust` for RDD; `ivreg2` for IV
- Always `bysort` rather than bare `by`
- Guard for missing: `gen x = (y > 0) if !missing(y)` — Stata missings sort to +∞
- See `skills/stata/SKILL.md` for the full reference

### LaTeX
- XeLaTeX (handles Unicode natively — å, ä, ö, é)
- Compile via `/compile-latex` (3-pass + bibtex)
- Paper sources in `writing/`, slide decks in `slides/`
- Tables produced by code go in `output/tables/*.tex`, then `\input{...}` from the paper — never hand-edit numbers in the paper

### Git
- `git add` specific files, never `-A` or `.`
- Never commit anything in `data/` or `output/` (see `.gitignore`)
- Commit messages focus on the *why*, not the *what*
- Use `/commit` to stage + commit

---

## Writing conventions

- **British English**: labour, behaviour, analyse, organisation, colour
- **Academic register** for papers; **plain prose** for policy and stakeholder writing
- **No unqualified superlatives.** Every substantive claim needs a reference or evidence
- **Minimise em-dashes** — use commas, colons, or parentheses
- Test: would Acemoglu or Autor write this sentence?

---

## Data security

If working with restricted data (e.g. register data on a secure server):
- Scripts only — never upload data files to cloud AI
- Strip identifiers before sharing any output
- Aggregated outputs only; check the environment's minimum-cell-size rule
- Print statements ASCII-only if the environment requires it

When in doubt, treat data as restricted.

---

## Citation protocol

Every reference is classified:
- **A (Structural):** Paper whose argument we build on. Must be read and defensible.
- **B (Checked):** Cited for one specific claim. Verify that exact claim in the original.
- **C (Inherited):** Standard citation everyone uses. Verify it exists; no further flagging needed.

**Never generate bibliographic details from memory.** Verify author names, titles, journals, volumes, and pages against the canonical source (DOI lookup, journal page, NBER/IZA/SSRN, author page) before writing any reference.

---

## Identification methods (in order of preference)

1. Difference-in-differences (DiD) — standard and staggered adoption
2. Event studies — dynamic treatment effects, pre-trend testing
3. Instrumental variables (IV)
4. Regression discontinuity (RDD)
5. Matching / propensity score methods

Key references: Callaway & Sant'Anna (2021), Sun & Abraham (2021), Roth et al. (2023), de Chaisemartin & D'Haultfœuille (2020).

---

## Skills

Skills live in `skills/`. Each is a markdown file the agent reads when invoked. In Claude Code, install for slash-command access with:

```bash
mkdir -p ~/.claude/skills
for f in skills/*.md; do
  name=$(basename "$f" .md)
  mkdir -p ~/.claude/skills/"$name"
  cp "$f" ~/.claude/skills/"$name"/"$name".md
done
cp -r skills/stata ~/.claude/skills/stata
```

In Codex, the skill files are referenced as plain docs — open `skills/<name>.md` when relevant or ask the agent to read it.

See `skills/README.md` for the index.

---

## Project-specific notes

[Add anything that doesn't fit above — collaborators' conventions, data quirks, journal-specific style requirements, deadlines.]
