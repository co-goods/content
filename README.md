# Co-Goods — content

Research content for the Co-Goods protocol — a system for co-created and networked physical products. This repository is the **content store**; the website (`co-goods/website`) renders it via a submodule.

The taxonomy and conventions live alongside the content under `docs/conventions/`. The canonical references:

- [**Taxonomy**](./docs/conventions/taxonomy.md) — collections, items, templates, the flat-vs-nested rule.
- [**Templates and versioning**](./docs/conventions/templates-and-versioning.md) — semver, naming, archive workflow.
- [**Frontmatter contract**](./docs/conventions/frontmatter.md) — universal + per-template fields.
- [**File naming and slugs**](./docs/conventions/file-naming.md) — flat .md files, per-collection slug patterns, serials.
- [**Wikilinks**](./docs/conventions/wikilinks.md) — qualified-path syntax and frontmatter array convention.
- [**The epistemic chain**](./docs/conventions/epistemic-chain.md) — observation → insight → hypothesis.

## Collections

| Collection | URL | Folder |
|---|---|---|
| `essays` | `/thinking/essays/<slug>` | `thinking/essays/` |
| `wiki` | `/resources/wiki/<slug>` | `resources/wiki/` |
| `glossary` | `/resources/glossary/<slug>` | `resources/glossary/` |
| `books` | `/resources/library/books/<slug>` | `resources/library/books/` |
| `papers` | `/resources/library/papers/<slug>` | `resources/library/papers/` |
| `publishers` | `/resources/library/publishers/<slug>` | `resources/library/publishers/` |
| `publications` | `/resources/library/publications/<slug>` | `resources/library/publications/` |
| `observations` | `/research/observations/<slug>` | `research/observations/` |
| `insights` | `/research/insights/<slug>` | `research/insights/` |
| `hypotheses` | `/research/hypotheses/<slug>` | `research/hypotheses/` |
| `blog` | `/blog/<slug>` *(flat URL)* | `blog/<year>/<month>/<slug>.md` |
| `people` | `/people/<slug>` | `people/` |
| `organizations` | `/organizations/<slug>` | `organizations/` |
| `tags` | `/tags/<slug>` | `tags/` |
| `conventions` (docs) | `/docs/conventions/<slug>` | `docs/conventions/` |
| `schemas` (docs) | `/docs/schemas/<slug>` | `docs/schemas/` |
| `contributing` (docs) | `/docs/contributing/<slug>` | `docs/contributing/` |

Future library entities (`podcasts`, `podcast-episodes`, `articles`, `videos`, `courses`, `posts`) and report types (`lightpapers`, `whitepapers`, `position-papers`, `model-papers`) get their own templates and folders when first content lands.

## Singletons

- `thinking/manifesto.md` → `/thinking/manifesto`
- `CONTRIBUTING.md` → `/contributing`

Both use the `plain-page` template.

## Templates

The active set lives at `templates/`; superseded versions sit in `templates/_archive/`. See [`docs/conventions/templates-and-versioning.md`](./docs/conventions/templates-and-versioning.md) for the convention.

## Content workflow

1. Pick the template that matches what you're writing — see [`docs/conventions/taxonomy.md`](./docs/conventions/taxonomy.md).
2. Copy the latest `templates/template-<entity>-v<X.Y.Z>.md` to the right folder under its real slug.
3. Fill in the frontmatter (`template`, `template_version`, `collection`, plus per-template fields) and the body.
4. For drafts, set `status: active, stage: draft` — the website renders a WIP banner.
5. Open a PR.

See [`CONTRIBUTING.md`](./CONTRIBUTING.md) for the full PR-based contribution flow.

## Wikilinks

Link concepts (glossary anchors) **bare**; link everything else with **qualified paths**:

```markdown
The [[coordination]] concept by [[people/jane-doe|Jane Doe]],
introduced in [[resources/library/papers/smith-network-coordination-2022|Smith (2022)]], shows
how [[network-effects|network effects]] can drive open systems.
```

In frontmatter arrays, use bare slugs — the collection is implicit from the field name:

```yaml
sources: [smith-network-coordination-2022]
authors: [jane-doe]
tags: [antirival-goods, network-effects, sharing-economy]
```

See [`docs/conventions/wikilinks.md`](./docs/conventions/wikilinks.md) for the full convention.

## Current content

**Curated:**

- **1 person (co-goods-team):** Pontus Karlsson (project lead)
- **7 tags:** antirival, network-effects, sharing-economy, commons, goods-theory, nonrival, co-goods

**Example content** (`example: true`; placeholder data used to exercise the website's templates, filtered from production renders, easy to remove in bulk):

- **1 book** (serial `x-00002`), **1 paper** (serial `x-00001`), **1 publisher**, **1 publication**
- **1 person** (external author placeholder)
- **2 observations**, **1 insight**, **1 hypothesis** (exercises the epistemic chain)
- **1 wiki article**, **1 essay**, **1 blog post**, **1 glossary item**, **1 tag** (coordination)

The first curated book / paper / podcast / etc. lands with serial `l-00001`.

## License

© 2025–2026 DePalma Workwear Limited. This work is licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/). See [`LICENSE`](./LICENSE).

Contributions are accepted under the same license (inbound = outbound). See [`CONTRIBUTING.md`](./CONTRIBUTING.md).
