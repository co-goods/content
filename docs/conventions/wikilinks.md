---
template: doc
template_version: 1.0.0
collection: conventions
slug: wikilinks
title: "Wikilinks"
description: "Qualified-path wikilink syntax and frontmatter array conventions."
order: 50
status: active
stage: draft
---

# Wikilinks

How wikilinks work in the Co-Goods content repo. The one rule to remember: **concepts (glossary anchors) are linked bare; everything else is qualified.**

## Concepts are linked bare

A glossary concept — any word/term/phrase that has a glossary entry — is linked with a **bare** slug (no slashes):

```markdown
[[antirival-goods]]   [[network-effects]]   [[demand-coordination]]
```

A bare link resolves to the concept's **topic hub** (`/topics/<slug>`) if the entry is `topic: true`, otherwise to the **glossary entry** (`/resources/glossary/<slug>`). Bare links work in Obsidian regardless of the entry's letter-folder, and on the site via the same routing — which is why concepts use them. There is no `[[tags/...]]` form any more; tags are glossary roles, not a collection.

## Qualified paths — everything else (Obsidian-native)

For non-concept targets (essays, library items, people, research, wiki articles, docs), use **qualified paths** that mirror the website URL. The path inside the brackets is the URL the link resolves to.

```markdown
[[resources/library/papers/smith-network-coordination-2022]]
[[resources/wiki/network-coordination]]
[[research/insights/asynchronous-coordination-density]]
[[research/observations/weekend-readership-spike]]
[[thinking/essays/on-collaboration]]
[[people/jane-doe]]
```

The path uses the URL navigation prefix (`resources/`, `thinking/`, `research/`, `docs/`) — wikilinks are about *where on the site* you're pointing.

## Custom display text

Add a display string after a pipe:

```markdown
[[people/f-xavier-olleros|F. Xavier Olleros]]
[[resources/library/papers/smith-network-coordination-2022|Smith (2022) — Network Coordination]]
[[resources/wiki/network-coordination|Network Coordination]]
```

When omitted, the rendered link text is derived from the target's title.

## Bare-link resolution (declared topics)

A bare slug resolves against the glossary anchor:

```markdown
[[network-effects]]   → /topics/network-effects        (entry is topic: true)
[[antirival-goods]]         → /resources/glossary/antirival-goods  (entry exists, not a topic)
```

Topic pages are **declared** (`topic: true` on the entry), not derived from a slug appearing in multiple collections. A bare slug with **no glossary entry at all** is a build error pointing at the offending link — so every bare link names a real concept.

## Inline license references

Besides path links, there's a special **license reference** form: writing
`[[license:<SPDX-id>]]` anywhere in a body renders a small license chip — the
license's short label, linked to its canonical text. For example, this source:

```markdown
The data is [[license:CC0-1.0]]; the prose is [[license:CC-BY-SA-4.0]].
```

renders as:

The data is [[license:CC0-1.0]]; the prose is [[license:CC-BY-SA-4.0]].

It's a *highlight*, not a navigation link — use it to call out the license of
something you're discussing inline. The value is an
[[spdx|SPDX]] identifier (the same codes used in the
`license:` and `work_license:` frontmatter fields). It works in any markdown
body — essays, wiki, docs, library entries.

This is only for *mentioning* a license. For the license of the **whole item**
use the `license:` frontmatter field; for the license of a **third-party work**
in the library use `work_license:`. See
[[docs/conventions/frontmatter|frontmatter]] for the fields and
[[docs/conventions/licensing|licensing]] for the full model.

## Frontmatter arrays use bare slugs

In frontmatter array fields, slugs stay bare — the collection is implicit from the field name:

```yaml
sources: [olleros-antirival-goods, smith-network-coordination-2022]   # implicit: library items
observations: [weekend-readership-spike]                              # implicit: observations
authors: [pontus-karlsson, jane-doe]                                   # implicit: people
tags: [antirival-goods, network-effects, sharing-economy]                    # glossary entries flagged tag: true
topics: [demand-coordination]                                          # glossary entries flagged topic: true
related_insights: [asynchronous-coordination-density]                  # implicit: insights
```

This keeps frontmatter compact and unambiguous. The website resolves each bare slug to the right URL based on which field it came from. `tags:` and `topics:` both reference glossary slugs — `tags:` is "touches on" (many, granular), `topics:` is "is about" (few, the record's primary subject); each must resolve to an entry carrying the matching flag (`tag: true` / `topic: true`) or the build fails.

For library items, the field name is just `sources:` — the website knows to look across all library sub-collections (books, papers, podcasts, etc.) for the matching slug. This works because library slugs are globally unique within the library namespace.

## Topics (declared, reference-based)

A topic hub at `/topics/<slug>` exists when the glossary entry is `topic: true` — declared, any size, even one item. Its membership is built from records that **reference** the slug in their `tags:` / `topics:` frontmatter (not from records sharing the slug), so differently-slugged records all aggregate under the one concept. See [[docs/schemas/glossary-schema|the glossary schema]] for the anchor model.

## Code spans are left alone

Wikilinks inside fenced code blocks or inline code spans are not processed:

````markdown
The syntax is `[[collection/slug]]` — note the double brackets.

```markdown
This [[wiki/example]] is shown as literal text in the code block.
```
````

This lets documentation about wikilinks (like this page) include literal examples without them being resolved.

## Related conventions

- **Taxonomy** (collections, items, templates): see `taxonomy.md`.
- **Frontmatter contract** (universal + per-template fields): see `frontmatter.md`.
- **Slug rules and file naming**: see `file-naming.md`.
