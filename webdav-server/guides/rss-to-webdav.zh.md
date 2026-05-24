---
title: 使用 .rss marker file 实现 RSS to WebDAV
description: 通过 Zwind RSS Projection Resolver 把 RSS feed 变成可浏览的 WebDAV 资源。
seoTitle: "使用 Zwind RSS Projection Resolver 实现 RSS to WebDAV"
keywords:
  - RSS to WebDAV
  - RSS 投影
  - WebDAV RSS
  - .rss marker file
productSlug: webdav-server
section: 指南
locale: zh
translationOf: webdav-server/guides/rss-to-webdav
order: 30
tags:
  - rss
  - projection
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## RSS Projection 是什么

RSS Projection 会把 feed URL 转换成 WebDAV 风格文件夹。你不需要单独打开 feed reader，只要创建一个 `.rss` marker file，Zwind 就能把 feed item 暴露成可浏览资源。

## 适合哪些场景

适合 podcast 类 feed、视频 feed、带媒体附件的 newsletter，或任何你希望从文件/媒体客户端浏览的 feed。

## 基本设置

1. 创建一个以 `.rss` 结尾的文本文件。
2. 在文件里写入 feed URL。
3. 把它放到启用 RSS resolver 的 Zwind server 下。
4. 像打开文件夹一样浏览 marker file 对应的投影目录。

Resolver 输出取决于 feed 内容，会尽量把附件、链接、标题和日期转换成资源。
