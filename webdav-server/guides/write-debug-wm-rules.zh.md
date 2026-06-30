---
title: 编写和调试 .wm 规则
description: 说明 Web Media Projection 的 .wm 字段如何把网页来源映射成 Zwind Browser 中的 WebDAV 目录、条目元数据和媒体文件。
seoTitle: "在 Zwind WebDAV Server 中编写和调试 .wm 规则"
keywords:
  - .wm 规则
  - Web Media Projection
  - WebDAV 网页媒体规则
  - Zwind Re-parse
  - Web Media 调试
productSlug: webdav-server
section: 指南
locale: zh
translationOf: webdav-server/guides/write-debug-wm-rules
parent: guides
order: 49
tags:
  - guide
  - web-media
  - wm-rule
  - debug
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-07-01
draft: false
---

`.wm` 文件是 Web Media Projection 读取的规则文件。它决定 Zwind 从哪个网页开始解析、用哪些 selector 找到列表条目、怎样命名目录、保留哪类媒体，以及最终在 Browser 里显示为“每个条目一个目录”还是“媒体文件平铺列表”。

本篇只从 WebDAV Server 的使用角度解释这些字段：在 **Text Editor（文本编辑器）** 里改什么、回到 **Browser** 会看到什么、规则失效后从哪里重新解析。完整字段索引可以看 [ZWMP 的 .wm 规则语法概览](/zh/docs/zwmp/concepts/wm-rule/)；命令行式 debug 输出的阅读顺序见 [调试 .wm 规则](/zh/docs/zwmp/guides/debug-wm-rules/)。

截图使用英文界面和本地示例网页。

## 先按字段组看规则

在 Browser 里长按 `.wm` 标记文件，选择 **Open in Text Editor（用文本编辑器打开）**。规则可以写成 `key=value`，也可以写成 `key: value`。空行和 `#` 开头的注释行会被忽略；如果第一行只有一个 URL，Zwind 会把它当作 `source`。

![Text Editor 中的 .wm 规则，框选 source、item selector、title、thumbnail、media type、projection 和 fast mode。](/assets/docs/webdav-server/write-debug-wm-rules/boxed/01-rule-fields.png)

示例规则可以分成这些部分：

| 字段组 | 影响什么 |
| --- | --- |
| `source` | Zwind 首先加载的列表页。这个 URL 无效或不可访问时，后面的 selector 还不会生效。 |
| `candidate_selector` | 列表页里重复出现的条目容器。示例中每个 `.video-card` 会变成一个候选条目。 |
| `candidate_link_selector` | 每个候选条目里的链接。通常它就是该条目的 detail URL，后续 detail-hop 字段可以继续替换或展开它。 |
| `title_selector` | 用来命名 Browser 条目目录、媒体文件和 `item.json` 里的标题。Zwind 会给条目目录加稳定序号，例如 `001-...`。 |
| `thumbnail_selector` | 用来生成 `thumbnail.url` 或缩略图元数据的图片链接。 |
| `media_type` | 保留哪类媒体。`video` 会保留视频、HLS、DASH；`audio` 保留音频；`image` 也接受 `images`、`photo`、`photos`；`all` 也接受 `any`、`media`。无法识别的值会按 `video` 处理。 |
| `projection` | `by-item` 表示每个条目一个目录；`flat` 表示媒体文件直接出现在 `.wm` 投影目录下。无法识别的值会按 `by-item` 处理。 |
| browser runtime 字段 | `fast_mode=true` 适合 HTML 响应里已经有条目和媒体线索的页面，会走静态解析。页面依赖浏览器渲染、播放器请求或延迟加载时，不要启用 fast mode，并按需要使用 `selector_wait_timeout`、`force_desktop_mode`、`force_network_sniff`、`network_sniff_timeout`、`play_button_selector` 这类字段。 |

## detail link 负责继续向里走

