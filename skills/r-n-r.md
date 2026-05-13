# /r-n-r — Revise & Resubmit Response Planner

Turn referee reports into a structured, dependency-ordered revision plan.

## Arguments

`$ARGUMENTS` can include:
- *(none)* — Expects referee report(s) to be pasted into the conversation or a PDF path provided
- `<path>` — Path to a PDF referee report (Claude will extract with pdftotext)
- `quick` — Skip dependency mapping, just extract and categorise comments

## Instructions

### Step 1: Ingest the reports

If a file path is given, extract text:
```bash
pdftotext -layout <path> /tmp/referee_reports.txt
cat /tmp/referee_reports.txt
```
If pasted text, read directly from the conversation.

Read every word. Do not skim.

### Step 2: Extract atomic tasks

For each referee (R1, R2, ...) and editor (Ed), extract every comment as a discrete task. Number them R1.1, R1.2, R2.1, etc. For each task record:

- **ID** — e.g. R1.3
- **Type** — one of: Data / Method / Framing / Writing / Robustness / New-analysis / Minor
- **Summary** — one sentence describing what is being asked
- **Effort** — Low / Medium / High (rough estimate)
- **[restricted data environment] flag** — yes if the task requires register data access (long lead time, flag immediately)

### Step 3: Map dependencies

For each task, ask: does completing this task require another task to be done first?

Common dependency patterns:
- A new regression (R1.2) must run before a table can be updated (R1.1)
- A framing change (R2.1) may affect the introduction and conclusion simultaneously
- A data extension (R1.4) blocks all downstream analysis
- Independent tasks can be parallelised

List explicit dependencies as: R1.3 → R1.1 (meaning R1.3 must be done before R1.1).

### Step 4: Identify the critical path

The critical path is the longest chain of dependent tasks. Flag it clearly — this is the minimum timeline and the sequence that must not slip.

Also flag:
- **Parallel tracks** — tasks with no dependencies on each other (can be worked simultaneously)
- **[restricted data environment]-gated tasks** — these have the longest external lead time and should be initiated first regardless of position in the critical path
- **Quick wins** — Low effort, no dependencies (do these first to build momentum)

### Step 5: Produce the revision plan

Output in three blocks:

**Block 1 — Task register**
Table: ID | Type | Summary | Effort | Dependencies | [restricted data environment]?

**Block 2 — Critical path**
Ordered list of tasks on the critical path, with estimated total effort.

**Block 3 — Recommended sequence**
A practical execution order that:
1. Initiates [restricted data environment]-gated tasks immediately
2. Clears quick wins first
3. Follows the critical path for the main work
4. Parallelises where possible

### Step 6: Response letter scaffold (optional)

If the user requests it (or if there are ≤15 total tasks), generate a response letter scaffold:
- Standard opening (one sentence: "We thank the referees for their careful reading...")
- For each task in R1, R2, ... order: a placeholder response block with the comment quoted and space for the user's response
- Standard closing

The scaffold is a working file only — save to the project's revision folder if one exists, otherwise to `/tmp/r_n_r_scaffold.md`.

## Notes

- [restricted data environment]-flagged tasks must be highlighted at the top of the output, regardless of their position in the task register. Every day of delay on [restricted data environment] tasks is a day added to the total revision timeline.
- If two referees ask for conflicting things, flag the conflict explicitly rather than trying to resolve it — the user decides.
- Do not suggest dropping tasks or dismissing referee comments. The plan is to respond to everything; the user decides how to respond.
- For papers in [restricted data environment] (P1207), remind the user that new scripts must pass the quality checks in `your data-environment quality checks` before upload.
