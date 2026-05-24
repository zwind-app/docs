---
title: Resource Projection
description: 解释外部资源如何出现在 Zwind 风格目录树中的概念文档。
seoTitle: Zwind Resource Projection 概念 - WebDAV 风格资源树
keywords:
  - Resource Projection
  - WebDAV resource tree
  - Zwind resolver
  - 资源投影
productSlug: webdav-server
section: 概念
parent: concepts
locale: zh
translationOf: webdav-server/concepts/resource-projection
order: 20
tags:
  - projection
  - resolver
  - resources
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## 概念

Resource Projection 指的是：普通文件夹以外的东西，也可以出现在一棵可浏览的资源树里。

外部来源可能是订阅、搜索结果、类网盘来源或网页列表。resolver 负责解释来源，并把它呈现成类似文件或文件夹的条目。

## 为什么重要

媒体通常不会只存在于一个干净目录里。Projection 给分散资源一个 WebDAV 风格浏览器、播放器和导入流程都更容易理解的形状。

## Resolver 生态

当前 Zwind 相关概念包括：

- RSS Projection Resolver
- Quark Search Import Resolver
- Web Media Projection Resolver

## Marker file 和意图文件夹

有些 resolver 从 `.rss` 或 `.wm` 这类 marker file 开始。有些 resolver 从表达意图的文件夹开始，例如夸克搜索/转存文件夹。resolver 读取 marker 或文件夹，生成虚拟 children，再由 WebDAV 层把它们呈现成普通资源。

## 为什么需要 lazy loading

Resolver 可能需要网络请求、浏览器式解析或云端 API 调用。因此 Zwind 会尽量保持投影懒加载：浏览父目录应该很轻，昂贵的 detail 解析只应在用户进入相关投影条目或打开媒体时发生。
