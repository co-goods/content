---
template: person
template_version: 1.0.0
collection: people
slug: ""
name: ""
affiliation: ""
institution: ""
bio: ""
expertise: []
email: ""
website: ""
github: ""
orcid: ""
aliases: []
key_publications: []
tags: []
sources_by_author: []
status: active
relevance: ""
created: "{{date}}"
updated: "{{date}}"
---

# {{name}}

## Bio
Brief biography and background.

## Relevance to Co-Goods
How this person's work relates to the co-goods project.

## Notes
Additional notes.

<!--
Person schema (template: person, v1.0.0).

Required:
- File location: `people/<slug>.md` (flat)
- `slug`: `firstname-lastname` (e.g. `f-xavier-olleros`, `pontus-karlsson`)
- `name`: display name
- `affiliation`: enum — `co-goods-team | depalma-pilot | external-author | unclaimed`
- `bio`: brief biography

Optional (add when relevant):
- `institution`: free-text employer / academic institution
- `expertise`, `aliases`, `key_publications`, `tags`, `sources_by_author[]`
- `account-status`: for the future Clerk/Supabase "claim profile" integration
- `relevance_to_project`

Person profiles aggregate the ways someone shows up across the repo. Roles
(`authors:`, `contributors:`, `editors:`, `designers:`, `reviewers:`) are
expressed on the content that references the person, not on the profile itself.
-->
