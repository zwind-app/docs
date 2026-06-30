---
title: 使用夸克资源自动转存解析器
description: 在 Zwind 中绑定 Quark Search Import，创建空文件夹触发夸克资源搜索转存，刷新结果，检查更新，并理解旧转存记录迁移提示。
seoTitle: 使用夸克资源自动转存解析器 - Zwind WebDAV 指南
keywords:
  - 夸克资源自动转存
  - Quark Search Import
  - 夸克 WebDAV
  - Update Imports
  - Zwind 解析器绑定
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/quark-search-import
order: 47
tags:
  - guide
  - quark
  - resolver
  - import
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-06-30
draft: false
---

Quark Search Import（夸克资源自动转存解析器）可以把 QuarkDrive WebDAV server 里的一个目录变成搜索转存入口。你把解析器绑定到 `/Imports` 这类目录，在里面创建一个空文件夹，文件夹名就是搜索词；打开或刷新这个文件夹后，Zwind 会搜索网盘分享来源，并把匹配到的夸克资源转存到你的 QuarkDrive server 中。

下面截图使用英文界面；中文界面位置相同。截图只覆盖稳定的配置入口和 Browser 操作形态，不展示真实夸克账号的成功转存结果。

## 前置条件

你需要一个能正常启动的 QuarkDrive server，并且它已经填入有效的夸克 Cookie。如果 QuarkDrive server 还没配置好，先按[夸克云盘 server 文档](/zh/docs/webdav-server/guides/quark-drive-server/)完成 server 本身的配置。

你还需要拥有 **Quark Search Import / 夸克资源自动转存解析器** 权限。在首页点 **Explore Resolvers / 资源解析器**，打开 **Quark Search Import**，查看状态。如果这里显示锁定，再按解锁页购买该解析器或开通 Zwind VIP；如果显示 **Unlocked / 已解锁**，可以继续配置。

![Quark Search Import 详情页，框选 QuarkDrive 支持、解锁状态和使用摘要。](/assets/docs/webdav-server/quark-search-import/boxed/01-resolver-detail.png)

## 绑定转存目录

打开 QuarkDrive server 设置，在 **Resolver Bindings / 解析器绑定** 里点 **Add / 添加**，选择 **Quark Search Import**，保持启用，并填写绑定路径。常见路径是 `/Imports`。

![解析器绑定编辑器中选择 Quark Search Import，路径为 /Imports，并框选转存和更新相关选项。](/assets/docs/webdav-server/quark-search-import/boxed/03-binding-editor.png)

绑定路径必须是这个 server 能暴露出来的可用 WebDAV 路径。如果你的可用路径在某个挂载目录下面，比如 `/Files`，就绑定 `/Files/Imports`；如果 QuarkDrive server 可以直接使用 `/Imports`，就绑定 `/Imports`。

保存前看一下这些选项：

| 选项 | 作用 |
| --- | --- |
| **Top Results / 结果数量上限** | 一个搜索文件夹最多导入多少条排名靠前的结果。 |
| **Media Organization / 媒体整理方式** | 生成便于播放器刮削的虚拟媒体库视图，或保持转存资源原样。 |
| **Media Type / 媒体类型** | 帮助虚拟媒体库命名逻辑按电影、剧集、动漫、综艺或自动识别处理。 |
| **Auto Check Updates / 自动检查更新** | server 启动时检查已经转存过的分享是否有新增内容。 |
| **Update Check Interval / 更新检查间隔** | 同一个已转存资源两次自动检查之间的最短间隔。 |

保存 binding 后，再保存 server。server 停止时，Zwind 可能提示暂时无法检查或创建 `/Imports`；确认后保存即可，之后在使用前创建或确认这个目录存在。修改解析器绑定后，需要启动或重启 server，原生 WebDAV server 才会读取新的绑定配置。

![QuarkDrive server 设置中，Resolver Bindings 下已经出现 /Imports 的 Quark Search Import 绑定。](/assets/docs/webdav-server/quark-search-import/boxed/04-server-binding.png)

## 用空文件夹名触发搜索

启动 QuarkDrive server 后，在 Browser 中打开绑定目录。新建一个空文件夹，文件夹名就是要搜索的资源名称，例如 `Dune 2021`。

![Browser 中 Imports 目录下有一个名为 Dune 2021 的空子文件夹，右下角仍可看到新建按钮。](/assets/docs/webdav-server/quark-search-import/boxed/05-search-intent-folder.png)

打开这个新文件夹，或刷新后重新进入它。进入目录会触发 materialization/import 任务：Zwind 会按 binding 设置搜索分享来源，筛选匹配的夸克资源，并把资源转存到这个文件夹中。

## 等待并刷新结果

搜索和转存需要一点时间。打开搜索文件夹后，回到 Browser 刷新当前目录，或者退出后重新进入。转存成功后，这个文件夹里会出现导入后的资源结构。根据 **Media Organization / 媒体整理方式** 的设置，你可能看到原始转存目录、虚拟媒体库视图；如果启用了 **Show Debug Files / 显示调试文件**，还会看到解析器诊断文件。

如果目录一直为空或任务失败，按下面几项排查：

| 检查项 | 处理方式 |
| --- | --- |
| 搜索词 | 重命名或重新创建空文件夹，使用更准确的片名、年份或关键词。 |
| 夸克 Cookie | 确认 QuarkDrive server 能启动，并且能正常浏览普通夸克云盘内容。 |
| 网络 | 确认设备可以访问夸克和当前配置的搜索服务。 |
| 解析器权限 | 重新打开 resolver 详情或 binding editor，确认 Quark Search Import 已解锁。 |

转存完成后的目录结构取决于你的夸克账号、搜索来源和媒体整理方式，所以这里的截图停在触发搜索的文件夹，不展示某个固定账号下的转存结果。

## 手动检查已转存资源更新

当 Browser 当前路径位于 Quark Search Import 绑定目录内时，右下角操作菜单可能出现 **Update Imports / 更新转存**。这个动作只检查已经被该 resolver 转存并记录过的资源，用来发现原分享后续新增的文件。

**Update Imports / 更新转存** 不是“重新搜索所有新关键词”。要搜索新的资源名称，仍然是在绑定目录下新建另一个空文件夹并打开它；要重试失败或匹配不理想的资源，可以改文件夹名，或创建新的搜索文件夹。

如果你在某个已转存的搜索文件夹内执行 **Update Imports**，Zwind 会尽量只检查这个搜索意图；如果在绑定目录根部执行，则按绑定范围检查。

## 旧转存记录迁移提示

如果 Browser 弹出 **Import Records Found / 发现转存记录**，表示 Zwind 发现当前夸克文件夹可能对应另一台 server 或另一条 binding 以前生成的 materialization 记录。恢复配置、修改绑定路径、重建 server 后可能会出现这个提示。

选择 **Migrate This Folder / 迁移此文件夹**，会把当前文件夹关联到已有记录，让后续更新检查继续追踪它。如果出现 **Migrate Matching Folders in This Binding / 迁移此绑定中的匹配文件夹**，表示可以批量恢复当前绑定下兼容文件夹的更新追踪。

迁移只恢复更新追踪元数据；它不会重新导入文件、不会重新搜索新关键词，也不会复制已有资源。
