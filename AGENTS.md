# OpenCode Global Workflow

These are reusable global instructions for feature work across projects.

## Workflow

- Inspect repo context before proposing implementation details.
- For non-trivial feature requests, create or update `doc/<feature-slug>.md` before making code changes.
- Keep the plan file as the source of truth during planning and review.
- If external ecosystem, standards, or library knowledge is needed, delegate web research to the `researcher` subagent.
- Keep planning and user discussion in the primary thread.
- For non-trivial work, wait for plan review before implementation.
- After implementation, update relevant documentation when schema, entities, contracts, or developer workflows change.

## Scope

- These global rules are generic and reusable.
- Project-local `AGENTS.md`, `opencode.json`, and `.opencode/` files may add stricter repo-specific rules.
- When global and project-local rules conflict, prefer the more specific project-local instruction.
