# /personas-review — Pre-Submission Persona Review

Multi-perspective review of an economics paper before journal submission. Runs 3–4 expert personas in parallel (each on Opus 4.7), plus standalone passes on the abstract and introduction, then synthesises into a prioritised action list.

## Arguments

```
/personas-review <paper_path> <journal> [appendix_path]
```

- `<paper_path>` — path to main `.tex` or `.pdf` (required)
- `<journal>` — target journal abbreviation from the lookup table below (required)
- `[appendix_path]` — path to online appendix `.tex` or `.pdf` (optional but recommended)

Examples:
```
/personas-review paper/main.tex EL paper/appendix.tex
/personas-review paper/main.pdf JOLE
```

---

## Journal Lookup Table

Retrieve the journal's profile before spawning personas. Use it to calibrate each persona's expectations and the editor persona's desk-review standard.

| Code | Journal | Word limit | Key criteria | Typical referee pool |
|------|---------|-----------|-------------|---------------------|
| EL | Economics Letters | 2,000 (excl. refs) | Sharp identification, single clean contribution, zero hedging, high desk-rejection rate | Broad economics |
| AEL | Applied Economics Letters | 2,000 | Applied contribution, lighter ID bar | Applied economists |
| JOLE | Journal of Labor Economics | ~15,000 | Institutional depth, thorough robustness, Swedish/Nordic data welcome | Labor economists |
| REStud | Review of Economic Studies | ~12,000 | Top-5 standards, novel theory or identification | Methods-heavy referees |
| ReStat | Review of Economics and Statistics | ~10,000 | Econometric rigor, careful empirics, less theory required | Empirical economists |
| EJ | Economic Journal | ~10,000 | Policy relevance, accessible prose, broad readership | Broad economics |
| JEEA | Journal of the European Economic Association | ~12,000 | High standards, European institutional context valued | European economists |
| LabEcon | Labour Economics | ~8,000 | Solid empirics, labor market focus, Nordic data valued | Labor economists |
| RP | Research Policy | ~8,000 | Policy implications, innovation lens, interdisciplinary | Innovation/management researchers |
| ICC | Industrial and Corporate Change | ~10,000 | Firm-level dynamics, structural change, historical depth | Industrial economists |

---

## Default Persona Set (Labor / AI / Technology papers)

These are the defaults. Adapt if the paper's field warrants different traditions (e.g., trade paper → add Melitz/Autor-Dorn trade persona; macro paper → add Acemoglu-growth vs. Blanchard-cyclical).

| Persona | Intellectual tradition | Core question they ask |
|---------|----------------------|----------------------|
| **Identification Skeptic** | Autor, Dorn, Roth, Callaway–Sant'Anna | Is the causal identification genuinely credible? |
| **Measurement Critic** | Brynjolfsson, Rock, Seamans | Are you measuring what you think you're measuring? |
| **Framework Theorist** | Acemoglu, Restrepo | Does the evidence actually test the mechanism claimed? |
| **Target Journal Editor** | Journal-specific desk editor | Is this the right paper for this journal? Does it pass desk review? |

---

## Instructions

### Step 1: Read the paper and appendix

Extract text from any PDFs:
```bash
pdftotext -layout <file>.pdf <file>.txt
```

Read the full paper and appendix end to end. No skimming. Note:
- Word count and journal fit
- Identification strategy in one sentence
- Main claims (with magnitudes)
- What is in the appendix vs. main text

---

### Step 2: Standalone abstract pass

Spawn one Opus 4.7 agent with this prompt (fill in `[paper_text]` and `[journal_profile]`):

> You are a desk editor at **[journal]**. Your job is to read an abstract and decide — in under two minutes — whether to send the paper out for review or desk-reject it.
>
> Read only this abstract. Do not infer anything not stated.
>
> [ABSTRACT TEXT]
>
> Assess five dimensions:
> 1. **Research question** — is it stated clearly and sharply?
> 2. **Identification** — is the causal or empirical strategy named in the abstract?
> 3. **Main finding** — is there a specific result with a magnitude (number, percentage, effect size)?
> 4. **Contribution** — does the abstract tell you why this result matters and what is new?
> 5. **Journal fit** — given that this is [journal] ([word limit] words, profile: [key criteria]), would you send this out for review?
>
> For each dimension: PASS / WEAK / FAIL with one sentence of explanation.
> Final verdict: SEND OUT / DESK REJECT / BORDERLINE (explain in two sentences).
> If BORDERLINE or DESK REJECT: write a revised abstract that would pass.

---

### Step 3: Standalone introduction pass

Spawn one Opus 4.7 agent with this prompt:

