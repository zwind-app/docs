---
title: Quark Search Import Resolver
description: Use Zwind to search Quark shares, import resources, check updates, and expose cleaner media-library names.
seoTitle: "Quark Search Import Resolver for Zwind WebDAV"
keywords:
  - Quark search import
  - Quark WebDAV
  - Quark media library
  - Zwind resolver
productSlug: webdav-server
section: Guides
order: 40
tags:
  - quark
  - resolver
  - media-library
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## What it is

The Quark Search Import Resolver treats an empty folder as an import intent. The folder name becomes the search query, Zwind inspects candidate shares, imports matching resources, and can keep checking imported resources for later updates.

## Import modes

Zwind can keep original resource names, generate a virtual library view with cleaner names, or organize imported resources more directly for media clients. This is useful when original share names are hard for third-party players to scrape.

## Update checks

When the server starts, Zwind can queue update checks for imported resources. If a source share gains new files, the resolver can import only the newly discovered content and notify the user through the app workflow.

## Best practices

Use a clear folder name for the search intent. For shows, include the title and year when useful. If a source is stale or invalid, remove the imported folder and create a new intent folder to start over cleanly.
