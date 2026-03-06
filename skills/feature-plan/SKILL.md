---
name: feature-plan
description: Create or update a review-ready feature plan by delegating to the /feature-plan command before implementation.
compatibility: opencode
metadata:
  command: /feature-plan
  category: planning
---

# Feature Plan Skill

Use `/feature-plan` to create or update a structured planning doc in `doc/` and stop before implementation.

## When to use

Use this when the user asks for a feature plan, when a request is non-trivial enough to need review before coding, or when repo rules require a plan file before implementation.

## Variables

FEATURE_REQUEST: $ARGUMENTS

## Instructions

- Prefer `/feature-plan` over manually drafting planning docs when the command is available.
- Pass through the clearest feature name, slug, and any short planning context from `FEATURE_REQUEST`.
- Treat the generated `doc/<feature-slug>.md` file as the planning source of truth for later implementation.
- Stop after the plan is created or updated; do not start implementation until the user reviews the plan.
- Fall back to a manual plan only if `/feature-plan` is unavailable, and keep the same planning intent and structure.

## Workflow

1. Distill the requested feature and constraints from `FEATURE_REQUEST`.
2. Run `/feature-plan` with the minimal useful guidance for the request.
3. Review the resulting `doc/<feature-slug>.md` for repo-specific paths, assumptions, validation, and open questions.
4. Return the plan path, whether it was created or updated, the main assumptions or open questions, and confirmation that implementation has not started.

## Report

Return the final result in chat. Include:

1. Whether `/feature-plan` was used and the guidance passed to it
2. Final plan path
3. Main assumptions or open questions captured
4. Confirmation that implementation has not started
