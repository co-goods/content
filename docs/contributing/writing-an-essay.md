---
template: doc
template_version: 1.0.0
collection: contributing
slug: writing-an-essay
title: "Writing an essay"
description: "When to choose essay over other collections; voice, structure, and frontmatter conventions."
order: 10
status: active
stage: draft
created: 2026-05-21
updated: 2026-05-21T22:20
---

# Writing an essay

Essays are POV writing by any contributor — interpretive, argumentative, opinionated. They sit alongside wiki articles (which aim for neutrality) and reports (which are versioned formal compilations).

## When to choose essay over other collections

- **Essay** — you want to make a case, sketch a model, walk through a line of reasoning. The author's voice is present.
- **Wiki article** — you want to describe an existing concept neutrally and encyclopedically, open to community editing.
- **Report** — you want to publish a polished, versioned compilation (lightpaper, whitepaper, model paper).
- **Insight** — you want to capture a single atomic finding with explicit upstream links to observations / sources.

If you find yourself drafting an essay that becomes long and self-contained enough to want versioning, it may want to graduate to a report. Until then, essays evolve in place.

## Frontmatter

```yaml
---
slug: <topic-descriptive-slug>
status: active
stage: draft
type: essay
title: <human-readable title>
authors: [<person-slug>]
sources: [<library-slug>, <library-slug>]
tags: [<tag>, <tag>]
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---
```

Start with `stage: draft` while the essay is taking shape — the page is published with a WIP banner so the community can engage early. Move to `stage: published` when ready.

## Wikilinks

Use qualified-path wikilinks to other content:

- `[[resources/library/olleros-antirival-goods]]` — link to a library item
- `[[people/f-xavier-olleros|F. Xavier Olleros]]` — link to a person profile with custom display text
- `[[resources/wiki/antirival]]` — link to a wiki article
- `[[topics/antirival]]` — link to the topic aggregation page

### Bare wikilinks

`[[antirival-goods]]` without qualification resolves to `/topics/antirival` if a topic-aggregation page exists for that slug. If not, the build emits an error — qualification is required.

## Submitting

Drafts are committed and pushed to a branch; a PR against `main` triggers a Vercel preview deploy. The essay is reviewable on the preview URL while the PR is open. On merge it lands on the production site.

If you don't have repo access, fork the research repo and PR from your fork.
