---
title: 连接第三方 WebDAV 客户端和播放器
description: 在电脑、手机、电视端或媒体播放器中填写 Zwind 的 WebDAV 地址、端口、路径和凭据。
seoTitle: 连接第三方 WebDAV 客户端和媒体播放器 - Zwind 指南
keywords:
  - Zwind WebDAV 客户端
  - WebDAV 播放器地址
  - 电视 WebDAV 连接
  - WebDAV 用户名密码
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/connect-third-party-webdav-clients
order: 57
tags:
  - guide
  - server
  - clients
  - playback
publishedAt: 2026-07-01
updatedAt: 2026-07-01
draft: false
---

第三方 WebDAV 客户端通常都需要同几项信息：协议、主机、端口、可选路径、可选用户名和密码。Zwind 启动 server 后会显示当前地址；电脑、手机、电视端 app 和媒体播放器都按这个地址填写。

下面截图使用英文 UI。中文界面中，**Running** 对应 **运行中**，**Address** 对应 **地址**，**Binding Address** 对应 **绑定地址**，**Port** 对应 **端口**，**Allow Anonymous Access** 对应 **允许匿名访问**。

## 先从 Zwind 读取当前 URL

启动 server 后，看运行中 server 卡片里的 **Address / 地址**。截图里的地址是 `192.168.50.49:52500`，所以 WebDAV URL 是：

```text
http://192.168.50.49:52500
```

![Running server 卡片中框选当前 Address。](/assets/docs/webdav-server/connect-third-party-webdav-clients/boxed/01-running-server-url.png)

如果运行中的迷你卡片已经显示完整 URL，就直接复制或照填这个完整值。如果卡片只显示 `地址:端口`，而客户端只有一个 URL 输入框，就在前面加上 `http://`。

不要在其他设备的客户端里填写 `0.0.0.0`。`0.0.0.0` 是 Zwind 内部的监听设置；第三方客户端要填 server **运行中 / Running** 时显示的可访问 IP。

## 端口是否会变化，看 Port 设置

需要判断端口为什么变化时，进入 server 的 **编辑 / Edit** 页面。

![Server 设置中框选 Binding Address 和 Port。](/assets/docs/webdav-server/connect-third-party-webdav-clients/boxed/02-address-port-settings.png)

**Port / 端口** 有两种情况：

- **Port** 精确为 `0` 时，Zwind 每次启动 server 都会向系统申请一个可用端口。server 重启后端口可能变化，第三方客户端要以 **Running / 运行中** 卡片为准更新。
- **Port** 填固定值，例如 `8080` 时，只要 server 能正常启动，客户端就继续使用这个固定端口。

局域网访问通常使用 **All Interfaces (0.0.0.0)**。如果绑定到 **Loopback (127.0.0.1)**，只有同一台 iPhone 或 iPad 能访问；同一 Wi-Fi 里的电脑、电视或另一台手机都连不上。

## 匿名访问决定是否填写账号密码

在 **Authentication / 身份验证** 区域看 **Allow Anonymous Access / 允许匿名访问**。

![Authentication 设置中框选 Allow Anonymous Access。](/assets/docs/webdav-server/connect-third-party-webdav-clients/boxed/03-authentication-settings.png)

打开 **Allow Anonymous Access / 允许匿名访问** 时，第三方客户端的用户名和密码留空。如果客户端必须选择登录方式，选 anonymous、guest、none，或保持账号密码为空。

关闭 **Allow Anonymous Access / 允许匿名访问** 时，在客户端里填写当前 server 的 Authentication 设置里的 **Username / 用户名** 和 **Password / 密码**。这组是 WebDAV 连接凭据，不是 SMB server 的 SMB 账号密码，也不是 Zwind 里保护启动或停止操作的 Server Lock 密码。

## 常见客户端字段这样对应

不同 app 会用不同字段名，但填入的内容相同：

| 客户端字段 | 填什么 |
| --- | --- |
| Protocol / Scheme / 协议 | `http`。只有你自己通过 HTTPS 反向代理、隧道或明确的 `https://` 地址访问时，才填 `https`。 |
| Server / Host / Address / 主机 | Zwind 运行卡片里的 IP 或主机名，例如 `192.168.50.49`。 |
| Port / 端口 | 冒号后面的数字，例如 `52500`。 |
| URL / Server URL | 完整 URL，例如 `http://192.168.50.49:52500`。 |
| Path / Remote path / Directory / 路径 | 通常填 `/`；要直接进某个目录时填 `/File Provider Storage/Movies/` 这类路径。 |
| Username / 用户名 | 匿名访问打开时留空；关闭匿名访问时填 server Authentication 用户名。 |
| Password / 密码 | 匿名访问打开时留空；关闭匿名访问时填 server Authentication 密码。 |
| Display name / Nickname / 显示名称 | 随便取一个名字，例如 `Zwind iPhone`。它不影响真正连接地址。 |

电脑文件管理器常见的是一个 **Server URL** 输入框；手机文件管理器可能把 host、port、path、username、password 拆成多行；电视端和媒体播放器常见字段是 **Server**、**Port**、**Path**、**Account**、**Password**。字段名不同，值按上表拆开即可。

## 播放器只想打开某个目录时，填写目录 URL

想让客户端从 Zwind 根目录开始浏览，使用根 URL：

```text
http://192.168.50.49:52500/
```

想让播放器直接进入某个媒体目录，使用目录 URL：

```text
http://192.168.50.49:52500/File%20Provider%20Storage/Movies/
```

如果客户端把 **Server URL** 和 **Path** 分开，就这样填：

```text
Server URL: http://192.168.50.49:52500
Path: /File Provider Storage/Movies/
```

路径里的文件夹名和斜杠要和 Zwind Browser 中看到的一致。客户端只有一个 URL 输入框时，空格写成 `%20`。客户端有单独 Path 字段时，通常可以直接输入带空格的文件夹名。

## 局域网、HTTP 和 Bonjour 的预期

Zwind 显示的本地地址通常只在同一局域网内可用。电脑、手机、电视或播放器要和运行 Zwind 的 iPhone 或 iPad 在同一个 Wi-Fi 下。手机热点、访客 Wi-Fi、VPN、路由器隔离都会让两台设备即使都能上网，也无法互相访问。

Zwind 本地 URL 通常是 `http://...`。如果客户端自动改成 `https://...`，而你没有在 Zwind 前面放 HTTPS 反向代理或隧道，连接会失败。

Bonjour 可以让兼容客户端在局域网里自动发现 server 名称。它只是发现入口，不是连接本身。电视端 app 和媒体播放器对 Bonjour 的支持经常不完整，手动填写 **Running / 运行中** 卡片里的完整 URL 最稳定。

访问权限设置的完整含义见 [配置 WebDAV 访问权限](/zh/docs/webdav-server/guides/webdav-access-permissions/)。
