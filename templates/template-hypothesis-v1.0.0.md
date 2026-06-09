---
template: hypothesis
template_version: 1.0.0
collection: hypotheses
slug: ""
title: ""
authors: []
insights: []
status: active
stage: draft
validation-status: pending
test-design: ""
tags: []
related_hypotheses: []
example: false
created: "{{date}}"
updated: "{{date}}"
---

# {{title}}

## Hypothesis

If [decision / condition / system property X], then [outcome Y].

## Underlying insight(s)

Reference the insight(s) this hypothesis is based on — wikilink them via `[[research/insights/<slug>]]`.

## Why this matters

Brief — what does validating or invalidating this tell us?

## Test design

How would we test this? What's the methodology? What evidence would count as validation? Invalidation? Revision?

## Validation history

Updates as evidence accumulates — date, source, what happened. The `validation-status` frontmatter field reflects current state.

## Notes

Open questions, caveats.

<!--
Hypothesis schema (template: hypothesis, v1.0.0).

- File location: `research/hypotheses/<slug>.md` (flat; slug-only naming, no serial)
- Form: testable prediction — "If [decision/condition/property], then [outcome]"
- `insights`: bare slugs in `research/insights/` — what the hypothesis is based on
- `validation-status`: enum — `pending | validated | invalidated | revised`
- `test-design`: free-text describing methodology and validation criteria
  (switch to block scalar `test-design: |` for multi-line content when filling in)
- `related_hypotheses`: bare slugs of sibling hypotheses
- `stage: draft` shows the WIP banner; `stage: published` removes it
- `example: true` marks dummy/test content (default `false`; opt-in only)

Living document — `validation-status` updates as evidence accumulates;
`## Validation history` body section captures how it got there.
-->
