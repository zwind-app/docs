---
title: 用 Video Player 播放 WebDAV 视频
description: 从 WebDAV 文件或文件夹启动播放，选择 FFmpeg、AVPlayer 或 Web Player，并使用播放列表、字幕、倍速和画中画。
seoTitle: 用 Zwind Video Player 播放 WebDAV 视频 - Zwind 指南
keywords:
  - Zwind Video Player
  - WebDAV 视频播放器
  - iPhone WebDAV 视频
  - FFmpeg AVPlayer Web Player
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/play-webdav-video
order: 39
tags:
  - guide
  - browser
  - video
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Zwind 的 Video Player 可以直接播放内置 Browser 里的 WebDAV 媒体地址，也可以从单个视频文件或整个视频文件夹启动。适合在应用内连续观看 WebDAV server 上的视频，而不是把文件先交给其他 app。

下面截图使用英文界面；中文界面里的菜单位置相同，正文会标注中文/英文按钮名对照。

## 从 Browser 打开视频

在 Browser 中点击视频文件，会使用 Zwind 的默认视频打开方式。默认路径会根据文件和来源选择播放器：HLS `.m3u8` 和支持的 Web Media 结果通常优先使用 AVPlayer，其他格式通常从 FFmpeg 播放器开始。

如果想自己指定播放器，长按视频文件。

![在 Browser 中长按项目会打开操作菜单；视频文件也在同一菜单位置显示播放器选择。](/assets/docs/webdav-server/play-webdav-video/video-open-menu.png)

视频文件可能显示这些操作：

| 操作 | 作用 |
| --- | --- |
| **打开（默认）/ Open (Default)** | 让 Zwind 自动选择播放器，并从附近的视频生成播放列表。 |
| **在视频播放器中打开 (FFmpeg) / Open in Video Player (FFmpeg)** | 直接使用 FFmpeg 播放路径。 |
| **在视频播放器中打开 (AVPlayer) / Open in Video Player (AVPlayer)** | 当前格式支持时，直接使用 Apple 原生 AVPlayer 路径。 |
| **在 WebView 中打开 / Open in WebView** | 不进入 Video Player 控件，直接用 Zwind 的 WebView 打开 WebDAV URL。 |
| **在系统浏览器中打开 / Open in System Browser** | 把媒体 URL 交给 iOS，让 Safari 或其他已安装 app 处理。 |

## 把文件夹作为播放列表打开

在 Browser 中长按文件夹，选择 **在视频播放器中打开 / Open in Video Player**。Zwind 会把这个文件夹里的可播放视频加载到 Video Player。看剧集、相机视频、投影出来的媒体目录时，这比逐个打开文件更直接。

已经进入 Video Player 后，打开 **选项 / Options**，选择 **选择目录 / Choose Folder**，可以把另一个文件夹追加到当前播放队列。如果所选文件夹里没有可播放视频，播放器会保留当前项目，并显示本次目录加载结果，不会用空队列替换播放。

## 选择 FFmpeg、AVPlayer 或 Web Player

视频打开后，在 Video Player 的选项菜单中切换播放引擎：

| 播放器 | 适合什么内容 | 说明 |
| --- | --- | --- |
| **使用 FFmpeg 播放器 / Use FFmpeg Player** | 需要更广格式支持的容器或编码，例如很多 `.mkv`、`.webm`，以及 Apple 原生支持不好的文件。 | FFmpeg 准备好后，可以选择内嵌字幕并调整字幕显示。 |
| **使用 AVPlayer / Use AVPlayer** | Apple 原生支持较好的格式，例如 `.mp4`、`.m4v`、`.mov` 和 HLS `.m3u8`。 | 使用 iOS 原生播放栈；当前视频支持时，Video Player 会显示 iOS 画中画按钮。不支持的格式会显示禁用原因。 |
| **使用 Web 播放器 / Use Web Player** | 更适合按网页资源处理的媒体 URL，或 FFmpeg、AVPlayer 都无法初始化的流。 | 这是 Video Player 内部的网页播放器。Browser 菜单里的 **在 WebView 中打开 / Open in WebView** 则是直接用普通 WebView 打开 URL。 |

