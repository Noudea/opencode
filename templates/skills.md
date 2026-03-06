# Skill Template

Use this as the canonical local reference when creating or updating OpenCode skills.

## Frontmatter

```md
---
name: <skill-name>
description: <one-sentence purpose>
compatibility: opencode
metadata:
  category: <optional-category>
  output: <optional-output>
---
```

## Preferred Body Structure

````md
# <Skill Title>

<One or two sentences explaining the job this skill performs.>

## When to use

Use this when <trigger or situation>.

## Variables

<VARIABLE_NAME>: $ARGUMENTS or use $[number]

## Variable Notes

- `$ARGUMENTS` - the full raw argument string passed into the skill
- `$1` - the first positional argument
- `$2` - the second positional argument
- `$3` - the third positional argument

Simple example:

```md
SKILL_REQUEST: $ARGUMENTS
REQUESTED_TOPIC: $1
OUTPUT_HINT: $2
```

Scope-aware example:

```md
SKILL_REQUEST: $ARGUMENTS
RESOLVED_SCOPE: <global-or-project>
RESOLVED_SKILL_NAME: <derived-name>
TARGET_SKILL_FILE: <resolved-path>
```

## Instructions

- <key behavioral rule>
- <quality bar>
- <scope guardrail>

## Workflow

1. <step one>
2. <step two>
3. <step three>

## Output

- Include this section only when the skill must create or update an output.
- Path: <required output path or variable>
- Format: <required output format such as markdown, json, text, yaml, or directory>
- Contents: <required sections, fields, or structure>

## Report

Return the final result in chat. Include:

1. <result item>
2. <result item>
3. <result item>
````
