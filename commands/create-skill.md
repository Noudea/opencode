---
description: Create a global or project-local OpenCode skill.
argument-hint: "skill-name [global|project] [optional purpose]"
allowed-tools: Read, Write, Bash, WebFetch
---

# Create Skill

Create or update an OpenCode skill for the requested skill name and purpose.

## Variables

SKILL_REQUEST: $ARGUMENTS
SCOPE: $2
SKILL_NAME: $1
SKILL_PURPOSE: <remaining-purpose-text>
GLOBAL_SKILL_DIRECTORY: ~/.config/opencode/skills/$1
GLOBAL_SKILL_FILE: ~/.config/opencode/skills/$1/SKILL.md
PROJECT_SKILL_DIRECTORY: .opencode/skills/$1
PROJECT_SKILL_FILE: .opencode/skills/$1/SKILL.md
TARGET_SKILL_DIRECTORY: <resolved-directory>
TARGET_SKILL_FILE: <resolved-path>
SKILL_NAME_REGEX: ^[a-z0-9]+(-[a-z0-9]+)*$

## Instructions

- Follow the prompt structure template when it helps, but do not force unnecessary sections.
- Follow the OpenCode skills spec for discovery, naming, and frontmatter.
- Parse the first argument as scope only when it is exactly `global` or `project`.
- If no explicit scope is provided, default to `global`.
- When scope is explicit, treat the next argument as the skill name.
- Create global skills in `GLOBAL_SKILL_DIRECTORY`.
- Create project-local skills in `PROJECT_SKILL_DIRECTORY`.
- Resolve `~` to the current user's home directory when using file tools.
- `TARGET_SKILL_FILE` must start with YAML frontmatter.
- Frontmatter must include `name` and `description`.
- Only use recognized frontmatter keys: `name`, `description`, `license`, `compatibility`, and `metadata`.
- `name` must match the skill directory name and `SKILL_NAME_REGEX`.
- The final skill name must be 1-64 characters.
- `compatibility` and `metadata` are optional; add them only when they improve clarity.
- Keep the skill concise, reusable, and specific enough for the `skill` tool description.
- Prefer a useful first draft over asking a question when the skill purpose is reasonably clear from `SKILL_REQUEST`.
- If `SKILL_NAME` is invalid, normalize it to lowercase kebab-case when the transformation is obvious; otherwise ask one targeted question.
- If the target skill file already exists, update it in place instead of creating a duplicate skill.
- Do not create files outside `GLOBAL_SKILL_DIRECTORY` or `PROJECT_SKILL_DIRECTORY` unless the user explicitly asks.

Examples:

- `/create-skill research-helper "Research a topic and summarize findings"` -> global skill
- `/create-skill project api-auth "Project-specific auth guidance"` -> project-local skill

## Workflow

1. Parse `SKILL_REQUEST`, resolve `SCOPE`, and resolve the final skill name.
2. Resolve the final target path in either `GLOBAL_SKILL_DIRECTORY` or `PROJECT_SKILL_DIRECTORY`.
3. Read the Documentation references, especially `templates/skills.md`, before drafting the skill.
4. Create `TARGET_SKILL_DIRECTORY` if it does not already exist.
5. Create or update `TARGET_SKILL_FILE` with valid OpenCode frontmatter and a concise Markdown body tailored to the requested skill.
6. Verify that the frontmatter `name` exactly matches the final directory name and that the path matches `skills/<name>/SKILL.md`.
7. Return a short report covering the created or updated skill and any assumptions.

## Documentation

- `templates/skills.md` - canonical local template and section guidance for `SKILL.md` files
- https://opencode.ai/docs/commands/ - command markdown format, arguments, and file references
- https://opencode.ai/docs/en/skills/ - skill discovery, frontmatter, and naming rules

## Report

Return the final result in chat. Include:

1. Final skill name and path
2. Resolved scope: global or project
3. Whether the skill was created or updated
4. Frontmatter fields added
5. Sections included in the skill body
6. Any normalization, assumptions, or follow-up items
