---
title: 调试 .wm 规则
description: 使用 ZWMP debug 输出理解网页媒体站点为什么无法正确解析。
seoTitle: "调试 Web Media Projection 的 .wm 规则"
keywords:
  - 调试 .wm 规则
  - web media resolver debug
  - ZWMP debug
  - media URL 提取
productSlug: zwmp
section: 指南
locale: zh
translationOf: zwmp/guides/debug-wm-rules
order: 30
tags:
  - debug
  - wm-rule
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## 按顺序看输出

先看 source loading。如果 source page 加载失败，selector 还不是当前重点。然后依次检查 candidate 数量、candidate links、中间 detail 页面，以及最终 media discovery。

## 常见失败

- candidate selector 匹配到了导航链接，而不是 item 卡片。
- candidate link selector 缺失，导致 resolver 选错 anchor。
- detail page 里有多集，但缺少 `detail_url_mode=expand`。
- `media_type` 过宽，导致图片过早终止了视频解析流程。
- 页面需要浏览器式 JavaScript 执行，但规则启用了 `fast_mode=true`。

## 调整规则的循环

一次只改一个字段。重新运行 debug。直到 item URL 和 media URL 与人工浏览网页看到的结构一致。
