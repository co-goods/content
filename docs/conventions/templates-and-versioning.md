---
template: doc
template_version: 1.0.0
collection: conventions
slug: templates-and-versioning
title: "Templates and versioning"
description: "Why templates are versioned, how to bump, and where the renderer fits."
order: 30
status: active
stage: draft
---

# Templates and versioning

Templates are **authoring scaffolds** — starting points contributors copy when creating a new item. Each template describes the schema (frontmatter fields) and structure (body conventions) for one kind of file.

Templates are versioned with semver so schemas can evolve while existing content keeps working.

## Where templates live

```
templates/
  template-essay-v1.0.0.md           ← currently latest
  template-book-v1.0.0.md
  template-wiki-article-v1.0.0.md
  …
  _archive/
    template-essay-v0.9.0.md         ← superseded versions live here
```

- **Latest version per entity** lives at `templates/template-<entity>-v<version>.md`. Filenames carry the version explicitly so the latest is obvious at a glance.
- **Superseded versions** move to `templates/_archive/` (kept for reference and migration scans).
- **One template per entity**, with a **singular** name (`book`, not `books`; `essay`, not `essays`; `glossary-item`, not `glossary`). Folder + URL + collection names stay plural; the template name describes one item.

## Frontmatter on a template file

Each template declares its own identity at the top of its frontmatter:

```yaml
---
template: essay
template_version: 1.0.0
slug: ""
title: ""
# …the rest of the schema fields the template defines
---

# {{title}}

…example body…

<!--
Essay schema (template: essay, v1.0.0)

- File location: thinking/essays/<slug>.md
- Frontmatter required: title, authors, summary, tags, …
- Voice: POV writing by an identified contributor.
- See related templates / docs as needed.
-->
```

The schema-notes comment block documents the template's contract — required and optional fields, file location, voice/role notes. This is what an author reads to understand the template.

## Semver scope

When a template's schema changes, bump the version according to the change scope:

| Bump | Reason | Examples |
|---|---|---|
| **Major** (X+1.0.0) | Breaking — content authored against previous versions will not render correctly without migration | Renaming a required field; removing a field; changing a field's type |
| **Minor** (1.X+1.0) | Additive — content on previous versions still works as-is | Adding an optional field; loosening a constraint |
| **Patch** (1.0.X+1) | Cosmetic — no schema change | Help-text edits; example body updates; comment clarifications |

## Content items back-reference the template

Each authored item declares which template + version it was authored against:

```yaml
---
template: essay
template_version: 1.0.0
collection: essays
title: "On Collaboration"
# …other essay fields
---

Body content.
```

The version back-reference enables migration scans — finding files still on a specific template version when planning to deprecate it.

## Bump workflow

When you need to evolve a template:

1. **Decide the bump scope** — major, minor, or patch (above).
2. **Move the current latest to `_archive/`:**
   ```bash
   git mv templates/template-essay-v1.0.0.md templates/_archive/
   ```
3. **Author the new latest:** `templates/template-essay-v1.1.0.md` (or v2.0.0 for major), updating the schema-notes block.
4. **Update the renderer** to recognise and dispatch on the new version (if the bump requires it — patches usually don't).
5. **For major bumps**, plan the migration of existing content (see "Migration scans" below).

Authors creating new content after the bump pick up the new template automatically; existing content stays on its declared version until migrated.

## Migration scans

To find content authored against a specific template version (e.g., when planning to deprecate essay v1.0.0):

```bash
# At the content repo root
grep -rln "template_version: 1.0.0" thinking/essays/

# Across all collections, filtered to one template
grep -rl "^template: essay$" . | xargs grep -l "template_version: 1.0.0"
```

Then update those files to the new version (renaming fields, adding required fields, etc.) before removing v1.0.0 support from the renderer.

## What the website does with versions

The templates folder is for **authoring** — humans (or agents) copy a starting point and fill in their content. **It's not consulted at render time.**

The website's renderer holds schema knowledge in code, dispatching on `template_version:` when multiple versions are supported. If a content file declares a version the renderer no longer supports, the build fails with a clear "update this file to v<latest>" message.

This separation means:

- The templates folder can evolve freely; existing content doesn't break because of folder rearrangements.
- The renderer is the source of truth for which versions are currently supported.
- Authors don't need to think about runtime — they just pick the latest template and fill it in.

## Cross-cutting templates

Three templates apply across the surface, not to a single collection:

- **`composed-page`** — section-composed pages (home, about, custom collection pages). Lives in `website/pages/<url-path>.md` in the website repo.
- **`overlay`** — splice fragments that layer site-specific framing onto a source page. Lives in `website/overlays/<source-folder>/<slug>.md` in the website repo.
- **`plain-page`** — plain-markdown standalones with minimal frontmatter (manifesto, contributing).

All three are versioned the same way (`template-composed-page-v1.0.0.md`, etc.), with the same archive workflow.

## Related conventions

- **Taxonomy** (collections, items, sub-collections): see `taxonomy.md`.
- **Frontmatter contract** (universal + per-template fields): see `frontmatter.md`.
