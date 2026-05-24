---
title: 在 iPhone 上把 SMB 转成 WebDAV
description: 使用 Zwind 浏览 SMB 共享，并把选中的网络文件夹通过 WebDAV 风格 server 暴露出去。
seoTitle: "用 Zwind 在 iPhone 上实现 SMB to WebDAV"
keywords:
  - SMB to WebDAV
  - iPhone SMB WebDAV
  - NAS WebDAV
  - Zwind SMB
productSlug: webdav-server
section: 指南
locale: zh
translationOf: webdav-server/guides/smb-to-webdav
order: 20
tags:
  - smb
  - webdav
  - nas
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## 为什么要把 SMB 桥接成 WebDAV

很多 NAS 和桌面共享使用 SMB，但不少媒体播放器和文件工具更容易配置 WebDAV。Zwind 可以作为中间层：在 App 内连接 SMB 共享，再把选中的来源通过 WebDAV 风格 server 暴露出去。

## 常见流程

1. 在 Zwind 中添加或打开 SMB 来源。
2. 为要暴露的文件创建 WebDAV server。
3. 在局域网中启动 server。
4. 从 WebDAV 客户端、电视端 App 或桌面浏览器打开生成的 URL。

## 使用建议

确保 iPhone 和客户端在同一网络。如果播放器不能直接浏览 SMB，但支持 WebDAV，这个工作流可以在不改变 NAS 配置的情况下访问 NAS 内容。
