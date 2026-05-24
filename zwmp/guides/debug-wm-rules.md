---
title: Debugging .wm rules
description: Use ZWMP debug output to understand why a web media site does not resolve correctly.
seoTitle: "Debug .wm rules for Web Media Projection"
keywords:
  - debug .wm rule
  - web media resolver debug
  - ZWMP debug
  - media URL extraction
productSlug: zwmp
section: Guides
order: 30
tags:
  - debug
  - wm-rule
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## Read the output in order

Start with source loading. If the source page fails, selectors do not matter yet. Then check candidate count, candidate links, intermediate detail pages, and finally media discovery.

## Common failures

- Candidate selector matches navigation links instead of item cards.
- Candidate link selector is missing, so the resolver uses the wrong anchor.
- `detail_url_mode=expand` is missing when a detail page contains multiple episodes.
- `media_type` is too broad and images stop a video workflow too early.
- The page needs browser-like JavaScript execution, but `fast_mode=true` is enabled.

## Rule tuning loop

Change one field at a time. Re-run debug. Stop when item URLs and media URLs match what a human sees on the page.
