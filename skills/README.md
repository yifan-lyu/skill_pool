# Skills

Curated skill files for empirical economics research with Python, Stata, and LaTeX. Designed for both Claude Code (as `/<name>` slash commands) and Codex (as plain markdown docs).

## Workflow

| Skill | When to use |
|-------|-------------|
| [`start.md`](start.md) | Beginning of a session — reads HANDOFF.md and orients |
| [`done.md`](done.md) | End of a session — writes HANDOFF.md and updates MEMORY.md |
| [`commit.md`](commit.md) | Stage, commit, push (safe defaults — never `-A`, never commit `data/`) |
| [`compile-latex.md`](compile-latex.md) | 3-pass XeLaTeX + bibtex build of paper or slides |

## Analysis

| Skill | When to use |
|-------|-------------|
| [`data-analysis.md`](data-analysis.md) | End-to-end pipeline: raw data → clean data → analysis → tables/figures |
| [`audit-reproducibility.md`](audit-reproducibility.md) | Verify the paper's numbers match what the code produces |
| [`stata/SKILL.md`](stata/SKILL.md) | Stata reference: syntax, econometrics, 20 community packages |

## Review (pre-circulation / pre-submission)

| Skill | When to use |
|-------|-------------|
| [`paper-review.md`](paper-review.md) | Structured pre-circulation review (one-pass, adversarial-but-fair) |
| [`personas-review.md`](personas-review.md) | Multi-persona pre-submission review (Identification Skeptic + Measurement Critic + Theorist + Editor, in parallel) |
| [`estimate-audit.md`](estimate-audit.md) | Deep audit of empirical strategy, data construction, and implementation |
| [`cite-audit.md`](cite-audit.md) | Citation-by-citation pre-submission audit |
| [`verify-claims.md`](verify-claims.md) | Independent fact-check of factual claims (chain-of-verification) |
| [`proofread.md`](proofread.md) | Typos, grammar, style polish |
| [`slide-review.md`](slide-review.md) | Beamer deck: layout + pedagogy + audience-fit |

## Refereeing & R&R

| Skill | When to use |
|-------|-------------|
| [`referee.md`](referee.md) | Draft a referee report on a paper assigned to you |
| [`r-n-r.md`](r-n-r.md) | Turn referee reports into a dependency-ordered revision plan |

## Research planning

| Skill | When to use |
|-------|-------------|
| [`lit-review.md`](lit-review.md) | Targeted literature scan with structured synthesis |
| [`research-ideation.md`](research-ideation.md) | Generate and pressure-test 5–8 candidate research questions |
| [`preregister.md`](preregister.md) | Draft an OSF / AsPredicted / AEA RCT preregistration |

---

## Reading order for a fresh project

1. `start.md` — every session
2. `research-ideation.md` → `lit-review.md` — early scoping
3. `preregister.md` — once the design is clear
4. `data-analysis.md` — running the analysis
5. `paper-review.md` → `estimate-audit.md` → `cite-audit.md` → `verify-claims.md` → `audit-reproducibility.md` — before circulation
6. `personas-review.md` — before submission
7. `proofread.md` → `compile-latex.md` → `commit.md` — final
8. `done.md` — every session

## Stata reference

`skills/stata/` is a self-contained progressive-disclosure reference (37 topic files + 20 community-package guides). Start with `skills/stata/SKILL.md` — it routes to whichever subset is relevant. Adapted from [dylantmoore/stata-skill](https://github.com/dylantmoore/stata-skill).

## Acknowledgements

The review/audit/preregister skills are adapted from the [AI-Econ Lab Claude Code repo](https://github.com/ai-econ-lab) at Örebro University. Stata reference adapted from dylantmoore/stata-skill. Personas-review owes its structure to OpenAIReview (ChicagoHAI 2026) and Cunningham's "Referee 2" concept.
