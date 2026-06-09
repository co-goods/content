---
template: insight
template_version: 1.0.0
collection: insights
slug: ""
title: ""
summary: ""
tags: []
sources: []
observations: []
authors: []
related_insights: []
status: active
stage: draft
example: false
key_findings: []
implications: []
research_questions: []
created: "{{date}}"
updated: "{{date}}"
---

# {{title}}

## Context
Background and context that led to this insight.

## Analysis
Detailed analysis and reasoning behind the findings.

## Supporting Evidence
Additional evidence, quotes, or data that support this insight.

## Notes
Additional notes, observations, or considerations.

<!--
Insight schema (template: insight, v1.0.0).

- File location: `research/insights/<slug>.md`
- Atomic research finding. Living document — updates in place.
- `authors`: bare people slugs — who wrote this insight (Co-Goods contributor[s])
- `sources`: bare library slugs — library entries this insight cites
- `observations`: bare observation slugs — observations this insight synthesises
- `tags`: bare tag slugs
- `stage: draft` shows a WIP banner on the website; `stage: published` removes it
- `example: true` marks dummy/test content (default `false`; opt-in only)

Chain rule: every insight must have at least one upstream link — either
`observations:` (preferred when synthesising across multiple signals) OR
`sources:` (when the insight is a direct theoretical extension of a published
source). Both can be populated; neither can be empty.

Wikilinks use qualified paths:

- `[[resources/library/papers/olleros-antirival-goods|Olleros (2018)]]` → /resources/library/papers/olleros-antirival-goods
- `[[people/f-xavier-olleros|F. Xavier Olleros]]` → /people/f-xavier-olleros
- `[[research/observations/<slug>]]`, `[[research/hypotheses/<slug>]]`, `[[resources/wiki/<slug>]]`,
  `[[thinking/essays/<slug>]]`, `[[resources/glossary/<slug>]]`, etc.
- Bare `[[antirival]]` resolves to `/topics/antirival` **if a topic-aggregation
  page exists** (slug appears in 2+ collections); otherwise build error.
-->
