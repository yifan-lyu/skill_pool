# /compile-latex — Build a LaTeX document

3-pass XeLaTeX + BibTeX build. Works for both papers (in `writing/`) and slides (in `slides/`).

## Arguments

- `<file>` — path to the `.tex` file (without or with the `.tex` extension)
- *(none)* — auto-detect the main `.tex` file in `writing/` first, then `slides/`

## Instructions

### Step 1: Locate the file

Resolve `$ARGUMENTS` to an absolute path. If ambiguous (more than one main `.tex` in the directory), list candidates and ask which to build.

### Step 2: Run the 3-pass build

`cd` into the file's directory so relative paths to figures and `references.bib` resolve correctly.

```bash
cd <dir>
xelatex -interaction=nonstopmode <file>.tex
bibtex <file>
xelatex -interaction=nonstopmode <file>.tex
xelatex -interaction=nonstopmode <file>.tex
```

If `\bibliography{}` is not used (e.g. a `\begin{filecontents}` setup or no citations), skip the `bibtex` pass.

### Step 3: Inspect the log

Grep the `.log` for `! ` (LaTeX errors) and `Warning:`. Report:
- All `!` errors with their line numbers (these stop compilation)
- Undefined references and citations
- Overfull/underfull boxes only if >5pt — minor ones are not actionable

### Step 4: Verify output

Confirm the `.pdf` exists and its modification time is from the current run. Report the page count.

### Step 5: Clean up (optional)

If asked: remove `.aux`, `.log`, `.bbl`, `.blg`, `.out`, `.toc`, `.nav`, `.snm` files. Keep the `.pdf`.

## Notes

- Use XeLaTeX (not pdflatex) — handles Unicode (å, ä, ö, é) natively.
- If the document uses `biblatex` instead of `bibtex`, run `biber <file>` in place of `bibtex`.
- If a figure is referenced but missing, the build will not fail but a `??` will appear in the PDF — flag this explicitly.
