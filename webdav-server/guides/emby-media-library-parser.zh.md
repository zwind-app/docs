---
title: 使用 Emby 媒体库解析器
description: 将 Emby 媒体库解析器绑定到 WebDAV 路径，在 Zwind Browser 或 WebDAV 客户端中浏览媒体库、最近入库、继续观看、搜索目录和可播放媒体文件。
seoTitle: "在 Zwind WebDAV Server 中使用 Emby 媒体库解析器"
keywords:
  - Emby
  - Emby WebDAV
  - 媒体库解析器
  - Zwind Browser
  - WebDAV 媒体服务器
productSlug: webdav-server
section: 指南
locale: zh
translationOf: webdav-server/guides/emby-media-library-parser
parent: guides
order: 50
tags:
  - guide
  - emby
  - media
  - resolver
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-07-01
draft: false
---

Emby 媒体库解析器会用一个 Emby 账号连接媒体服务器，并把媒体库投影成 WebDAV 目录。绑定保存并重新启动 server 后，Browser 和 WebDAV 客户端都能打开媒体库、最近入库、继续观看、搜索结果、媒体文件、海报、元数据和播放辅助文件。

截图使用英文界面和本地 Emby fixture。实际使用时，把示例里的 endpoint 和账号换成你的 Emby server 信息。

## 绑定到一个 WebDAV 路径

进入 server 配置页，在 **Resolver Bindings（解析器绑定）** 里新增或编辑一条绑定。解析器选择 **Emby Library Projection Resolver（Emby 媒体库投影解析器）**，绑定路径就是这个 Emby 目录在 WebDAV 中出现的位置。

![Configure Server 页面中，Resolver Bindings 下框选了 Emby 解析器绑定。](/assets/docs/webdav-server/emby-media-library-parser/boxed/01-server-binding.png)

截图里的路径是 `/copy-audit-files/Emby`，因为文档 fixture 把本地数据目录暴露在 `/copy-audit-files` 下。你可以使用 server 暴露范围内的任意路径，例如 `/Emby`，或某个数据目录下面的 `/Files/Emby`。

解析器绑定会在 server 启动时加载。改完绑定后保存绑定、保存 server；如果 server 已经在运行，需要重新启动这台 server。

## 填写 Emby 连接信息

在 **Edit Resolver Binding（编辑解析器绑定）** 页面里，确认 **Resolver（解析器）** 是 **Emby Library Projection Resolver**，**Enabled（启用）** 已打开，然后填写 **Configuration（配置）**。

![Edit Resolver Binding 页面中，框选 Emby Endpoints、Username、Password 和 Media Delivery。](/assets/docs/webdav-server/emby-media-library-parser/boxed/03-password-media-delivery.png)

主要字段如下：

| 字段 | 填什么 |
| --- | --- |
| **Path（路径）** | 这个 Emby 投影在 WebDAV 里的路径。它决定 Browser 和 WebDAV 客户端从哪里进入 Emby 目录。 |
| **Emby Endpoints（Emby 端点）** | Emby server 的基础地址，例如 `https://emby.example.com` 或 `http://192.168.1.20:8096`。Zwind 用它调用 Emby API，也用它生成播放请求。 |
| **Username（用户名）** 和 **Password（密码）** | 要暴露媒体库的 Emby 账号。最近入库、继续观看、搜索结果都按这个账号的权限和播放状态返回。使用 API key/token 的环境可以改填 **Token（令牌）**。 |
| **Media Delivery（媒体交付）** | WebDAV 客户端打开媒体文件时的播放方式，见下文“代理播放和重定向播放”。 |
| Cache TTL 字段 | 控制媒体库、元数据、图片、播放信息可以缓存多久。截图 fixture 使用 `0`，表示不复用缓存；媒体库变化不频繁时可以设为更长时间。 |
| **Proxy Read-Ahead (MB)（代理预读）** | 代理播放时 Zwind 可以提前读取的媒体数据量，只影响 **Proxy Media（代理媒体）** 模式。 |

## 在 Browser 中打开 Emby 根目录

回到 Browser，打开刚才设置的绑定路径。这个路径会显示为 Emby 投影目录，不再只是底层本地文件夹。

![Browser 中的 Emby 根目录，框选 Continue Watching、Libraries、Recently Added、Search 等入口。](/assets/docs/webdav-server/emby-media-library-parser/boxed/04-emby-root.png)

常见入口如下：

