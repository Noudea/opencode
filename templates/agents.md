# Agent Template

Use this as the canonical local reference when creating or updating OpenCode agents and subagents.

## Frontmatter

```md
---
description: <one-line summary>
mode: <primary-or-subagent>
hidden: <optional true-or-false>
model: <optional model override>
temperature: <optional numeric value>
steps: <optional step budget>
permission:
  skill:
    "*": deny
    <skill-name>: allow
  task:
    "*": deny
    <subagent-name>: allow
  bash: <allow-or-deny>
  webfetch: <allow-or-deny>
  edit:
    "*": deny
    <path-glob>: allow
---
```

## Preferred Body Structure

```md
---
description: <one-line summary>
mode: <primary-or-subagent>
permission: <permission-rules>
---

You are <agent role>.

- <core responsibility>
- <main workflow rule>
- <when to delegate or load a skill>
- <scope boundary>
- <output expectation>
```
