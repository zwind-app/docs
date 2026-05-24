---
title: Getting started with ZWMP
description: Learn how ZWMP .wm rules turn web media listings into projected resources.
seoTitle: "Getting started with ZWMP .wm rules"
keywords:
  - ZWMP
  - .wm rule
  - web media projection
  - WebDAV resource projection
productSlug: zwmp
section: Start
order: 1
tags:
  - zwmp
  - projection
  - toolkit
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## What ZWMP is

ZWMP is an open-source toolkit for turning a web listing page into projected WebDAV-style media resources. The practical artifact is a `.wm` rule: a small text file that explains where the listing lives, how to find items, how to follow detail pages, and what kind of media should be extracted.

It is for developers and advanced users who want ordinary web pages, media links, and resource trees to meet in the middle.

## Start here

1. Read the projection concept.
2. Identify a web listing page shape.
3. Decide which links and metadata should become item resources.
4. Generate or write a `.wm` rule.
5. Run debug output until item URLs and media URLs match what you expect.
6. Import the rule into Zwind WebDAV or another compatible resolver.

## What a good rule captures

A good rule captures stable CSS selectors, the intended media type, whether the site needs browser-like JavaScript execution, and whether intermediate pages should be expanded into child items.

## Where ZWMP fits

Zwind WebDAV uses this idea to expose web media pages as folders and files. ZWMP keeps the site-specific logic in an inspectable rule instead of embedding one-off parsers in application code.
