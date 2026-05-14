# Research project template — Claude Code + Codex

A minimal, Python/Stata + LaTeX project skeleton with a curated set of skills for empirical economics work. Designed to work with both **Claude Code** and **Codex**.

## What's in here

```
.
├── CLAUDE.md         conventions, identification hierarchy, tooling — read by both agents
├── AGENTS.md         Codex pointer to CLAUDE.md + skill index
├── MEMORY.md         durable [LEARN] entries across sessions
├── HANDOFF.md        last-session state
├── data/             raw/ + clean/ (gitignored)
├── code/             python/ + stata/ scripts, numbered
├── writing/          LaTeX paper, .bib, paper figures
├── slides/           Beamer decks
├── output/           tables, figures, logs (gitignored)
└── skills/           curated skill files (start, done, paper-review, …) + full Stata reference
```

## Use as a template (Codex as an example)

I'm starting [PROJECT NAME] in this repo: [2–3 sentence description]. 

Before start, use the folder under [path name]/skill_pool as a readable reference for your workflow instructions, skills, templates, and conventions.

Read AGENTS.md first, then CLAUDE.md — that's the project configuration. Fill in the bracketed placeholders in CLAUDE.md (project name, status, co-authors, target journal, what this project is, project-specific notes) using the values I'll give you. Don't touch AGENTS.md — it's a pointer file with no placeholders.
Once placeholders are filled, save a DRAFT plan as plans/setup-[YYYY-MM-DD].md describing any further customisations you'd recommend (folder additions, .gitignore extensions, journal-specific style, anything else). Create the plans/ folder if needed. Wait for my approval before executing anything beyond filling placeholders and creating empty folders.
Workflow norms:
1. Plan-first for non-trivial tasks: save the plan to plans/ before doing the work.
2. Invoke skills by name when relevant (/start, /done, /commit, /paper-review, etc. — full list in skills/README.md).
3. When I correct you on something durable, append a [LEARN:category] entry to MEMORY.md (not AGENTS.md).
4. End every session by running /done so HANDOFF.md is current — this is how Codex and Claude Code stay in sync.
5. British spelling throughout (labour, analyse, organisation).


[Optional]
Set up Git version control for this project.
1. First check whether this folder is already a Git repository.
2. If not, run `git init`.
3. Create a `.gitignore` suitable for this project.
4. Run `git status`, then propose the initial files to track.
5. Commit automatically whenever you reach big checkpoints/have big changes. Use appropriate name of the commit.
7. For future large changes, always:
   - make the edits first
   - show me `git diff --stat`
   - summarize the changed files
   - Commit automatically



## Use with Claude Code

The skills work two ways:

1. **As docs in the project.** Claude Code reads `CLAUDE.md` automatically and will find `skills/<name>.md` when you mention a skill by name.

2. **As slash commands.** To call them with `/<name>`, install them into your user skills directory:

   ```bash
   mkdir -p ~/.claude/skills
   for f in skills/*.md; do
     name=$(basename "$f" .md)
     mkdir -p ~/.claude/skills/"$name"
     cp "$f" ~/.claude/skills/"$name"/"$name".md
   done
   cp -r skills/stata ~/.claude/skills/stata
   ```

## Use with Codex

Codex reads `AGENTS.md` automatically, which points at `CLAUDE.md` and the skill index. Skills are referenced as plain markdown — ask Codex to read `skills/<name>.md` when relevant, or it will do so on its own when you mention a matching task.

## Skills at a glance

See [skills/README.md](skills/README.md). Workflow skills (start, done, commit, compile-latex), analysis (data-analysis, audit-reproducibility), review (paper-review, personas-review, estimate-audit, cite-audit, verify-claims, proofread, slide-review), refereeing (referee, r-n-r), and research (lit-review, research-ideation, preregister). Plus a comprehensive Stata reference under `skills/stata/`.

## Conventions in one line

Python 3.10+ · Stata with reghdfe/estout · XeLaTeX · British English · DiD-first identification · never commit `data/` or `output/` · verify every citation against the canonical source.

Full details in [CLAUDE.md](CLAUDE.md).
