---
template: doc
template_version: 1.0.0
collection: conventions
slug: taxonomy
title: "Content taxonomy"
description: "The three concepts (collections, items, templates) and how they fit together."
order: 10
status: active
stage: draft
---

# Content taxonomy

How content is organised in the Co-Goods content repo: what concepts exist, how they relate, and where each kind of file lives.

The model rests on **three primary concepts** — collections, items, and templates — plus a small set of cross-cutting templates (composed page, overlay, plain page) for files that don't belong to a content collection, and a few pages the website generates on the fly.

## The three concepts

- A **collection** is a folder of items, all of one template.
- An **item** is a content file in a collection.
- A **template** is the schema (and authoring scaffold) for one kind of file.

Every authored file is an item in some collection or follows a cross-cutting template. There are no exceptions.

## Flat and nested collections

Most collections are **flat** — they hold items directly, one level deep:

- The `wiki` collection holds wiki-article items at `resources/wiki/<slug>.md`.
- The `books` collection holds book items at `resources/library/books/<slug>.md`.
- The `people` collection holds person items at `people/<slug>.md`.

A **nested collection** has sub-collections — folders inside it whose items share the same template. The nesting is structural; it's part of the collection's identity.

In docs, `conventions` is currently the load-bearing example. It holds doc articles directly and has sub-collections `naming` and `frontmatter`, each also holding doc articles.

## The flat-vs-nested rule

The distinction is empirical — look at the templates of items in sibling sub-folders:

- **Same template across siblings** → those siblings are sub-collections of a single nested parent. The nesting is part of the collection's identity.
- **Different templates across siblings** → those siblings are independent flat collections that happen to share a URL prefix. The shared prefix above them is presentation routing, not structure.

## Worked example — docs vs library

Both look similar from outside: each has multiple folders sharing a URL prefix. But they're structurally opposite cases.

| | `library` (under `/resources/library/`) | `conventions` (under `/docs/`) |
|---|---|---|
| Sibling folders inside | books, papers, publishers, publications | naming, frontmatter |
| Templates across siblings | **different** (book, paper, publisher, publication) | **same** (all `doc`) |
| Structural reading | independent flat collections sharing a URL prefix | one nested collection with sub-collections |
| Item `collection:` value | `books`, `papers`, `publishers`, `publications` | `conventions`, `conventions/naming`, `conventions/frontmatter` |
| Role of the shared name | "library" is a URL grouping — no formal taxonomy role | "conventions" is a collection (template `doc`); sub-collections share that template |

In `library/`, books are books and papers are papers — different things sharing a shelf. In `conventions/`, naming docs and frontmatter docs are both doc articles — the same kind of thing organised by topic.

## Tags and topics are glossary roles, not collections

There is no `tags` or `topics` collection. The **glossary** is the canonical anchor for every concept: a tag is a glossary entry flagged `tag: true`, a topic is one flagged `topic: true`. Records reference them by slug — `tags:` (granular, "touches on") and `topics:` (primary, "is about") — and the website derives the tag listings and `/topics/<slug>` hubs from those references. See `glossary-schema.md` and `wikilinks.md`.

The glossary is also the one flat collection that uses **alphabetical letter-folders** for browsing — `resources/glossary/<letter>/<slug>.md` — while its URLs stay flat (`/resources/glossary/<slug>`), the same folder-for-browse / flatten-in-URL pattern blog uses.

## Collection names

A collection's name is its identifier. Items declare it in YAML (`collection: <name>`). The website's registry maps each name to a folder + URL pattern + template.

Two rules govern the name:

- **Include structural nesting.** When a collection is nested inside another, its name reflects the nesting: `conventions/naming`, not just `naming`.
- **Exclude URL navigation prefixes.** The website's URL groupings (`resources/`, `thinking/`, `research/`, `docs/`) don't appear in collection names. Those prefixes are presentation choices that live in the website's registry; items don't repeat them.

Examples:

