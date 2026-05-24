---
title: .wm rule syntax overview
description: A user-facing overview of the Web Media Projection rule format used by ZWMP and Zwind.
seoTitle: ".wm rule syntax for Web Media Projection"
keywords:
  - .wm rule
  - wm rule spec
  - web media projection syntax
  - ZWMP rules
productSlug: zwmp
section: Concepts
order: 20
tags:
  - wm-rule
  - syntax
  - projection
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## Core fields

A `.wm` rule is a plain text marker file. The most common fields are:

- `source`: listing page URL.
- `candidate_selector`: CSS selector for item cards.
- `candidate_link_selector`: link selector inside each item.
- `title_selector`: selector used to name each item.
- `thumbnail_selector`: selector used to find item artwork.
- `detail_url_selector`: optional selector for intermediate pages or episode lists.
- `detail_url_mode`: `expand` creates child items; other modes can follow detail pages.
- `projection`: `by-item` creates item folders; `flat` places media resources directly.
- `media_type`: defaults to `video`; can be widened when the site is image-first or mixed media.
- `fast_mode`: when true, prefer static HTTP parsing for sites that do not need JavaScript.

## Browser behavior

Rules can stay fast by avoiding browser execution. When a site builds the useful DOM with JavaScript, use browser-like runtime settings such as selector wait time and desktop-mode controls.

## Debug expectation

The debug command should show the same logical phases as the resolver: source load, candidate extraction, item URL extraction, detail hop expansion, and media URL discovery. If one phase is wrong, fix the rule at that phase before tuning later steps.
