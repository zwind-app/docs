---
title: 配置服务器锁和启动保护
description: 在 Zwind 中区分 Server Lock、启动密码、Face ID 启动验证、自动启动和 WebDAV 客户端凭据。
seoTitle: 配置 Zwind 服务器锁、Face ID 启动验证和自动启动 - Zwind 指南
keywords:
  - Zwind 服务器锁
  - Zwind 启动密码
  - WebDAV Face ID 启动
  - Zwind 自动启动
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/server-lock-start-protection
order: 35
tags:
  - guide
  - server
  - security
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Server Lock / 服务器锁保护的是 Zwind 自己的 server 启动流程。WebDAV 身份验证保护的是第三方客户端连接。两者都可能出现用户名和密码，但使用时机完全不同。

在首页选中 server，点击 **编辑 / Edit** 进入配置页。下面截图使用英文界面；中文界面里的控件位置相同。

## 先区分两组密码

**AUTHENTICATION / 身份验证** 区域控制 WebDAV 客户端。关闭 **Allow Anonymous Access / 允许匿名访问** 后，这里的 **Username / 用户名** 和 **Password / 密码** 要填到 Finder、文件 App、Infuse、VLC、NAS 工具或其他 WebDAV 客户端里。

**SERVER LOCK / 服务器锁** 区域控制 Zwind 内部的启动保护。它不会修改第三方 WebDAV 客户端连接时使用的用户名和密码。

![Authentication 凭据和 Server Lock 控件是两套设置。](/assets/docs/webdav-server/server-lock-start-protection/authentication-vs-server-lock.png)

排查时按这个表分辨：

| 现象 | 检查哪组设置 |
| --- | --- |
| 第三方 WebDAV 客户端要求登录 | **AUTHENTICATION / 身份验证** 里的用户名和密码。 |
| Zwind 在启动 server 前要求验证 | **SERVER LOCK / 服务器锁** 里的启动密码或 Face ID 设置。 |
| 客户端不用密码也能连接 | **Allow Anonymous Access / 允许匿名访问** 仍然打开，和 Server Lock 无关。 |
| Zwind 没有自动启动某个 server | **SERVER LOCK / 服务器锁** 和 **Start on Launch / 应用启动时自动启动** 正在互相影响。 |

## 用启动密码控制谁能在 Zwind 里启动 server

需要避免别人随手在 Zwind 里启动某个 server 时，打开 **Require password on start / 启动时需要密码**。功能允许后，Zwind 会显示 **Lock Username / 启动用户名** 和 **Lock Password / 启动密码**。启动这个 server 前，Zwind 会校验这组启动凭据。

![Require password on start 和 Require Face ID on start 是 Server Lock 控件。](/assets/docs/webdav-server/server-lock-start-protection/server-lock-controls.png)

这个能力适合多人会接触同一台 iPhone 或 iPad、或者你想保留 server 配置但不希望一次误触就让它上线的场景。它不负责拦截已经拿到有效 WebDAV 凭据的客户端；客户端连接权限要在 **AUTHENTICATION / 身份验证** 里配置。

启动密码是 Zwind VIP 功能。如果当前账号没有 VIP 权限，点击开关会先进入解锁流程，而不是直接显示输入框。调试或测试构建里可能在说明后继续放行，但正式版本需要对应权益。

## 设备可用时再加 Face ID 启动验证

**Require Face ID on start / 启动时需要面容 ID** 会在 server 启动前追加一次 iOS 生物识别验证。它同样是 Zwind VIP 功能。

这个开关只有在 iOS 判断当前设备可以进行生物识别时才可用。如果设备没有设置 Face ID、系统设置禁止使用、当前设备不支持，或者模拟器会话无法稳定提供 Face ID，Zwind 会让开关不可用，或者验证无法完成。

同时打开启动密码和 Face ID 时，Zwind 会先要求输入启动密码，再进行 Face ID 验证。任一步取消或失败，server 都不会启动。

## 理解自动启动的边界

**Start on Launch / 应用启动时自动启动** 位于 **ADVANCED / 高级** 区域。它表示 Zwind 打开时自动启动这个 server。

![Start on Launch 和 Server Lock、Bonjour Broadcasting 是不同设置。](/assets/docs/webdav-server/server-lock-start-protection/start-on-launch.png)

自动启动不能替用户填写启动密码，也不能替用户完成 Face ID。因此，只要启用了 **Require password on start / 启动时需要密码** 或 **Require Face ID on start / 启动时需要面容 ID**，Zwind 会关闭这个 server 的 **Start on Launch / 应用启动时自动启动**，应用启动时也会跳过需要交互验证的 server。

想让 server 随 Zwind 打开就上线时，使用 **Start on Launch / 应用启动时自动启动**，并保持交互式 Server Lock 关闭。想让 server 保留配置但必须有人在设备前确认后才上线时，使用 Server Lock。

## 每种保护适合什么

| 场景 | 使用 |
| --- | --- |
| 希望 WebDAV 客户端浏览文件前必须登录 | 关闭 **Allow Anonymous Access / 允许匿名访问**，设置 **AUTHENTICATION / 身份验证** 用户名和密码。 |
| 希望 Zwind 在 app 内启动 server 前先问一次密码 | 打开 **Require password on start / 启动时需要密码**，填写 **Lock Username / 启动用户名** 和 **Lock Password / 启动密码**。 |
| 希望启动 server 前进行生物识别 | 在 Face ID 可用的设备上打开 **Require Face ID on start / 启动时需要面容 ID**。 |
| 希望 Zwind 打开时自动启动某个 server | 打开 **Start on Launch / 应用启动时自动启动**，并关闭交互式 Server Lock。 |
| 希望兼容客户端能在局域网自动发现 server | 使用 **Bonjour Broadcasting / Bonjour 广播**；它不替代 WebDAV 凭据或 Server Lock。 |

修改其中一项不会自动改变其他项。例如，设置启动密码不会让第三方客户端改用这组密码；关闭匿名 WebDAV 访问，也不会让自动启动去弹 Face ID。
