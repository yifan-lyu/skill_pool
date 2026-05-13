# /lit-review — Literature search and synthesis

Targeted literature scan on a topic, producing a structured synthesis rather than a list of papers.

## Arguments

- `<topic>` — short description of the research question or area
- *(none)* — ask the user

## Instructions

### Step 1: Clarify scope

Ask 2–3 short questions before searching:
- What is the unit of analysis (worker, firm, country)?
- What time period and geography?
- Are you looking for the seminal papers, the most recent frontier, or both?
- Any specific methods (DiD, IV, structural) that bound the relevance?

Do not search until these are answered — generic searches produce generic synthesis.

### Step 2: Search

Use web search and, where available, Google Scholar / Semantic Scholar / NBER / IZA. Aim for:
- 5–10 most-cited papers in the area (the structural canon)
- 3–5 papers from the last 2 years (the frontier)
- 1–2 close-substitute papers (same question, different answer or method)

For every paper, capture: authors, year, journal, full title, the question, the method, the headline finding (with magnitude), and the dataset.

### Step 3: Synthesise — by question, not by paper

Group findings by what they argue, not who wrote them. A good synthesis has paragraphs like:

> Two strands estimate the labour-market impact of AI exposure. The "automation" strand (X, Y) finds negative effects on employment in exposed occupations, with magnitudes of 1–3 pp over 5 years. The "complementarity" strand (A, B) finds positive wage effects in adopting firms with sufficient organisational capital. The two findings are not necessarily contradictory: …

Flag disagreements explicitly. Where the methods differ, say what would resolve the disagreement.

### Step 4: Position

Close with a "How this paper fits in" paragraph: what gap does the user's project address, and which of the cited papers it most directly engages with or differs from.

### Step 5: Output

Save to `writing/lit-review-[topic]-[YYYY-MM-DD].md`. Include a `.bib`-formatted block at the bottom with all referenced papers so they can be pasted into the project bibliography.

## Notes

- Never invent citations. If you cannot find the paper, say so.
- Working papers are fine but mark them clearly (NBER WP, IZA DP).
- This is a scan, not an exhaustive review. State the scope and stop at the boundary.
