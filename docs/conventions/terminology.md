---
template: doc
template_version: 1.0.0
collection: conventions
slug: terminology
title: "Terminology"
description: "Which words to use, and how the glossary settles preferred vocabulary for open contribution."
order: 60
status: active
stage: draft
---

# Terminology

Open research and innovation means many hands writing across the same concepts. For that to stay coherent, contributors need a shared answer to "which word do we use, and what does it mean?" The **glossary is that answer** — it is the canonical vocabulary, and this page explains how to use it.

## The glossary is canonical

Every concept has one glossary entry (the [anchor](/docs/schemas/glossary-schema)). When you write about a concept, link it bare — `[[antirival-goods]]` — and use its **canonical headword** as the surface term. Aliases (plurals, the bare adjective, alternate spellings) still resolve, but prefer the headword in prose so the same idea reads the same way everywhere.

If the word you want isn't in the glossary yet, that's a signal to add an entry rather than coin a one-off term in passing.

## Use the established term where one exists

Co-Goods connects its ideas to existing fields, so reach for the **established term** when there is one — "network effects", "wicked problem", "antirival goods" — and introduce a Co-Goods coinage only when nothing established fits. This is also why topic hubs use established vocabulary: readers should meet the material on familiar ground. New or coined concepts are glossary terms surfaced *within* those topics, not topics of their own.

## Keep distinct concepts distinct

Some words look related but name different things, and blurring them costs clarity:

- **rivalry** (the consumption axis) is not *competition* (a contest between firms).
- **antirivalness** (a property) is not **antirival goods** (the goods that have it).
- **physical vs. digital** is a category error — the real distinction is **physical vs. non-physical** (digital is one kind of non-physical).

When a concept is routinely confused with another, the glossary entry records it in `not_to_be_confused_with`, which renders as a "Not to be confused with" note. Reach for that field rather than re-litigating the distinction in every body.

## Casing

Display titles use **sentence case** — capitalise only the first word and proper nouns ("Network effects", "Antirival goods"; but "SPDX", "GitHub", "Co-Goods"). Slugs are kebab-case. See `file-naming.md` for the full rules.

## Related conventions

- **Glossary schema** (the anchor model, fields, aliases, comparisons): see `../schemas/glossary-schema`.
- **Wikilinks** (bare for concepts, qualified for everything else): see `wikilinks.md`.
- **File naming** (slugs, singular headwords, the goods exception, casing): see `file-naming.md`.
