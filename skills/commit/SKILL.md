---
name: commit
description: Create an atomic git commit by delegating to the /git-commit command with optional guidance.
compatibility: opencode
metadata:
  command: /git-commit
  category: git
---

# Commit Skill

Use `/git-commit` to create one atomic git commit from the current worktree.

## When to use

Use this when the user explicitly asks to create a commit, finalize the current work into one commit, or package a coherent change with a good commit message.

## Variables

COMMIT_GUIDANCE: $1

## Instructions

- Prefer `/git-commit` over a manual git workflow.
- Pass `COMMIT_GUIDANCE` through when the user points to a file, feature, or intent.
- Keep the commit atomic and limited to one coherent change.
- Let `/git-commit` match the repo's local commit style when a clear style exists.
- Do not commit likely secrets such as `.env`, private keys, tokens, or raw credentials.
- Do not use destructive git commands.
- Do not amend unless the user explicitly asks.

## Workflow

1. Check whether `COMMIT_GUIDANCE` was provided.
2. Run `/git-commit` when no guidance is provided.
3. Run `/git-commit <guidance>` when the user supplies `COMMIT_GUIDANCE`.
4. Let `/git-commit` inspect changes, stage the minimal coherent file set, create the commit, and verify the result.
5. Fall back to a manual git flow only if `/git-commit` is unavailable or the user explicitly asks for a manual workflow.

## Report

Return the final result in chat. Include:

1. Whether `/git-commit` was used with or without guidance
2. The final commit hash and subject
3. Any follow-up item if the commit could not be created
