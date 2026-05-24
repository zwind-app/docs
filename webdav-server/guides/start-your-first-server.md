---
title: Start your first server
description: A short guide for the first WebDAV server run on iPhone or iPad.
seoTitle: "Start your first iPhone WebDAV server"
keywords:
  - start WebDAV server iPhone
  - iOS WebDAV server
  - Zwind setup
  - WebDAV URL
productSlug: webdav-server
section: Guides
parent: guides
order: 30
tags:
  - guide
  - server
  - first-run
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## Goal

Create one WebDAV server, expose a small source, and verify it from another device.

## Steps

1. Open Zwind.
2. Create a server.
3. Select one local folder or a small test source.
4. Start the server.
5. Copy or share the WebDAV URL.
6. Open the URL from a WebDAV-compatible client.

Use a small local folder first. If the client can list files and open one test file, the server path, network, and permissions are working.

## Add more sources

After the first server works, add one advanced source at a time:

- SMB when you want to browse NAS or desktop shares.
- RSS when feed items should appear as resources.
- Quark Search Import when an empty folder should search and import matching resources.
- Web Media Projection when a `.wm` rule should turn a listing page into media entries.

## Troubleshooting checklist

- Confirm both devices are reachable on the same network.
- Confirm the chosen source is available on the device.
- If server lock is enabled, confirm the client is using the expected credentials.
- Try a different WebDAV client if one TV or player app shows an empty directory.
