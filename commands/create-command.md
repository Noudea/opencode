---
description: Create a global or project-local OpenCode command.
argument-hint: "command-name [global|project] [optional-purpose-in-quotes]"
allowed-tools: Read, Write, Bash, WebFetch
---

# Create Command

Create or update an OpenCode command markdown file for the requested command name and purpose.

## Variables

COMMAND_REQUEST: $ARGUMENTS
SCOPE: $2
COMMAND_NAME: $1
COMMAND_PURPOSE: <remaining-purpose-text>
GLOBAL_COMMAND_DIRECTORY: ~/.config/opencode/commands
PROJECT_COMMAND_DIRECTORY: .opencode/commands
COMMAND_NAME_REGEX: ^[a-z0-9]+(-[a-z0-9]+)*$

## Instructions

- Follow the prompt structure template when it helps, but do not force unnecessary sections.
- Follow the OpenCode commands markdown format for file location, frontmatter, arguments, and prompt body.
- Parse the first argument as scope only when it is exactly `global` or `project`.
- If no explicit scope is provided, default to `global`.
- When scope is explicit, treat the next argument as the command name.
- Create global commands in `GLOBAL_COMMAND_DIRECTORY`.
- Create project-local commands in `PROJECT_COMMAND_DIRECTORY`.
- Resolve `~` to the current user's home directory when using file tools.
- Start the file with YAML frontmatter.
- Include `description` in frontmatter.
- Add `argument-hint` and `allowed-tools` when they improve usability and safety.
- Add `agent`, `subtask`, or `model` only when there is a clear reason.
- Keep the command prompt concise, reusable, and specific to the requested task.
- If `COMMAND_PURPOSE` is omitted, infer a reasonable first draft from `COMMAND_NAME`.
- If the user provides remaining text after the command name, treat it as the purpose. Quoted text is preferred for multi-word purposes.
- If `COMMAND_NAME` is invalid, normalize it to lowercase kebab-case when the transformation is obvious; otherwise ask one targeted question.
- If the target command file already exists, update it in place instead of creating a duplicate command.
- Do not create files outside `GLOBAL_COMMAND_DIRECTORY` or `PROJECT_COMMAND_DIRECTORY` unless the user explicitly asks.

Examples:

- `/create-command "feature-plan" "Create a structured feature planning command"` -> global command
- `/create-command "release-check" "project"  "Check project release readiness"` -> project-local command

## Workflow

1. Parse `COMMAND_REQUEST`, resolve `SCOPE`, and resolve the final command name.
2. Resolve the final target path in either `GLOBAL_COMMAND_DIRECTORY` or `PROJECT_COMMAND_DIRECTORY`.
3. Read the Documentation references, especially `templates/commands.md`, before drafting the command.
4. Determine the command goal, variables, and prompt sections from `COMMAND_NAME` and `COMMAND_PURPOSE`.
5. Verify that the filename matches the final slash command name and that the prompt body is internally consistent.
6. Return a short report covering the created or updated command and any assumptions.

## Documentation

- `templates/commands.md` - canonical local template and section guidance for command files
- https://opencode.ai/docs/commands/ - command markdown format, arguments, and file references
- https://opencode.ai/docs/en/skills/ - reference when the requested command interacts with skills

## Report

Return the final result in chat. Include:

1. Final command name and path
2. Resolved scope: global or project
3. Whether the command was created or updated
4. Frontmatter fields added
5. Sections included in the command body
6. Any normalization, assumptions, or follow-up items