| 目录 | 内容 |
| --- | --- |
| **Libraries（媒体库）** | 当前 Emby 账号可见的媒体库，例如 Movies、TV Shows。进入某个库后，只浏览这个库下面的条目。 |
| **Recently Added（最近入库）** | Emby 为这个账号返回的最新入库媒体。 |
| **Continue Watching（继续观看）** | 这个 Emby 用户有播放进度、可以继续看的条目。如果该用户没有可续播条目，这个目录可以为空。 |
| **Movies、Series、Genres、People、Studios、Collections、Top** | 根据 Emby 媒体库和条目元数据生成的视图。哪些目录有内容，取决于 Emby server 对该账号返回的数据。 |
| **Search（搜索）** | 可写的意图目录。在它下面新建子文件夹，就会触发一次 Emby 搜索。 |

同一组目录也可以从 WebDAV 客户端访问。例如 server 地址是 `http://192.168.1.10:8080`，绑定路径是 `/Emby`，客户端打开 `http://192.168.1.10:8080/Emby/` 即可。

## 打开一个媒体条目

从媒体库、最近入库、继续观看或搜索结果进入某个媒体条目目录。Zwind 会把可播放入口和辅助文件放在同一个目录里。

![Emby 媒体条目目录中，框选可播放媒体、.strm、metadata 和 playback.json 文件。](/assets/docs/webdav-server/emby-media-library-parser/boxed/06-media-item-files.png)

常见文件含义：

| 文件 | 含义 |
| --- | --- |
| `Aurora Station (2026) - Direct 1080p.mp4` 这类媒体文件 | WebDAV 中的可播放媒体入口。代理播放时，Zwind 读取 Emby 流并把数据返回给客户端；重定向播放时，这个入口会把客户端指向 Emby 的直连播放地址。 |
| `.strm` 文件 | 给支持 `.strm` 的播放器使用的流地址文件。 |
| `metadata.json` | 从 Emby 条目整理出的结构化元数据。 |
| `metadata.md` | 便于阅读的条目元数据摘要。 |
| `playback.json` | Emby 为这个账号和条目返回的播放源信息。 |
| `poster.jpg`、`backdrop.jpg` | Emby 返回的海报和背景图。 |
| `bing.url`、`douban.url` | 根据标题、年份等信息生成的辅助链接文件；元数据不足时可能不会出现。 |

如果某个 Emby 条目对当前账号没有可播放来源，目录里仍可能有元数据和图片，但不会出现对应的媒体文件入口。

## 用 Search 意图目录搜索

**Search（搜索）** 不是输入框，而是一个可写的 WebDAV 意图目录。在 **Search** 下新建普通子文件夹，文件夹名就是搜索词，例如 `aurora`、片名、人名或年份。打开这个子文件夹时，Zwind 会调用 Emby 搜索并显示结果条目。

![Browser 中打开 Search/aurora 后，显示一个 Emby 搜索结果目录。](/assets/docs/webdav-server/emby-media-library-parser/boxed/08-search-results.png)

搜索词完全来自子目录名。`/Emby/Search/aurora` 搜索 `aurora`，`/Emby/Search/2026` 搜索 `2026`。结果仍受 Emby 账号权限限制。

## 代理播放和重定向播放

**Media Delivery（媒体交付）** 决定 WebDAV 客户端打开媒体文件时，Zwind 怎样处理播放请求。

| 模式 | 行为 |
| --- | --- |
| **Proxy Media（代理媒体）** | WebDAV 文件 URL 保持在 Zwind server 上。客户端的 Range 请求发给 Zwind，Zwind 再从 Emby 读取对应媒体数据并返回给客户端。**Proxy Read-Ahead (MB)（代理预读）** 只在这个模式下生效。客户端能访问 Zwind、但不能或不想直连 Emby 时使用这个模式。 |
| **Redirect to Emby（重定向到 Emby）** | Zwind 为媒体入口返回 Emby 的直连播放 URL。客户端必须能访问 Emby endpoint，并且能处理 Emby 的直连播放地址。此时 Zwind 不转发媒体字节。 |
| **Auto（自动）** | 当选中的 Emby 媒体源有已知大小且可以代理时，Zwind 使用代理播放；不满足这个条件时回退到重定向播放。 |

修改 **Media Delivery（媒体交付）** 会影响后续解析出的播放信息。如果 **Playback Cache TTL（播放缓存时间）** 仍在生效，需要清掉缓存或等缓存过期后再检查新模式。
