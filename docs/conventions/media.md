---
template: doc
template_version: 1.0.0
collection: conventions
slug: media
title: "Images and video"
description: "How to add images and video, where assets live, and how attribution and licensing work."
order: 70
status: active
stage: draft
created: 2026-05-28
updated: 2026-05-28
---

# Images and video

How to add images and video to pages, where the files live, and how attribution and licensing work.

Media is added through two **sections** — `image` and `video` — authored as fenced sections, the same way as every other section (see the section syntax in the website's authoring notes). Both carry optional attribution so a credit and license line can sit under the media.

## The image section

```image
src: ./assets/coordination-diagram.svg
alt: A diagram of asynchronous coordination across participants
caption: How coordination density rises with asynchronous participation.
credit: Jane Doe
creditUrl: https://example.com/jane
license: CC BY-SA 4.0
licenseUrl: https://creativecommons.org/licenses/by-sa/4.0/
sourceUrl: https://example.com/original
aspectRatio: "16 / 9"
```

- `src` (required) — the image path. See **Where assets live** below.
- `alt` (required) — describe the image for screen readers; use `alt: ""` for purely decorative images.
- `caption` — visible caption under the image.
- `aspectRatio` — e.g. `"16 / 9"`, `"4 / 3"`. Optional; reserves space so the layout doesn't jump while the image loads.
- `width` / `height` — pixel dimensions when known; helps the renderer size the image.
- Attribution fields — `credit`, `creditUrl`, `license`, `licenseUrl`, `sourceUrl`. See **Attribution and licensing**.

## The video section

Two ways to add video: **embed** a hosted video (YouTube or Vimeo), or **self-host** a short MP4. Embeds are the default — prefer them for anything substantial.

Embed:

```video
provider: youtube
videoId: dQw4w9WgXcQ
title: How co-goods work — a primer
caption: A short introduction to the core idea.
```

```video
provider: vimeo
videoId: "76979871"
title: Field notes
```

Self-hosted MP4:

```video
provider: file
src: ./assets/loop.mp4
poster: ./assets/loop-poster.jpg
caption: A short loop.
```

- `provider` (required) — `youtube`, `vimeo`, or `file`.
- `videoId` — the platform's video id (embeds only). It's `videoId`, not `id`, because `id` is reserved for in-page section anchors.
- `src` — the MP4 path (`provider: file` only).
- `poster` — a still shown before a self-hosted video plays.
- `title` — used as the embed's accessible title.
- `caption`, `aspectRatio`, and the attribution fields work as on the image section.

**On self-hosting:** a `provider: file` video is served from the site's own bandwidth, which has a cost. Keep self-hosted clips short; for anything longer, upload to YouTube or Vimeo and embed it.

## Where assets live

Media files live in one of two places, depending on whether they're **content** or **presentation**:

- **Content media** — diagrams, figures, charts, book covers: media that is *part of the content* and would travel with it to another surface (print, syndication, a different site). These live in the **content repo**, in an `assets/` folder next to the item, referenced with a local-style path:

  ```
  resources/wiki/network-coordination.md
  resources/wiki/assets/coordination-diagram.svg   →  src: ./assets/coordination-diagram.svg
  ```

- **Presentation media** — hero backgrounds, decorative site imagery: choices specific to *this website*. These live in the **website repo** under `public/`, referenced by absolute path:

  ```
  public/hero/home-bg.jpg   →  src: /hero/home-bg.jpg
  ```

The test: **would another surface want this image?** If yes, it's content — put it in the content repo's `assets/`. If it's a framing choice for this site, it's presentation — put it in the website's `public/`. See `file-naming` for asset slug rules, and the taxonomy doc for why content stays portable.

## Attribution and licensing

Every media section can carry an attribution line:

- `credit` / `creditUrl` — who made it (and a link).
- `license` / `licenseUrl` — the media's license (and a link to the license text).
- `sourceUrl` — where the original lives.

**A media item's license is independent of the text around it.** An embedded YouTube video carries YouTube's terms; a photo carries whatever license its creator set (CC BY, public domain, all-rights-reserved). This is separate from the site's default content license — declare the media's own license whenever it isn't plainly your own original work.

This matters most for media you didn't create. If you're embedding or reusing someone else's image or video, set `credit` and `license` so the attribution shows, and make sure the terms allow the use. When in doubt, ask in the PR or on Discord.

For the site-wide licensing model — the default and how to override it per item — see the licensing notes in `CONTRIBUTING.md`.

## Related conventions

- **File naming and slugs** (asset slug rules, `assets/` folders): see `file-naming`.
- **Frontmatter contract** (the per-item `license:` override): see `frontmatter`.
- **Taxonomy** (why content stays portable): see `taxonomy`.
