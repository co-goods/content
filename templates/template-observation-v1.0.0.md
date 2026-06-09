---
template: observation
template_version: 1.0.0
collection: observations
slug: ""
title: ""
authors: []
sources: []
year-of-observation: ""
status: active
stage: draft
tags: []
related_observations: []
example: false
created: "{{date}}"
updated: "{{date}}"
---

# {{title}}

## What was observed

1–3 paragraphs describing the external signal — data point, trend, case, field observation, interview finding. Cite sources where the evidence comes from.

## Why it matters

Brief — what does this observation make visible that wasn't visible before?

## Related observations

Cross-references to other observations that share context or contrast with this one.

## Notes

Open questions, caveats, things to verify.

<!--
Observation schema (template: observation, v1.0.0).

- File location: `research/observations/<slug>.md` (flat; slug-only naming, no serial)
- Voice: external signal from the world (data, trend, case, field finding, interview)
- `sources`: bare library slugs that ground the observation in evidence
- `year-of-observation`: when the phenomenon was observed (not the entry date — that's `created`)
- `related_observations`: bare slugs of other observations that share context
- `stage: draft` shows the WIP banner on the website; `stage: published` removes it
- `example: true` marks dummy/test content (default `false`; opt-in only)

Living document — updates in place; git history is the version log.

Chain:
- Insights link upstream to observations (via `observations:`) and/or library
  items (via `sources:`); at least one upstream link required
- Hypotheses link upstream to insights (via `insights:`)
- No `decisions/` collection in this repo
-->
