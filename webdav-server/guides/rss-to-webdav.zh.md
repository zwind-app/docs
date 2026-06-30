---
title: 把 RSS 或 OPML 投影成 WebDAV 目录
description: 在 Zwind 中把 RSS Projection 绑定到 WebDAV 目录，创建 .rss 标记文件，并把 RSS、Atom 或 OPML 来源作为虚拟目录浏览。
seoTitle: 把 RSS 和 OPML 投影成 WebDAV 目录 - Zwind 指南
keywords:
  - RSS to WebDAV
  - OPML to WebDAV
  - RSS Projection
  - WebDAV RSS 目录
  - .rss 标记文件
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/rss-to-webdav
order: 46
tags:
  - guide
  - rss
  - opml
  - projection
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-06-30
draft: false
---

RSS Projection 可以把 RSS、Atom 或 OPML URL 变成 WebDAV 目录。你先把解析器绑定到一个目录，比如 `/Feeds`，再把以 `.rss` 结尾的标记文件放进去。Zwind 会把这些标记文件投影成可浏览的 feed 目录，里面包含 feed metadata、条目文件夹、Markdown 摘要，以及 feed 提供的媒体或链接文件。

下面截图使用英文界面；中文界面位置相同。**RSS Projection** 对应 **RSS 解析器**，**Text Editor** 对应 **文本编辑器**，**Materialize on Resolve** 对应解析时持久化当前窗口。

## 绑定 RSS Projection 目录

打开 server 设置，新增或编辑解析器绑定，选择 **RSS Projection / RSS 解析器**，保持启用，并把绑定路径设为保存 feed 标记文件的目录。常见做法是把一个数据文件夹挂载成 `/Feeds`，然后把 RSS Projection 也绑定到 `/Feeds`。

![Server 设置中框选 /Feeds 的 RSS Projection 绑定。](/assets/docs/webdav-server/rss-to-webdav/boxed/rss-binding.png)

绑定路径必须落在这个 WebDAV server 暴露的数据文件夹下面。如果你的数据文件夹在 Browser 里显示为 `/Files`，可以绑定 `/Files/Feeds`；如果数据文件夹本身挂载成 `/Feeds`，就绑定 `/Feeds`。

保存新的绑定或修改绑定后，需要从首页重启或重新启动这个 server。原生 WebDAV server 会在启动时读取 resolver binding。如果添加绑定时 RSS Projection Resolver 被锁定，先按弹出的解锁页购买该 resolver 或开通 Zwind VIP，再继续配置。

## 创建 .rss 标记文件

在 Browser 里打开绑定目录。新建一个以 `.rss` 结尾的文本文件，例如 `news.rss`、`podcasts.rss` 或 `reading-list.rss`。

用 **Text Editor / 文本编辑器** 打开这个文件，写入一行 URL，然后点 **Save / 保存**。这个 URL 可以是 RSS、Atom，也可以是 OPML 文件地址。

![Text Editor 中的 .rss 标记文件，内容是一行 feed URL。](/assets/docs/webdav-server/rss-to-webdav/boxed/rss-url-text-editor.png)

`.rss` 文件内容只写 URL，不要写成 `source=...` 这类键值格式。你可以在 Browser 里手动创建，也可以从其他 WebDAV 客户端写入；如果使用 Feed View 的 Add Feed，它也会把订阅来源保存成 `.rss` 标记文件。

## 刷新后浏览投影目录

回到 Browser，刷新或重新进入绑定目录。RSS 绑定目录里的 `.rss` 文件会显示为可进入的条目。

![Browser 中 /Feeds 目录下的 .rss 标记文件。](/assets/docs/webdav-server/rss-to-webdav/boxed/marker-files.png)

打开其中一个标记文件，例如 `last-week-in-ai.rss`。Zwind 会解析 feed，并把当前 feed 窗口显示成目录。feed 级别的 `feed.json`、`feed.xml` 会和条目文件夹一起出现。

![解析后的 .rss 目录，包含 feed item 文件夹、feed.json 和 feed.xml。](/assets/docs/webdav-server/rss-to-webdav/boxed/projected-feed-items.png)

进入某个条目文件夹，可以看到这个 feed item 生成的文件。RSS 文章通常会有 `item.json`、`link.url` 和 Markdown 摘要；如果 feed 带媒体附件，还可能根据 media mode 显示媒体代理文件或链接文件。

![RSS 条目文件夹中包含 item.json、link.url 和 Markdown 摘要。](/assets/docs/webdav-server/rss-to-webdav/boxed/item-folder-output.png)

## 使用 OPML 来源

`.rss` 标记文件里也可以写 OPML URL。这样 resolver 会读取 OPML outline，把分类和 feed 变成多层目录。进入某个子 feed 时才会继续解析那个 feed，因此 OPML 里某个慢源不会阻塞整个 OPML 根目录。

Feed View 的 **Add Feed / 添加订阅** 处理 OPML 的方式不同。选择 **OPML Import / OPML 导入** 后，Zwind 会先发现 outline，再把你勾选的每个 feed 保存成单独的 `.rss` 文件。需要分别删除、重命名、分组或同步多个 feed 时，用 Add Feed 更合适；如果你希望整个 OPML outline 保持为一个投影树，就把 OPML URL 直接写进一个 `.rss` 标记文件。

## materialize、archive 和 cache

需要持久化或缓存时，进入 binding editor。RSS Projection 的设置里可以看到 **Materialize on Resolve**、**Archive Retention Days**、**Maximum Archived Items**、**Cache Full Text** 和 **Download Images**。

![RSS Projection 绑定设置中框选 materialize、archive retention、full-text cache 和 image download。](/assets/docs/webdav-server/rss-to-webdav/boxed/materialize-settings.png)

这些行为只有在对应 resolver 设置启用时才会发生：

| 设置 | 用途 |
| --- | --- |
| **Materialize on Resolve** | 解析 feed 时把当前 RSS 窗口持久化下来，让当前条目在上游 feed 变化或临时不可访问后仍可读取。 |
| **Archive Retention Days** | 控制已经离开当前 feed 窗口的持久化条目按天清理。`0` 表示不按时间清理。 |
| **Maximum Archived Items** | 限制离开当前窗口后的历史条目保留数量。`0` 表示这个数量限制不设上限。 |
| **Cache Full Text** | 为 materialized RSS item 保留全文缓存行为。 |
| **Download Images** | 为 materialized RSS item 持久化图片引用。 |

materialize 和 cache 适合离线访问、feed 只保留较短近期窗口，或媒体客户端需要稳定文件名的场景。它们会占用本地存储，并不表示 Zwind 默认会保存所有历史内容。archive 保存的是曾经出现在当前 feed 窗口、后来离开窗口的条目，并受 retention 和最大条目数限制。
