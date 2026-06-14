---
template: glossary-item
template_version: 1.2.0
collection: glossary
slug: git
title: Git
type: word
tag: true
classes:
  - type: noun
    definitions:
      - A distributed version-control system that tracks changes to files and lets many people work on them in parallel, with every clone holding the full history. Created by Linus Torvalds in 2005, it is the substrate beneath collaboration platforms such as GitHub and GitLab.
relationships:
  related_terms:
    - participation
    - governance
status: active
stage: draft
created: 2026-06-14
updated: 2026-06-14
---

# Git

**Git** records the history of a set of files as a chain of commits, lets people branch off to work independently, and merges that work back together. Because every clone is a complete copy, contributors can work offline and in parallel and reconcile afterwards. Hosting platforms — **GitHub**, GitLab, and others — add a shared home, reviews, and the pull-request flow on top of git itself.

Co-Goods runs on this model. The content and the website both live in git, and contributions arrive as proposed changes (forks and pull requests) that can be reviewed in the open before they are merged. That makes the version-control system also a *governance* and *participation* mechanism: a transparent, forkable record that anyone can build on — a good fit for open research and innovation.
