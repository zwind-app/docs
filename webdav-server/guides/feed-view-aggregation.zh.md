---
title: 使用 Feed View 聚合内容
description: 在 Zwind Feed View 中添加 RSS、OPML、YouTube、Bilibili、Reddit 和已有 server 来源，并筛选、阅读、跳转 Browser 或移除失效 feed。
seoTitle: 使用 Zwind Feed View 聚合 RSS 和网页内容 - Zwind 指南
keywords:
  - Zwind Feed View
  - RSS 阅读器 WebDAV
  - OPML 导入
  - YouTube RSS
  - Bilibili Web Media
  - Reddit RSS
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/feed-view-aggregation
order: 45
tags:
  - guide
  - feed-view
  - rss
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Feed View 是 Zwind 里用来集中阅读订阅内容的界面。RSS、OPML、YouTube、Reddit 来源会保存成 RSS 标记文件；Bilibili 来源会保存成 Web Media 规则文件。已经在运行的 server 如果暴露了 projection feed，也会在刷新后出现在 Feed View 列表里。

下面截图使用英文界面；中文界面位置相同。**Feed View** 对应中文里的 **订阅视图**，**Add Feed** 对应 **添加订阅**，**Reveal in Folder** 对应 **在文件夹中显示**，**Remove from List** 对应 **从列表移除**。

## 打开 Feed View

在首页选中一个运行中的 server，点 **Browse as Feed / 以 Feed 形式浏览内容**；也可以打开首页侧边栏，点 **Feed View / 订阅视图**。进入后会看到手动创建的 **Feed Groups / 订阅组**、可搜索的 **Feeds / 订阅源** 列表，以及 **RSS** 这样的来源分组。

![Feed View 中框选订阅组、搜索框、可用订阅源和不可用订阅源状态。](/assets/docs/webdav-server/feed-view-aggregation/boxed/feed-list.png)

点某个 feed 行会打开它的时间线。长按 feed 行可以打开这个 feed 的操作菜单。

## 添加来源

点 **+**，再点 **Add Feed / 添加订阅**。在表单里点 **Source Type / 来源类型**，选择要创建的来源。

![Source Type 菜单列出 Site / Feed URL、OPML Import、YouTube Channel、Reddit Subreddit 和 Bilibili UP。](/assets/docs/webdav-server/feed-view-aggregation/boxed/source-types.png)

不同来源这样填写：

| 来源类型 | 填什么 | Zwind 会保存什么 |
| --- | --- | --- |
| **Site / Feed URL / 网站或 Feed URL** | 网站 URL、RSS URL 或 Atom URL。 | 发现结果里的一个或多个 `.rss` 标记文件。 |
| **OPML Import / OPML 导入** | OPML URL，或通过 **Choose OPML File / 选择 OPML 文件** 选本地 OPML。 | 每个被选中的 outline 项会保存成一个 `.rss` 标记文件。 |
| **YouTube Channel / YouTube 频道** | 频道 URL、频道 feed URL 或 `@handle`。 | YouTube RSS `.rss` 标记文件。 |
| **Reddit Subreddit** | 例如 `r/selfhosted` 这样的 subreddit 名称，或 subreddit URL。 | Reddit RSS `.rss` 标记文件。 |
| **Bilibili UP / Bilibili UP 主** | Bilibili UID 或空间 URL。 | Web Media `.wm` 规则文件。 |

填好来源后点 **Discover / 发现**。检查发现结果，取消不想保存的候选项，选择保存位置，然后点 **Add / 添加**。

## 选择正确的保存目录

Add Feed 不是把内容保存到普通目录里，而是把标记文件保存到对应解析器绑定目录下。这样同一份来源既能在 Browser 里浏览，也能被 Feed View 聚合。

![OPML Import 表单框选 OPML 输入、Discover 按钮和解析器绑定检查。](/assets/docs/webdav-server/feed-view-aggregation/boxed/opml-form.png)

RSS、OPML、YouTube、Reddit 要选择 **RSS Projection / RSS 解析器** 绑定下的目录，常见路径是 `/Feeds`。Bilibili 要选择 **Web Media Projection / Web Media 解析器** 绑定下的目录。如果表单显示 **RSS Projection binding required / 需要 RSS Projection 绑定**，或显示对应的 Web Media 提示，就先从这里打开 resolver guide，或者回到 server 设置里配置解析器绑定后再保存。

如果某个 server 里已经有 feed 标记文件或 Web Media projection 目录，启动这个 server 后回到 Feed View；列表没有更新时点右上角刷新。

## 筛选和分组

用 **Search feeds / 搜索订阅源** 按标题或来源缩小列表。点 **RSS** 这样的分组标题可以展开或收起一类来源。

在 **+** 菜单里点 **New Feed Group / 新建订阅组**，可以把已有 feed 组成一个手动阅读列表。订阅组打开的是合并时间线，不会复制或移动原来的 feed 文件。

## 查看条目

点 feed 或订阅组进入时间线。Feed View 会按最近更新时间排序，把文章、图片、音频、视频条目放在同一个阅读界面里。

![Feed 时间线框选同一个 feed 里的文章和图片条目。](/assets/docs/webdav-server/feed-view-aggregation/boxed/feed-timeline.png)

点条目会用 Zwind 的默认打开方式打开。RSS 文章通常会打开生成的 Markdown 文章；图片、音频、视频资源会在条目暴露可打开资源时进入对应的内置查看器或播放器。

## 跳转到 Browser 中的来源目录

长按时间线条目，点 **Reveal in Folder / 在文件夹中显示**，可以跳到这个条目背后的 WebDAV 目录。需要用 Browser 刷新、排序、做文件操作，或查看同一 projection 目录里的其他文件时，用这个入口。

![条目操作菜单框选 Open 和 Reveal in Folder。](/assets/docs/webdav-server/feed-view-aggregation/boxed/item-menu.png)

feed 行的长按菜单里也有 **Reveal in Folder / 在文件夹中显示**。只有当这个 feed 还能对应到当前运行中的 server 时，这个动作才可用；如果 feed 已不可用，Feed View 找不到当前 server 路径，就会禁用跳转。

## 移除不可用 feed

长按不可用 feed，点 **Remove from List / 从列表移除**。

![不可用 feed 菜单框选 Remove from List。](/assets/docs/webdav-server/feed-view-aggregation/boxed/unavailable-feed-menu.png)

这个操作只清理 Feed View 本地目录缓存里的失效行，不会删除 WebDAV server 上的 `.rss` 或 `.wm` 文件。它出现的条件是：Feed View 还记得这个 feed，但当前扫描没有找到它，例如 server 被移除、解析器绑定变更、feed 文件被移动，或 server 没有运行。
