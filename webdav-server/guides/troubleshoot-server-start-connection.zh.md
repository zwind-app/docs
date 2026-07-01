---
title: 排查无法启动或无法连接 server
description: 排查 Zwind server 无法启动、端口变化、局域网不可达、锁验证失败和 WebDAV 客户端凭据错误。
seoTitle: 排查 Zwind server 启动、端口、局域网和 WebDAV 连接问题
keywords:
  - Zwind server 无法启动
  - Zwind WebDAV 无法连接
  - WebDAV 端口被占用
  - iOS 局域网权限 WebDAV
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/troubleshoot-server-start-connection
order: 58
tags:
  - guide
  - server
  - troubleshooting
publishedAt: 2026-07-01
updatedAt: 2026-07-01
draft: false
---

server 无法启动，或显示已经运行但 WebDAV 客户端连不上时，按下面顺序排查：先看 server 卡片是否真的 **Running / 运行中**，再检查端口、绑定地址、iOS 局域网权限、设备所在网络、Server Lock 和 WebDAV 凭据。

下面截图使用英文 UI。中文界面中，**Running** 对应 **运行中**，**Address** 对应 **地址**，**Binding Address** 对应 **绑定地址**，**Port** 对应 **端口**，**Authentication** 对应 **身份验证**，**Server Lock** 对应 **服务器锁**。

## 先确认 server 真的在运行

Home 上的 server 卡片必须显示 **Running / 运行中**，并且有 **Address / 地址**。客户端要使用这个地址。

![Running server 卡片中框选状态和地址。](/assets/docs/webdav-server/troubleshoot-server-start-connection/boxed/running-address.png)

如果 server 还没有 **Running / 运行中**，先不要排第三方客户端。进入 **Edit / 编辑** 检查启动设置。

如果 server 已经运行，但客户端还在使用旧 URL，就把客户端地址改成当前 **Address / 地址**。当 **Port / 端口** 设置为 `0` 时尤其要这样做，因为 server 重启后端口可能变化。

## 处理端口无效或被占用

进入 **Edit / 编辑**，查看 **SERVER** 区域里的 **Port / 端口**。

![Configure Server 页面中框选 Binding Address 和 Port。](/assets/docs/webdav-server/troubleshoot-server-start-connection/boxed/address-port.png)

按这些规则检查：

- **Port / 端口** 必须是 `0`，或 `1` 到 `65535` 之间的有效 TCP 端口。
- **Port** 填 `0` 表示“启动时自动选择一个可用端口”。最终端口以 **Running / 运行中** 卡片显示为准。
- 固定端口，例如 `8080`，地址更稳定；但如果同一绑定地址上已有其他 app 或另一个 Zwind server 占用这个端口，server 就无法在这个端口启动。
- 固定端口启动失败时，可以停止占用该端口的服务、换一个固定端口，或把 **Port** 改成 `0`，再把新的 **Running / 运行中** 地址填到客户端。

修改 **Port / 端口** 后，保存 server 并重新启动。已经保存过的客户端配置也要改成新端口。

## 选择合适的 Binding Address

电脑、电视、另一台手机或媒体播放器要从同一 Wi-Fi 访问时，通常使用 **All Interfaces (0.0.0.0)**。这样 Zwind 会在 iPhone 或 iPad 的 Wi-Fi 网络接口上监听。

**Loopback (127.0.0.1)** 只适合同一台 iPhone 或 iPad 本机访问。另一台设备不能通过你 iPhone 上的 `127.0.0.1` 连接；在那台设备上，`127.0.0.1` 指向它自己。

不要把 `0.0.0.0` 填到另一台设备的 WebDAV 客户端里。`0.0.0.0` 是 Zwind 内部监听设置；客户端要填 **Running / 运行中** 卡片显示的可访问 IP，例如：

```text
http://192.168.50.49:52500
```

iPhone 或 iPad 换 Wi-Fi 后，可访问 IP 可能变化。重启 server 后重新读取当前 **Address / 地址**。

## 允许 iOS Local Network 权限

iOS 可能会阻止 app 访问局域网。server 显示运行，但其他设备连不上时，打开 iOS **设置** > **隐私与安全性** > **本地网络**，允许 Zwind。

如果启动或使用 server 时 iOS 弹出 Local Network / 本地网络权限提示，选择允许。拒绝这个权限后，Zwind 内部看起来配置正确，但同一 Wi-Fi 的其他设备可能无法访问。