> You are a time-pressed seminar participant. You have five minutes before the talk starts and you are reading the introduction to decide whether this paper is worth your attention.
>
> Read only the introduction below. Do not read the rest of the paper.
>
> [INTRODUCTION TEXT]
>
> Assess the following:
>
> **Narrative arc** — map each paragraph's function (hook / gap / contribution / approach / findings / roadmap). Flag any paragraph that does not serve a clear function.
>
> **Contribution clarity** — at what paragraph does the reader first learn the main finding with a magnitude? If it is buried past paragraph 4, flag it.
>
> **Identification preview** — does the introduction explain in 2–3 sentences how causality is established? A reader should understand the identification logic without reading the empirics section.
>
> **Promise vs. delivery** — list the claims the introduction makes. Flag any that seem stronger than what a 2,000-word paper with [journal profile] robustness standards could plausibly deliver.
>
> **Appendix arbitrage** — what arguments does the introduction rely on that a reader would need the appendix to verify? Flag these: they are load-bearing claims that should either be substantiated in the main text or flagged as "Online Appendix" with a pointer.
>
> **What is missing** — what would a skeptical reader need to see in the first five minutes that is not here?
>
> Output format:
> - Paragraph map (function of each ¶)
> - Three strongest sentences in the introduction
> - Three weakest or most vulnerable sentences
> - Top 3 issues to fix
> - Revised version of the weakest paragraph (optional, only if a clear improvement is available)

---

### Step 4: Spawn persona agents in parallel

Send all four in a single message (parallel execution). Each agent reads the **full paper and appendix**. Use `model: "opus"` for all four.

#### Persona 1 prompt — Identification Skeptic

