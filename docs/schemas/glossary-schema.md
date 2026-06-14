---
template: doc
template_version: 1.0.0
collection: schemas
slug: glossary-schema
title: "Glossary schema"
description: "The Dictionary Schema, the glossary-as-anchor model, and how Co-Goods uses both."
order: 10
status: active
stage: draft
created: 2026-05-21
updated: 2026-06-11
---

# Glossary schema

Glossary entries use the DePalma Workshop Dictionary Schema as their YAML frontmatter contract — a shared dictionary shape used across enterprises — extended with a small set of Co-Goods capability flags.

## The glossary is the canonical anchor

The glossary entry is the **single canonical node** for any word, term, or phrase. Every **tag** and every **topic** *is* a glossary entry — there are no standalone `tags/` or `topics/` files. A **wiki article** on the same slug is an optional long-form *facet* of the same concept, not a separate identity.

A concept's roles are declared as boolean flags on its entry, and records point *at* the concept (via `tags:` / `topics:` reference lists) rather than the concept being defined in many places. This keeps one identity per concept and makes tags / topics enforceable graph edges rather than orphan-prone files.

## Capability flags

Declare a flag **only when true** (omit = false):

- **`tag: true`** — the concept is usable as a content label. Records reference it via `tags: [<slug>]` ("touches on / related to"), and it surfaces a tagged-items listing.
- **`topic: true`** — the concept has a generated `/topics/<slug>` hub. Records reference it via `topics: [<slug>]` ("is about" — primary subject). **Topic anchors should use established vocabulary** — Co-Goods's own coined concepts are terms surfaced *within* topics, not topics themselves.
- **`keyword`** — **not authored here.** It is internal SEO/preferred-vocabulary metadata and belongs to the future MCC database, not this public repo.

A concept may carry any combination (e.g. `network-effects` is both tag and topic; most terms are neither).

## Why a shared schema

The dictionary schema handles linguistic complexity that simple "term + definition" structures miss: acronyms, aliases, multiple grammatical classes, definitions per sense, related terms, comparisons. Sharing the schema across enterprises means a glossary entry written here is structurally compatible with a future cross-enterprise dictionary surface (the MCC database) without rewrites. The schema is open-licensed (CC BY-SA 4.0), which matches Co-Goods's own licensing.

> **Note:** Co-Goods normalises the entry's display field to **`title`** (the taxonomy-v1 universal field), where the upstream Dictionary JSON Schema uses `name`. This is a deliberate divergence — the JSON-schema side is to be reconciled before any database sync.

## Location — alphabetical letter-folders

Entries live in letter sub-folders keyed on the slug's first letter:

- `resources/glossary/a/antirival.md`, `resources/glossary/n/network-effects.md`, …
- Non-alphabetic first char → a `_` folder.
- The **URL stays flat**: `/resources/glossary/<slug>`. The letter folder is a browse/authoring aid only (the resolver computes the letter from the slug).

## Base form canonical

The `slug` uses the base form of the term; grammatical variants live inside the entry, not as separate files.

- `resources/glossary/c/co-goods.md` — base form
- `co-goodsing` (verb), `co-goodser` (noun-agent) — declared under `classes[type=verb].forms`, **not** as separate entries.

Where a concept is naturally a **noun phrase** ("antirival goods"), that phrase is the entry's `title`, the slug is its kebab form (`antirival-goods`), and the bare adjective is an **alias**: `slug: antirival-goods`, `title: Antirival goods`, `aliases: [antirival, antirival good]`. A *property noun* for the same axis (`rivalry`, `nonrivalness`, `antirivalness`) names a **distinct concept** — the property, not the good — so it gets its **own entry** and a `related_terms` edge, never an alias of the good.

Singular is the default headword, with the plural as an alias (`wicked-problem`, alias `wicked problems`). The goods cluster is the documented exception — it keeps the established economics plural (`rival-goods`, `nonrival-goods`, `antirival-goods`). See `file-naming.md`.

## Minimum frontmatter

```yaml
---
template: glossary-item
template_version: 1.2.0
collection: glossary
slug: <kebab-case-base-form>
title: <human-readable form>
type: word | term | comparison
tag: true            # only if it is a tag (omit otherwise)
topic: true          # only if it is a topic (omit otherwise)
aliases:             # optional — surface variants of the SAME concept
  - <plural / bare adjective / spelling / acronym>
classes:
  - type: noun | verb | adjective | adverb
    definitions:
      - <definition text>
relationships:
  related_terms:
    - <other-glossary-slug>
not_to_be_confused_with:   # optional — distinct concepts it is commonly conflated with
  - <other-glossary-slug>
status: active
stage: draft
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---
```

- **`type`** is the *entry kind*: `word` (a single lexical word), `term` (a multi-word term of art), or `comparison` (an entry that contrasts two concepts — see "Comparison entries" below). It is distinct from `classes[].type`, the *grammatical* class.
- **`relationships.related_terms`** is the single related-concepts list (it absorbs what tag files used to call `related_tags`). Every slug must resolve to a glossary entry — there is **hard build-enforcement** against dangling concept edges.

## Aliases and their lifecycle

`aliases:` lists alternate names for the *same* concept — surface variants only: the plural form, the bare adjective of a noun-phrase headword, an alternate spelling, an acronym (e.g. `antirival good`, `antirival`). Aliases resolve to, and are findable as, the host entry. If an alias later gains its own weight or its meaning diverges, **break it out into its own entry** — at which point it stops being an alias and becomes a `related_terms` edge instead. It stays findable on the website throughout.

This is exactly what happened to `antirivalness`: it began as an alias of `antirival-goods`, then became its **own entry** — the *property* (a good gets more valuable the more it is shared), distinct from the *good* — with a `related_terms` edge between the two. The lesson: a word that names a different concept is never an alias, even when the words look related.

## Comparison entries

An entry with `type: comparison` contrasts two concepts rather than defining one. It carries a `comparison` block instead of grammatical `classes`:

```yaml
type: comparison
comparison:
  terms: [physical, digital]        # the two glossary slugs being compared
  description:                      # prose framing of the difference (one or more paragraphs)
    - "Physical and digital are routinely opposed, but ..."
  detailed_comparison:              # aspect-by-aspect; term_a -> terms[0], term_b -> terms[1]
    - aspect: "What kind of category it is"
      term_a: "A mode of existence — ..."
      term_b: "A mode of representation — ..."
```

`comparison.terms` must resolve to glossary entries (so the site links them and pulls their definitions). The website renders a comparison with a dedicated view — the `description` plus an aspect table — not the noun/verb class blocks.

## Not to be confused with

`not_to_be_confused_with:` lists glossary slugs this concept is commonly conflated with but is **distinct** from (e.g. the `physical-vs-digital` comparison vs `non-physical`). It renders as a short "Not to be confused with" note. Unlike `aliases` (which assert *sameness*), this field asserts *difference* — use it for exactly the distinctions that keep getting blurred.

## Richer fields

As entries mature, additional dictionary fields become useful — `acronym` / `expanded_form`, per-sense definitions, etymology, comparison-target slugs, example sentences. Start minimal; grow the entry as usage stabilises.

## Body conventions

The markdown body is for **prose discussion** — context, history, why the term matters to Co-Goods, references to other concepts (linked **bare**: `[[antirival-goods]]`) and to library items (qualified). The frontmatter is the structured contract; the body is the human-readable elaboration. Don't restate the definition as the whole body.
