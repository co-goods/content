---
template: doc
template_version: 1.0.0
collection: conventions
slug: file-naming
title: "File naming and slugs"
description: "How content files are named in the repo, and how slugs are formed."
order: 40
status: active
stage: draft
---

# File naming and slugs

How content files are named in the repo, how slugs are formed, and where serials apply.

## File naming

**Flat `.md` files everywhere**, with the filename matching the slug. Two exceptions:

- **Reports**: folder-per-version structure — `research/reports/<type>/<slug>/<version>/<slug>.md` (e.g. `research/reports/lightpapers/co-goods-overview/v0.1/co-goods-overview.md`).
- **Blog**: year/month organisation — `blog/<year>/<month>/<slug>.md` for human file-tree navigation. The URL flattens to `/blog/<slug>`.

No `SOURCE.md` / `AUTHOR.md` / `REPORT.md` generic-inside-folder naming. The filename always carries the slug.

## Slug rules

- **Kebab-case, lowercase, hyphen-separated.** No underscores.
- The `slug:` frontmatter field is always the **bare form** — never includes serials or other prefixes.
- Keep slugs short and stable. Don't rename slugs once content has been published — it breaks links and URL stability.

### Per-collection slug conventions

| Collection | Pattern | Example |
|---|---|---|
| Library (books, papers, articles, posts, videos, courses) | `<lastname>-<2–3 headline words>` | `olleros-antirival-goods`, `smith-network-coordination-2022` |
| Library (podcasts, podcast-episodes) | `<show-slug>` for podcasts; `<show-slug>-<episode-keywords>` for episodes | `the-knowledge-project`, `the-knowledge-project-shane-parrish-on-learning` |
| Publishers | `<organisation-slug>` | `example-press`, `oxford-university-press` |
| Publications | `<publication-slug>` | `nature`, `the-atlantic`, `the-knowledge-project` |
| People | `<firstname-lastname>` | `jane-doe`, `f-xavier-olleros` |
| Glossary items | Base form canonical | `co-goods` (not `co-goodsing`); grammatical variants live under `classes[type=verb].forms` per the dictionary schema |
| Essays, wiki articles, insights, observations, hypotheses | Descriptive short slug | `on-collaboration`, `network-coordination`, `asynchronous-coordination-density` |
| Blog posts | Descriptive short slug | `welcome-to-the-blog` |
| Doc articles | Descriptive short slug | `slug-rules`, `required-fields` |

## Display titles

The `title:` field uses **sentence case** — capitalise only the first word and any proper nouns. Prefer "Network effects", "Eight forms of capital", "Value uncaptured" over Title Case ("Network Effects", …). Acronyms and proper nouns keep their own casing ("SPDX", "GitHub"). For **library entries**, use the work's *published* title as-is — it's a citation, not our heading.

Slugs are independent of titles and always follow the kebab-case rules above.

## Serials

Some library items get a **serial** in YAML frontmatter (never in the filename or folder name):

| Prefix | Used by | Notes |
|---|---|---|
| `l-#####` | **Library items only** (books, papers, podcasts, etc.) | Every library item in the repo gets one. Rule: **in repo = has a serial.** Items kept externally but not promoted into the repo have no serial. |
| `x-#####` | **Example library items only** | Placeholder content used to exercise the website's library templates without claiming research-domain status. Keeps `l-00001+` reserved for the first curated library entries. |

Other content types (people, insights, observations, hypotheses, wiki, essays, reports, glossary, blog posts, docs) do **not** use serials.

`resources/library/INDEX.md` is the registry of assigned serials.

## Why no `nn-` prefix on doc filenames

Doc articles used to use numeric prefixes (`01-taxonomy.md`, `02-frontmatter.md`) for sort order. That has been retired — renaming files to reorder them broke URLs and links.

Instead, ordering lives in YAML:

```yaml
order: 20
```

Filenames are slugs only; the `order:` field on each doc article sorts siblings within a collection (or sub-collection). Numbers in tens (10, 20, 30) leave room to insert without renumbering. See `taxonomy.md` and `frontmatter.md` for the doc article template.

## Asset files

Images and other media that are **part of the content** (diagrams, figures, charts, book covers) live in an `assets/` folder next to the item that uses them, and are referenced with a local-style path:

```
resources/wiki/network-coordination.md
resources/wiki/assets/coordination-diagram.svg   →  ![](./assets/coordination-diagram.svg)
```

Asset filenames follow the same slug rules as everything else: **kebab-case, lowercase, hyphen-separated**, descriptive and stable. Keep the extension (`.svg`, `.png`, `.jpg`, `.mp4`). Don't rename an asset once content references it — it breaks the reference.

- **Reports** keep their per-version `assets/` folders with cascading lookup — a version's `assets/` holds only what changed in that version. (Unchanged here.)
- **Presentation imagery** (hero backgrounds, decorative site images) is *not* a content asset — it lives in the website repo's `public/`, not in a content `assets/` folder. See `media.md` for the content-vs-presentation split.

## Related conventions

- **Taxonomy** (collections, items, templates): see `taxonomy.md`.
- **Frontmatter contract** (universal + per-template fields): see `frontmatter.md`.
- **Templates and versioning** (semver, archive workflow): see `templates-and-versioning.md`.
- **Wikilinks** (qualified-path syntax): see `wikilinks.md`.
- **Images and video** (media blocks, asset location): see `media.md`.
