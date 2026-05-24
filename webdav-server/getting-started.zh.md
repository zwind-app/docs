---
title: Zwind WebDAV Server 入门
description: 安装 Zwind，创建第一个 iPhone WebDAV server，并从另一台设备打开 WebDAV URL。
seoTitle: "Zwind WebDAV Server 入门：把 iPhone 变成 WebDAV 文件服务器"
keywords:
  - iPhone WebDAV server
  - iPad WebDAV server
  - WebDAV 播放器
  - 局域网文件服务器
productSlug: webdav-server
section: 入门
locale: zh
translationOf: webdav-server/getting-started
order: 1
tags:
  - webdav
  - ios
  - server
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## Zwind 能做什么

Zwind WebDAV Server & Player 可以把 iPhone 或 iPad 变成个人 WebDAV server。你选择要暴露的内容，启动 server，然后从另一台浏览器、播放器、电视端客户端或兼容文件 App 打开生成的 WebDAV URL。

同一个 App 还可以浏览 WebDAV server、播放媒体、编辑文本文件、映射 SMB、投影 RSS、导入夸克资源，并通过 `.wm` 规则把网页媒体页面变成可浏览目录。

## 第一次运行

1. 从 App Store 安装 Zwind。
2. 创建一个 WebDAV server。
3. 选择本地文件夹、iOS Files 来源、SMB 共享、夸克导入、RSS marker file 或 Web Media marker file。
4. 启动 server。
5. 从同一网络中的另一台设备打开 WebDAV URL。

建议先用一个小的本地文件夹验证连通性，再逐步加入 SMB、RSS、夸克搜索导入或 Web Media Projection。

## 建议的第一个场景

创建一个名为 `Media` 的 server，选择包含几个视频的本地文件夹，然后启动 server。从桌面浏览器或媒体播放器打开 WebDAV URL。确认成功后，可以继续加入：

- NAS 或电脑上的 SMB 共享。
- 用于 RSS to WebDAV 的 `.rss` 文件。
- 用于 Web Media Projection 的 `.wm` 文件。
- 用于夸克搜索转存的空意图文件夹。

## 适合配合哪些客户端

Zwind 可以配合普通 WebDAV 客户端、桌面文件浏览器、手机 App 和支持 WebDAV 的媒体播放器使用。具体刮削和播放体验取决于客户端，但 Zwind 暴露的目录树尽量保持熟悉：文件夹、文件、URL shortcut、媒体条目和 resolver 生成的资源。

## 价格说明

Zwind 可以免费开始使用。Premium 解锁多个 servers 和高级能力。当前价格以 App Store 页面为准。
