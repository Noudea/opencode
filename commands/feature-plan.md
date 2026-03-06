---
description: Create or update a structured feature plan in doc and stop before implementation.
argument-hint: '"feature name or request" [optional planning context]'
allowed-tools: Read, Write, Glob, Grep, Bash, WebFetch
---

# Feature Plan

Create or update a structured feature plan Markdown file in `./doc/` for the requested feature, and stop after planning so the user can review the plan before any implementation begins.

## Variables

FEATURE_REQUEST: $ARGUMENTS
REQUESTED_FEATURE_NAME: <derive from FEATURE_REQUEST>
OPTIONAL_PLANNING_CONTEXT: <derive from FEATURE_REQUEST when present>
PLAN_DIRECTORY: doc
PLAN_FILE: doc/<feature-slug>.md
RELATED_RESEARCH_DIRECTORY: .doc/research

## Instructions

- Treat `FEATURE_REQUEST` as the source of truth for parsing the feature name and any extra planning context.
- Do not assume `$1` contains the full feature name unless the user intentionally passed a quoted multi-word name or a single-token slug.
- Resolve a stable lowercase kebab-case feature slug from `REQUESTED_FEATURE_NAME` when the transformation is obvious.
- If `FEATURE_REQUEST` mixes the feature title and extra context, infer the shortest reasonable feature name and treat the rest as planning context.
- Use `./doc/<feature-slug>.md` as the single source of truth for planning.
- If the plan file already exists, update it in place instead of creating a duplicate plan.
- Inspect relevant repo context before writing the plan.
- If useful research already exists under `.doc/research/`, reference it in the plan instead of duplicating it.
- Use external web research only when it materially improves the plan.
- Keep the plan practical and implementation-oriented, but do not start coding.
- Preserve the same section structure every time.
- Match the canonical heading order from `templates/feature-plan.md`.
- Prefer concrete file paths, commands, and validation steps when they can be derived from the repo.
- Call out assumptions, unknowns, and tradeoffs explicitly instead of hiding them in the steps.
- End with the plan ready for user review, and make it clear that implementation has not started.

## Required Plan Template

```md
# <Feature Title>

Status: draft
Owner: agent + user
Related research: <path or none>

## Goal

## Scope

## Out of scope

## Repo context

## External research

## Assumptions and open questions

## Implementation steps

1. ...

## Validation

## Documentation updates

## Risks and tradeoffs
```

## Workflow

1. Resolve the final feature title, slug, and `PLAN_FILE` path.
2. Inspect any existing plan file plus the most relevant repo files, docs, and scripts needed to plan accurately.
3. Check for related artifacts in `.doc/research/`, `./doc/`, or other relevant docs and incorporate them by reference.
4. Create or update `PLAN_FILE` using the required template and fill each section with concrete, repo-specific content.
5. Keep the plan focused on planning only; do not edit implementation files or make code changes.
6. Return a short report with the plan path, whether it was created or updated, key assumptions, and any open questions for review.

## Command

```bash
mkdir -p "doc"
```

## Output

- Path: `PLAN_FILE`
- Format: markdown
- Contents: follow `templates/feature-plan.md`

## Documentation

- `templates/feature-plan.md` - canonical feature plan headings and metadata fields

## Report

Return the final result in chat. Include:

1. Final feature title, slug, and plan path
2. Whether the plan was created or updated
3. Related research or docs referenced
4. Main assumptions or open questions captured
5. Confirmation that implementation has not started
