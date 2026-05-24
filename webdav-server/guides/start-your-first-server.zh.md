---
title: 启动第一个 server
description: 在 iPhone 或 iPad 上第一次运行 WebDAV server 的简短指南。
seoTitle: 如何在 iPhone 上启动 WebDAV Server - Zwind 指南
keywords:
  - iPhone WebDAV
  - start WebDAV server
  - Zwind guide
  - 局域网文件共享
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/start-your-first-server
order: 30
tags:
  - guide
  - server
  - first-run
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## 目标

创建一个 WebDAV server，暴露一个小的来源，并从另一台设备验证。

## 步骤

1. 打开 Zwind。
2. 创建 server。
3. 选择一个本地文件夹或小型测试来源。
4. 启动 server。
5. 复制或分享 WebDAV URL。
6. 从兼容 WebDAV 的客户端打开 URL。

先使用一个小的本地文件夹。如果客户端可以列出文件并打开一个测试文件，说明 server 路径、网络和权限都已经正常。

## 加入更多来源

第一个 server 成功后，再一次加入一个高级来源：

- SMB：访问 NAS 或电脑共享。
- RSS：让 feed item 显示为资源。
- Quark Search Import：让空文件夹搜索并导入匹配资源。
- Web Media Projection：让 `.wm` 规则把网页列表变成媒体条目。

## 排查清单

- 确认两台设备在同一网络中可互相访问。
- 确认选中的来源在设备上可用。
- 如果启用了 server lock，确认客户端使用了正确凭据。
- 如果某个电视端或播放器显示空目录，换一个 WebDAV 客户端交叉验证。
