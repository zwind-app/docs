---
title: 使用首页侧边栏内置工具
description: 从首页侧边栏打开 Feed View、Web Browser、Video Player、Music Player、Image Viewer、Text Editor、Markdown Preview 和 Bookmarks。
seoTitle: 使用 Zwind 首页侧边栏内置工具 - Zwind 指南
keywords:
  - Zwind 首页侧边栏
  - Zwind 内置工具
  - WebDAV 工具
  - Zwind Text Editor
  - Zwind Bookmarks
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/home-sidebar-tools
order: 43
tags:
  - guide
  - home
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

首页侧边栏适合在还没有进入 Browser、还没有选中文件时，直接打开 Zwind 的独立工具。你可以先选择要做的事：读 feed、打开网页、启动播放器、从工具里选择目录、编辑文本、预览 Markdown，或者打开保存过的 WebDAV 位置。

下面截图使用英文界面；中文界面位置相同。截图里的 **Builtin Apps** 对应中文里的内置工具列表，**Choose Folder** 对应 **选择目录**。

## 打开侧边栏

在首页点左上角的侧边栏按钮，**Builtin Apps / 内置工具** 面板会从左侧展开。

![首页侧边栏列出 Feed View、Web Browser、Video Player、Music Player、Image Viewer、Text Editor、Markdown Preview 和 Bookmarks。](/assets/docs/webdav-server/home-sidebar-tools/boxed/home-sidebar-tools.png)

点某一行就会打开对应工具。只是想看一眼列表时，可以向左滑关闭面板，或点面板外侧区域。

## 每个入口适合做什么

| 侧边栏入口 | 适合的任务 |
| --- | --- |
| **Feed View** | 阅读从 RSS、OPML、支持的网页来源或 resolver 目录汇总出来的内容。想看时间线式阅读列表，而不是目录树时，从这里进入。 |
| **Web Browser / 网页浏览器** | 打开普通网页或用内置网页运行环境搜索。它不是 WebDAV 文件目录 Browser；要浏览 server 文件夹，请用文件 Browser。 |
| **Video Player / 视频播放器** | 不先选中文件，直接启动视频播放器。空播放器里可以点 **Choose Folder / 选择目录**，把一个视频目录加载成播放队列。 |
| **Music Player / 音乐播放器** | 启动或恢复音乐播放器。适合选择音频目录、继续当前播放会话，或从文件夹建立音频队列。 |
| **Image Viewer / 图片查看器** | 先选择图片文件或图片目录，再在工具里前后切换查看。 |
| **Text Editor / 文本编辑器** | 先选择文本类文件或目录，再编辑文本，或在加载到的文本文件之间切换。 |
| **Markdown Preview / Markdown 预览** | 先选择 Markdown 文件或目录，再阅读渲染后的 Markdown。需要修改 Markdown 源码时，改用 Text Editor。 |
| **Bookmarks / 书签** | 打开保存过的 WebDAV URL 或位置，不需要再次从 server 卡片或 Browser 目录一步步进入。 |

## 从独立工具里选择文件或目录

从侧边栏打开的媒体和内容工具一开始是空状态，因为你还没有指定 WebDAV 文件。此时点工具里的 **Choose Folder / 选择目录**，或顶部的文件夹按钮，打开 Zwind 的内置选择器。

![从首页侧边栏打开 Text Editor 后会进入空状态，框选位置是 Choose Folder 入口。](/assets/docs/webdav-server/home-sidebar-tools/boxed/text-editor-empty.png)

在选择器里先选 server。如果 server 还没运行，Zwind 可以先启动它，再列出目录。然后按工具选择匹配的文件或文件夹：

| 工具 | 应该选择什么 |
| --- | --- |
| **Video Player / 视频播放器** | 包含视频的目录；选择器允许时，也可以选单个视频文件。 |
| **Music Player / 音乐播放器** | 包含音频的目录，或单个音频文件。 |
| **Image Viewer / 图片查看器** | 图片文件，或包含支持图片格式的目录。 |
| **Text Editor / 文本编辑器** | 文本类文件，或包含文本文件的目录。 |
| **Markdown Preview / Markdown 预览** | `.md`、`.markdown` 文件，或包含 Markdown 文件的目录。 |

选完后会留在当前工具里。例如 Text Editor 打开可写文本文件后，顶部 **Save / 保存** 才会启用。

## 已经看到文件时，优先用 Browser

如果你已经在内置 **Browser** 的目录里看到了目标文件，通常直接在 Browser 里操作更快：点文件使用默认打开方式，或长按文件、文件夹，选择 **Open in Video Player / 在视频播放器中打开**、**Open in Music Player / 在音乐播放器中打开**、**Open in Text Editor / 在文本编辑器中打开**、**Open in WebView / 在 WebView 中打开** 等具体动作。

下面这些情况更适合用 Browser：

| 场景 | 为什么用 Browser 更合适 |
| --- | --- |
| 你已经进入文件所在目录 | 直接点或长按当前行，比重新打开独立工具再选目录更快。 |
| 想让 Zwind 按文件类型自动选择打开方式 | Browser 可以直接识别视频、音频、图片、文本、Markdown、URL shortcut 和普通文件。 |
| 希望同目录附近文件一起进入队列 | 从 Browser 打开时，视频、音频或图片可以带上同一列表里的相邻可播放项目。 |
| 需要先做文件操作 | 新建、重命名、复制、移动、删除、分享和添加书签都在 Browser 里完成。 |

首页侧边栏更适合“先选工具再选内容”的任务：打开 Feed View 阅读，打开 Web Browser 访问网页，恢复音乐播放，给播放器选择一个目录，或先打开保存过的位置再继续浏览。
