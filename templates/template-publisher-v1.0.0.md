---
template: publisher
template_version: 1.0.0
collection: publishers
slug: ""
name: ""
publisher_type: ""
url: ""
founded: ""
description: ""
status: active
created: "{{date}}"
updated: "{{date}}"
---

# {{name}}

## About
Brief description of the publisher.

## Notes
Additional notes — editorial focus, notable series, anything worth recording for citation context.

<!--
Publisher schema (template: publisher, v1.0.0).

Required:
- File location: `resources/library/publishers/<slug>.md`
- `slug`: bare kebab-case (e.g. `oxford-university-press`, `example-press`); matches filename
- `name`: display form

Optional (add when relevant):
- `publisher_type`: free-text — `academic | trade | independent | university-press | …`
- `url`, `founded` (year), `description`
- `status`: `active | defunct`

Publishers are referenced from book items by slug (`publisher: example-press`).
The publisher entity captures the organisation; the relationship lives on
the books/papers that cite it.
-->
