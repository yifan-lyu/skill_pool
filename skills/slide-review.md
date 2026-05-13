# /slide-review — Beamer slide deck review

Combined review of a Beamer slide deck for layout, pedagogy, and overall excellence. Merges what would otherwise be three separate passes (visual audit, pedagogy review, slide excellence) into one structured walk-through.

## Arguments

- `<file>` — path to a `.tex` slide deck (must compile to PDF)
- *(none)* — auto-detect the most recent deck in `slides/`

## Instructions

### Step 1: Compile and read

Compile the deck first with `/compile-latex` if no PDF exists or the PDF is older than the `.tex`. Then read the `.tex` source end to end. Extract slide count and section structure.

### Step 2: Three-pass review

Run three passes over the deck. Report findings grouped by pass, not by slide.

#### Pass A — Visual / layout

For each slide, check:
- **Overflow** — does any frame run off the page? (look for `Overfull \vbox` in the log)
- **Density** — too many bullets, too much text, font too small? Rule of thumb: ≤6 lines of body text per slide, ≤7 words per bullet
- **Hierarchy** — is the title clear? Is the takeaway visible at a glance?
- **Figures** — are figures legible at projection size? Are axes labelled? Are units shown?
- **Inconsistencies** — fonts, colours, capitalisation of titles, alignment

#### Pass B — Pedagogy / narrative

For the deck as a whole:
- **Arc** — is there a clear opening (question), middle (evidence), close (takeaway)?
- **Signposting** — does the audience know where they are? Section dividers, "roadmap" slides at transitions
- **Notation** — introduced before use? Consistent across slides?
- **Pacing** — too many slides on one idea, or one slide trying to cover too much?
- **Motivation** — does each major section open with *why*, not *what*?
- **Takeaway slide** — is there a final summary the audience can photograph?

#### Pass C — Audience-fit / excellence

Ask: who is this for? Then check:
- For a **seminar** (technical audience): are the identification details surfaced? Are robustness checks previewed?
- For a **policy / general audience**: is jargon defined? Are magnitudes given in interpretable units?
- For **conference**: is the contribution sharp? Is the headline result on slide 2 or 3, not slide 15?

### Step 3: Report

Structure:

```
## Slide Review: [Deck title]
Date: [YYYY-MM-DD]
Slide count: N

### Overall assessment
[One paragraph: strongest aspect, weakest aspect, single most important fix.]

### Critical issues
*(Would derail the talk. Fix before presenting.)*
- [slide N] type — description — fix

### Moderate issues
*(Reduce clarity or polish. Fix if time permits.)*
- [slide N] type — description — fix

### Minor issues
*(Cosmetic.)*
- [slide N] type — description — fix
```

Number issues sequentially. State totals: X critical, Y moderate, Z minor.

### Step 4: Offer next steps

- "Want me to fix the moderate/minor issues now?"
- "Want me to restructure a specific section?"
- "Want me to draft a takeaway slide?"

## Notes

- Compile after any fix to confirm no overflow or broken references introduced.
- If the deck uses TikZ figures, flag any that fail to render or have illegible labels.
- Do not change the deck's content claims — only their presentation.
