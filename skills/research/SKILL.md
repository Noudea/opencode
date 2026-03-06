---
name: research
description: Research a topic on the web and write a concise report to .doc/research.
compatibility: opencode
metadata:
  category: web-research
  output: .doc/research
---

# Web Research Skill

Investigate a problem, topic, or implementation question on the web, then save the synthesized findings in `.doc/research`.

## Variables

RESEARCH_TOPIC: $ARGUMENTS
OUTPUT_DIRECTORY: .doc/research

## Instructions

- Treat this as web-only research unless the user explicitly asks for repo context.
- Start with the narrowest practical interpretation of `RESEARCH_TOPIC`.
- Prefer primary sources, official docs, standards, vendor docs, and maintainer guidance over secondary summaries.
- Do not rely on low-quality sources such as SEO content farms, unverified AI-generated articles, spammy blogs, or unsourced summaries when better sources are available.
- Use this source priority order when available: official docs and specs, maintainer or vendor guidance, issue trackers and RFCs, then reputable technical articles.
- Cross-check notable claims across multiple credible sources when the topic is ambiguous or fast-moving.
- Synthesize findings into actionable guidance instead of dumping raw search results.
- Treat this as research-first work: do not change product code unless the user explicitly asks.
- Include a `Last updated: YYYY-MM-DD` line near the top of the report so readers know when the research was last refreshed.
- Write the final report to `OUTPUT_DIRECTORY/<slug>.md`, where `<slug>` is a short kebab-case version of the topic. If a matching report already exists, update it instead of creating a duplicate.

## Workflow

1. Parse `RESEARCH_TOPIC` and define the concrete question, constraints, and likely output shape.
2. Search the web for authoritative references, known solutions, tradeoffs, examples, and recent guidance.
3. Compare sources, resolve conflicts where possible, and call out uncertainty when sources disagree.
4. Create `OUTPUT_DIRECTORY` if needed and write a concise report with findings, recommendations, and source references.
5. Reply with the report path and the key recommendation or takeaway.

## Output

- Path: `OUTPUT_DIRECTORY/<slug>.md`
- Format: markdown
- Contents:
  1. Topic and scope
  2. Last updated date in `YYYY-MM-DD` format
  3. External findings
  4. Key options or tradeoffs
  5. Recommended solution or next steps
  6. References with URLs

## Report

Return the final result in chat. Include:

1. Report path
2. Key recommendation or takeaway
