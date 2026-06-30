---
title: 从零启动第一个 server
description: 创建本地 Zwind WebDAV server，添加文件夹，启动后从另一台设备验证访问。
seoTitle: 从零到可访问的 iPhone WebDAV server - Zwind 指南
keywords:
  - iPhone WebDAV
  - start WebDAV server
  - Zwind guide
  - 局域网文件共享
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/start-your-first-server
order: 30
tags:
  - guide
  - server
  - first-run
publishedAt: 2026-05-21
updatedAt: 2026-06-30
draft: false
---

这篇文档从第一步开始：安装并打开 Zwind，创建一个本地文件系统 server，添加一个数据文件夹，启动 server，复制 WebDAV URL，然后用另一台设备确认可以访问。

## 准备

- iPhone 或 iPad 上已安装 Zwind。
- iPhone 或 iPad 和第二台设备在同一个可互通的 Wi-Fi 网络里。
- 第二台设备上有浏览器、文件管理器、媒体播放器或 WebDAV 客户端。
- 准备一个要通过 WebDAV 暴露的本地文件夹。

如果第二台设备在蜂窝网络、访客 Wi-Fi、VPN，或当前网络禁止设备之间互访，即使 Zwind 里 server 已经 Running，客户端也可能打不开 WebDAV URL。

## 1. 打开 Zwind，创建本地 server

先从 App Store 安装 Zwind，然后在要作为 server 的 iPhone 或 iPad 上打开它。首次启动时完成或跳过引导，然后在第一个 server 卡片中选择 **使用本地目录 / Use Local Folder**。这篇文档的截图使用英文界面；如果你的 app 是中文，对应按钮在相同位置。

![从首次使用卡片创建本地 server。](/assets/docs/webdav-server/start-your-first-server/create-local-server.png)

Zwind 会进入 server 配置页，并选中 **Local FileSystem**。第一次使用时，可以先保留默认名称和存储类型，直接保存。

## 2. 添加一个数据文件夹

本地 server 至少需要一个数据文件夹，才有内容可以通过 WebDAV 暴露。点击 **添加文件夹 / Add Folder**，在 iOS 文件选择器里选择一个文件夹，然后点 **打开 / Open** 确认。

![启动本地 server 前先添加数据文件夹。](/assets/docs/webdav-server/start-your-first-server/add-data-folder.png)

## 3. 启动 server，复制 WebDAV URL

点击 **启动服务器 / Start Server**。状态变成 **运行中 / Running** 后，Zwind 会在当前 server 卡片上显示地址。

![server 已经 Running，并显示 WebDAV 地址。](/assets/docs/webdav-server/start-your-first-server/server-running-url.png)

客户端里要填写完整的 WebDAV URL：

```text
http://<屏幕上显示的 IP>:<屏幕上显示的端口>
```

例如 Zwind 显示 `192.168.50.49:52500`，客户端里就输入 `http://192.168.50.49:52500`。如果客户端把地址拆成多个字段，就把 `192.168.50.49` 填到 host，把冒号后面的数字填到 port，协议选择 HTTP。

如果 server 的端口设置为 `0`，Zwind 会在启动时向系统申请一个可用的随机端口。这种情况下，以 **Running** 卡片里显示的地址为准。如果你在 server 设置里填写了固定端口，只要网络地址和凭据没有变化，客户端就可以继续使用这个端口。

## 4. 用另一台设备验证访问

在第二台设备上，用兼容的客户端打开 WebDAV URL。桌面浏览器可以做最基础的连通性检查；如果要浏览目录和打开文件，WebDAV 文件管理器或媒体播放器更合适。

第一次验证只看三件事：

1. 客户端可以连接，没有超时。
2. 能看到文件夹列表。
3. 能打开或下载一个测试文件。

你也可以在 Zwind 内点击数据文件夹行，打开内置 Browser，确认这个 Running server 能访问同一个目录。

![Browser 可以打开这个 Running server 暴露的数据文件夹。](/assets/docs/webdav-server/start-your-first-server/browser-access.png)

如果 Zwind 内置 Browser 可以打开，但另一台设备打不开，说明 app 和文件夹配置基本正常。优先检查网络：是否同一个 Wi-Fi、是否访客网络隔离、是否 VPN 改写路由、IP 和端口是否完整复制。

## 常见处理

- 确认两台设备在同一个本地网络，并且能互相访问。
- URL 开头要包含 `http://`。
- 使用 server 处于 **Running** 时显示的当前地址。
- 如果某个电视端或播放器显示空目录，先用桌面浏览器或另一个 WebDAV 客户端交叉验证。
- 如果之后开启 server lock，客户端里要填写对应用户名和密码。

客户端能列出文件夹并打开文件后，这个 server 就可以使用了。
