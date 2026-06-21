---
template: overlay
template_version: 1.0.0
title: ""
note: ""
---

```callout
name: example-top-callout
region: top
position: top
type: info
title: ""
```
Body markdown for the callout — appears in the rendered overlay above the
default content of the source page.

```cta
name: example-bottom-cta
region: bottom
heading: ""
description: ""
label: ""
href: ""
variant: secondary
```

<!--
Overlay schema (template: overlay, v1.0.0).

Splice fragments that layer site-specific framing onto a source page
without the source content knowing about it. Lives in
`website/overlays/<source-folder>/<slug>.md` in the website repo (not the
content repo). The path mirrors the source's content path — e.g. an
overlay for `thinking/essays/on-collaboration.md` lives at
`website/overlays/thinking/essays/on-collaboration.md`.

Frontmatter is minimal: optional title and note for human reference. No
`collection:` — overlays aren't items in a collection.

Body: one or more fenced sections. Each section is one spliced
section; its splice metadata rides as reserved props:

- `region`: `top | body | sidebar | bottom` (default `body`).
- `position`: `top | bottom | { before: <anchor> } | { after: <anchor> }`.
  Anchor `default` refers to the layout's own content (the markdown body
  in `body`).
- `name` (optional): an anchor other sections can target.

Reserved props are stripped before the section's normal props reach its
component.
-->
