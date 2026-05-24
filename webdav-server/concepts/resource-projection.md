---
title: Resource Projection
description: A concise concept page for how external resources can appear inside a Zwind-style directory tree.
seoTitle: "Resource Projection in Zwind WebDAV"
keywords:
  - Resource Projection
  - WebDAV resolver
  - RSS to WebDAV
  - Quark Search Import
  - Web Media Projection
productSlug: webdav-server
section: Concepts
parent: concepts
order: 20
tags:
  - projection
  - resolver
  - resources
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## Concept

Resource Projection is the idea that something outside a normal folder can appear inside a browseable resource tree.

That external thing might be a feed, a search result, a cloud-style source, or a web listing. A resolver interprets the source and presents it as file-like or folder-like entries.

## Why it matters

Media rarely lives in one clean directory. Projection gives scattered resources a shape that WebDAV-style browsers, players, and import flows can understand.

## Resolver ecosystem

Current Zwind-facing concepts include:

- RSS Projection Resolver
- Quark Search Import Resolver
- Web Media Projection Resolver

## Marker files and intent folders

Some resolvers start from marker files such as `.rss` or `.wm`. Others start from folders that express intent, such as a Quark search/import folder. The resolver reads that marker or folder, generates virtual children, and lets the WebDAV layer present them as normal resources.

## Why lazy loading matters

Resolvers may need network requests, browser-like parsing, or cloud API calls. Zwind therefore keeps projection lazy where possible: browsing a parent folder should be cheap, and expensive detail parsing should happen only when the user enters the relevant projected item or opens media.
