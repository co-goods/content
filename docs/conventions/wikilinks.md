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

How wikilinks work in the Co-Goods content repo — the qualified-path syntax, custom display text, bare-slug behaviour, and frontmatter arrays.

## Qualified-path syntax (Obsidian-native)

Wikilinks use **qualified paths** that mirror the website URL. The path inside the brackets is the URL the link resolves to.

```markdown
[[resources/library/papers/smith-network-coordination-2022]]
[[resources/wiki/network-coordination]]
[[research/insights/asynchronous-coordination-density]]
[[research/observations/weekend-readership-spike]]
[[thinking/essays/on-collaboration]]
[[people/jane-doe]]
[[tags/antirival]]
```

The path uses the URL navigation prefix (`resources/`, `thinking/`, `research/`, `docs/`) — wikilinks are about *where on the site* you're pointing, not *what collection* the target belongs to.

## Custom display text

Add a display string after a pipe:

```markdown
[[people/f-xavier-olleros|F. Xavier Olleros]]
[[resources/library/papers/smith-network-coordination-2022|Smith (2022) — Network Coordination]]
[[resources/wiki/network-coordination|Network Coordination]]
```

When omitted, the rendered link text is derived from the target's title.

## Bare wikilinks → topic pages

A bare slug (no slashes) resolves to a **topic aggregation page** if one exists:

```markdown
[[antirival]]   → /topics/antirival   (if the slug appears in 2+ collections)
```

If no topic page exists for the slug, the build fails with an error message pointing at the offending wikilink. This forces qualification — every wikilink either targets a specific URL or an existing topic page.

To intentionally link to a tag (not a topic page), qualify it:

```markdown
[[tags/antirival]]
```

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
[[resources/glossary/spdx|SPDX]] identifier (the same codes used in the
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
tags: [antirival, network-effects, sharing-economy]                    # implicit: tags
related_insights: [asynchronous-coordination-density]                  # implicit: insights
```

This keeps frontmatter compact and unambiguous. The website resolves each bare slug to the right URL based on which field it came from.

For library items, the field name is just `sources:` — the website knows to look across all library sub-collections (books, papers, podcasts, etc.) for the matching slug. This works because library slugs are globally unique within the library namespace.

## Cross-collection topics

When the same slug appears in 2+ collections (e.g., a `tags/antirival` tag and a `resources/wiki/antirival` wiki article on the same concept), the build generates a **topic page** at `/topics/<slug>` that aggregates all instances. Bare wikilinks to that slug then resolve to the topic page.

When the slug appears in only one collection, no topic page is generated, and bare wikilinks to it fail at build time — qualify them to be explicit.

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
