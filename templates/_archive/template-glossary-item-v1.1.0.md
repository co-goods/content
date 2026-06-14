---
template: glossary-item
template_version: 1.1.0
collection: glossary
slug: ""
title: ""
tag: false
topic: false
classes: []
relationships:
  related_terms: []
links: []
sources: []
status: active
stage: draft
created: "{{date}}"
updated: "{{date}}"
---

# {{title}}

<!--
Glossary item schema (template: glossary-item, v1.1.0).

The glossary entry is the CANONICAL ANCHOR for a word / term / phrase: every
tag and topic IS a glossary entry, not a separate file. A wiki article (same
slug) is an optional long-form facet of the same concept.

Co-Goods adopts the DePalma Workshop Dictionary Schema (CC BY-SA 4.0) as the
contract. Start with this minimal subset; grow into richer fields (comparisons,
multiple grammatical classes, aliases, acronyms) as content matures.

LOCATION — alphabetical letter-folders by slug's first letter:
  `resources/glossary/<a-z>/<slug>.md`  (e.g. resources/glossary/a/antirival.md)
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
  - slug: bare kebab-case, BASE FORM (e.g. `co-goods`, not `co-goodsing`)
  - title: display form (taxonomy-v1 universal field; replaced `name` in v1.1.0)
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

    The inner `classes[].type` is the grammatical class (noun / verb / adjective / …).

  - relationships.related_terms: slugs of related glossary concepts (one list;
    folds in what used to be a tag's `related_tags`). Each must resolve to a
    glossary entry (hard build-enforcement — no dangling concept edges).

LINKING: concepts (glossary anchors) are linked BARE — `[[antirival-goods]]` (Obsidian
  resolves by filename regardless of letter-folder; the site routes bare -> topic
  hub if topic:true, else the glossary entry). Everything else stays qualified
  (`[[thinking/essays/…]]`, `[[people/…]]`). See docs/conventions/wikilinks.md.

Optional (richer dictionary fields): `aliases`, `acronyms`, `comparisons`,
`usage`, `register`. Base form is canonical; grammatical variants live under
`classes[type=verb].forms`. Cross-enterprise compatibility (the future MCC
dictionary uses the same schema) is why we adopt it now even if fields are unused.
-->
