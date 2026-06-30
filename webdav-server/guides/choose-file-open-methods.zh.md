---
title: 选择文件打开方式
description: 在 Zwind Browser 中为视频、音频、图片、文本、Markdown、URL shortcut、普通文件和文件夹选择合适的打开方式。
seoTitle: 在 Zwind Browser 中选择文件打开方式 - Zwind 指南
keywords:
  - Zwind Browser 打开文件
  - WebDAV 文件打开方式
  - iPhone WebDAV 视频播放器
  - WebDAV Markdown 预览
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/choose-file-open-methods
order: 38
tags:
  - guide
  - browser
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Browser 会根据选中项目的类型选择打开工具。点击文件夹行会进入文件夹，点击文件行会使用 Zwind 的默认打开方式；当你想指定某个工具时，在 Browser 中长按文件或文件夹行。

下面截图使用英文界面；中文界面里的菜单位置相同。

## 打开长按菜单

在 Browser 中长按一个文件或文件夹行。菜单标题会显示当前选中的名称，第一组操作就是这个项目可用的打开方式。

![长按文件后可以选择 Open Default、Text Editor、WebView、System Browser、分享和文件操作。](/assets/docs/webdav-server/choose-file-open-methods/file-actions-menu.png)

想让 Zwind 自动匹配时，选择 **打开（默认）/ Open (Default)**。想指定工具、切换播放器，或交给 iOS 处理时，选择对应的工具名称。

## Open Default 会做什么

**打开（默认）/ Open (Default)** 会按 Zwind 内置规则匹配：

| 项目类型 | 默认结果 |
| --- | --- |
| 视频文件，例如 `.mp4`、`.mov`、`.mkv`、`.webm`、`.m3u8` 或 `.mpd` | 打开 **Video Player / 视频播放器**，并从同目录附近的可播放视频生成播放列表。 |
| 音频文件，例如 `.mp3`、`.m4a`、`.aac`、`.wav`、`.flac` 或 `.ogg` | 打开 **Music Player / 音乐播放器**，并从同目录附近的音频生成播放队列。 |
| 图片，例如 `.png`、`.jpg`、`.jpeg`、`.gif`、`.bmp`、`.webp`、`.heic` 或 `.tiff` | 打开 **Image Viewer / 图片查看器**，可继续切换附近图片。 |
| Markdown 文件 `.md` 或 `.markdown` | 打开 **Markdown Preview / Markdown 预览**。 |
| 文本类文件，例如 `.txt`、`.json`、`.rss`、`.wm`、`.log`、`.csv`、`.yaml`、`.xml`、`.opml`、`.ini` 或 `.cfg` | 打开 **Text Editor / 文本编辑器**。 |
| 以 `.url` 结尾的 URL shortcut | 读取 shortcut 里的目标地址，并在可能时用 Zwind 的网页运行环境打开 HTTP 或 HTTPS URL；否则回退到 WebView。 |
| PDF 和其他普通文件 | 用 **WebView** 做应用内预览，前提是这个格式能被 WebView 显示。 |

如果文件没有扩展名，Zwind 可能会先探测内容类型再选择默认工具。仍然无法识别时，会回退到 WebView。

## 视频和音频的选择

视频文件会显示专用播放器选项：

| 操作 | 适合什么情况 |
| --- | --- |
| **在视频播放器中打开 (FFmpeg) / Open in Video Player (FFmpeg)** | 需要 FFmpeg 播放器或更强容器格式支持的视频。 |
| **在视频播放器中打开 (AVPlayer) / Open in Video Player (AVPlayer)** | Apple 原生播放器支持较好的格式，例如 MP4、MOV、M4V 和 HLS。 |
| **在音乐播放器中打开 / Open in Music Player** | 播放媒体文件里的音轨，或把它加入音乐播放队列。 |
| **在 WebView 中打开 / Open in WebView** | 更适合用网页方式播放的 URL 或媒体响应。 |

音频文件的主要显式选项是 **在音乐播放器中打开 / Open in Music Player**。如果想使用视频播放器控件，也可以选 **在视频播放器中打开 (FFmpeg) / Open in Video Player (FFmpeg)**；如果来源更适合当作网页资源处理，可以选 **在 WebView 中打开 / Open in WebView**。

## 图片、文本和 Markdown 工具

图片的 **打开（默认）/ Open (Default)** 会进入 **Image Viewer / 图片查看器**。如果想看 WebView 的原始渲染，例如 SVG 或某个服务返回的特殊图片响应，可以选择 **在 WebView 中打开 / Open in WebView**。

文本类文件可用 **在文本编辑器中打开 / Open in Text Editor**。`.rss` 和 `.wm` marker file 也用这个入口编辑 resolver URL 或网页媒体规则。

Markdown 文件的 **打开（默认）/ Open (Default)** 会进入 **Markdown Preview / Markdown 预览**。想改 Markdown 源码时，选择 **在文本编辑器中打开 / Open in Text Editor**；想查看原始 WebDAV 响应时，选择 **在 WebView 中打开 / Open in WebView**。

## URL shortcut 和普通文件

`.url` 文件可以只写一个 URL，也可以使用 Internet Shortcut 风格的 `URL=` 行。**打开（默认）/ Open (Default)** 会读取文件内容，并在目标是 `http` 或 `https` URL 时打开它。想查看或编辑 shortcut 文件本身时，选择 **在文本编辑器中打开 / Open in Text Editor**。

对于类型未知的普通文件，菜单会提供 **在视频播放器中打开 / Open in Video Player**、**在音乐播放器中打开 / Open in Music Player**、**在文本编辑器中打开 / Open in Text Editor** 和 **在 WebView 中打开 / Open in WebView** 等手动选择。你知道文件内容属于哪一类时，直接选择对应工具。

**在系统浏览器中打开 / Open in System Browser** 会把 WebDAV URL 交给 iOS。**分享 / Share** 分享文件内容到 iOS 分享面板。**复制链接 / Copy Link** 和 **分享链接 / Share Link** 分享的是 WebDAV URL，不是已下载文件；接收方 app 或设备需要能访问这个 server，并在需要时提供凭据。

## 打开文件夹

长按文件夹会显示文件夹专用打开方式：

| 操作 | 打开什么 |
| --- | --- |
| **打开文件夹 / Open Folder** | 在 Browser 中进入这个文件夹。 |
| **在视频播放器中打开 / Open in Video Player** | 把文件夹里的可播放视频加载到 Video Player。 |
| **在音乐播放器中打开 / Open in Music Player** | 把文件夹里的可播放音频加载到 Music Player。 |
| **在 WebView 中打开 / Open in WebView** | 用 Zwind 的 WebView 打开这个文件夹 URL。 |
| **在系统浏览器中打开 / Open in System Browser** | 把文件夹 URL 交给 iOS。 |

RSS 或 Web Media 的投影边界文件夹还可能显示 **在文本编辑器中打开 / Open in Text Editor**，这个入口会编辑投影文件夹背后的 `.rss` 或 `.wm` marker file。
