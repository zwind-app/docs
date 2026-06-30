---
title: 创建和管理不同类型的 server
description: 选择本地文件系统、夸克云盘或 SMB 共享 server，并理解创建、编辑、删除时的关键字段。
seoTitle: 创建和管理 Zwind WebDAV server 类型 - Zwind 指南
keywords:
  - Zwind server 类型
  - iPhone WebDAV server
  - 夸克云盘 WebDAV
  - SMB WebDAV
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/manage-server-types
order: 31
tags:
  - guide
  - server
  - storage
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Zwind 的一个 server 可以连接三类来源：iPhone 或 iPad 上的本地文件夹、夸克云盘、局域网里的 SMB 共享。先选类型，再填写这个类型需要的字段。

## 选择 server 类型

首次打开 Zwind 时，第一个 server 卡片里有三个入口：**使用本地目录 / Use Local Folder**、**使用夸克云盘 / Use Quark Drive**、**使用 SMB 共享 / Use SMB Share**。已经创建过 server 后，可以点左下角 **+** 再新增一个。

![从第一个 server 卡片选择 storage 类型。](/assets/docs/webdav-server/manage-server-types/create-server-types.png)

选择 **Local FileSystem**：文件在这台 iPhone 或 iPad 上，或在 iOS Files 能打开的 iCloud Drive、文件提供器里。保存本地 server 后，还需要添加至少一个数据文件夹。

选择 **QuarkDrive**：要把夸克云盘账号里的文件通过 Zwind server 暴露出来。这个类型需要在配置页填入夸克 Cookie。

选择 **SMB2/3 Share**：来源是同一局域网里的 NAS、Mac 或 Windows 共享。Zwind 先连接 SMB 共享，再通过当前 server 对外提供访问。

## 通用字段

三种类型都会先显示同一组基础字段。

![Local FileSystem 只需要填写通用 server 字段。](/assets/docs/webdav-server/manage-server-types/local-filesystem-fields.png)

**Server Name** 是首页 server 卡片和列表里显示的名字。可以直接写来源名，例如 `iPad Downloads`、`Quark Drive`、`NAS Movies`。

**Storage Type** 决定这个 server 连接哪一种来源。切换它后，下方会显示对应类型的专属字段。

**Binding Address** 决定 server 监听哪个本机地址。默认的 **All Interfaces (0.0.0.0)** 会使用 server 卡片上显示的可访问地址。只有需要限制到某个本机网络接口时，才改成其他绑定地址。

**Port** 是 WebDAV 端口。填 `0` 时，Zwind 会在启动 server 时自动拿一个可用端口；客户端要使用 **Running** 卡片上显示的地址。填固定端口时，只要设备地址和 server 设置没有变化，客户端可以继续用这个端口。

## Local FileSystem

**Local FileSystem** 没有额外账号字段。保存 server 后，回到首页 server 卡片，继续添加一个或多个数据文件夹。

这个 server 暴露的是你添加进去的文件夹。修改 Server Name 不会重命名文件夹；删除 server 也不会删除原始文件。

## QuarkDrive

**QuarkDrive** 除了通用字段，还需要填写 **Quark Cookie**。

![QuarkDrive 会在通用字段中加入 Quark Cookie。](/assets/docs/webdav-server/manage-server-types/quark-drive-fields.png)

**Quark Cookie** 是 Zwind 访问夸克账号时使用的会话信息。创建 QuarkDrive server 时，把 Cookie 粘贴到这个字段后再保存。这里不讲 Cookie 怎么准备和刷新，后面会有单独文档。

如果 **保存 / Save** 是灰色，先检查当前类型的必填字段。QuarkDrive 至少要填 Cookie。

## SMB2/3 Share

**SMB2/3 Share** 在通用字段后面还有一组 SMB 来源字段。

![SMB2/3 Share 字段用于填写 SMB 主机、路径和可选账号。](/assets/docs/webdav-server/manage-server-types/smb-share-fields.png)

**SMB Host** 填 SMB 服务器地址，可以是 IP，例如 `192.168.1.10`，也可以是 NAS 主机名。

**Default Share (optional)** 填默认打开的共享名。不填时，Zwind 会先浏览可用共享。

**Base Path (optional)** 填共享内部的路径，例如 `/Movies`。不填就是从共享根目录开始。

**SMB Port** 默认是 `445`，这是常见 SMB 端口。

**SMB Username** 不填表示尝试访客访问。共享需要账号时，在这里填用户名。

**SMB Password** 是 SMB 密码。用户名需要密码时才填写。

**Domain / Workgroup** 是可选项。只有你的 SMB 服务器要求域或工作组时才填。

## 编辑 server

在首页选中一个 server，然后点当前 server 卡片右侧的 **编辑 / Edit**。Zwind 会打开创建 server 时同一个配置页。

![点选中 server 卡片上的 Edit 修改配置。](/assets/docs/webdav-server/manage-server-types/server-card-edit.png)

保存修改后，回到 server 卡片确认当前地址和状态。如果 Port 是 `0`，下次启动时地址里的端口可能变化。如果你改过 Storage Type，启动前再检查一次对应类型的专属字段。

## 删除 server

点 **编辑 / Edit** 进入配置页，滚动到底部，点击 **Delete Server / 删除 server**，再按确认提示删除。

删除 server 只会移除 Zwind 里的这个 server 条目，不会删除本地文件、夸克云盘账号或 SMB 共享里的原始内容。
