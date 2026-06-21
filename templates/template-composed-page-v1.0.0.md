---
template: composed-page
template_version: 1.0.0
title: ""
---

```hero
variant: default
eyebrow: ""
title: ""
subtitle: ""
```

```prose
```
## A section heading

Body markdown belongs to the most recently opened body-rich section (here,
`prose`). It runs until the next fenced section opens (or end of file).

```cta
heading: ""
description: ""
label: ""
href: ""
variant: secondary
```

<!--
Composed page schema (template: composed-page, v1.0.0).

A page composed entirely of sections. Lives in
`website/pages/<url-path>.md` in the website repo (not the content repo).

Two uses:
- **Standalone pages** at any URL (home → `website/pages/home.md`, about →
  `website/pages/about.md`, etc.).
- **Custom collection pages** that substitute for the default derived
  collection page (e.g. `website/pages/resources/library.md` for the
  `/resources/library` listing).

Frontmatter is minimal: title only (plus universal `template` +
`template_version`). No `collection:` — composed pages aren't items in a
collection.

Body: one or more fenced sections. Bare prose outside any section is a
build error — wrap plain markdown in a `prose` section. The website's section
registry defines the available section names (hero, prose, callout, quote,
emailsignup, cta, …).
-->
