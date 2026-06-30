---
title: 配置 SMB 到 WebDAV
description: 在 Zwind 中填写 SMB2/3 Share 字段，连接 NAS、Windows 或 Mac 共享，也可以配置访客访问。
seoTitle: 配置 SMB 到 WebDAV - Zwind iPhone 指南
keywords:
  - SMB to WebDAV
  - iPhone SMB WebDAV
  - NAS WebDAV
  - Zwind SMB
productSlug: webdav-server
section: 指南
locale: zh
translationOf: webdav-server/guides/smb-to-webdav
order: 20
tags:
  - smb
  - webdav
  - nas
publishedAt: 2026-05-24
updatedAt: 2026-06-30
draft: false
---

来源文件在 NAS、Windows 共享文件夹、Mac 文件共享或其他 SMB server 上时，server 类型选择 **SMB2/3 Share**。Zwind 会先连接这个 SMB 来源，再用当前 server 对外提供访问。

## 选择 SMB2/3 Share

首次首页的 server 卡片里，点击 **使用 SMB 共享 / Use SMB Share**。如果已经创建过 server，点左下角 **+**，再选择 SMB 类型。

![在第一个 server 卡片中选择 Use SMB Share。](/assets/docs/webdav-server/smb-to-webdav/choose-smb-share.png)

进入配置页后，确认 **Storage Type** 显示为 **SMB2/3 Share**。中文界面里这一行仍用于确认当前 server 连接的是 SMB 来源。

![Storage Type 已选择 SMB2/3 Share。](/assets/docs/webdav-server/smb-to-webdav/smb-storage-type.png)

## 填写 SMB 字段

向下滚动到 **SMB SHARE**。这里填的是上游 SMB server，不是后面给 WebDAV 客户端使用的地址。

![SMB SHARE 区域包含主机、共享名、路径、端口、账号和域字段。](/assets/docs/webdav-server/smb-to-webdav/smb-fields-empty.png)

**SMB Host / SMB 主机** 填 SMB server 地址，只填主机名或 IP，例如 `192.168.1.50`、`nas.local`、`office-pc`。不要写 `smb://`，不要把共享名或文件夹路径放进这个字段。

**Default Share (optional) / 默认共享（可选）** 填共享名，例如 `Media`、`Public`、`Movies`、`Users`。这里要填 NAS 或电脑共享设置里显示的共享名，不加斜杠。留空时，Zwind 会先浏览这个 SMB server 上可用的 shares。

**Base Path (optional) / 基础路径（可选）** 是共享内部的文件夹路径，例如 `/Movies`、`/Videos/TV`、`/Backups/iPhone`。它不是共享名。如果 **Default Share** 留空，**Base Path** 暂时不会生效，因为 Zwind 会先列出 shares。

**SMB Port / SMB 端口** 是 SMB 服务端口。通常保持 `445`。只有 SMB server 明确改过端口时，才填其他端口。

**SMB Username / SMB 用户名** 是 SMB 账号。共享要求登录时填写；访客访问时留空。

**SMB Password / SMB 密码** 是 SMB 账号密码。用户名需要密码时填写；访客访问或该账号没有密码时留空。

**Domain / Workgroup / 域或工作组** 是可选项。只有 SMB server 要求域或工作组时才填，例如 `WORKGROUP`、`HOME` 或公司域。大多数家用 NAS、Windows 共享和 Mac 共享可以留空。

![示例中填写了 SMB Host、默认端口、用户名和密码。](/assets/docs/webdav-server/smb-to-webdav/smb-fields-example.png)

## NAS 示例

NAS 上有一个名为 `Media` 的共享，并用普通账号访问时，可以这样填：

| 字段 | 填写值 |
| --- | --- |
| SMB Host | `192.168.1.50` |
| Default Share | `Media` |
| Base Path | `/Movies`，或留空表示共享根目录 |
| SMB Port | `445` |
| SMB Username | `mediauser` |
| SMB Password | `mediauser` 在 NAS 上的密码 |
| Domain / Workgroup | 留空，除非 NAS 要求填写 |

如果 NAS 页面给出的路径类似 `smb://192.168.1.50/Media/Movies`，拆开填写：Host 是 `192.168.1.50`，Default Share 是 `Media`，Base Path 是 `/Movies`。

## 电脑共享示例

Windows 共享文件夹可以按下面方式填写：

| 字段 | 示例 |
| --- | --- |
| SMB Host | `office-pc` 或 `192.168.1.23` |
| Default Share | `Videos` |
| Base Path | 要从 `Videos/Projects` 开始就填 `/Projects`，否则留空 |
| SMB Username | 有权限访问该共享的 Windows 账号 |
| Domain / Workgroup | 只有共享要求时填写 |

Mac 文件共享可以按下面方式填写：

| 字段 | 示例 |
| --- | --- |
| SMB Host | `mac-mini.local` 或 Mac 的 IP 地址 |
| Default Share | `Movies` |
| Base Path | 要从 `Movies/Archive` 开始就填 `/Archive`，否则留空 |
| SMB Username | 有权限访问该共享的 macOS 用户 |
| Domain / Workgroup | 通常留空 |

## 访客访问

只有 SMB server 本身允许该共享使用 guest 访问时，才这样配置。

| 字段 | 填写值 |
| --- | --- |
| SMB Host | NAS 或电脑地址 |
| Default Share | 允许访客读取的共享名；也可以留空先浏览 shares |
| Base Path | 共享内的文件夹路径，或留空 |
| SMB Port | `445` |
| SMB Username | 留空 |
| SMB Password | 留空 |
| Domain / Workgroup | 留空，除非 server 要求 |

填完必需字段后点 **保存 / Save**。如果 **保存 / Save** 还是灰色，检查 **SMB Host** 是否已填写，以及 **SMB Port** 是否是有效数字。
