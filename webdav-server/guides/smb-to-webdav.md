---
title: SMB to WebDAV on iPhone
description: Use Zwind to browse SMB shares and expose selected network folders through a WebDAV-style server.
seoTitle: "SMB to WebDAV on iPhone with Zwind"
keywords:
  - SMB to WebDAV
  - iPhone SMB WebDAV
  - NAS WebDAV iPhone
  - Zwind SMB
productSlug: webdav-server
section: Guides
order: 20
tags:
  - smb
  - webdav
  - nas
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## Why bridge SMB to WebDAV

Many NAS devices and desktop shares speak SMB, while many media players and file tools are easier to configure with WebDAV. Zwind can sit in the middle: connect to an SMB share from the app, then expose the selected source through a WebDAV-style server entry.

## Typical workflow

1. Add or open the SMB source in Zwind.
2. Create a WebDAV server entry for the files you want to expose.
3. Start the server on the local network.
4. Point a WebDAV client, TV app, or desktop browser at the generated URL.

## Practical notes

Keep the iPhone and the client on the same network. If a media player cannot browse SMB directly but supports WebDAV, this workflow can make NAS folders available without changing the NAS configuration.
