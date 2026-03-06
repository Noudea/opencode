# OpenCode Routing

Use the configured subagents and skills as the primary workflow entry points.

## Subagents

- `planner` - plan feature work and create `doc/` plans via the `feature-plan` skill.
- `git` - handle git inspection and safe commit workflows via the `commit` skill.
- `researcher` - research topics on the web and write reports via the `research` skill.

## Skills

- `feature-plan` - create or update a review-ready plan in `doc/` and stop before implementation.
- `commit` - create one atomic git commit from the current worktree.
- `research` - investigate a topic on the web and write a concise report to `doc/research`.
