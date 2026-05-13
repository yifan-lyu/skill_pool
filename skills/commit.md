# /commit — Stage, Commit, Push

Standard git commit workflow with safety checks.

## Arguments

- *(none)* — Stage tracked changes and prompt for a message
- `<message>` — Use this commit message directly
- `push` — Also push to the current branch's upstream after committing

## Instructions

### Step 1: Survey state

Run in parallel:
- `git status` (no `-uall` flag)
- `git diff --staged` and `git diff`
- `git log --oneline -10` to match the repo's commit style

### Step 2: Choose what to stage

Never run `git add -A` or `git add .` blindly. Stage specific files. Refuse to stage anything matching:
- `data/raw/**`, `data/clean/**` — datasets do not belong in git
- `output/**` — regenerated artefacts
- `.env`, `*.key`, credentials of any kind
- Files larger than 50 MB without explicit user confirmation

If the working tree includes any of the above as untracked, list them and ask the user how to handle them (likely: add to `.gitignore`).

### Step 3: Draft the message

If the user did not provide one, draft a 1–2 sentence message that focuses on the *why*, matching the style observed in `git log`. Present it for approval before committing.

### Step 4: Commit

```bash
git commit -m "your message"
```

Never use `--no-verify` or `--amend` unless the user explicitly asks.

### Step 5: Push (only if asked)

If `push` was requested:
```bash
git push
```

If the branch has no upstream, ask before running `git push -u origin <branch>` — do not assume the remote name.

### Step 6: Report

Show the new commit hash, branch, and ahead/behind status relative to upstream.

## Notes

- This skill commits; it does not review code. Run `/paper-review`, `/estimate-audit`, or your usual lint/test pass before invoking it.
- Force pushes, branch deletions, and `reset --hard` are out of scope. Use raw git for those, with care.
