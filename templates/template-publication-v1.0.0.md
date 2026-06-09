---
template: publication
template_version: 1.0.0
collection: publications
slug: ""
name: ""
publication_type: ""
publisher: ""
url: ""
founded: ""
description: ""
status: active
created: "{{date}}"
updated: "{{date}}"
---

# {{name}}

## About
Brief description of the publication — what it covers, editorial focus, audience.

## Notes
Additional notes.

<!--
Publication schema (template: publication, v1.0.0).

Required:
- File location: `resources/library/publications/<slug>.md`
- `slug`: bare kebab-case (e.g. `nature`, `the-atlantic`, `the-knowledge-project`); matches filename
- `name`: display form
- `publication_type`: free-text — `journal | magazine | newspaper | podcast-channel | newsletter | blog | …`

Optional (add when relevant):
- `publisher`: slug of organisation in `resources/library/publishers/`
- `url`, `founded` (year), `description`
- `status`: `active | inactive | defunct`

Publications are the channels that carry individual papers, articles,
episodes, and so on. Items reference their publication by slug
(`publication: nature`). The publication's own page aggregates everything
published under it.
-->
