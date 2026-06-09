---
slug: library-index
type: index
status: active
created: 2026-05-19
updated: 2026-05-21
---

# Library Index

Metadata for items in the Co-Goods library. Serials are assigned on entry to the repo — every library item has one (`in repo = has a serial`). The full record is in each item's `.md` file; this index is the at-a-glance view.

## Items

| Serial | Title | Slug | Type | Authors | Year | Cited | Featured | Added by | Added |
|---|---|---|---|---|---|---|---|---|---|
| l-00001 | SPDX (Software Package Data Exchange) | spdx | standard | — | 2021 |   | ✓ | [[people/pontus-karlsson\|Pontus Karlsson]] | 2026-06-03 |
| l-00002 | Value uncaptured perspective for sustainable business model innovation | yang-value-uncaptured-2017 | paper | Yang, Evans, Vladimirova, Rana | 2017 |   | ✓ | [[people/pontus-karlsson\|Pontus Karlsson]] | 2026-06-08 |
| l-00003 | The 8 Forms of Capital | roland-landua-eight-forms-of-capital-2011 | article | Roland, Landua | 2011 |   | ✓ | [[people/pontus-karlsson\|Pontus Karlsson]] | 2026-06-08 |

## Example items

Dummy content used to exercise website templates. Serials use the `x-#####` namespace so the curated `l-#####` numbering remains untouched. Items here all carry `example: true` in their frontmatter and can be bulk-filtered or removed.

| Serial | Title | Slug | Type | Authors | Year | Cited | Featured | Added by | Added |
|---|---|---|---|---|---|---|---|---|---|
| x-00001 | Network Coordination Under Asynchronous Participation | smith-network-coordination-2022 | paper | [[people/jane-doe\|Jane Doe]] | 2022 | ✓ | ✓ | [[people/pontus-karlsson\|Pontus Karlsson]] | 2026-05-21 |
| x-00002 | Systems Thinking for the Curious | johnson-systems-thinking-2019 | book | [[people/jane-doe\|Jane Doe]] | 2019 | ✓ |   | [[people/pontus-karlsson\|Pontus Karlsson]] | 2026-05-21 |

## Columns

- **Serial** — `l-#####` (zero-padded; assigned on entry to repo)
- **Title** — display title
- **Slug** — bare slug (for grep / wikilink)
- **Type** — `book` / `paper` / `article` / `standard` / `podcast-episode` / `post` / `video` / `course`
- **Authors** — [[people/<slug>|Display Name]] wikilink
- **Year** — for sorting; matches the item's `year:` frontmatter
- **Cited** — ✓ if `is-cited: true`, empty otherwise
- **Featured** — ✓ if `is-featured: true`, empty otherwise
- **Added by** — the Co-Goods contributor who curated this entry into the repo (wikilink to `people/`)
- **Added** — ISO date (`YYYY-MM-DD`) when added to the repo
