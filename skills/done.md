# /done — Session capture

Capture decisions, follow-ups, and project state for the next session.

## Arguments

- *(none)* — Full capture
- `quick` — Decisions and follow-ups only

## Instructions

### Step 1: Extract from the conversation

Identify:
- **Topic** — one-line summary of this session
- **Decisions** — approaches chosen, things agreed
- **Open questions** — unresolved items
- **Follow-ups** — concrete next steps
- **Files changed** — what was created/modified

For `quick` mode: decisions and follow-ups only.

### Step 2: Write HANDOFF.md (overwrite)

Write the project's `HANDOFF.md` at the repo root with this block:

```
Last updated: [YYYY-MM-DD HH:MM]
Topic: [topic]

Key decisions:
- [decision]

Open questions:
- [question]

Next priority: [concrete next action]

Follow-ups:
- [ ] [action]

Files changed this session:
- [path]
```

This is what `/start` reads next time.

### Step 3: Update MEMORY.md (only if something was learned)

If the user corrected an approach, named a non-obvious convention, or you discovered a project-specific gotcha, append a `[LEARN:category]` entry to `MEMORY.md`:

```
[LEARN:category] Brief, durable lesson — why it matters / how to apply.
```

Do NOT append session-specific facts. MEMORY.md is for durable lessons that should bear on future sessions.

### Step 4: Suggest a commit (only if appropriate)

If there are uncommitted code or document changes worth saving, suggest `/commit` with a draft message. Do not auto-commit.
