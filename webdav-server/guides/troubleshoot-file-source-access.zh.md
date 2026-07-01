---
title: 排查文件操作和来源访问失败
description: 按 WebDAV 写入层、server source 层、resolver/upstream 层定位 Zwind 文件创建、打开、刷新和投影失败。
seoTitle: 排查 Zwind 文件操作、来源访问、解析器、夸克、SMB、RSS、Web Media 和 Emby 失败
keywords:
  - Zwind 文件操作失败
  - Zwind 来源访问失败
  - WebDAV 根目录只读
  - Zwind 解析器排查
  - 夸克 Cookie 失效
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/troubleshoot-file-source-access
order: 59
tags:
  - guide
  - troubleshooting
  - browser
  - resolver
  - webdav
publishedAt: 2026-07-01
updatedAt: 2026-07-01
draft: false
---

文件不能新建、重命名、打开、刷新或投影时，先判断失败发生在哪一层：

| 层级 | 常见现象 | 先查什么 |
| --- | --- | --- |
| WebDAV 写入层 | Browser 或 WebDAV 客户端里的 **New File / 新建文件**、**New Directory / 新建文件夹**、重命名、移动、复制、创建副本、删除、保存失败 | 当前 WebDAV 路径是否可写，是否在根目录 `/` 直接写入。 |
| server source 层 | 本地文件夹、SMB 共享或夸克云盘不能列目录或打开文件 | Files 权限/Provider 状态、SMB 主机/共享名/账号/路径、夸克 Cookie。 |
| resolver/upstream 层 | RSS、Web Media、夸克转存、Emby 投影目录为空、过期或刷新失败 | 解析器绑定路径、启用状态、缓存刷新，以及外部 feed、网页、夸克或 Emby endpoint。 |

下面截图使用英文 UI。中文界面中，**New File** 对应 **新建文件**，**New Directory** 对应 **新建文件夹**，**Resolver Bindings** 对应 **解析器绑定**，**Re-parse** 对应 **重新解析**，**App Logs** 对应 **应用日志**。

## 先看当前路径能不能写

打开 Browser，先看路径。写操作必须发生在支持写入的来源目录里。右下角 **+** 按钮是在当前目录中新建文件或文件夹的入口。

![Browser 可写文件夹中框选加号按钮。](/assets/docs/webdav-server/troubleshoot-file-source-access/boxed/browser-write-entry.png)

如果 **New File / 新建文件**、**New Directory / 新建文件夹**、重命名、移动、复制、创建副本、删除，或 Text Editor 保存失败，按下面检查：

| 检查项 | 含义 |
| --- | --- |
| 当前路径是 `/` | server 根目录只负责列出挂载来源，不是普通可写文件夹。先进入一个挂载目录。 |
| 当前路径是投影目录 | RSS、Web Media、Emby、夸克转存输出通常由解析器生成。很多投影条目看起来像文件或文件夹，但本身是只读的。 |
| 来源账号只有只读权限 | SMB、Files provider 或云盘权限可能拒绝写入，即使 Zwind 能显示这个目录。 |
| 目标位置已有同名项目 | 重命名、复制、移动或创建副本可能因为同名冲突失败。先刷新目录再操作。 |
| 其他客户端改动了同一项目 | 如果另一个 WebDAV 客户端移动或删除了同一个文件，先刷新 Browser，再基于当前列表重试。 |

最常见的是根目录规则：文件要建在 `/File_Provider_Storage/` 这类挂载目录下面，不要直接建在 `/`。

![Browser 根目录中框选挂载目录和根路径。](/assets/docs/webdav-server/troubleshoot-file-source-access/boxed/root-mount-list.png)

Browser 常规操作见 [在 Browser 中创建、编辑和整理文件](/zh/docs/webdav-server/guides/browser-file-operations/)。挂载名和本地文件夹规则见 [添加和管理本地数据文件夹](/zh/docs/webdav-server/guides/manage-local-data-folders/)。

## 重新检查本地文件夹访问

**Local FileSystem / 本地文件系统** server 依赖 iOS Files 或所选 Files provider 授权给 Zwind 的文件夹访问。

如果本地挂载以前可用，现在不能列目录、打开、保存或删除，按下面查：

