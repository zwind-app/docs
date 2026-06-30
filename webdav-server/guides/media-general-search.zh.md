---
title: 使用媒体通搜
description: 从 Browser 当前目录进入媒体通搜，按关键词、媒体类型、预览大小和文件大小、日期、名称排序查找文件。
seoTitle: 使用 Zwind Browser 媒体通搜 - Zwind 指南
keywords:
  - Zwind 媒体通搜
  - WebDAV 媒体搜索
  - Browser 文件搜索
  - WebDAV 文件预览
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/media-general-search
order: 42
tags:
  - guide
  - browser
  - media
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

媒体通搜从 Browser 当前目录进入，用来搜索当前目录及其子目录里的文件。它会从你正在看的目录开始扫描，然后按文件名关键词、媒体类型、预览大小和排序条件缩小结果。

下面截图使用英文界面；中文界面里的位置相同，正文会标注中文/英文名称。

## 从当前目录进入搜索

打开 **Browser**，先进入你要搜索的目录，然后点击悬浮搜索按钮。

![在要搜索的 Browser 目录里点击悬浮搜索按钮。](/assets/docs/webdav-server/media-general-search/boxed/browser-search-entry.png)

进入后顶部会显示 **当前目录 / Current directory**，这里就是本次搜索的起点。除非你本来就在更上层目录，否则媒体通搜不会跨到整个 app 或所有 server 里搜索。

![媒体通搜会显示当前目录、文件数量、类型筛选、预览大小、排序控件和匹配文件。](/assets/docs/webdav-server/media-general-search/boxed/media-search-results.png)

Zwind 会随着扫描逐步加入文件结果。文件夹只用于继续向下扫描，结果列表显示的是文件。每一行包含文件名、文件大小、修改日期、完整路径和右侧预览区域。

## 按关键词和媒体类型筛选

在 **搜索文件 / Search files** 输入文件名关键词。关键词只匹配文件名，并作用在当前目录及其子目录已经扫描到的文件上。

媒体类型分段控件可以决定保留哪些结果：

| 中文标签 | 英文标签 | 保留的文件 |
| --- | --- | --- |
| **全部** | **All** | 当前扫描到的所有文件类别。 |
| **视频** | **Video** | Zwind 按扩展名或内容处理方式识别为视频的文件。 |
| **音频** | **Audio** | 音频文件。 |
| **图片** | **Image** | 图片文件。 |
| **PDF** | **PDF** | PDF 文件。 |
| **文本** | **Text** | 文本类文件，例如纯文本、JSON、RSS、WM 规则、日志、CSV、YAML、XML、OPML、INI 和 CFG。 |

当关键词和类型条件筛完没有结果时，列表会显示 **没有找到文件 / No files found**。

![关键词可以把当前目录的结果筛到空状态。](/assets/docs/webdav-server/media-general-search/boxed/media-search-empty.png)

## 调整预览大小和排序

**小 / Small**、**中 / Medium**、**大 / Large** 控制的是结果行高度和右侧预览区域大小。它不是按文件容量筛选的条件。

下面的排序控件可以选择：

| 中文标签 | 英文标签 | 排序依据 |
| --- | --- | --- |
| **文件名** | **Name** | 文件名，也是默认排序字段。 |
| **日期** | **Date** | 修改日期。 |
| **大小** | **Size** | 文件字节大小。 |

点击排序字段右侧的圆形箭头按钮，可以在升序和降序之间切换。每个结果行都会显示文件大小；当前 UI 中要把大文件或小文件排到一起，应使用 **大小 / Size** 排序。

## 理解预览生成和重试

图片文件会直接从 WebDAV URL 加载图片预览。视频文件会在结果行里生成帧预览；Zwind 大约每 5 分钟取一帧，并在准备过程中显示预览进度。

音频、PDF、文本和其他非图片、非视频文件会显示类别图标和文件名。如果视频预览无法生成，结果行会显示 **该文件无法生成预览 / Preview unavailable for this file** 或具体错误。点击 **点击重试 / Tap to retry** 可以重新尝试这个文件或某一帧的预览生成。

预览生成和打开文件是两件事。重试预览不会重命名、移动或编辑 WebDAV 文件。

## 打开结果或在上层目录中显示

点击结果行，会按 Zwind 默认打开方式打开这个文件。长按结果行，会打开结果操作菜单。

![长按结果可以打开文件、复制链接、在上层目录中显示或添加书签。](/assets/docs/webdav-server/media-general-search/boxed/result-actions.png)

结果操作菜单里常见的项目有：

| 操作 | 作用 |
| --- | --- |
| **打开（默认）/ Open (Default)** | 使用 Browser 对该文件类型的默认打开方式。 |
| **复制链接 / Copy Link** | 复制这个文件的 WebDAV URL。 |
| **在上层目录中显示 / Show in parent folder** | 用 Browser 打开这个文件所在的父目录，让你在原目录列表里看到它。 |
| **添加书签 / Bookmark** | 在书签功能可用时，把这个文件 URL 保存到 Zwind 书签。 |

不同文件类型还会出现额外打开方式。视频文件可能显示 **在视频播放器中打开 (FFmpeg) / Open in Video Player (FFmpeg)**；音频和视频文件可能显示 **在音乐播放器中打开 / Open in Music Player**；文本文件可能显示 **在文本编辑器中打开 / Open in Text Editor**。

当搜索结果来自子目录，而你想继续进行普通 Browser 操作时，使用 **在上层目录中显示 / Show in parent folder**。它会进入文件所在目录，方便你再打开附近文件、复制、移动、重命名或删除。
