---
title: 配置 WebDAV 访问权限
description: 在 Zwind 中配置匿名访问、WebDAV 用户名密码、Bonjour 发现、绑定地址和端口。
seoTitle: 配置 Zwind WebDAV 访问权限和网络设置 - Zwind 指南
keywords:
  - Zwind WebDAV 权限
  - WebDAV 用户名密码
  - iPhone WebDAV Bonjour
  - WebDAV 绑定地址
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/webdav-access-permissions
order: 34
tags:
  - guide
  - server
  - permissions
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Zwind 里有两组设置会决定其他设备怎样连接一个 server。**身份验证 / Authentication** 决定客户端是否要填写用户名和密码。**绑定地址 / Binding Address**、**端口 / Port**、**Bonjour 广播 / Bonjour Broadcasting** 决定 server 监听在哪里，以及局域网客户端能不能发现它。

在首页选中 server，点击 **编辑 / Edit** 进入配置页。下面截图使用英文界面；中文界面里的控件位置相同。

## 监听正确的地址和端口

**SERVER** 区域里的地址字段会影响 WebDAV URL。

![Binding Address 和 Port 决定 WebDAV server 监听在哪个地址和端口。](/assets/docs/webdav-server/webdav-access-permissions/network-listening-settings.png)

**Binding Address / 绑定地址** 是 Zwind 启动 server 时绑定的本机地址。

- **All Interfaces (0.0.0.0)** 表示监听所有可用的本地网络接口。手机、电脑、电视或播放器要通过 Wi-Fi 访问时，通常用这个选项。
- **Loopback (127.0.0.1)** 只允许同一台设备访问。局域网里的其他设备不能连接到绑定在 loopback 上的 server。
- 某个具体接口地址，例如 Wi-Fi 地址，只监听这个接口。设备切换网络后 IP 可能变化，所以客户端实际要用 **Running / 运行中** 卡片显示的地址。

**Port / 端口** 是 WebDAV 端口。只有 **Port** 精确填 `0` 时，Zwind 才会在启动 server 时向系统申请一个可用端口；最终端口以 **Running / 运行中** 卡片为准。如果你填写固定端口，Zwind 会按这个端口启动，前提是这个端口可以在当前绑定地址上成功绑定。固定端口已被占用或不可绑定时，server 不能在这个端口启动。

## 决定客户端是否需要凭据

在 **AUTHENTICATION / 身份验证** 区域，打开 **Allow Anonymous Access / 允许匿名访问** 时，客户端连接 WebDAV 不需要用户名和密码。

![Allow Anonymous Access 打开时，客户端无需 WebDAV 用户名和密码。](/assets/docs/webdav-server/webdav-access-permissions/anonymous-access.png)

关闭 **Allow Anonymous Access / 允许匿名访问** 后，Zwind 会要求填写连接用的 **Username / 用户名** 和 **Password / 密码**。第三方 WebDAV 客户端、文件管理器、电视端 app 或媒体播放器里，也要填写同一组用户名和密码。客户端反复弹出登录框时，逐项检查它使用的用户名、密码、协议、host 和 port。

这组凭据保护的是客户端到当前 server 的 WebDAV 连接。它和 **Server Lock / 服务器锁** 不是同一组设置：Server Lock 保护的是 Zwind 内部启动或停止 server 的操作。修改启动密码不会自动修改 WebDAV 客户端使用的密码，除非你也在 **AUTHENTICATION / 身份验证** 里修改连接 **Password / 密码**。

如果关闭匿名访问时 Zwind 提示解锁 VIP，需要先完成对应解锁；设置被允许后，用户名和密码字段才会出现。

## 选择 Bonjour 发现方式

**Bonjour Broadcasting / Bonjour 广播** 在 **ADVANCED / 高级** 区域。它控制局域网自动发现，不是访问权限本身。

![Bonjour Broadcasting 控制兼容客户端是否可以自动发现这个 server。](/assets/docs/webdav-server/webdav-access-permissions/bonjour-broadcasting.png)

Bonjour 打开时，同一局域网里的兼容 app 可能会自动显示这个 Zwind server。Bonjour 关闭时，只要绑定地址、端口、网络和凭据正确，客户端仍然可以通过手动输入完整 URL 访问。

Bonjour 不会让不可达的地址变可达，不会绕过身份验证，也不会让绑定到 `127.0.0.1` 的 server 被其他设备访问。把它理解成“自动发现入口”即可。

## 以 Running 卡片为最终地址

保存设置后启动 server。当前 server 卡片会显示状态和地址。

![Running 卡片显示客户端应该使用的当前地址。](/assets/docs/webdav-server/webdav-access-permissions/running-address.png)

客户端里填写完整 URL：

```text
http://<屏幕上显示的地址>:<屏幕上显示的端口>
```

按截图示例，URL 是：

```text
http://192.168.50.49:52500
```

当 **Port / 端口** 是 `0` 时，server 重启后端口可能变化。当 server 使用 **All Interfaces (0.0.0.0)** 时，配置里保存的可能是 `0.0.0.0`，但客户端不要填写 `0.0.0.0`；要填写 server **Running / 运行中** 时卡片上显示的可访问 IP。

## 哪些设置会影响局域网访问

局域网客户端连不上时，按这张表检查。

| 设置 | 它改变什么 | 对连接的影响 |
| --- | --- | --- |
| Allow Anonymous Access / 允许匿名访问 | WebDAV 客户端是否需要凭据 | 关闭后，每个客户端都必须发送配置里的用户名和密码。 |
| Username / Password | 当前 server 的 WebDAV 连接凭据 | 填错会导致客户端反复要求登录，或出现类似 401 的认证失败。 |
| Binding Address / 绑定地址 | 哪个本机网络接口接受连接 | `127.0.0.1` 会阻止其他设备访问；`0.0.0.0` 通常适合局域网访问。 |
| Port / 端口 | URL 里的 TCP 端口 | `0` 会在启动时选择可用端口；固定端口必须能成功绑定。 |
| Bonjour Broadcasting / Bonjour 广播 | 局域网里的自动发现 | 关闭后不会自动出现在兼容客户端里，但不阻止手动输入 URL。 |

如果 server 已经 **Running / 运行中**，同一个 URL 在 Zwind 内置 Browser 能打开，但另一台设备打不开，优先检查另一台设备实际发送的 URL、账号密码以及它所在网络到这台 iPhone 或 iPad 的访问路径。
