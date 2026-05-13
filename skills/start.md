# /start — Session start

Orient at the beginning of a session. Brief on where the project stands.

## Instructions

### Step 1: Read CLAUDE.md / AGENTS.md

Read the project context file at the repo root. Note the project name, status, data, identification strategy, and current focus.

### Step 2: Read HANDOFF.md

If `HANDOFF.md` exists in the project root, read it.
- Display: what was last worked on, key decisions, what's next
- Ask: "Continue from there, or something else?"

If no HANDOFF.md exists, say so and ask: "What are we working on today?"

### Step 3: Read MEMORY.md (skim)

Read `MEMORY.md` for any `[LEARN]` entries that might bear on today's work. Mention any that look directly relevant — do not list them all.

### Step 4: Check git state (if a git repo)

```bash
git status
git log --oneline -5
```

Report: branch, uncommitted changes, recent commits. Flag anything unusual (uncommitted work in `data/` or `output/` that should be gitignored, detached HEAD, etc.).

### Step 5: Stand by

Say what's loaded, then wait for the user.
