---
template: standard
template_version: 1.0.0
collection: standards
slug: spdx
serial: l-00001
title: SPDX (Software Package Data Exchange)
steward: Linux Foundation
version: 2.2.1 (ISO/IEC 5962:2021)
year: 2021
url: https://spdx.org/licenses/
work_license: Community-Spec-1.0
summary: An open standard for communicating software and content licensing via short, machine-readable identifiers (e.g. `MIT`, `CC-BY-SA-4.0`).
relevance_to_project: SPDX identifiers are the vocabulary behind the per-item and library license fields across the content repo, and the source for the inline license reference.
key_points:
  - A standard for communicating software and content licensing, maintained by the Linux Foundation under the Community Specification License 1.0 (pre-existing portions under CC-BY-3.0).
  - Standardised as ISO/IEC 5962:2021 (based on SPDX 2.2.1) — note that ISO's own publication is copyrighted by ISO; the openly-licensed version is the one the Linux Foundation publishes.
  - The SPDX License List — the identifier data we actually use — is published separately under CC0-1.0, so the identifiers are free to reference and build on.
is-cited: false
is-featured: true
status: active
added-by: pontus-karlsson
added: 2026-06-03
created: 2026-06-03
updated: 2026-06-03
tags:
  - licensing
  - standards
---

# SPDX (Software Package Data Exchange)

## Overview

SPDX is an open standard for communicating the licensing of software and content
using short, unambiguous identifiers — for example `MIT`, `Apache-2.0`, or
`CC-BY-SA-4.0`. The identifier list is maintained by the Linux Foundation and
published at <https://spdx.org/licenses/>. The specification has also been
standardised as ISO/IEC 5962:2021 (based on SPDX 2.2.1); that ISO publication is
copyrighted by ISO, whereas the openly-licensed specification is the one the
Linux Foundation publishes.

We catalogue and link to SPDX — we don't host it. The canonical identifier list
always lives upstream.

## Our take

SPDX is the vocabulary the whole content repo leans on. Every per-item
`license:` field, every library `work_license:`, and the inline
`[[license:<id>]]` reference all use SPDX identifiers, so a single change to an
upstream identifier flows through cleanly. Using an existing, machine-readable
standard — rather than inventing license labels of our own — keeps our content
interoperable with the wider open-source and open-content ecosystems.

## Notes

SPDX has two licensing layers worth keeping straight. The **specification** is
provided under the Community Specification License 1.0 (with pre-existing
portions under CC-BY-3.0) — that's the `work_license` recorded above. The **SPDX
License List data** (the identifiers themselves) is published separately under
CC0-1.0, which is why we're free to map identifiers to labels and links in the
website's renderer without further permission.

## Related

- Glossary: [[resources/glossary/spdx|SPDX]]
- Convention: [[docs/conventions/licensing|Licensing]]
