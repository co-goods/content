---
template: glossary-item
template_version: 1.2.0
collection: glossary
slug: ""
title: ""
type: ""
tag: false
topic: false
aliases: []
classes: []
relationships:
  related_terms: []
not_to_be_confused_with: []
relevance: ""
links: []
sources: []
status: active
stage: draft
created: "{{date}}"
updated: "{{date}}"
---

# {{title}}

<!--
Glossary item schema (template: glossary-item, v1.2.0).

The glossary entry is the CANONICAL ANCHOR for a word / term / phrase: every
tag and topic IS a glossary entry, not a separate file. A wiki article (same
slug) is an optional long-form facet of the same concept.

Co-Goods adopts the DePalma Workshop Dictionary Schema (CC BY-SA 4.0) as the
contract. Start with this minimal subset; grow into richer fields (comparisons,
multiple grammatical classes, aliases, acronyms) as content matures.

LOCATION — alphabetical letter-folders by slug's first letter:
  `resources/glossary/<a-z>/<slug>.md`  (e.g. resources/glossary/a/antirival-goods.md)
  Non-alphabetic first char -> `_` folder. The URL stays flat:
  /resources/glossary/<slug> (the letter folder is a browse aid only).

CAPABILITY FLAGS (declare ONLY when true; omit = false):
  - tag: true    — usable as a content label; records reference it via `tags: [slug]`
                   ("touches on / related to"). Surfaces a tagged-items listing.
  - topic: true  — has a generated /topics/<slug> hub; records reference it via
                   `topics: [slug]` ("is about" — primary subject). Topic anchors
                   should use ESTABLISHED vocabulary; Co-Goods's
                   own coined concepts are terms surfaced WITHIN topics, not topics.
  (keyword is a DB-era / internal concern — NOT authored in this public repo.)

CORE FIELDS:
  - slug: bare kebab-case, BASE FORM. Singular by default (`wicked-problem`, not
    `wicked-problems`); the plural is an alias. Exception: the goods cluster keeps
    the established economics plural (`rival-goods`, `antirival-goods`). See
    docs/conventions/file-naming.md.
  - title: display form, sentence case (taxonomy-v1 universal field; replaced `name`).
  - type: the ENTRY KIND — `word` (single lexical word), `term` (multi-word term of
    art), or `comparison` (an entry that contrasts two+ concepts — see below).
    Distinct from classes[].type, the GRAMMATICAL class.
  - aliases: alternate names for the SAME concept (surface variants — plural forms,
    spellings, acronyms, the bare adjective of a noun-phrase headword). NOT a place
    for a sibling concept: if a word names a distinct concept (e.g. `antirivalness`
    is the property, `antirival-goods` is the good), it gets its OWN entry and a
    `related_terms` edge — never an alias. (See "Aliases and their lifecycle" in
    docs/schemas/glossary-schema.md.)
  - classes: grammatical classes + definitions. Example:

      classes:
        - type: noun
          definitions:
            - "A class of goods designed for shared use that ..."
        - type: verb
          forms:
            present: co-goodsing
            past: co-goodsed
          definitions:
            - "To do ..."

  - relationships.related_terms: slugs of related glossary concepts (one list).
    Each must resolve to a glossary entry (hard build-enforcement — no dangling edges).
  - not_to_be_confused_with: slugs of glossary concepts this is commonly conflated
    with but is distinct from (e.g. rivalry vs competition; physical-vs-digital vs
    non-physical). Rendered as a "Not to be confused with" note.
  - relevance: a one-line "why this matters to Co-Goods" — the editorial angle,
    rendered as a "Relevance to Co-Goods" callout (as on library/people entries).
    Carry it even on a stub.

STUBS (stage: stub): keep them lightweight — the concise `classes` definition +
  `relevance` + the `related_terms` edges, with an EMPTY body. The Stub banner and
  the relevance line give context; don't write prose until the entry is drafted or
  researched, so unreviewed placeholders stay visibly unfinished.

COMPARISON ENTRIES (type: comparison):
  A comparison entry explicitly contrasts two concepts. It carries a `comparison`
  block instead of (or alongside) `classes`:

      type: comparison
      comparison:
        terms: [physical, digital]        # the two anchored glossary slugs compared
        description:                       # general prose framing of the difference
          - "Physical and digital are routinely opposed, but ..."
        detailed_comparison:               # aspect-by-aspect; term_a -> terms[0], term_b -> terms[1]
          - aspect: "What it is"
            term_a: "A mode of existence — matter in space."
            term_b: "A mode of representing information — encoded in bits."

  `comparison.terms` must resolve to glossary entries (so the site links them and
  pulls their definitions). The website renders `type: comparison` with a dedicated
  comparison view (description + aspect table) rather than the grammatical class blocks.

LINKING: concepts (glossary anchors) are linked BARE — `[[antirival-goods]]` (Obsidian
  resolves by filename regardless of letter-folder; the site routes bare -> topic
  hub if topic:true, else the glossary entry). Everything else stays qualified
  (`[[thinking/essays/…]]`, `[[people/…]]`). See docs/conventions/wikilinks.md.

Field-name casing: snake_case (`related_terms`, `not_to_be_confused_with`,
`detailed_comparison`), matching the rest of the frontmatter contract.
-->
