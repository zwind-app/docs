---
title: Web Media Projection Resolver
description: 使用 .wm 规则把网页媒体列表页面转换成可浏览的 WebDAV 风格媒体资源。
seoTitle: "Zwind Web Media Projection Resolver 与 .wm 规则"
keywords:
  - Web Media Projection
  - .wm 规则
  - 网页媒体解析器
  - 网页视频 WebDAV
  - 网页图片 WebDAV
productSlug: webdav-server
section: 指南
locale: zh
translationOf: webdav-server/guides/web-media-projection
order: 50
tags:
  - web-media
  - wm-rule
  - projection
publishedAt: 2026-05-24
updatedAt: 2026-05-24
draft: false
---

## .wm 规则描述什么

`.wm` marker file 告诉 Zwind 如何读取网站：source page、item selector、可选 detail link、title selector、thumbnail selector、media type、projection mode，以及是否需要浏览器式解析等 runtime 设置。

## 常见投影结构

当每个列表卡片都应该变成一个文件夹时，使用 `projection=by-item`。当媒体资源应该直接平铺在目录里时，使用 `projection=flat`。当一个 item 页面包含多集或多个 part 链接时，使用 `detail_url_mode=expand`。

## Debug 优先的工作流

网站无法解析时，优先运行 generator 的 debug 命令。debug 输出应该告诉你：

- source page 是否成功加载。
- candidate item 是否匹配。
- item URL 是否正确提取。
- 中间 detail page 是否正确 expand。
- 最终 media URL 是否被发现。

这通常能最快判断问题是 selector、browser runtime、selector wait 还是 media type 配置。
