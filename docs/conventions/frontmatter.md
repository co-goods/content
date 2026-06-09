---
template: doc
template_version: 1.0.0
collection: conventions
slug: frontmatter
title: "Frontmatter contract"
description: "The universal frontmatter contract every authored file carries."
order: 20
status: active
stage: draft
---

# Frontmatter contract

Every authored file in the Co-Goods content repo (and the website's `pages/` and `overlays/` folders) carries a YAML frontmatter block. This doc defines the **universal contract** — the fields every item must have — and points to where per-template schemas are defined.

## Universal fields

Every content item (file in a collection) declares at minimum:

```yaml
---
template: <entity name>           # the schema this item follows
template_version: 1.0.0           # semver matching the template
collection: <collection name>     # which collection this item belongs to
title: "..."                      # human-readable title
---
```

That's the universal contract. Every item, in every collection, carries these four fields.

### `template:`

The name of the schema/template this item follows. Singular entity name:

- `essay`, `wiki-article`, `glossary-item`, `book`, `paper`, `publisher`, `publication`, `observation`, `insight`, `hypothesis`, `person`, `tag`, `blog-post`, `doc`, `lightpaper`, `whitepaper`, …

Matches the template filename `templates/template-<entity>-v<version>.md`.

### `template_version:`

The semver version of the template the item was authored against. Matches the version in the template's filename and frontmatter (e.g., `1.0.0`).

This is a back-reference — the renderer uses it to dispatch on version; migration scans grep for it; humans use it to know what schema applies.

### `collection:`

The collection this item belongs to. Matches a registered collection in the website's registry.

For flat collections, just the leaf: `essays`, `books`, `papers`, `wiki`, `people`, `tags`, …

For sub-collections of a nested collection, the full path: `conventions/naming`, `conventions/frontmatter`, …

URL navigation prefixes (`resources/`, `docs/`, etc.) don't appear here — they're presentation, not identity.

See `taxonomy.md` for the model.

### `title:`

Human-readable title. Required by most templates. A few use `name:` instead (glossary items, people, tags, organisations) — see the template's schema notes.

## Per-template fields

Each template defines additional required and optional fields specific to its content type. The authoritative reference for those is each template's own schema-notes block at `templates/template-<entity>-v<version>.md`.

Examples of per-template fields:

- **Essay**: `authors`, `summary`, `tags`, `publishedAt`, `status`, `stage`, …
- **Book**: `authors`, `year`, `publisher`, `isbn`, `language`, …
- **Person**: `name`, `affiliation`, `bio`, `github`, `email`, `expertise`, …
- **Insight**: `authors`, `observations`, `sources`, `tags`, `key_findings`, `implications`, …
- **Doc**: `description`, `order`, …

When starting a new item, copy the latest template — it documents its own schema inline.

## Common patterns across templates

Several optional patterns appear in multiple templates:

### `tags:`

Many content types accept tags — a list of bare slugs referring to entries in the `tags` collection:

```yaml
tags:
  - antirival
  - network-effects
  - sharing-economy
```

### `summary:`

A one- or two-sentence summary used in listings, search results, and as a meta description. Common on essays, insights, observations, hypotheses, wiki articles, library entries.

### `relevance:` and `related:` — data in the frontmatter, not the body

Both live in the **YAML frontmatter** and are **rendered by the website** — there is **no hand-written `## Relevance to Co-Goods` or `## Related` section in the body**. The frontmatter is the single source of truth (and the graph/card data); a body section would just duplicate it.

- **`relevance:`** — a short statement of *why this node matters to us* (its relevance to Co-Goods). Use it on nodes we **reference or describe** (library entries, people, organisations) and on concept nodes (wiki) — not on our own first-party content (essays, research, blog), where the relevance is implicit. The site renders it through the markdown pipeline under a "Relevance to Co-Goods" heading, so it may use light emphasis or a second paragraph (a `>` block scalar):

  ```yaml
  relevance: How to harness network effects as a force *for* a commons, not a moat for extraction.
  ```

- **`related:`** — a list of bare qualified paths to related nodes; the site renders the Related list at the foot of the page. (Some types carry richer *typed* relations instead — glossary `related_terms`, tags `related_tags`, people `sources_by_author`, the research epistemic chain — left as-is for now.)

  ```yaml
  related:
    - resources/wiki/network-coordination
    - resources/library/papers/smith-network-coordination-2022
  ```

### `status:` and `stage:`

Two independent flags: `status:` controls **visibility**, `stage:` controls **maturity**.

```yaml
status: active     # active | inactive — is the item on the site at all?
stage: draft       # stub | draft | published — how mature is it?
```

The maturity ladder is **`stub → draft → published`**:

- **`stub`** — a placeholder: the *intention* or outline of a page, before it has real content. Use it to stake out a doc that's coming.
- **`draft`** — real work-in-progress. The website renders a visible "Draft — work in progress" banner.
- **`published`** — complete; no banner.

Visibility is separate: `status: inactive` keeps an item off the site regardless of stage. Cross-collection convention; check each template's notes for specifics.

### `example: true`

For placeholder content used to exercise the website's templates without claiming research-domain status:

```yaml
example: true
```

The website may filter `example: true` content from production renders.

### `created:` and `updated:`

ISO date strings for the item's creation and last update. Optional but recommended:

```yaml
created: 2026-05-21
updated: 2026-05-27
```

### `discord:`

An optional reference to where this page is discussed on Discord. It accepts **either a full URL or a channel key**:

```yaml
# A full URL — a specific channel or thread:
discord: https://discord.com/channels/<server>/<channel-or-thread>

# Or a key — resolves to a configured channel invite:
discord: research        # one of: research, calls, thinking, resources, invite
```

The page's "Discuss on Discord" link (next to "Edit this page on GitHub") always resolves, in this order:

1. the item's own `discord:` (the URL or key above), else
2. the channel for the page's **area** — items under `thinking/` → the thinking channel, `resources/` → resources, `research/` → research, else
3. the **general** server invite.

So you only set `discord:` when a page has a *specific* discussion that differs from its area's channel. The keys and their invites are configured site-side (env-backed); a contributor just uses the key or a URL.

### `license:` and `license_url:`

Original content defaults to **CC BY-SA 4.0** — you don't declare it per item. Set `license:` (and optionally `license_url:`) only to **override** the default for a specific item:

```yaml
license: CC-BY-4.0
license_url: https://creativecommons.org/licenses/by/4.0/
```

Write the value as an **SPDX identifier** — the standard short code for a license (`CC-BY-4.0`, `CC-BY-SA-4.0`, `CC0-1.0`, `MIT`, …). It's unambiguous and machine-readable, and the site renders a friendly, linked label from it, so `license_url:` is optional.

Absent = the item inherits the site default. This is for the occasional item under a different (compatible) license. Note that **media carries its own license independently** — set that on the image/video block, not here (see `media.md`); and **library entries don't relicense the works they describe** — the record is first-party, the described work's rights are untouched. The full licensing model is in [[docs/conventions/licensing|licensing]].

### `work_license:`

Used **only on library entries**. It records the SPDX license of the **work being catalogued** — the book, paper, or standard itself — which is independent of the license on our own content:

```yaml
work_license: CC-BY-SA-4.0   # the described work's own license
```

Keep the two straight: `license:` is the license of *this page's* content (our prose) — library records use the site default, so they rarely set it — while `work_license:` is the *third-party work's* own license, which we record but neither grant nor change. See the library three-layer in [[docs/conventions/licensing|licensing]].

## Cross-cutting templates

Composed pages, overlays, and plain pages declare `template:` + `template_version:` but no `collection:` (they're not items in a content collection):

A composed page (home, about, custom collection page):

````markdown
---
template: composed-page
template_version: 1.0.0
title: "About Co-Goods"
---

```hero
variant: gradient
title: About Co-Goods
subtitle: …
```

```prose
```
## Project overview

…body…
````

An overlay (splice fragment):

````markdown
---
template: overlay
template_version: 1.0.0
title: "Overlay — On Collaboration"   # optional; for human reference
---

```callout
name: editor-note
region: top
position: top
type: info
title: Editor's note
```
This essay is an early placeholder — shared so the community can engage as the thinking develops.
````

A plain-markdown standalone (manifesto, contributing):

```yaml
---
template: plain-page
template_version: 1.0.0
title: "Co-Goods Manifesto"
---

# {{title}}

Body content as plain markdown.
```

## Examples — full items

A wiki article:

```yaml
---
template: wiki-article
template_version: 1.0.0
collection: wiki
title: "Network Coordination"
summary: "Patterns and mechanisms by which distributed participants align their actions across a network without central direction."
tags:
  - coordination
  - network-effects
status: active
stage: draft
---

# Network Coordination

Body content as plain markdown.
```

An insight:

```yaml
---
template: insight
template_version: 1.0.0
collection: insights
title: "Engagement Density Predicts Coordination Quality in Asynchronous Networks"
summary: "When participation is asynchronous, engagement DENSITY (concentration per unit time) matters more than total engagement volume for coordination quality."
authors:
  - jane-doe
observations:
  - expert-interview-pattern
  - weekend-readership-spike
sources:
  - smith-network-coordination-2022
tags:
  - coordination
  - network-effects
status: active
stage: draft
---

# {{title}}

…body…
```

A doc article in a sub-collection:

```yaml
---
template: doc
template_version: 1.0.0
collection: conventions/naming
title: "Slug rules"
description: "How content slugs are formed and validated."
order: 20
---

# Slug rules

…body…
```

A book (in the `books` flat collection, presented under `/resources/library/books/`):

```yaml
---
template: book
template_version: 1.0.0
collection: books
title: "Systems Thinking for the Curious"
authors:
  - jane-doe
year: 2019
publisher: example-press
isbn: "978-0-12345-678-9"
language: en
tags:
  - coordination
  - sharing-economy
---

# Notes / annotations on the book

…body…
```

## Related conventions

- **Taxonomy** (collections, items, templates): see `taxonomy.md`.
- **Templates and versioning** (semver, archive workflow): see `templates-and-versioning.md`.
- **Slug rules and file naming**: see `file-naming.md`.