`candidate_link_selector` 通常把列表卡片指向条目详情页。有些网站还会再多一层，比如详情页里才有剧集列表，或者详情页再跳到播放页。这时需要加 `detail_url_selector`，让 Zwind 在 detail page 里继续找下一层链接。

`detail_url_mode=single` 表示选择一个下一层页面，仍然算同一个条目。`detail_url_mode=expand` 表示 selector 匹配到多个子条目，例如多集内容；在 `by-item` 投影模式下，这些子条目会显示成嵌套目录。第二层、第三层 detail hop 用 `detail_url_selector_2`、`detail_url_mode_2` 这类编号字段。

## 看 .wm 根目录输出

保存规则后回到 Browser，打开这个 `.wm` 标记文件。它会像一个投影目录一样显示。

![Browser 中打开 .wm 后的投影根目录，框选条目目录、source.json 和当前路径。](/assets/docs/webdav-server/write-debug-wm-rules/boxed/02-projected-root.png)

在 `by-item` 模式下，根目录里通常有：

| Browser 中看到的内容 | 来自哪些规则字段 |
| --- | --- |
| `001-Alpha Launch Recap`、`002-Beta Field Notes` | `candidate_selector` 找到条目，`candidate_link_selector` 取出 detail URL，`title_selector` 决定目录名。 |
| `source.json` | source page 的解析报告，包含归一化后的规则字段、item 数量，以及 Zwind 从列表页提取到的条目。 |

如果规则写的是 `projection=flat`，这里不会显示每个条目的目录，而是直接显示解析出的媒体文件，再加上 `source.json`。播放器或 WebDAV 客户端只需要一层文件列表时用 `flat`；需要保留条目上下文、辅助链接和元数据时用 `by-item`。

## 进入一个条目目录检查媒体结果

打开任意条目目录，可以看到 detail page 和媒体发现阶段的结果。

![by-item 条目目录中显示 MP4 媒体文件、detail.url、item.json、media.url 和 thumbnail.url。](/assets/docs/webdav-server/write-debug-wm-rules/boxed/03-item-output.png)

常见文件含义如下：

| 文件 | 为什么会出现 |
| --- | --- |
| `001-Alpha Launch Recap.mp4` 这类媒体文件 | detail page 里找到了符合 `media_type` 的媒体 URL。文件名来自条目标题和检测到的媒体扩展名。 |
| `item.json` | 当前条目的元数据、detail 状态、发现到的媒体 URL，以及这个条目上的解析错误。 |
| `detail.url` | `candidate_link_selector` 或最后一层 detail hop 选中的详情页链接。 |
| `media.url` | 主媒体 URL，对外表现为 Internet Shortcut 文件。 |
| `thumbnail.url` | `thumbnail_selector` 找到的缩略图链接。 |
| `discovery.txt` | Zwind 能解析这个条目，但没有找到符合 `media_type` 的媒体 URL 时出现。 |

## 改规则后重新解析

Web Media 结果会被缓存。你改了 `.wm` 文件、调整 selector，或网站页面结构发生变化后，在 Browser 中打开对应 Web Media 路径，点右下角操作菜单。

![Browser 右下角菜单中的 Re-parse 入口。](/assets/docs/webdav-server/write-debug-wm-rules/boxed/04-reparse-menu.png)

点 **Re-parse（重新解析）** 会清掉当前 Web Media 范围的缓存并重新跑解析。在 `.wm` 根目录执行时，会刷新 source page 和 item 列表；在条目目录执行时，会刷新这个条目的 detail/media discovery；如果当前条目是 `detail_url_mode=expand` 生成的容器，则会刷新子条目展开结果。

当一次浏览器式解析为当前 Web Media 路径留下报告时，Browser 可能显示 **Web Media Debug（Web Media 调试）** 卡片。需要把问题交给规则维护者时，用 **Copy report（复制报告）** 复制最新的 source/detail 状态、selector 数量、最终 URL 和错误信息。只有报告里的浏览器会话仍可用时，**Open browser（打开浏览器）** 才能回到那次调试会话。
