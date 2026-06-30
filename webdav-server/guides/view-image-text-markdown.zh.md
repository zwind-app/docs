---
title: 用图片、文本和 Markdown 工具查看内容
description: 从 Browser 或首页侧边栏打开 Image Viewer、Text Editor 和 Markdown Preview，了解适用文件类型、内置选择器和保存限制。
seoTitle: 用 Zwind 查看图片、文本和 Markdown - Zwind 指南
keywords:
  - Zwind Image Viewer
  - Zwind Text Editor
  - Zwind Markdown Preview
  - WebDAV 文本编辑器
  - WebDAV Markdown 预览
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/view-image-text-markdown
order: 41
tags:
  - guide
  - browser
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Zwind 内置了三个轻量内容工具：**Image Viewer / 图片查看器** 用来看图片，**Text Editor / 文本编辑器** 用来打开和编辑文本文件，**Markdown Preview / Markdown 预览** 用来阅读渲染后的 Markdown。

下面截图使用英文界面；中文界面里的菜单位置相同。截图只展示 Browser 长按菜单的位置，不同文件类型会显示不同工具。

## 从 Browser 打开

在 Browser 中点击支持的文件，会使用 Zwind 的默认打开方式：

| 文件类型 | 默认打开结果 |
| --- | --- |
| `.png`、`.jpg`、`.jpeg`、`.gif`、`.bmp`、`.webp`、`.heic` 或 `.tiff` | 打开 **Image Viewer / 图片查看器**。同一列表里的附近图片可用于上一张、下一张切换。 |
| `.txt`、`.json`、`.rss`、`.wm`、`.log`、`.csv`、`.yaml`、`.yml`、`.xml`、`.opml`、`.ini` 或 `.cfg` | 打开 **Text Editor / 文本编辑器**。 |
| `.md` 或 `.markdown` | 打开 **Markdown Preview / Markdown 预览**。 |

想自己指定打开路径时，在 Browser 中长按文件。

![在 Browser 中长按文件会打开操作菜单；实际显示的工具取决于选中的文件类型。](/assets/docs/webdav-server/view-image-text-markdown/viewer-open-menu.png)

图片文件选择 **打开（默认）/ Open (Default)** 会进入 **Image Viewer / 图片查看器**。如果想走 WebView 的原始渲染路径，例如 SVG 或某个服务返回的网页式图片响应，选择 **在 WebView 中打开 / Open in WebView**。

文本文件可以在菜单中选择 **在文本编辑器中打开 / Open in Text Editor**。`.rss` 和 `.wm` 这类投影 marker file 需要修改 resolver URL 或 Web Media rule 时，也应该用 Text Editor 打开。

Markdown 文件选择 **打开（默认）/ Open (Default)** 会进入 **Markdown Preview / Markdown 预览**。想改 Markdown 源码时，选择 **在文本编辑器中打开 / Open in Text Editor**；想用网页方式检查 WebDAV 响应时，选择 **在 WebView 中打开 / Open in WebView**。

## 从首页侧边栏打开

首页侧边栏里有独立的 **Image Viewer / 图片查看器**、**Text Editor / 文本编辑器** 和 **Markdown Preview / Markdown 预览** 入口。打开侧边栏后选择对应工具，再在空状态里点 **选择目录 / Choose Folder**，或点顶部的文件夹按钮。

这个入口会打开 Zwind 的内置文件夹选择器。先选择一个 server，再选择文件或文件夹：

| 工具 | 选择器会加载什么 |
| --- | --- |
| **Image Viewer / 图片查看器** | 选择一个图片文件，或选择包含支持图片的文件夹。Image Viewer 会加载匹配到的图片，并支持前后切换。 |
| **Text Editor / 文本编辑器** | 选择一个文本文件，或选择包含文本类文件的文件夹。Text Editor 会打开第一个文档，并可在加载到的文本队列里切换。 |
| **Markdown Preview / Markdown 预览** | 选择一个 Markdown 文件，或选择包含 `.md` 或 `.markdown` 文件的文件夹。Markdown Preview 会渲染选中的 Markdown，并可在 Markdown 队列里切换。 |

内置选择器使用和 Browser 相同的 WebDAV 来源。如果 server 还没有运行，选择器可以先启动它，再列出目录。

## 使用三个工具

**Image Viewer / 图片查看器** 会在深色背景上显示单张图片。加载多张图片时，用上一张、下一张按钮切换。点击图片区域可以隐藏或显示工具栏，双指缩放可以放大图片，下滑可以关闭查看器。

**Text Editor / 文本编辑器** 会把文件下载为文本，显示一个大输入区域，并在打开文档后启用 **保存 / Save**。如果从文件夹或多选结果加载了多个文本文件，可以用底部上一项、下一项控件切换。

**Markdown Preview / Markdown 预览** 会渲染标题、列表、代码块、链接和 Markdown 图片。预览里的文字可以选中复制；点击 Markdown 链接会打开链接，点击渲染出的 Markdown 图片会用 Image Viewer 查看。需要修改 Markdown 源码时，请改用 Text Editor。

## 保存限制

Text Editor 保存时，会把编辑后的文本写回当前文件 URL。文件来自支持写入的 WebDAV 来源时可以保存，例如可写的本地 server 文件夹，或其他允许写入的 WebDAV 后端。

来源只读、当前项目只是投影结果而不是可写的真实后端文件，或上游 WebDAV server 拒绝写入时，Text Editor 不能保存。这时保存动作会返回 server 错误，不会改写文件。

Image Viewer 和 Markdown Preview 主要用于查看，不会保存图片改动，也不会保存 Markdown 源码改动。要编辑 Markdown 文件，请把 `.md` 或 `.markdown` 文件打开到 Text Editor，再从 Text Editor 保存。
