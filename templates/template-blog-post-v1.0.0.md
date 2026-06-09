---
template: blog-post
template_version: 1.0.0
collection: blog
slug: ""
title: ""
authors: []
publishedAt: ""
tags: []
summary: ""
coverImage: ""
status: active
stage: published
created: "{{date}}"
updated: "{{date}}"
---

# {{title}}

{{summary}}

## ...post body...

<!--
Blog post schema (template: blog-post, v1.0.0).

- File location: `blog/<year>/<month>/<slug>.md`
  Year/month folders are for human file-tree navigation. URLs are flat at
  `/blog/<slug>` (the year/month folders don't appear in the URL).
- Time-stamped narrative. Not rewritten in place — new posts supersede old
  framings but the old posts stay as-is (citation accuracy).
- `publishedAt`: ISO date `YYYY-MM-DD`.
- `coverImage`: relative path to an image in the same folder, or an external URL.
- `authors`: bare people slugs.
- Posts default to `stage: published` (they're time-stamped narrative — drafts
  are rare).
-->