| 情况 | 处理 |
| --- | --- |
| 文件夹在 Files 中被移动、改名、删除或移除 | 编辑 server，从当前位置重新添加这个文件夹。 |
| 文件夹来自 iCloud Drive 或第三方 Files provider | 打开 iOS Files，确认 provider 仍然登录，且这个文件夹能在 Files 里看到。 |
| Provider app 被卸载、退出登录或关闭 | 先恢复该 provider；如果 Zwind 保存的访问不再有效，再重新添加文件夹。 |
| 文件在 Files 里只是云端占位 | 在 Files 中先下载或打开一次，再回到 Zwind 重试。 |
| 读可以，写不行 | 检查 provider 或该目录是否允许写入。有些 provider 位置只读。 |

重新添加本地文件夹或改变 provider 状态后，停止并重新启动 server，让 WebDAV 客户端使用当前挂载。

## 重新检查 SMB 来源字段

SMB server 如果访问不到共享或配置路径，失败会发生在 source 层，还没到 WebDAV 写入逻辑。

检查 SMB server 配置里的这些字段：

| 字段 | 失败模式 |
| --- | --- |
| Host | IP 或主机名不可达、NAS 休眠、VPN 阻断局域网，或设备不在同一网络。 |
| Port | 通常是 `445`。只有 NAS 或电脑共享使用自定义端口时才改。 |
| Share Name | 填 SMB 导出的共享名，不要填 `smb://nas/Movies` 这种完整路径。 |
| Base Path | 填共享内部的文件夹路径。文件夹被改名或删除后，这个路径下面会列目录失败。 |
| Username、Password、Domain 或 Workgroup | 凭据要和 SMB server 一致。访客访问只有在 SMB server 对该共享允许 guest 时才可用。 |

如果 Browser 能看到 SMB 根目录，但某个子路径失败，主机和共享大概率可达，重点查 **Base Path / 基础路径**、权限和文件夹是否仍存在。如果完全列不出内容，先查 host、port、share name 和账号。

字段填写示例见 [配置 SMB 到 WebDAV](/zh/docs/webdav-server/guides/smb-to-webdav/)。

## 重新检查夸克云盘和夸克转存

夸克访问依赖 server 或解析器配置里保存的 Cookie。Cookie 过期、复制不完整，或 Cookie 所属账号无法访问目标内容时，Zwind 可能无法列出夸克云盘，也无法更新已转存资源。

按失败位置拆开看：

| 失败项 | 检查 |
| --- | --- |
| Quark Drive server 不能列云盘目录 | 在 Quark Drive server 中更新 Cookie，然后重启 server。 |
| Quark Search Import 目录没有生成结果 | 检查夸克转存解析器绑定、Cookie、搜索关键词文件夹，以及原分享是否仍可访问。 |
| **Update Imports / 更新转存** 完成但没有新文件 | 已跟踪的转存记录可能没有新增上游文件，或原分享链接已经不再暴露新增内容。 |
| 网页里夸克可用，但 Zwind 仍失败 | 从同一个已登录夸克账号重新复制 Cookie，保存到 Zwind。 |

Cookie 是账号令牌。不要把 Cookie 放进截图、issue 评论或公开日志。

## 重新检查解析器绑定路径和启用状态

进入 server 的 **Edit / 编辑**，检查 **Resolver Bindings / 解析器绑定**。解析器只有在绑定已保存、已启用，并且路径有效时才会出现在 WebDAV 中。

![Configure Server 页面中框选 Resolver Bindings。](/assets/docs/webdav-server/troubleshoot-file-source-access/boxed/resolver-bindings.png)

按这些规则查：

| 检查项 | 含义 |
| --- | --- |
| **Enabled / 启用** 关闭 | 绑定可以保存在配置里，但 WebDAV 中不会显示这个目录。打开后保存。 |
| 路径不在本地数据文件夹下 | Local FileSystem 绑定路径必须落在挂载的数据文件夹下，例如 `/File_Provider_Storage/Feeds`。除非你本来就有一个数据文件夹挂载为 `/Feeds`。 |
| 路径没有创建 | 保存时如果 Zwind 不能创建缺失文件夹，就到来源里手动创建，或在 server 可检查该路径时重新保存。 |
| 另一个绑定使用同一路径 | 已启用的绑定不能共享同一个规范化 WebDAV 路径。 |
| server 没有重启 | 修改绑定后，如果没有自动重启成功，手动停止并重新启动 server。 |

