# /referee — Write a Referee Report

Draft a referee report following a structured workflow. Adversarial but fair — focused on what the argument actually supports, not surface polish.

## Arguments

- *(none)* — Start from scratch: set up folder, extract manuscript, prompt for your first take
- `<path>` — Path to manuscript PDF (skips setup prompt)
- `assess` — Only Steps 1–4 (argument map + assessment of your take), no draft yet
- `draft` — Jump to drafting (assumes manuscript already read)

## Instructions

### Step 1: Set up

Create a folder:
```bash
mkdir -p ~/[your-workspace]/admin/referee/<JOURNAL>-<YYYY>-<MM>
```
Create `README.md` with: journal, editor, manuscript ID, round, deadline, status.
Create `review.md` with a "first take" block at the top and section headers below.

Ask if not already provided: journal, editor, deadline, manuscript ID.

### Step 2: Extract manuscript

```bash
pdftotext -layout <manuscript>.pdf manuscript.txt
```

Read `manuscript.txt` end to end. No skimming. Including appendices and robustness tables.

### Step 3: Map the argument structure

Before reading your first take, map the paper's argument:

- **Core claim** — the paper's central finding in one sentence
- **Load-bearing nodes** — the 3–5 claims the core finding depends on
- **Decorative nodes** — claims that add texture but whose failure would not sink the paper
- **Weak points** — nodes where support is thinnest

Present this map before you write your first take, so your critique anchors on load-bearing structure rather than surface features.

### Step 4: Write your first take

Fill in the "first take" block in `review.md`. Raw notes, no structure needed — overall lean, main concerns, specific passages. Claude waits.

### Step 5: Evaluate your take

For each point you raise:
- **Strong** — well-supported, survives a targeted author rebuttal
- **Partially valid** — correct direction but overstated, or applies only to part of the evidence
- **Overstated** — the manuscript actually addresses this, or the claim is too strong

Cross-check every claim against `manuscript.txt`. Add issues you did not catch, especially from robustness tables and appendices.

Flag any point that would not survive a targeted rebuttal from the author.

### Step 6: Consistency check

Before drafting, check your combined feedback for internal consistency:
- Do any two comments contradict each other?
- Is the major/minor classification consistent with the argument map?
- Are major comments ordered from most fundamental to least?

Surface any conflicts before drafting.

### Step 7: Draft the report

Style rules:
- British English (labour, behaviour, analyse)
- No em-dashes — use commas, colons, parentheses
- First-person, direct, measured
- Section headers: Summary / Some major comments / Some minor comments
- Major comments numbered, plain sentence lead (no bold labels)
- Do NOT advise against publication in the author-facing report

Save draft below the assessment block in `review.md`.

### Step 8: Iterate

Push back on specific sections; Claude tightens or rewrites. Repeat until satisfied.

### Step 9: Extract and convert

Extract clean report to `report.md` (no raw notes or assessment scaffolding).

Convert to .docx:
```bash
pandoc report.md -o report.docx
```

### Step 10: Editor note

Draft a separate confidential note to the editor. Keep it in `editor-note.txt` — paste into the journal system's confidential field, not into the report.

## Style reminder

Test sentence: would Acemoglu or Autor write this? If not, rewrite.
Never generate bibliographic details from memory — verify against the manuscript's bibliography.

## Common gotchas

- Some journal systems (e.g. ScholarOne for ILR) reject PDFs — use .docx
- `O*NET` in markdown breaks pandoc — escape as `O\*NET`
- Clipboard copy on Mac: `cat file | pbcopy`
