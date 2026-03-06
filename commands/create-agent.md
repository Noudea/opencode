---
description: Create a global or project-local OpenCode agent or subagent.
argument-hint: " agent-name [global|project] [primary|subagent] [optional-purpose-in-quotes]"
allowed-tools: Read, Write, Bash, WebFetch
---

# Create Agent

Create or update an OpenCode agent markdown file for the requested agent name, scope, and mode.

## Variables

AGENT_REQUEST: $ARGUMENTS
SCOPE: $2
AGENT_NAME: $1
MODE: $3
AGENT_PURPOSE: <remaining-purpose-text>
GLOBAL_AGENT_DIRECTORY: ~/.config/opencode/agents
PROJECT_AGENT_DIRECTORY: .opencode/agents
AGENT_NAME_REGEX: ^[a-z0-9]+(-[a-z0-9]+)*$

## Instructions

- Follow the OpenCode agent markdown format for file location, frontmatter, permissions, and prompt body.
- Parse the first argument as scope only when it is exactly `global` or `project`.
- If no explicit scope is provided, default to `global`.
- Treat the next argument as the agent name.
- Parse the next argument as mode only when it is exactly `primary` or `subagent`.
- If no explicit mode is provided, default to `subagent`.
- Create global agents in `GLOBAL_AGENT_DIRECTORY`.
- Create project-local agents in `PROJECT_AGENT_DIRECTORY`.
- Resolve `~` to the current user's home directory when using file tools.
- Read `templates/agents.md` before drafting the agent.
- Start the file with YAML frontmatter.
- Include `description` and `mode` in frontmatter.
- Add `hidden`, `model`, `temperature`, `steps`, or `permission` only when they improve the requested agent.
- Keep permissions minimal and explicit when you add them.
- Keep the body concise and role-focused.
- If `AGENT_PURPOSE` is omitted, infer a reasonable first draft from `AGENT_NAME` and `MODE`.
- If the user provides remaining text after the mode or name, treat it as the purpose. Quoted text is preferred for multi-word purposes.
- If `AGENT_NAME` is invalid, normalize it to lowercase kebab-case when the transformation is obvious; otherwise ask one targeted question.
- If the target agent file already exists, update it in place instead of creating a duplicate agent.
- Do not create files outside `GLOBAL_AGENT_DIRECTORY` or `PROJECT_AGENT_DIRECTORY` unless the user explicitly asks.

Examples:

- `/create-agent "reviewer" "Review code changes and summarize risks"` -> global subagent
- `/create-agent "main-agent" "primary" "Main coding agent for daily work"` -> global primary agent
- `/create-agent "git-helper" "subagent" "Project-specific git helper"` -> project-local subagent

## Workflow

1. Parse `AGENT_REQUEST`, resolve `SCOPE`, `AGENT_NAME`, and `MODE`.
2. Resolve the final target path in either `GLOBAL_AGENT_DIRECTORY` or `PROJECT_AGENT_DIRECTORY`.
3. Read the Documentation references, especially `templates/agents.md`, before drafting the agent.
4. Determine the agent role, frontmatter fields, permission hints, and body bullets from `AGENT_NAME`, `MODE`, and `AGENT_PURPOSE`.
5. Verify that the filename matches the final agent name and that the prompt body is internally consistent.
6. Return a short report covering the created or updated agent and any assumptions.

## Documentation

- `templates/agents.md` - canonical local template and section guidance for agent files
- https://opencode.ai/docs/en/agents/ - agent format, modes, and behavior
- https://opencode.ai/docs/en/skills/ - reference when the requested agent should load specific skills

## Report

Return the final result in chat. Include:

1. Final agent name and path
2. Resolved scope: global or project
3. Resolved mode: primary or subagent
4. Whether the agent was created or updated
5. Frontmatter fields added
6. Any normalization, assumptions, or follow-up items