修改权限后，停止并重新启动 server，再用当前 **Running / 运行中** 地址重试客户端。

## 检查设备是否真的在同一网络

两台设备都能上网，不代表它们能互相访问。按下面情况检查：

| 情况 | 处理方法 |
| --- | --- |
| iPhone 用蜂窝网络或热点，客户端在 Wi-Fi | 让两台设备连接同一个 Wi-Fi，或让客户端连接同一个热点网络。 |
| 其中一台连在访客 Wi-Fi | 把两台设备都切到主 Wi-Fi。访客网络经常禁止设备互相访问。 |
| 任一设备开着 VPN | 先断开 VPN，或把 VPN 配成不接管局域网流量。 |
| 路由器开启 AP isolation / client isolation | 在设备所在 Wi-Fi 上关闭隔离。 |
| 客户端把本地 Zwind URL 改成 `https://` | 改回 `http://`，除非你自己配置了 HTTPS 反向代理或隧道。 |

如果同一个 Zwind URL 在某台设备能打开，在另一台设备打不开，server 本身已经在运行；重点检查失败设备的网络、VPN、URL 字段和凭据。

## 区分 Server Lock 和 WebDAV 凭据

**Authentication / 身份验证** 控制 WebDAV 客户端。**Server Lock / 服务器锁** 控制 Zwind 在启动 server 前是否要求密码或 Face ID。

![Authentication 和 Server Lock 区域被框选。](/assets/docs/webdav-server/troubleshoot-server-start-connection/boxed/authentication-server-lock.png)

如果 Zwind 要求启动密码或 Face ID，而验证失败或被取消，server 不会启动。输入 **Server Lock / 服务器锁** 中配置的 **Lock Username** 和 **Lock Password**，或关闭这项启动保护。

Server Lock 不会改变 Finder、Files、VLC、Infuse、电视端 app 或其他 WebDAV 客户端使用的用户名密码。客户端要求登录时，要检查 **Authentication / 身份验证**，不是 **Server Lock / 服务器锁**。

![Server Lock 和 Start on Launch 控件被框选。](/assets/docs/webdav-server/troubleshoot-server-start-connection/boxed/server-lock.png)

如果打开了 **Start on Launch / 启动时启动**，但 server 没有自动启动，检查是否启用了 **Require password on start** 或 **Require Face ID on start**。自动启动无法完成交互式密码或 Face ID 验证，所以带锁的 server 需要人在 app 里手动启动。

## 处理客户端用户名密码错误

在 **Authentication / 身份验证** 中，**Allow Anonymous Access / 允许匿名访问** 决定客户端是否需要 WebDAV 凭据。

- **Allow Anonymous Access / 允许匿名访问** 打开时，客户端用户名和密码留空。如果客户端要求选择登录方式，选 anonymous、guest、none，或保持账号密码为空。
- **Allow Anonymous Access / 允许匿名访问** 关闭时，在客户端中精确填写该 server 的 **Username / 用户名** 和 **Password / 密码**。
- 不要把 Server Lock 密码当成 WebDAV 密码。
- 不要使用 SMB、夸克、Emby 或其他上游账号密码，除非你也把同一个值填进了这个 server 的 **Authentication / 身份验证** 密码字段。

如果客户端一直反复要求密码，手动重新输入 URL、用户名和密码。客户端保存的旧配置可能还在使用旧端口或旧密码。

## 本机连接或配置变更后重启 server

有些设置只会在下次启动 server 时生效。修改 **Binding Address / 绑定地址**、**Port / 端口**、**Authentication / 身份验证**、**Server Lock / 服务器锁**、本地文件夹、解析器绑定，或 iOS Local Network / 本地网络权限后，先停止正在运行的 server，再重新启动。

然后把新的 **Running / 运行中** 地址复制到保存了 URL 的客户端。**Port / 端口** 为 `0` 时必须这样做；固定端口改动后也建议这样确认一次，确保 server 正在监听你预期的地址。

客户端字段的常规填写方式见 [连接第三方 WebDAV 客户端和播放器](/zh/docs/webdav-server/guides/connect-third-party-webdav-clients/)。各项访问权限设置的含义见 [配置 WebDAV 访问权限](/zh/docs/webdav-server/guides/webdav-access-permissions/)。
