---
template: plain-page
template_version: 1.0.0
title: ""
status: active
created: "{{date}}"
updated: "{{date}}"
---

# {{title}}

Body content as plain markdown.

<!--
Plain page schema (template: plain-page, v1.0.0).

For unique standalone pages that aren't part of any collection and don't need
the section-composition model — manifesto, contributing, that sort of thing.

- Minimal frontmatter: just title (plus universal `template` + `template_version`).
- Body: plain markdown. The website renders title + body with default
  typographic styling.
- Site-specific framing (banners, CTAs, custom layout) is added via an
  overlay in the website repo (`website/overlays/<source-folder>/<slug>.md`),
  so the source stays portable.
- Used for files like `thinking/manifesto.md` and the repo-root
  `CONTRIBUTING.md`. These aren't items in a collection — they have no
  `collection:` field.
-->
