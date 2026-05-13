# /paper-review — Pre-Circulation Paper Review

Structured self-review of an economics paper before sending to co-authors, external reviewers, or submission. Modelled on Cunningham's "Referee 2" idea: adversarial but constructive, focused on what a seminar discussant or journal referee would flag.

## Arguments

`$ARGUMENTS` can include:
- A file path to a `.tex`, `.md`, or `.pdf` file
- A project folder path (will auto-detect the main paper file)
- *(none)* — auto-detect from current working context

## Instructions

### Step 1: Read the Full Paper

Read the entire paper using the Read tool. For PDFs, extract with `pdftotext` first. **Read every word — no skimming.** Note the word count if relevant (e.g., Economics Letters: 2,000 words).

---

### Step 2: Write a Structured Summary

Before reviewing, write a summary to `[project]/notes/review-summary-[YYYY-MM-DD].md`. This forces complete comprehension and creates a reference document for the review.

```markdown
# Review Summary: [Title]
Date: [YYYY-MM-DD]

## Research question
[One sentence — what does the paper ask?]

## Identification strategy
[How does the paper answer the question? Name the method and key assumptions.]

## Key data
[What data, what period, what unit of observation?]

## Main claims (with location)
1. "[Claim as stated]" — [Section/paragraph where it appears]
2. ...

## Key magnitudes
- [Coefficient/effect size]: [value, SE, interpretation]

## Stated contributions
1. [What the paper says is new]

## Stated limitations
1. [What the paper acknowledges it cannot do]
```

---

### Step 3: Cross-Cutting Consistency Checks

Run these checks systematically. Each one compares two parts of the paper against each other. Report any inconsistency found.

**3a. Claims vs. Evidence**
- Does each claim in the abstract and introduction have a corresponding result in the paper?
- Are any results overstated relative to point estimates and standard errors?
- Does the conclusion introduce claims not supported by the analysis?

**3b. Causal Language vs. Identification**
- Is the causal language consistent with the identification strategy throughout?
- Are there places where the paper slips into causal language without warrant?
- Would a careful reader (Roth et al. 2023 level) object to any phrasing?

**3c. Magnitudes and Comparisons**
- Are effect sizes interpreted in meaningful units?
- Are comparisons to other studies fair (same outcome, same population, same margin)?
- Are any numbers stated in the text inconsistent with tables or figures?

**3d. Internal Consistency**
- Do the data description and the regression tables use the same sample sizes?
- Are variable definitions consistent between text, tables, and appendix?
- Do footnotes contradict or qualify main-text claims in ways a reader might miss?

**3e. What's Missing?**
- What is the most obvious alternative explanation a referee would raise?
- What robustness check would a seminar discussant ask for?
- Is there a relevant literature the paper doesn't engage with?

---

### Step 4: Section-by-Section Review

#### Introduction Structure Audit

Before flagging individual issues, map the introduction's structure. Label each paragraph's function, then assess against three standard economics templates:

**Template A: The Classic** (most common in top economics journals)
| ¶ | Purpose | Content |
|---|---------|---------|
| 1 | Hook | Motivating fact, puzzle, or policy question |
| 2–3 | Gap | What we know, what we don't, why the gap matters |
| 4 | Contribution | "This paper does X. We find Y." — state the result |
| 5–6 | Approach | Data, identification strategy, key assumptions |
| 7–8 | Results | Main findings with economic magnitudes |
| 9 | Roadmap | Section-by-section preview |

**Template B: The Puzzle-First** (effective when a stylised fact needs explaining)
| ¶ | Purpose | Content |
|---|---------|---------|
| 1 | Puzzle | Present a specific empirical puzzle or policy paradox |
| 2 | Resolution | "We show that X explains this" |
| 3–4 | Mechanism | Why does the resolution work? Economic intuition |
| 5–6 | Identification | How do we know causally? |
| 7–8 | Results | Evidence supporting the resolution, with magnitudes |
| 9 | Implications | What this means for policy or the literature |

