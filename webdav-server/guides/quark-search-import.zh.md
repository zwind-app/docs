---
title: 夸克资源自动转存解析器
description: 使用 Zwind 搜索夸克分享、导入资源、检查更新，并暴露更干净的媒体库命名。
seoTitle: "Zwind 夸克资源自动转存解析器"
keywords:
  - 夸克资源自动转存
  - 夸克 WebDAV
  - 夸克媒体库
  - Zwind resolver
productSlug: webdav-server
section: 指南
locale: zh
translationOf: webdav-server/guides/quark-search-import
order: 40
tags:
  - quark
  - resolver
  - media-library
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## 它是什么

夸克资源自动转存解析器会把一个空文件夹当作导入意图。文件夹名就是搜索词，Zwind 会检查候选分享、导入匹配资源，并可以继续检查后续更新。

## 导入模式

Zwind 可以保留资源原始命名、生成干净命名的虚拟媒体库视图，或直接按更适合播放器刮削的方式整理导入资源。当原始分享命名不适合第三方播放器时，这会很有用。

## 更新检查

server 启动后，Zwind 可以把已导入资源加入更新检查队列。如果源分享新增文件，resolver 会尽量只导入新增内容，并通过 App 工作流提醒用户。

## 使用建议

用清晰的文件夹名表达搜索意图。对于剧集，必要时包含标题和年份。如果一个来源已经失效或导入不理想，删除导入目录并创建新的意图文件夹可以更干净地重新开始。
