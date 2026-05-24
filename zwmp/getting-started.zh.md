---
title: ZWMP 入门
description: 了解 ZWMP 如何用 .wm 规则把网页媒体列表变成投影资源。
seoTitle: "ZWMP .wm 规则入门"
keywords:
  - ZWMP
  - .wm 规则
  - Web Media Projection
  - WebDAV 资源投影
productSlug: zwmp
section: 入门
locale: zh
translationOf: zwmp/getting-started
order: 1
tags:
  - zwmp
  - projection
  - toolkit
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## ZWMP 是什么

ZWMP 是一个开源工具包，用于把网页列表页面转换成投影的 WebDAV 风格媒体资源。实际使用时，核心产物是 `.wm` 规则：一个小文本文件，描述列表页在哪里、如何找到 item、如何跟随 detail 页面，以及应该提取哪类媒体。

它面向开发者和高级用户，帮助网页、媒体链接和资源树在中间层连接起来。

## 从这里开始

1. 阅读 projection 概念。
2. 确认一个网页列表的结构。
3. 决定哪些链接和元数据应该成为 item resource。
4. 生成或编写 `.wm` 规则。
5. 运行 debug 输出，直到 item URL 和 media URL 符合预期。
6. 把规则导入 Zwind WebDAV 或其他兼容 resolver。

## 一个好规则应该捕获什么

一个好规则应该包含稳定的 CSS selector、目标 media type、站点是否需要浏览器式 JavaScript 执行，以及中间页面是否需要 expand 成子 item。

## ZWMP 放在哪个位置

Zwind WebDAV 使用这套思路把网页媒体页面暴露为文件夹和文件。ZWMP 让站点特定逻辑保存在可检查的规则中，而不是把一次性 parser 写死在 App 代码里。
