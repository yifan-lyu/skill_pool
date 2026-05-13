# /cite-audit — Citation Audit

Systematic pre-submission audit of all references in a paper. Walks you through verification one reference at a time.

## Arguments

`$ARGUMENTS` can include:
- A file path to a `.tex` or `.bib` file
- A project folder path (will auto-detect `.tex` and `.bib` files)
- *(none)* — auto-detect from current working context

## Instructions

### Step 1: Identify the Paper

- Find the main `.tex` file and `references.bib` (or inline bibliography)
- Parse all `\cite`, `\citet`, `\citep`, `\citeauthor`, `\citeyear` commands
- Extract the full reference list from the `.bib` file
- Count total references

### Step 2: Classify Each Reference

For each reference, determine category:

- **A (Structural):** The paper builds an argument on this source. Used in framing, framework, methodology, or core claims. Appears in multiple sections or is discussed at length.
- **B (Checked):** Cited for one specific claim, number, or finding. Typically appears once, attached to a specific sentence.
- **C (Inherited):** Standard/classic citation (textbooks, foundational works everyone cites). No verification needed beyond existence.

### Step 3: Verify Bibliographic Details

For each reference, verify against an authoritative source:
1. Journal articles with a DOI — confirm via the Crossref REST API (`https://api.crossref.org/works/<DOI>`) or the journal page. Check that title, authors, year, journal, volume, and pages match the `.bib` entry exactly.
2. Working papers, books, reports without a DOI — verify via NBER, IZA, SSRN, the publisher's catalogue, or the author's homepage.
3. Flag any entry where the canonical title or author list differs from the `.bib` entry — likely a bibliographic error.

Never trust model recall for bibliographic details. Always verify against the canonical source.

### Step 4: Walk Through A-Category Papers

For each A-category reference:
- Show: citation key, full bibliographic details, where it appears in the paper, how it's used
- Provide a readable link (working paper version if paywalled)
- Ask the user: "Have you read the relevant sections? [Y / N / partially]"
- If N: flag for reading before submission

### Step 5: Walk Through B-Category Papers (Survey Mode)

For each B-category reference, present in this format:

```
**[B] AuthorKey (Year)** — cited for: "[the specific claim in our paper]"
Paper: [readable link]
Relevant passage (p. XX): "[exact quote or close paraphrase from the source]"
Does this support our claim? [Y / N / needs nuance / skip for now]
```

Wait for your response before proceeding to the next one.

If the full text is not accessible (paywalled, no working paper found):
```
**[B] AuthorKey (Year)** — cited for: "[the specific claim]"
Paper: [best available link]
⚠️ Full text not accessible. Check in Papers.app: [page/table/section reference if known]
Does this support our claim? [Y / N / needs nuance / skip for now]
```

### Step 6: Summary Report

After walking through all references, provide:

```
## Citation Audit Summary — [Paper Title]
Date: [YYYY-MM-DD]

### Counts
- Total references: X
- A (Structural): X — verified: X, unread: X
- B (Checked): X — confirmed: X, needs nuance: X, unverified: X
- C (Inherited): X

### Action Items
- [ ] Read before submission: [list of unread A-papers]
- [ ] Verify in Papers.app: [list of inaccessible B-papers]
- [ ] Fix bibliographic details: [list of any broken references]
- [ ] References needing nuance: [list with notes]
```

Save this summary to the project folder as `cite-audit-[YYYY-MM-DD].md`.

### Notes

- Do NOT rush through. Wait for your response on each B-category item.
- If the audit is long (>20 references), offer to do it in batches (e.g., "Shall we do 10 now and continue later?").
- For any reference where the claim needs nuance, draft a revised sentence for you to consider.
- This skill complements the always-on citation protocol in CLAUDE.md. The protocol handles references as they are added; this skill handles the full audit before submission.
