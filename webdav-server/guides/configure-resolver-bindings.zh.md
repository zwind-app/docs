---
title: 配置解析器绑定
description: 说明 Zwind WebDAV Server 中解析器绑定的路径、启用状态、付费解锁、数据文件夹范围、自动创建文件夹和保存后重启规则。
seoTitle: 配置 Zwind WebDAV Server 解析器绑定
keywords:
  - 解析器绑定
  - WebDAV resolver path
  - Zwind 资源解析器
  - WebDAV 虚拟目录
  - resolver 解锁
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/configure-resolver-bindings
order: 51
tags:
  - guide
  - resolver
  - projection
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-07-01
draft: false
---

解析器绑定决定某个 resolver 出现在当前 WebDAV server 的哪一个目录入口。它不展开 RSS、Web Media、夸克转存或 Emby 的全部业务配置；这一层只负责选择 resolver、设置 WebDAV 入口路径、启用或停用，以及填写这个 resolver 暴露在 **Configuration / 配置** 里的绑定级选项。

下面截图使用英文界面；中文界面位置相同。**Resolver Bindings** 对应 **解析器绑定**，**Enabled** 对应 **启用**，**Path** 对应 **路径**。

## 查看 resolver 是否可用

打开 **Explore Resolvers / 资源解析器**，进入要使用的 resolver 详情页，先看 **Storage / 存储** 和 **Status / 状态**。**Storage** 表示这个 resolver 支持哪些 server 存储类型；**Status** 表示当前账号或设备是否已经解锁。

![resolver 详情页中框选支持的存储类型和解锁状态。](/assets/docs/webdav-server/configure-resolver-bindings/boxed/resolver-detail-status.png)

带单独商品解锁的 resolver 必须先可用，绑定才能保存。如果未解锁，点击保存绑定时 Zwind 会弹出 resolver 解锁页。单独买断只解锁该 resolver；Zwind VIP 会解锁 VIP 覆盖的全部 resolver 扩展；看广告领取的 VIP 在有效期内也会让这些 resolver 可用。

## 进入 Resolver Bindings

打开 server，点 **Edit / 编辑**，在 **Configure Server / 配置 Server** 页面找到 **Resolver Bindings / 解析器绑定**。第一行显示当前存储类型可用的 resolver，并提供 **Add / 添加** 入口；已有绑定显示在下面。

![Configure Server 页面中框选 Available Resolvers、Add 和已有绑定。](/assets/docs/webdav-server/configure-resolver-bindings/boxed/server-resolver-bindings.png)

点 **Add / 添加** 可以新增绑定。点已有绑定行，再选择 **Edit Binding / 编辑绑定** 或 **Remove Binding / 移除绑定**。绑定可以保存为停用状态；**Enabled / 启用** 关闭后，这个绑定不会出现在 WebDAV 目录树里。

## 设置 Resolver、Enabled 和 Path

在 **Add Resolver Binding / 添加解析器绑定** 或 **Edit Resolver Binding / 编辑解析器绑定** 页面，选择 resolver；需要让目录出现在 WebDAV 中时保持 **Enabled / 启用** 打开；把 **Path / 路径** 填成这个 resolver 在 WebDAV 树里的入口。

![解析器绑定编辑器中框选 Resolver、Enabled 和 Path。](/assets/docs/webdav-server/configure-resolver-bindings/boxed/binding-editor-path-enabled.png)

**Path / 路径** 是客户端真正打开的目录。如果把 RSS Projection 绑定到 `/Feeds`，WebDAV 客户端就从 `/Feeds` 进入 RSS resolver；如果把 Emby 绑定到 `/Media/Emby`，客户端就打开 `/Media/Emby`。

路径规则：

