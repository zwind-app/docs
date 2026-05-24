---
title: Projection
description: ZWMP 如何把杂乱网页列表变成文件系统形状的媒体资源。
seoTitle: ZWMP Projection 概念 - 把网页列表变成媒体资源树
keywords:
  - web listing projection
  - media resource tree
  - ZWMP projection
  - WebDAV-style resources
productSlug: zwmp
section: 概念
parent: concepts
locale: zh
translationOf: zwmp/concepts/projection
order: 20
tags:
  - projection
  - web-listing
  - resources
publishedAt: 2026-05-21
updatedAt: 2026-05-24
draft: false
---

## 形状

Projection 从网页列表页面开始。页面里可能有链接、标题、日期、媒体名称或其他人容易扫读、但对媒体客户端不够结构化的信息。

ZWMP 解释这些页面，并把有用部分投影成 WebDAV 风格资源树。

## 三个步骤

1. 读取网页列表。
2. 解析媒体链接和元数据。
3. 暴露一棵客户端可以浏览的资源树。

## 和 Zwind 的关系

Zwind Resource Projection 是更大的产品概念。ZWMP 是面向网页列表的工具包路径。

## Projection 应该保留什么

Projection 应该保留页面提供的稳定事实：标题、item URL、缩略图、media URL 和有意义的分组。不要编造无法从来源推导出的元数据。

## 为什么需要 .wm 规则

不同网站有不同的 HTML 结构。`.wm` 规则把站点特定知识保存在一个小的、可检查的文件里，让 runtime 本身保持通用。
