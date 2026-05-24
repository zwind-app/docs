---
title: .wm 规则语法概览
description: 面向用户介绍 ZWMP 与 Zwind 使用的 Web Media Projection 规则格式。
seoTitle: ".wm 规则语法：Web Media Projection"
keywords:
  - .wm 规则
  - wm rule spec
  - 网页媒体投影语法
  - ZWMP rules
productSlug: zwmp
section: 概念
locale: zh
translationOf: zwmp/concepts/wm-rule
order: 20
tags:
  - wm-rule
  - syntax
  - projection
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## 核心字段

`.wm` 规则是普通文本 marker file。最常用字段包括：

- `source`：列表页 URL。
- `candidate_selector`：item 卡片的 CSS selector。
- `candidate_link_selector`：每个 item 内部的链接 selector。
- `title_selector`：用于命名 item 的 selector。
- `thumbnail_selector`：用于查找缩略图的 selector。
- `detail_url_selector`：可选，用于中间页或剧集列表。
- `detail_url_mode`：`expand` 会创建子 item；其他模式可以跟随 detail 页面。
- `projection`：`by-item` 创建 item 文件夹；`flat` 直接平铺媒体资源。
- `media_type`：默认是 `video`；图片站或混合媒体站可以调整。
- `fast_mode`：为 true 时优先使用静态 HTTP 解析，适合不需要 JavaScript 的网站。

## 浏览器行为

不需要 JavaScript 的网站应尽量保持 fast mode。若站点依赖客户端渲染生成有用 DOM，可以使用浏览器式 runtime、selector wait 和桌面模式等设置。

## Debug 预期

debug 命令应该展示与 resolver 一致的逻辑阶段：source load、candidate extraction、item URL extraction、detail hop expansion 和 media URL discovery。哪个阶段出错，就先修哪个阶段的规则。
