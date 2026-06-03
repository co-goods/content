---
template: plain-page
template_version: 1.0.0
title: "Contributing to Co-Goods Research"
status: active
stage: published
---

# Contributing to Co-Goods Research

Welcome! Co-Goods is an open-innovation research project. Anyone is welcome to contribute — drafts, refinements, citations, new wiki articles, essays, glossary items, library entries, fixes.

This document covers *how* to contribute. For the *what* — collections, items, templates — see [`docs/conventions/taxonomy.md`](./docs/conventions/taxonomy.md) and the `templates/` directory.

## Quick start

1. **Fork** this repository on GitHub.
2. **Create a branch** for your change (`feature/add-wiki-antirival`, `docs/fix-typo`, etc.).
3. **Pick the right template** from `templates/` — copy the latest `template-<entity>-v<X.Y.Z>.md` to the target folder under your slug.
4. **Fill in the frontmatter** (`template`, `template_version`, `collection`, plus per-template fields) and the body.
5. For new or in-progress content, set frontmatter `status: active, stage: draft`. The website renders it with a "Draft — work in progress" banner.
6. **Open a pull request** to `main`. Describe your change briefly and link any relevant Discord discussion.
7. The Co-Goods core team reviews. When ready, the maintainer flips `stage: draft` → `stage: published` and merges.

## Where things go

| Content | Folder | Template |
|---|---|---|
| Essay (POV) | `thinking/essays/<slug>.md` | `template-essay-v1.0.0.md` |
| Wiki article (neutral encyclopedic) | `resources/wiki/<slug>.md` | `template-wiki-article-v1.0.0.md` |
| Glossary item | `resources/glossary/<slug>.md` | `template-glossary-item-v1.0.0.md` |
| Book | `resources/library/books/<slug>.md` | `template-book-v1.0.0.md` |
| Paper | `resources/library/papers/<slug>.md` | `template-paper-v1.0.0.md` |
| Publisher | `resources/library/publishers/<slug>.md` | `template-publisher-v1.0.0.md` |
| Publication (journal, podcast channel, …) | `resources/library/publications/<slug>.md` | `template-publication-v1.0.0.md` |
| Observation | `research/observations/<slug>.md` | `template-observation-v1.0.0.md` |
| Insight | `research/insights/<slug>.md` | `template-insight-v1.0.0.md` |
| Hypothesis | `research/hypotheses/<slug>.md` | `template-hypothesis-v1.0.0.md` |
| Blog post | `blog/<year>/<month>/<slug>.md` | `template-blog-post-v1.0.0.md` |
| Person profile | `people/<slug>.md` | `template-person-v1.0.0.md` |
| Tag | `tags/<slug>.md` | `template-tag-v1.0.0.md` |
| Doc article | `docs/<collection>/<slug>.md` (or `docs/<collection>/<sub-collection>/<slug>.md`) | `template-doc-v1.0.0.md` |

For books and papers, the maintainer assigns the next `l-#####` serial on merge and updates `resources/library/INDEX.md`. Example content (placeholder, `example: true`) uses the `x-#####` namespace instead.

Future library entities (`podcast`, `podcast-episode`, `article`, `video`, `course`, `post`) and report types (`lightpaper`, `whitepaper`, `position-paper`, `model-paper`) get their own templates when the first content lands.

See [`docs/conventions/taxonomy.md`](./docs/conventions/taxonomy.md) for the full model and [`docs/conventions/file-naming.md`](./docs/conventions/file-naming.md) for slug conventions per collection.

## Frontmatter

Every content file starts with a YAML frontmatter block. The universal contract is:

```yaml
template: <entity name>           # singular: essay, book, paper, doc, tag, person, …
template_version: 1.0.0
collection: <collection name>     # plural: essays, books, papers, conventions/naming, …
title: "..."
```

Each template's `<!-- schema notes -->` block documents its per-template fields. See [`docs/conventions/frontmatter.md`](./docs/conventions/frontmatter.md) for the universal contract and common patterns.

## Wikilinks

Use qualified-path Obsidian-style wikilinks in body markdown:

```markdown
The [[tags/coordination]] concept by [[people/jane-doe|Jane Doe]],
introduced in [[resources/library/papers/smith-network-coordination-2022|Smith (2022)]], shows how
[[tags/network-effects|network effects]] can drive open systems.
```

