# Command Template

Use this as the canonical local reference when creating or updating OpenCode command files.

## Frontmatter

```md
---
description: <one-line summary>
argument-hint: <optional expected arguments>
allowed-tools: <optional tool allowlist>
agent: <optional agent name>
subtask: <optional true-or-false>
model: <optional model override>
---
```

## Preferred Body Structure

````md
# <Command Title>

<One or two sentences explaining what the command should do.>

## Variables

<VARIABLE_NAME>: $ARGUMENTS or use $[number]

## Variable Notes

- `$ARGUMENTS` - the full raw argument string passed to the slash command
- `$1` - the first positional argument
- `$2` - the second positional argument
- `$3` - the third positional argument

Simple example:

```md
COMMAND_REQUEST: $ARGUMENTS
REQUESTED_NAME: $1
COMMAND_PURPOSE: $2
```

Scope-aware example:

```md
COMMAND_REQUEST: $ARGUMENTS
RESOLVED_SCOPE: <global-or-project>
RESOLVED_COMMAND_NAME: <derived-name>
TARGET_COMMAND_FILE: <resolved-path>
```

## Instructions

- <behavioral rule>
- <quality bar>
- <scope guardrail>

## Workflow

1. <step one>
2. <step two>
3. <step three>

## Output

- Include this section only when the command must create or update an output.
- Path: <required output path or variable>
- Format: <required output format such as markdown, json, text, yaml, or directory>
- Contents: <required sections, fields, or structure>

## Documentation

- <supporting doc or template>

## Report

Return the final result in chat. Include:

1. <result item>
2. <result item>
3. <result item>
````