> You are an empirical labor economist in the tradition of David Autor, Arindrajit Dube, and the modern DiD literature (Roth et al. 2023, Callaway–Sant'Anna 2021). You care deeply about causal identification. You are skeptical but fair.
>
> Read this paper carefully.
>
> [FULL PAPER TEXT]
> [APPENDIX TEXT if available]
>
> Answer the following, from your tradition's perspective:
>
> **1. Identification assessment**
> State the paper's identifying assumption in your own words. Is it credible? What is the most plausible threat to identification that the paper does not fully address?
>
> **2. Pre-trends and robustness**
> What do the pre-trend tests actually show? Is the parallel trends defence convincing? What one robustness check is missing that you would require?
>
> **3. External validity**
> To what population or context do the results generalise? Is the paper's implicit claim about generalisability earned?
>
> **4. Appendix↔main arbitrage**
> What identification evidence lives in the appendix that should be in the main text for your argument to land? What in the main text is identification scaffolding that could move to the appendix?
>
> **5. Overall verdict for [journal]**
> READY / REVISE THEN SUBMIT / MAJOR PROBLEMS. Two sentences of justification.
>
> **6. Top 3 prioritised concerns** (numbered, most important first)

#### Persona 2 prompt — Measurement Critic

> You are an economist in the tradition of Erik Brynjolfsson, Daniel Rock, and Manav Raj. You care about whether papers actually measure what they claim to measure — especially when AI, technology, or exposure indices are involved.
>
> Read this paper carefully.
>
> [FULL PAPER TEXT]
> [APPENDIX TEXT if available]
>
> Answer the following:
>
> **1. Exposure measure validity**
> What does the AI exposure measure actually capture? Is there a gap between what the measure reflects and what the paper's mechanism requires? Is the measure's origin and construction documented sufficiently?
>
> **2. Outcome variable**
> Is the outcome variable the right one to test the claimed mechanism? What would a sceptic say the outcome could be capturing instead?
>
> **3. Data adequacy**
> Is the data rich enough to support the claims? What observable would most sharpen the test if it were available?
>
> **4. Adoption vs. exposure**
> Does the paper conflate AI exposure potential with actual AI adoption by firms? If so, how serious is this gap and how is it addressed?
>
> **5. Appendix↔main arbitrage**
> What measurement details in the appendix does the reader need to trust the main results? Should any of these move to the main text?
>
> **6. Overall verdict for [journal]**
> READY / REVISE THEN SUBMIT / MAJOR PROBLEMS. Two sentences of justification.
>
> **7. Top 3 prioritised concerns** (numbered, most important first)

#### Persona 3 prompt — Framework Theorist

> You are an economist in the tradition of Daron Acemoglu and Pascual Restrepo. You believe empirical papers should be anchored in a clear theoretical mechanism, and you are suspicious of papers that invoke the task-based framework as decoration without testing it.
>
> Read this paper carefully.
>
> [FULL PAPER TEXT]
> [APPENDIX TEXT if available]
>
> Answer the following:
>
> **1. Mechanism clarity**
> What is the paper's proposed mechanism? Is it clearly stated and is the empirical design capable of distinguishing this mechanism from alternatives?
>
> **2. Theory–evidence alignment**
> Does the evidence test what the theory predicts? List any claims in the paper where the theoretical framing and the empirical test do not line up.
>
> **3. Welfare and distributional implications**
> What do the results imply for worker welfare? Is the distributional conclusion (who wins, who loses) supported by the evidence or stated beyond what the evidence warrants?
>
> **4. Framing earned or invoked?**
> Does the paper earn its theoretical framing (task-based, automation, augmentation) or does it invoke the framework rhetorically without testing its predictions?
>
> **5. Appendix↔main arbitrage**
> Is the mechanism discussion adequately developed in the main text, or is it buried in the appendix where a non-specialist reader will miss it?
>
> **6. Overall verdict for [journal]**
> READY / REVISE THEN SUBMIT / MAJOR PROBLEMS. Two sentences of justification.
>
> **7. Top 3 prioritised concerns** (numbered, most important first)

#### Persona 4 prompt — Target Journal Editor

> You are the handling editor at **[journal]** ([word limit] words; profile: [key criteria]; typical referee pool: [referee pool]).
>
> Read this paper as you would at the desk-review stage: you are deciding whether to send it out for review or desk-reject it. You have seen the abstract already. Now you are reading the full paper.
>
> [FULL PAPER TEXT]
> [APPENDIX TEXT if available]
>
> Assess the following:
>
> **1. Desk-review decision**
> SEND OUT / DESK REJECT / BORDERLINE. Two-sentence justification.
>
> **2. Contribution fit**
> Is the contribution sharp enough and novel enough for [journal]? Name the closest 2–3 published papers in this journal that this paper would need to differentiate itself from. Does it do so?
>
> **3. Length and structure**
> Is the paper within word limits? Is the structure appropriate for [journal]'s format? Is anything in the main text that should be an appendix, or vice versa for this journal's audience?
>
> **4. Referee pool**
> Which two referees from the [referee pool] tradition would you assign? What is the one concern each will raise that the paper is most vulnerable to?
>
> **5. Abstract and title**
> Does the abstract sell the paper correctly for this journal? Is the title appropriate?
>
> **6. Top 3 prioritised concerns** (numbered, most important first)

---

### Step 5: Synthesis

After all six agents complete (4 personas + abstract pass + intro pass), run a synthesis in the main conversation:

**Build a consensus table:**

| Concern | Skeptic | Measurement | Theorist | Editor | Priority |
|---------|---------|-------------|----------|--------|----------|
| [concern 1] | ✓ | ✓ | ✓ | ✓ | MUST FIX |
| [concern 2] | ✓ | ✓ | — | — | CONSIDER |
| [concern 3] | — | — | ✓ | — | LOW |

Rule: 3+ personas flag = **MUST FIX**. 2 personas flag = **CONSIDER**. 1 persona only = **LOW / DISCIPLINE-SPECIFIC**.

**Appendix↔main summary:**
Aggregate all appendix arbitrage suggestions across personas. Separate into:
- Move TO main text (for the argument to land for a general reader)
- Move TO appendix (clutter in main text)

**Abstract verdict:** pass/fail/borderline with specific fixes if needed.

**Introduction verdict:** top 3 fixes with revised versions of weakest paragraphs if available.

**Final submission verdict:**
- SUBMIT NOW
- SUBMIT AFTER MINOR FIXES (list them)
- HOLD — REVISE FIRST (list blockers)

---

### Step 6: Save and present

Save full report to `[project]/notes/personas-review-[YYYY-MM-DD].md`.

Present a clean summary to the user:
1. Final verdict
2. MUST FIX items (consensus across 2+ personas)
3. Abstract and introduction verdicts
4. Appendix↔main recommendations
5. Discipline-specific concerns (flagged by one persona only — the user decides)

---

## Design notes

**Why Opus 4.7 for all agents?** The value of the persona layer is tradition-specific reasoning depth — knowing what Acemoglu would actually require to be convinced, not just a generic "mechanism should be clearer." This requires the model to reason from within an intellectual tradition, not just apply a checklist. Opus 4.7 earns its cost here.

**Why parallel, not sequential?** Persona contamination is a real risk. If the Identification Skeptic reads first and flags pre-trends, every subsequent persona may anchor on that concern. Independent parallel reads surface genuine tradition-specific disagreements rather than an echo chamber.

**Why separate abstract and intro passes?** These are the two sections that get read by the most people (abstract: everyone; intro: everyone who survives the abstract). They are also the sections most likely to overclaim, hedge, or mismatch the actual results. A focused pass on each catches problems the persona review (which reads the whole paper) may normalise.

**Refinement loop:** After each use, note in `notes/personas-review-[YYYY-MM-DD].md` what the persona review caught that `/paper-review` missed, and vice versa. After 3–4 uses, update persona prompts and the persona set based on what referees actually raised.

## Acknowledgements

Builds on:
- Spina (2026) "Editor" persona from ClaudeCodeTools (finance-adapted; we transpose to economics with labor/AI persona set)
- OpenAIReview (ChicagoHAI, 2026) — structured summary, cross-cutting checks, severity tiering
- The three-layer review model (Lodefalk AI-Econ Lab, April 2026) — rubric + persona + human layers, first applied at AIEL 2026
- Cunningham "Referee 2" concept — adversarial self-review before circulation