Bare wikilinks (no slash) default to `/topics/<slug>` if a topic-aggregation page exists; otherwise they cause a build error. When in doubt, qualify.

In frontmatter arrays, use bare slugs — the collection is implicit from the field name:

```yaml
sources: [smith-network-coordination-2022]
authors: [jane-doe]
tags: [antirival, network-effects, sharing-economy]
```

See [`docs/conventions/wikilinks.md`](./docs/conventions/wikilinks.md).

## Assets (images and files)

Content media — diagrams, figures, charts, book covers — lives in an `assets/` folder next to the item that uses it, referenced with a local-style path (`./assets/<name>`). Add images and video to a page with the `image` and `video` blocks. For the full picture — where assets live, the blocks, and embeds vs self-hosted video — see [`docs/conventions/media.md`](./docs/conventions/media.md).

- **Small images or files** — include them in your PR. Drop into the item's `assets/` folder (or attach in the PR description and the maintainer will place them at merge).
- **Larger or many files** — include a download link in the PR description (any share that works for you). The maintainer downloads and places at merge.

Media you didn't create must carry attribution — set `credit` and `license` on the block — and the license must permit the use. See the licensing section below.

## Discussion

- **Discord** — community discussion and async chat: [Discord — link TBD]
- **PR comments** — issue-specific discussion lives in the PR itself.

For substantial changes (new templates, new collections, structural changes), please open a Discord thread first — these touch the conventions docs and benefit from broader alignment.

## Review process

A Co-Goods core-team maintainer reviews each PR. Typical timeline:

1. Acknowledgement within a few days.
2. Comments / requests for changes if needed.
3. Merge once aligned.
4. The maintainer may flip `stage: draft` → `stage: published` at merge time if the content is mature, or leave it as a draft for further iteration.

## Licensing

**Your contribution's license (outbound).** Original first-party prose you author — wiki, essays, glossary, research — is licensed **CC-BY-SA-4.0** (see [`LICENSE`](./LICENSE)); it applies without you declaring it per file. Essays may carry a per-item override (below).

**What we can accept (inbound).** Contributions must be **CC-BY-SA-4.0 or a more-permissive, compatible** license (`CC-BY-4.0`, `CC0-1.0`). We can't accept NonCommercial (NC) or NoDerivatives (ND) terms — they can't flow into a share-alike commons.

**Overriding per item.** An item can set its own `license:` in its YAML frontmatter using an **SPDX identifier** (e.g. `CC-BY-4.0`); it must still be compatible. See [`docs/conventions/frontmatter.md`](./docs/conventions/frontmatter.md).

**Things you bring with you (inherited / third-party).**

- **Media** keeps *its own* license — set `credit` and `license` on the `image` / `video` block, and the terms must permit the use. See [`docs/conventions/media.md`](./docs/conventions/media.md).
- **Library entries** have three layers: the *described work* (its own license, untouched), the *catalogue record* (factual), and your *summary / commentary* (CC-BY-SA). Citing or quoting is fair-use citation, not relicensing — never relicense someone else's work.
- **Quotes and figures** from elsewhere must be compatible (public domain, CC-compatible, or fair-use citation). When in doubt, ask in the PR.

**Multiple authors.** Credit everyone involved in the item's YAML frontmatter. Ideas developed collaboratively — in discussions, working sessions, events, on Discord, or anywhere else — are fine to synthesize and credit. If you reuse someone's substantial **wording** (not just their idea), they must also be a covered contributor.

## Contributor License Agreement

Contributing requires agreeing to our **Contributor License Agreement** (current: [`cla-v1`](https://github.com/co-goods/.github/blob/main/cla/cla-v1.md)). You keep your copyright; you grant a broad, sublicensable, assignable license so the work can stay open and, if needed, move to a future neutral entity. It's deliberately broad while we're small — we expect to relax it in a later version; if a term is a dealbreaker, please reach out, it's a matter of priorities, not principle.

**Signing:** add your name and the CLA version to [`CLA-SIGNATURES.md`](https://github.com/co-goods/.github/blob/main/CLA-SIGNATURES.md) in your pull request. (We'll automate this with cla-assistant as we grow.)

## Developer Certificate of Origin

Some projects use a [DCO](https://developercertificate.org) sign-off (`git commit -s`). We rely on the CLA above, which already covers provenance, so **no sign-off is required here** — we mention it only because you may recognize it from other projects.

---

Thanks for contributing!
