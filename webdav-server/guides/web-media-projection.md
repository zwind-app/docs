---
title: Web Media Projection Resolver
description: Use .wm rules to turn web media listing pages into browseable WebDAV-style media resources.
seoTitle: "Web Media Projection Resolver and .wm rules for Zwind"
keywords:
  - Web Media Projection
  - .wm rule
  - web media resolver
  - web video to WebDAV
  - web image to WebDAV
productSlug: webdav-server
section: Guides
order: 50
tags:
  - web-media
  - wm-rule
  - projection
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## What a .wm rule describes

A `.wm` marker file tells Zwind how to read a website: the source page, item selector, optional detail links, title selector, thumbnail selector, media type, projection mode, and runtime settings such as browser-like parsing.

## Common projection shapes

Use `projection=by-item` when each listing card should become a folder. Use `projection=flat` when media resources should appear directly in the projected directory. Use `detail_url_mode=expand` when one item page contains multiple episode or part links.

## Debug-first workflow

When a site does not resolve, run the generator debug command. The debug output should answer:

- Which source page was loaded.
- Which candidate items matched.
- Which item URLs were extracted.
- Whether intermediate detail pages were expanded.
- Which media URLs were found.

This is the fastest way to tell whether the rule needs a selector change, a browser runtime, a longer selector wait, or a different media type.
