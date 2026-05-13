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

## Use as a template

```bash
cp -r path/to/this/template ~/projects/my-new-paper
cd ~/projects/my-new-paper
git init
# Edit CLAUDE.md — fill in project name, status, data, identification
```

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