| Item path | `collection:` value |
|---|---|
| `resources/wiki/<slug>.md` | `wiki` |
| `resources/glossary/<letter>/<slug>.md` | `glossary` |
| `resources/library/books/<slug>.md` | `books` |
| `resources/library/papers/<slug>.md` | `papers` |
| `resources/library/publishers/<slug>.md` | `publishers` |
| `resources/library/publications/<slug>.md` | `publications` |
| `thinking/essays/<slug>.md` | `essays` |
| `research/observations/<slug>.md` | `observations` |
| `research/insights/<slug>.md` | `insights` |
| `research/hypotheses/<slug>.md` | `hypotheses` |
| `research/reports/lightpapers/<slug>/<v>/<slug>.md` | `lightpapers` |
| `docs/conventions/<slug>.md` | `conventions` |
| `docs/conventions/naming/<slug>.md` | `conventions/naming` |
| `docs/conventions/frontmatter/<slug>.md` | `conventions/frontmatter` |
| `docs/schemas/<slug>.md` | `schemas` |
| `docs/contributing/<slug>.md` | `contributing` |
| `blog/<y>/<m>/<slug>.md` | `blog` |
| `people/<slug>.md` | `people` |
| `organizations/<slug>.md` | `organizations` |

## Template names

Each collection has one template. Template names follow one rule:

- **Singular, the kind of one item.** A book, an essay, a person, a doc, a glossary-item. The folder + URL + collection name stay plural; the template name describes one item.

| Collection (plural) | Template (singular) |
|---|---|
| essays | essay |
| wiki | wiki-article |
| glossary | glossary-item |
| observations | observation |
| insights | insight |
| hypotheses | hypothesis |
| books | book |
| papers | paper |
| publishers | publisher |
| publications | publication |
| people | person |
| blog | blog-post |
| conventions / schemas / contributing | doc |
| lightpapers / whitepapers | lightpaper / whitepaper |

Within a nested collection, sub-collections inherit the parent's template by default — naming and frontmatter under conventions both use `template: doc`.

## Cross-cutting templates

Three templates apply across the surface, not to a single collection:

- **`composed-page`** — block-composed pages (home, about, custom collection pages). Files live in `website/pages/<url-path>.md` in the **website repo**. Each composed page renders at its URL position — as a standalone page or as a custom version of a page the website would otherwise derive.
- **`overlay`** — splice fragments that layer site-specific framing onto a source page. Files live in `website/overlays/<source-folder>/<slug>.md` in the **website repo**. Mirrors the source's content folder path.
- **`plain-page`** — plain-markdown standalones (manifesto, contributing) with minimal frontmatter. The website renders title + body. Site-specific framing is added via an overlay so the source stays portable.

Composed pages and overlays live in the **website repo**, not the content repo. They're presentation artefacts specific to this site; the content repo holds only portable research content.

## Pages the website generates

Every URL that isn't an item page is handled by one rule:

1. If `website/pages/<url-path>.md` exists, render that composed page.
2. Otherwise, render a default derived page based on the URL position:
   - **Collection page** (e.g. `/resources/wiki`) — lists items in the collection, plus cards for any sub-collections if it's nested.
   - **Sub-collection page** (e.g. `/docs/conventions/naming`) — lists items in the sub-collection.
   - **URL-prefix page** (e.g. `/docs`, `/resources/library`) — lists the collections rendered under that URL prefix.

The default is enough for most cases. Author a composed page when you want a hand-crafted version.

## Singletons

A few files are unique standalone pages, not part of a collection:

- `thinking/manifesto.md` — `template: plain-page`. Renders at `/thinking/manifesto`.
- `CONTRIBUTING.md` (repo root) — `template: plain-page`. Renders at `/contributing`.

Both use the plain-page template. Site-specific framing (banners, CTAs, custom layout) is added via an overlay in the website repo.

## Where new content goes

**Adding an item to an existing collection:**

1. Pick the right template (singular entity name).
2. Drop the file in the collection's folder.
3. Set `template:` + `template_version:` + `collection:` in frontmatter, plus the template's required fields. See `frontmatter.md` for the universal contract and the specific template for its schema.

**Adding a new collection:**

1. Author a `template-<entity>-v1.0.0.md` for the entity if it doesn't exist.
2. Create the folder.
3. Register the collection in the website's registry (`folder`, `urlPattern`, `template`, optional `parent` for sub-collections).
4. Author your first item.

See `templates-and-versioning.md` for template authoring.

**Adding a sub-collection to a nested collection** (e.g. a new chapter under `conventions`):

1. Create the sub-folder inside the parent collection.
2. Register the sub-collection with `parent:` pointing at the parent in the website's registry.
3. Author items there — their `collection:` value is the path `parent/sub-collection`.

## Related conventions

- **Frontmatter contract** (universal + per-template fields): see `frontmatter.md`.
- **Templates and versioning** (semver, archive workflow): see `templates-and-versioning.md`.
- **Slug rules and file naming**: see `file-naming.md`.
- **Wikilinks**: see `wikilinks.md`.
- **Epistemic chain** (observation → insight → hypothesis): see `epistemic-chain.md`.
