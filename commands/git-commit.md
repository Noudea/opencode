---
description: Inspect the worktree, stage one coherent change, and create a commit that matches the repo's style.
argument-hint: "[optional commit guidance]"
allowed-tools: Read, Bash
---

# Git Commit

Create one atomic git commit from the current worktree.

## Variables

COMMIT_GUIDANCE: $1

## Instructions

- Inspect recent commit history before drafting the message so the new commit matches the repo's local style when that style is clear.
- Treat already staged files as the intended commit when they form one coherent change.
- If nothing is staged, stage only the minimal relevant file set for one commit.
- If the worktree mixes unrelated changes that should not be committed together, stop and explain the split instead of forcing one commit.
- Never commit likely secrets such as `.env`, private keys, tokens, raw credentials, or machine-local config.
- Never create an empty commit.
- Never use destructive git commands.
- Never amend unless the user explicitly asked for an amend workflow.
- Keep the subject concise, imperative, and specific, with no trailing period.
- If recent history clearly follows gitmoji, conventional commits, or another stable pattern, match that pattern.
- If no clear style is visible, default to a concise gitmoji-style subject using a real emoji character.
- Keep scope optional. Add a short scope only when it improves clarity and can be derived safely from the changed area or existing repo convention.
- Useful fallback gitmoji choices when no repo convention is obvious:
  - `✨` new feature
  - `🐛` bug fix
  - `🩹` small fix
  - `♻️` refactor
  - `📝` docs
  - `✅` tests
  - `🔧` config change
  - `🚚` move or rename
- Use `COMMIT_GUIDANCE` only as extra intent, not as a replacement for inspecting the diff.
- For complex, breaking, or issue-related changes, add a commit body that explains why, impact, and references.

## Workflow

1. Inspect `git status --short`, staged and unstaged diffs, changed paths, and recent commit history.
2. Decide whether the staged set already defines the commit; otherwise stage the minimal coherent file set.
3. Determine the repo's commit style from recent history. If unclear, use the gitmoji fallback described above.
4. Draft a concise subject and an optional body when the change needs extra context.
5. Create the commit with `git commit -m`, adding a second `-m` only when a body is warranted.
6. Verify the result with `git status --short` and `git log -1 --stat --oneline`.

## Command

```bash
git status --short
git diff --cached --name-only
git diff --cached
git diff --name-only
git diff
git log -10 --oneline
git add <files>
git commit -m "<subject>"
git commit -m "<subject>" -m "<body>"
git status --short
git log -1 --stat --oneline
```

## Report

Return the final result in chat. Include:

1. Branch name, commit hash, and final subject
2. Style used for the message and why it was chosen
3. Whether a commit body was used, and the body text if present
4. Files included in the commit
5. Any files intentionally excluded and why