| 规则 | 含义 |
| --- | --- |
| 使用非根绝对路径 | 编辑器接受 `/Feeds`、`/Files/WebMedia`、`/Media/Emby` 这类路径；`/` 或不以 `/` 开头的路径会被拒绝。 |
| 本地 server 的路径要落在 Data Folder 下 | 对 Local FileSystem server，路径第一段必须匹配一个数据文件夹的挂载名。如果 Browser 里数据文件夹显示为 `/copy-audit-files`，就使用 `/copy-audit-files/Feeds`；除非你另外把某个数据文件夹挂载成 `/Feeds`，否则不要直接写 `/Feeds`。 |
| SMB 和 Quark 路径位于各自存储根内 | SMB 绑定在已配置的共享目录和 base path 下面；QuarkDrive 绑定在这个 server 暴露的夸克云盘存储范围内。 |
| 不要启用两个相同路径的绑定 | 另一个已启用绑定已经占用同一个规范化路径时，Zwind 会阻止保存。 |

## 填写 Configuration

**Configuration / 配置** 区域属于当前选中的 resolver。切换 resolver 后，这里的字段会跟着变化。

![解析器绑定编辑器中框选 resolver 专属的 Configuration 字段。](/assets/docs/webdav-server/configure-resolver-bindings/boxed/binding-editor-configuration.png)

这里填写的是 resolver 级别的选项，例如 cache TTL、media mode、Emby endpoints、夸克转存选项或 Web Media 请求行为。`.rss` 文件内容、Emby 媒体库浏览、夸克搜索意图文件夹、`.wm` 规则字段分别在对应指南里说明，本篇只解释 binding 层规则。

点击 **Save / 保存** 时，必填字段会被检查。URL 字段需要是有效的 `http` 或 `https` 地址。密码、token 这类 secret 字段会作为绑定配置保存，编辑器里不会明文显示。

## 自动创建文件夹的规则

从正在运行的 server 保存 binding 时，如果路径合法但文件夹不存在，Zwind 会询问是否现在创建这个文件夹。

![路径不存在时出现 Create Folder 确认框。](/assets/docs/webdav-server/configure-resolver-bindings/boxed/create-folder-confirmation.png)

点 **Create and Save / 创建并保存** 会通过当前 WebDAV server 创建这个目录，然后保存绑定。点 **Cancel / 取消** 不会创建目录，也不会保存这次绑定修改。

其他路径结果：

| 情况 | 结果 |
| --- | --- |
| 路径已经是文件夹 | 直接保存绑定，不弹出创建确认。 |
| 路径已经被文件占用 | 阻止保存，因为解析器绑定路径必须是文件夹。 |
| Local FileSystem 路径不在数据文件夹挂载范围内 | 阻止或提示先准备对应的数据文件夹挂载。 |
| server 停止运行，Zwind 无法检查或创建目录 | 可以先保存绑定，但使用前需要你自己在暴露的存储中创建该目录。 |

对本地 server 来说，binding path 必须和 Browser 里看到的数据文件夹挂载名对齐。`/Documents/Feeds` 只有在 `/Documents` 是已暴露数据文件夹时才成立；`/Feeds` 只有在某个数据文件夹本身挂载成 `/Feeds` 时才成立。

## 保存并让 binding 生效

先在 binding 编辑器里点 **Save / 保存** 回到 **Configure Server / 配置 Server**，再点 server 页面右上角 **Save / 保存**。原生 WebDAV server 在启动时读取 resolver bindings。

如果 server 已经在运行，并且你从 **Configure Server / 配置 Server** 修改了解析器绑定，Zwind 保存 server 后会尝试自动重启这个 server。从 Browser 里配置正在运行 server 的 binding 时，也会保存后尝试重启。重启失败时，app 会显示重启失败提示；在下一次成功启动前，当前运行的 server 仍按旧 binding 状态工作。

如果 server 原本是停止状态，保存后再启动它。若保存时 Zwind 因为 server 停止而无法检查或创建绑定目录，使用前先在对应数据文件夹、SMB 共享或 QuarkDrive 存储范围内创建该目录。