完整规则见 [配置解析器绑定](/zh/docs/webdav-server/guides/configure-resolver-bindings/)。

## 重新检查 RSS 和 Web Media 上游

RSS 和 Web Media 投影目录依赖外部 feed、网页、规则和网络访问。

| 解析器 | 常见原因 | 处理 |
| --- | --- | --- |
| RSS Projection | Feed URL 不可达、返回的不是 feed、跳到登录页，或请求超时 | 在浏览器中打开 feed URL；如果 URL 已变，编辑 `.rss` marker file 或绑定配置。 |
| RSS Projection | Feed 能打开，但投影条目过期 | 刷新 Browser 目录；如果绑定使用 materialize/archive，再按该绑定方式清理或重建输出。 |
| Web Media Projection | 来源页面结构变化 | 编辑 `.wm` 规则选择器，然后在投影目录中执行 **Re-parse / 重新解析**。 |
| Web Media Projection | 详情页或媒体 URL 被阻止、过期或要求登录 | 确认同一网络和浏览会话下，来源页面仍然暴露可播放媒体。 |
| Web Media Projection | 修改规则后输出没变 | 在当前 Web Media 路径执行 **Re-parse / 重新解析**，先让解析器输出失效，再重新加载 Browser。 |

![Web Media 路径中 Browser 操作菜单框选 Re-parse。](/assets/docs/webdav-server/troubleshoot-file-source-access/boxed/resolver-refresh-menu.png)

Web Media 规则字段见 [编写和调试 .wm 规则](/zh/docs/webdav-server/guides/write-debug-wm-rules/)。刷新行为见 [刷新解析器缓存和更新结果](/zh/docs/webdav-server/guides/refresh-resolver-cache-results/)。

## 重新检查 Emby endpoint 和账号

Emby 投影目录失败，通常是 Zwind 无法登录配置的 Emby server，或 Emby API 响应不可用。

检查 Emby 解析器绑定里的这些字段：

| 字段 | 检查 |
| --- | --- |
| Endpoint | 使用 iPhone 或 iPad 能访问的 Emby server URL，包含协议和端口，例如 `http://192.168.50.10:8096`。 |
| Username 和 Password | 使用能浏览媒体库的 Emby 账号。密码改过后，要更新绑定。 |
| Remote access | 如果 endpoint 不在局域网，确认 Emby server、反向代理或 VPN 从当前设备可访问。 |
| Library permission | 该账号必须有权限访问你想看到的媒体库。 |
| Search、Recently Added、Continue Watching | endpoint 可用但这些视图过期时，在对应投影路径执行 **Refresh Emby / 刷新 Emby**。 |

如果 Emby 根目录失败，先查 endpoint 和登录。如果只有某个媒体库或某个条目失败，再查媒体库权限、条目是否仍存在，以及播放源是否可访问。

## 复现后用 App Logs 辅助定位

可见错误不够具体时，先复现一次失败，再进入 **Settings / 设置** > **App Logs / 应用日志**。上方筛选 chip 可以区分 app 逻辑、原生 WebDAV、bridge 和解析器相关消息。

![App Logs 页面中框选来源筛选和 server/resolver 日志。](/assets/docs/webdav-server/troubleshoot-file-source-access/boxed/app-logs-screen.png)

按日志来源看：

| 日志来源 | 有用线索 |
| --- | --- |
| **SwiftWebDAV** | WebDAV 请求路径、状态码、路由错误、写入拒绝或投影分发。 |
| **Native Bridge** | server 启停和原生 bridge 结果。 |
| **App Logic** | 解析器刷新、转存、配置、权限和 app 已处理错误。 |
| **Flutter SDK** | app 捕获到的 Flutter framework 错误。 |

日志可能包含 server 名称、路径、URL、状态码和外部服务错误。分享前先阅读内容。如果日志指向 root write 或 read-only projection，就改 WebDAV 路径；如果指向 SMB、Files、夸克、RSS、Web Media 或 Emby，就回到对应 source 或 upstream 排查。
