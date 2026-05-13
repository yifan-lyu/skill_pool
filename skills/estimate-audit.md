# /estimate-audit — Estimation and Data Audit

Deep audit of the empirical strategy, data construction, and statistical implementation in an economics paper. This is the "econometrician referee" pass — focused on whether the estimation does what the paper claims it does.

## Arguments

`$ARGUMENTS` can include:
- A file path to a `.tex`, `.md`, or `.pdf` file
- A project folder path (will auto-detect the main paper file)
- *(none)* — auto-detect from current working context

## Instructions

### Step 1: Read Everything

Read the full paper, appendix, and any code files in the project's `src/` or `scripts/` folder. For PDFs, extract with `pdftotext` first. **Read every word — no skimming.** If code is available, read it — discrepancies between described and implemented methods are among the most common errors.

---

### Step 2: Map the Empirical Architecture

Write a structured map to `[project]/notes/estimate-audit-map-[YYYY-MM-DD].md`:

```markdown
# Empirical Architecture: [Title]
Date: [YYYY-MM-DD]

## Identification strategy
[Name the method. State the key identifying assumption in one sentence.]

## Estimating equation(s)
[Write out each equation as stated in the paper. Note equation numbers.]

## Treatment and outcome
- Treatment: [variable, how measured, variation exploited]
- Outcome: [variable, how measured, level of observation]
- Unit of observation: [what is a row in the regression?]

## Sample construction
- Source data: [dataset, years, population]
- Key restrictions: [who is dropped and why]
- Final sample size: [N, as stated]

## Fixed effects and controls
- Fixed effects: [list, with level]
- Controls: [list]
- Why these? [does the paper justify the specification?]

## Standard errors
- Clustering level: [as stated]
- Justification: [does the paper explain the clustering choice?]

## Key tables/figures
- [Table X]: [what it shows, specification]
- [Figure X]: [what it shows]
```

---

### Step 3: Identification Audit

Work through these checks systematically. For each, state whether the paper passes, fails, or is ambiguous.

**3a. Does the method match the claim?**
- If DiD: are there two periods and two groups, or is this staggered? If staggered, does the paper use appropriate methods (Callaway & Sant'Anna, Sun & Abraham, or justify TWFE)?
- If IV: is the first stage reported? Is the instrument discussed for both relevance and exclusion?
- If RDD: is the running variable shown? Bandwidth sensitivity? McCrary test?
- If event study: are pre-trends shown and discussed? How many pre-periods? Is the reference period clear?
- If matching/PSM: is balance shown? Common support? Sensitivity to specification?

**3b. Threats to identification**
- What is the most obvious confound? Does the paper address it?
- Could reverse causality operate? Does the paper discuss timing?
- Is there selection into treatment? How is it handled?
- For DiD specifically: is the parallel trends assumption testable here, and is it tested?

**3c. Treatment variable scrutiny**
- Is the treatment clearly defined and measured?
- Is there measurement error in the treatment? What direction would attenuation bias go?
- For continuous treatment: is linearity assumed? Is a dose-response shown?
- For AI exposure measures specifically: which measure, what vintage, what crosswalk to occupation codes?

---

### Step 4: Data Audit

**4a. Sample construction**
- Can a reader replicate the sample from the description? Are all restrictions stated?
- Are there unexplained jumps in sample size between tables?
- Is attrition or missing data discussed? What share is lost at each step?

**4b. Variable definitions**
- Is every variable in the tables defined in the text or appendix?
- Are outcome variables measured consistently across the sample period?
- For occupation-level variables: what classification (SSYK, ISCO, SOC)? What digit level? Any crosswalk issues?

**4c. Descriptive statistics**
- Is there a summary statistics table? Does it cover treatment and outcome?
- Do the means and SDs make sense given the population?
- Are there outliers that could drive results? Is winsorisation discussed?

---

### Step 5: Implementation Audit

**5a. Tables vs. text**
- Does every regression coefficient mentioned in the text match the corresponding table cell?
- Are significance levels correctly reported (check stars against SEs)?
- Do sample sizes in table notes match the described sample?

**5b. Standard errors**
- Is the clustering level appropriate for the level of treatment variation?
- If treatment varies at group level but SEs are clustered at individual level, flag this.
- For few clusters (<50): does the paper discuss or use wild bootstrap, randomisation inference, or effective degrees of freedom?

**5c. Robustness**
- Does the paper run robustness checks that actually address the main identification threat?
- Or are the robustness checks "easy wins" that don't test what matters?
- What robustness check is missing that a referee would ask for?

**5d. Code vs. paper (if code is available)**
- Do the variable names in code match the described variables?
- Are the fixed effects and clustering in the code what the paper says?
- Are there data cleaning steps in the code not mentioned in the paper?

---

### Step 6: Present the Audit

Present as follows:

---

**Empirical assessment**

[One paragraph: the core strength of the identification, the main vulnerability, and overall confidence in the results. Be direct.]

---

### Critical issues
*(Issues that could invalidate the main result. A referee would demand revision.)*

**[1] Title** `identification` / `data` / `implementation`
> "Exact quote from the paper."
Problem: ...
What to do: ...

### Substantive issues
*(Real gaps a careful referee would flag. Fixable but require work.)*

**[N] Title** `identification` / `data` / `implementation`
> "Exact quote from the paper."
Problem: ...
What to do: ...

### Minor issues
*(Presentation, completeness, or ambiguity. Quick fixes.)*

**[N] Title** `identification` / `data` / `implementation`
> "Exact quote from the paper."
Problem: ...
What to do: ...

---

Number issues sequentially. State totals: X critical, Y substantive, Z minor.

---

### Step 7: Save and Offer Next Steps

Save the full audit to `[project]/notes/estimate-audit-[YYYY-MM-DD].md`.

Then offer:
1. "Want me to fix the minor/presentation issues now?"
2. "Want me to draft responses or revisions for the substantive issues?"
3. "Want me to check the code against the paper systematically?" (if code exists but wasn't fully audited)
4. "Ready for `/paper-review` or `/cite-audit`?" (if those haven't been run yet)

---

## Design Principles

- **This is the econometrician referee.** Think Angrist, Imbens, or Roth reading the methods section. What would they flag?
- **Code is evidence.** When code is available, discrepancies between code and paper are findings, not noise.
- **Calibrate to the method.** A DiD paper gets DiD-specific checks; an IV paper gets IV-specific checks. Don't run irrelevant checklists.
- **Complements `/paper-review` and `/cite-audit`.** This skill audits the empirical engine; `/paper-review` audits the argument; `/cite-audit` audits the references.
- **Honest about limits.** This cannot substitute for running the code on the actual data. It audits internal consistency and methodological appropriateness. For papers using restricted-access data, the data audit is necessarily incomplete. Flag where only a replication on the data would resolve a question.

## Acknowledgements

The structure of this skill builds on standard practices in empirical economics refereeing, particularly the methodological checklists implicit in Angrist & Pischke (2009, *Mostly Harmless Econometrics*), the DiD audit points in Roth et al. (2023, *Journal of Econometrics*), and the replication protocol of the AEA Data Editor. The idea of systematic pre-submission self-auditing as an AI-assisted workflow draws on Cunningham (2025-26) and the multi-pass architecture of OpenAIReview (ChicagoHAI, 2026).
