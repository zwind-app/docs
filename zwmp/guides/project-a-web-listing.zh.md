---
title: 投影一个网页列表
description: 通过生成或编写 .wm 规则，把网页媒体列表转换成投影资源。
seoTitle: 如何把网页列表投影成媒体资源 - ZWMP 指南
keywords:
  - project web listing
  - ZWMP adapter
  - media links
  - WebDAV resources
productSlug: zwmp
section: 指南
parent: guides
locale: zh
translationOf: zwmp/guides/project-a-web-listing
order: 30
tags:
  - guide
  - adapter
  - web-listing
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## 目标

把一个列出媒体链接的页面转换成可浏览的资源树。

## 工作流

1. 选择一个列表页面。
2. 找出稳定的链接模式。
3. 提取媒体 URL 和可读名称。
4. 解析可选元数据。
5. 暴露为 WebDAV 风格资源。

## 起步字段

先从 `source`、`candidate_selector`、`candidate_link_selector`、`title_selector` 和 `media_type` 开始。只有当列表 item 会进入包含更多链接或剧集的中间页时，才加入 `detail_url_selector`。

当最终媒体资源应该直接出现在当前目录下时，使用 `projection=flat`。当每张卡片或每集都应该有独立目录时，使用 `projection=by-item`。

## 保持投影诚实

不要编造页面没有提供的元数据。相比误导性输出，清晰的占位或省略字段更好。
