---
title: Project a web listing
description: Turn a web media listing into projected resources by writing or generating a .wm rule.
seoTitle: "Project a web listing with a ZWMP .wm rule"
keywords:
  - project web listing
  - .wm rule guide
  - web media parser
  - ZWMP guide
productSlug: zwmp
section: Guides
parent: guides
order: 30
tags:
  - guide
  - adapter
  - web-listing
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## Goal

Take a page that lists media links and turn it into a browseable resource tree.

## Workflow

1. Choose a listing page.
2. Identify stable link patterns.
3. Extract media URLs and human-readable names.
4. Resolve optional metadata.
5. Expose the result as WebDAV-style resources.

## Rule fields to start with

Start with `source`, `candidate_selector`, `candidate_link_selector`, `title_selector`, and `media_type`. Add `detail_url_selector` only when the listing item points to an intermediate page that contains more links or episodes.

Use `projection=flat` when the final media resources should be directly under the current folder. Use `projection=by-item` when each card or episode should have its own directory.

## Keep projections honest

Do not invent metadata that the page does not provide. Prefer clear placeholders or omitted fields over misleading output.