**Template C: The Result-First** (strong when the headline finding is surprising)
| ¶ | Purpose | Content |
|---|---------|---------|
| 1 | Main result | State the headline finding immediately |
| 2–3 | Why surprising | Why is this non-obvious or contrary to priors? |
| 4–5 | How we know | Identification strategy and key threats addressed |
| 6–7 | Robustness | Address obvious objections upfront |
| 8 | Implications | What changes because of this finding? |
| 9 | Roadmap | Section preview |

**Deliverable:** Map the current introduction paragraph by paragraph, identify which template it most resembles (or whether it's a hybrid), and flag structural problems:
- Buried contribution (main result doesn't appear until page 3+)
- Literature review in disguise (paragraphs summarising other papers rather than positioning this one)
- Missing magnitudes in the results preview
- Weak motivation ("no one has studied this" is not motivation)
- Hedging the findings in the introduction (signals weak results)
- Missing identification preview (reader has no idea how causality is established)

Propose a restructured introduction if the current one has structural problems. Explain trade-offs between templates.

---

#### Section-Level Issues

Go through each section and flag specific issues. For each issue:

> **[Section]** `severity` `type`
> "[Exact quote from the paper]"
> Problem: ...
> Suggestion: ...

**Types:** `logic` `evidence` `language` `structure` `missing` `consistency`

**Severity (assign to each issue):**
- **major** — Undermines a key claim or would likely cause a desk rejection or R&R demand. A seminar discussant would raise this.
- **moderate** — Real issue, localisable and fixable. A careful referee would flag it.
- **minor** — Phrasing, framing, or ambiguity. Improves the paper but doesn't affect the argument.

**Calibration rule:** If all issues are the same severity, reconsider. Most papers have a mix. If you find zero major issues, say so explicitly — that's a good sign, not a failure of the review.

---

### Step 5: Present the Review

Present as follows:

---

**Overall assessment**

[One paragraph: the paper's core strength, its main vulnerability, and the single most important thing to fix before circulation. Be honest but constructive — this is for the user, not a referee report.]

---

### Major issues
*(or "No major issues found.")*

**[1] Title** `type`
> "Exact quote."
Problem: ...
Suggestion: ...

### Moderate issues

**[N] Title** `type`
> "Exact quote."
Problem: ...
Suggestion: ...

### Minor issues

**[N] Title** `type`
> "Exact quote."
Problem: ...
Suggestion: ...

---

Number issues sequentially across all tiers. At the end, state total counts: X major, Y moderate, Z minor.

---

### Step 6: Save and Offer Next Steps

Save the full review to `[project]/notes/review-[YYYY-MM-DD].md`.

Then offer:
1. "Want me to fix the moderate/minor issues now?" (for language, consistency, structure issues)
2. "Want me to draft responses to the major issues?" (for substantive issues that need the user's judgement)
3. "Ready for `/cite-audit`?" (if references haven't been audited yet)

---

## Design Principles

- **This is adversarial, not editorial.** The goal is to find problems, not polish prose. Save polishing for after the review.
- **Economics-specific.** The cross-cutting checks target what economics referees actually care about: identification, causal language, magnitudes, missing robustness.
- **Complements `/cite-audit`.** This skill reviews the argument; `/cite-audit` reviews the references. Run both before submission.
- **Honest about limits.** This catches logical and structural issues. It cannot substitute for domain experts (Hansson on tax policy, Lechner on CML, Skans on Swedish labour markets). Flag where expert input is needed.

## Acknowledgements

The structure of this skill builds on three ideas from **OpenAIReview** (ChicagoHAI, 2026; https://github.com/ChicagoHAI/OpenAIReview): (1) writing a structured summary before reviewing to anchor comprehension, (2) explicit cross-cutting consistency checks as separate review dimensions, and (3) severity tiering with a calibration rule. Their tool targets STEM papers with math-heavy notation; this adaptation focuses on what economics referees and seminar discussants actually flag. The adversarial self-review concept also draws on Cunningham's (2025-26) "Referee 2" idea of running a separate critical session on your own work. The introduction structure templates are adapted from Spina's (2026) "Editor" persona (https://github.com/aspi6246/ClaudeCodeTools), transposed from finance to economics conventions.
