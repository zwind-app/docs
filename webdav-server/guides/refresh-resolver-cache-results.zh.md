---
title: 刷新解析器缓存和更新结果
description: 说明 Browser 右下角菜单里的更新转存、重新解析和刷新 Emby 分别在哪些目录出现，以及它们刷新哪一层解析器结果。
seoTitle: 刷新 Zwind WebDAV Server 解析器缓存和结果
keywords:
  - 解析器缓存
  - 更新转存
  - 重新解析
  - 刷新 Emby
  - Zwind Browser
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/refresh-resolver-cache-results
order: 52
tags:
  - guide
  - resolver
  - projection
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-07-01
draft: false
---

有些解析器结果不是每次打开目录都从头抓取。Browser 进入投影目录后，右下角菜单会根据当前位置增加解析器专用动作：夸克转存目录里是 **Update Imports / 更新转存**，Web Media 目录里是 **Re-parse / 重新解析**，Emby 目录里是 **Refresh Emby / 刷新 Emby**。

这些动作适合处理“当前投影结果过旧”的情况：夸克已经转存过的资源没有显示后续新增文件，Web Media 规则或网页结构变了，或者 Emby 的媒体库、继续观看、搜索结果、播放信息需要重新从 Emby 获取。

下面截图使用英文界面；中文界面位置相同。

## 先看对应关系

| Browser 动作 | 出现位置 | 刷新内容 |
| --- | --- | --- |
| **Update Imports / 更新转存** | **Quark Search Import / 夸克资源自动转存解析器** 绑定目录内，例如 `/Imports` 或 `/Imports/Dune 2021` | 当前绑定或当前搜索意图目录里，已经被这个解析器记录过的夸克转存结果。 |
| **Re-parse / 重新解析** | **Web Media Projection / 网页媒体解析器** 绑定目录内，包括 `.wm` 投影目录和条目目录 | 当前路径对应的 source list、item detail、media discovery 或 expansion 缓存。 |
| **Refresh Emby / 刷新 Emby** | **Emby Library Projection Resolver / Emby 媒体库解析器** 绑定目录内，包括根目录、媒体库、条目、Recently Added、Continue Watching 和 Search 路径 | 当前路径范围内的 Emby 媒体库树、搜索结果、最近入库、继续观看、条目元数据视图和播放响应缓存。 |

它们和 Browser 的普通下拉刷新不是同一个动作。普通刷新只是重新读取当前 WebDAV 目录列表；这些解析器动作会先让对应 resolver 丢弃某一层结果，再重新加载当前路径。

## 更新夸克已转存资源

进入 Quark Search Import 绑定目录下的某个路径，点右下角菜单，会看到 **Update Imports / 更新转存**。

![夸克转存目录的 Browser 右下角菜单，框选 Update Imports。](/assets/docs/webdav-server/refresh-resolver-cache-results/boxed/quark-update-menu.png)

当一个搜索文件夹已经完成过转存，而原始分享链接后来新增了文件时，用 **Update Imports / 更新转存** 检查后续更新。

当前位置决定检查范围：

| 当前 Browser 路径 | 作用范围 |
| --- | --- |
| 绑定根目录，例如 `/Imports` | 检查这个绑定里已有转存记录。 |
| 搜索意图目录，例如 `/Imports/Dune 2021` | 只检查这个搜索意图目录的已有转存记录。 |
| 搜索意图目录下的子路径 | 仍按绑定下第一层目录作为搜索意图，例如 `/Imports/Dune 2021/Library` 仍指向 `/Imports/Dune 2021`。 |

这个动作不会重新搜索一个新关键词。它读取解析器保存的转存记录，检查原始分享链接，把新增条目导入到已经跟踪的目标目录，更新已知条目列表，并让对应搜索意图目录的列表失效后重新加载。如果当前目录还没有这个解析器跟踪到的已转存记录，结果可能是 0 个更新。

要搜索另一个片名或关键词，仍然是在绑定目录下新建一个空文件夹，再打开它。

## 重新解析 Web Media

进入 Web Media 绑定目录下的 `.wm` 投影目录或条目目录，打开右下角菜单，会看到 **Re-parse / 重新解析**。

![Web Media 条目目录的 Browser 右下角菜单，框选 Re-parse。](/assets/docs/webdav-server/refresh-resolver-cache-results/boxed/web-media-reparse-menu.png)

当源网页更新、`.wm` 规则被修改、条目页里的媒体地址变了，或者当前结果还停留在旧解析结果时，用 **Re-parse / 重新解析**。

当前路径决定刷新哪一层：

| 当前 Browser 路径 | 刷新层级 |
| --- | --- |
| 包含 `.wm` 标记文件的 Web Media 绑定目录 | 重新解析当前目录里每个 `.wm` 标记文件的 source list；不会递归扫描所有子目录。 |
| 某个 `.wm` 投影目录或它的 `source.json` | 重新解析这个 marker 的源列表页，重建条目列表。 |
| 使用 expansion 规则的顶层条目目录 | 刷新这个条目的 expansion 结果，也就是它下面展开出来的子条目。 |
| 普通条目目录，或 `detail.url`、`media.url`、已解析出的媒体文件所在路径 | 刷新这个条目的 detail/media discovery 结果。 |

动作完成后，Browser 会重新加载当前路径。完成弹窗里的 scope 会显示 `source`、`detail`、`expansion` 或 `directory`，对应上面的刷新层级。

## 刷新 Emby 投影

进入 Emby 绑定目录下的路径，点右下角菜单，会看到 **Refresh Emby / 刷新 Emby**。它会按当前路径清掉对应的 Emby 投影缓存。

![Emby 根目录的 Browser 右下角菜单，框选 Refresh Emby。](/assets/docs/webdav-server/refresh-resolver-cache-results/boxed/emby-root-refresh-menu.png)

当 Emby 已经有新内容或状态变化，而 Zwind Browser 还显示旧结果时使用它：新入库内容、元数据变更、继续观看变化、搜索结果变化，或播放源信息需要重新获取。

当前位置对应的刷新范围如下：

| 当前 Browser 路径 | 刷新层级 |
| --- | --- |
| Emby 根目录，例如 `/Emby` | 清掉这个绑定下的 Emby 会话和全部 Emby 投影缓存。 |
| `/Emby/Search/<query>` | 清掉 Emby 搜索结果缓存。 |
| `/Emby/Recently Added` | 清掉最近入库列表。 |
| `/Emby/Continue Watching` | 清掉继续观看列表。 |
| `/Emby/Movies` 或 `/Emby/Series` | 清掉这些顶层视图的条目分页缓存。 |
| `/Emby/Genres`、`/Emby/People`、`/Emby/Years` 或 `/Emby/Collections` | 清掉对应筛选分类和结果缓存。 |
| 媒体库路径和媒体条目目录 | 刷新媒体库树这一侧的投影；当路径落在媒体库树解析范围内时，也会清掉相关播放响应缓存。 |

Search 下面的查询目录也有同一个入口。进入具体查询结果路径后点 **Refresh Emby / 刷新 Emby**，只刷新这个搜索结果范围。

![Emby Search 结果路径的 Browser 右下角菜单，框选 Refresh Emby。](/assets/docs/webdav-server/refresh-resolver-cache-results/boxed/emby-search-refresh-menu.png)

如果你从 Zwind 的 Video Player 播放 Emby 媒体，播放进度上报成功后，Continue Watching 相关缓存也会自动失效。**Refresh Emby / 刷新 Emby** 是 Browser 里手动处理当前路径旧数据的入口。
