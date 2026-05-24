---
title: RSS to WebDAV with .rss marker files
description: Turn RSS feeds into browseable WebDAV resources with Zwind's RSS Projection Resolver.
seoTitle: "RSS to WebDAV with Zwind RSS Projection Resolver"
keywords:
  - RSS to WebDAV
  - RSS projection
  - WebDAV RSS reader
  - .rss marker file
productSlug: webdav-server
section: Guides
order: 30
tags:
  - rss
  - projection
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## What RSS Projection does

RSS Projection turns a feed URL into a WebDAV-style folder. Instead of opening a separate feed reader, you create a `.rss` marker file and let Zwind expose feed items as browseable resources.

## When it helps

Use it for podcast-like feeds, video feeds, newsletters with media attachments, or any feed you want to browse from a file or media client.

## Basic setup

1. Create a text file ending in `.rss`.
2. Put the feed URL inside the file.
3. Place it under a Zwind server that has the RSS resolver enabled.
4. Browse the marker file path as a projected folder.

The resolver output depends on the feed contents. Attachments, links, titles, and dates are reflected as resources where possible.