如果 AVPlayer 初始化失败，错误页会提供 **打开 Web 播放器 / Open Web Player** 和切到 FFmpeg 的路径。如果 FFmpeg 播放失败，可以点 **重新尝试 FFmpeg / Retry FFmpeg**，Apple 支持的格式可改用 AVPlayer，网页流可改用 Web Player。

## 使用播放列表

从 Browser 打开单个文件时，Zwind 可能会把同一位置附近的可播放视频一并加入列表。从文件夹打开时，文件夹里的可播放视频会成为播放列表。

在 Video Player 中打开 **选项 / Options**，选择 **播放列表 / Playlist** 可以查看已加载项目。当前项目旁边有勾选标记，点击其他行会跳到对应视频。

当列表里有多个项目时，可以使用播放器控制区里的上一首和下一首按钮。**选项 / Options** 里的播放顺序项会在 **Sequential**、**Repeat One** 和 **Shuffle** 之间切换。

## 字幕

打开 **选项 / Options**，选择 **字幕 / Subtitles** 可以选择内嵌字幕轨道。字幕选择需要 FFmpeg 播放器准备好后才可用；AVPlayer 和 Web Player 下的字幕控制会显示“仅 FFmpeg 支持”的原因。

同一个选项菜单里还有这些字幕控制：

| 控制 | 作用 |
| --- | --- |
| **字幕变大 / Subtitle Size +** | 增大字幕字号。 |
| **字幕变小 / Subtitle Size -** | 减小字幕字号。 |
| **字幕上移 / Subtitle Up** | 把字幕位置上移。 |
| **字幕下移 / Subtitle Down** | 把字幕位置下移。 |
| **重置字幕显示 / Reset Subtitle Display** | 恢复字幕字号和位置。 |

在字幕列表中选择 **关闭 / Off** 可以隐藏内嵌字幕。

## 倍速和画中画

点击播放器控制区里的倍速控件，可以选择 **0.50x**、**0.75x**、**1.00x**、**1.25x**、**1.50x** 或 **2.00x**。倍速作用于当前播放会话。

在 iOS 上，如果当前视频和原生播放路径允许，Video Player 控制区会显示画中画按钮。当前视频或播放器状态无法启动画中画时，Zwind 会显示 **此视频暂时无法使用画中画 / Picture in Picture is unavailable for this video**，或显示 iOS 返回的失败详情。

## 播放失败时怎么处理

按你看到的失败位置选择下一步：

| 看到的情况 | 可以尝试 |
| --- | --- |
| 出现 **AVPlayer cannot open .mkv here** 或其他 AVPlayer 禁用原因 | 从 Browser 选择 **在视频播放器中打开 (FFmpeg) / Open in Video Player (FFmpeg)**，或在 Video Player 里选择 **使用 FFmpeg 播放器 / Use FFmpeg Player**。 |
| AVPlayer 打开后进入错误页 | 点 **打开 Web 播放器 / Open Web Player** 尝试网页播放；如果文件不是 Apple 原生友好格式，切换到 FFmpeg。 |
| FFmpeg 报播放失败 | 点 **重新尝试 FFmpeg / Retry FFmpeg**。如果文件是 `.mp4`、`.mov`、`.m4v` 或 `.m3u8`，尝试 AVPlayer；如果 URL 更像网页流，尝试 Web Player 或从 Browser 选择 **在 WebView 中打开 / Open in WebView**。 |
| 字幕菜单不可用 | 切到 **使用 FFmpeg 播放器 / Use FFmpeg Player**，并等播放器准备好；内嵌字幕控制目前只支持 FFmpeg。 |
| 画中画不可用 | 对 Apple 支持的媒体切到 AVPlayer，等视频初始化完成后再点画中画按钮。 |
| 播放列表缺少预期文件 | 重新从 Browser 用 **在视频播放器中打开 / Open in Video Player** 打开文件夹，或在 Video Player 里用 **选择目录 / Choose Folder** 让 Zwind 重新从该文件夹生成队列。 |
