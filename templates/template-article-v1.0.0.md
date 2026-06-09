---
template: article
template_version: 1.0.0
collection: articles
discord: ""
slug: ""
serial: ""
title: ""
authors: []
year: ""
publication: ""
issue: ""
url: ""
work_license: ""
language: ""
open_access: false
summary: ""
key_points: []
relevance: ""
is-cited: false
is-featured: false
status: active
added-by: ""
added: "{{date}}"
tags: []
created: "{{date}}"
updated: "{{date}}"
---

# {{title}}

## Overview
Brief overview of the article and its main argument.

## Relevance to Co-Goods
Our project's perspective on this article and how it informs co-goods thinking.

## Quotes & citations
> "Important quote."
>
> — Author Name

## Notes
Additional notes, thoughts, or questions.

<!--
Article schema (template: article, v1.0.0).

An `article` catalogues a non-academic article — a magazine piece, an online or
blog article, an essay published elsewhere. Academic papers use the `paper`
type; books use `book`. We **link out** to the source — we never host it.

Required:
- File location: `resources/library/articles/<slug>.md`
- `slug`: bare kebab-case, `<lastname>-<2-3 headline words>-<year>`; matches filename
- `serial`: `l-#####` — every article in the repo gets one; register in `resources/library/INDEX.md`. Example/placeholder articles use `x-#####`.
- `authors`: bare people slugs
- `year`: publication year
- `url`: where the article lives (we link, never host)
- `is-cited`: true if any research-side content cites this
- `is-featured`: true if surfaced on the public library page
- `added-by`: bare people slug — who curated this entry

Optional (add when relevant):
- `publication`: the magazine / site / outlet it appeared in (freetext, e.g. `Permaculture Magazine`)
- `issue`: issue or edition (e.g. `68`)
- `work_license`: SPDX identifier of the article's own license (the described work's license)
- `language`, `open_access`
- `summary`, `key_points`, `relevance_to_project`, `tags`
- `discord`: optional discussion-thread URL for this entry
-->
