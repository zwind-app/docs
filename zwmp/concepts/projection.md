---
title: Projection
description: How ZWMP turns messy web listings into filesystem-shaped media resources.
seoTitle: "Web Media Projection concept in ZWMP"
keywords:
  - Web Media Projection
  - web listing projection
  - WebDAV-style resources
  - media resource tree
productSlug: zwmp
section: Concepts
parent: concepts
order: 20
tags:
  - projection
  - web-listing
  - resources
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## The shape

Projection starts with a web listing page. The page may contain links, titles, dates, media names, or fragments that are easy for a person to scan but not structured enough for a media client.

ZWMP interprets that page and projects the useful parts into a WebDAV-style resource tree.

## Three steps

1. Read a listing page.
2. Resolve media links and metadata.
3. Expose a resource tree that clients can browse.

## Relationship to Zwind

Zwind Resource Projection is the broader product concept. ZWMP is one toolkit-shaped path for web listings specifically.

## What projection should preserve

Projection should preserve stable facts from the page: title, item URL, thumbnail, media URL, and useful grouping. It should avoid inventing metadata that cannot be derived from the source.

## Why .wm rules exist

Different websites have different HTML shapes. A `.wm` rule keeps that site-specific knowledge in a small, inspectable file so the runtime can stay generic.
