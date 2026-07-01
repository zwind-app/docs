---
title: 理解 VIP、单独买断和广告领取 VIP
description: 了解 Zwind 免费版能做什么、VIP 解锁什么、什么时候只买断一个解析器就够，以及广告领取 1 天 VIP 的规则。
seoTitle: Zwind VIP、解析器单独买断和广告领取 VIP - Zwind 指南
keywords:
  - Zwind VIP
  - Zwind 解析器买断
  - Zwind 广告领取 VIP
  - Zwind 恢复购买
  - Zwind 免费版限制
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/vip-buy-once-rewarded-vip
order: 56
tags:
  - guide
  - vip
  - paywall
  - resolvers
publishedAt: 2026-07-01
updatedAt: 2026-07-01
draft: false
---

Zwind 的基础 WebDAV 服务可以免费使用。只有当你点击 **Unlock Zwind VIP / 解锁 Zwind VIP**、使用 VIP 功能，或打开尚未解锁的付费解析器时，才会看到解锁页。

下面截图使用英文 UI。中文界面中，**Unlock Zwind VIP** 对应 **解锁 Zwind VIP**，**Projection Resolvers** 对应 **投影解析器**，**Restore Purchases** 对应 **恢复购买**，**Watch Ad to get 1 day VIP** 对应 **看广告领取 1 天 VIP**。商品名称和价格由 App Store 返回，可能仍按你的商店语言显示。

## 先判断该选哪种解锁

被权限拦住时，先看你要做的事：

| 你要做什么 | 该用哪种解锁 |
| --- | --- |
| 超过免费 server 启动限制 | Zwind VIP |
| 使用现在和未来的全部解析器扩展 | Zwind VIP |
| 只使用某一个付费解析器，例如 Web Media Projection 或 Emby 媒体库解析 | 单独买断这个解析器，或使用 Zwind VIP |
| 使用 Server Lock、Face ID 启动保护、关闭匿名访问、投屏、App Logs、去广告 | Zwind VIP |
| 临时试用 1 天 VIP 功能 | 入口可用时，看广告领取 1 天 VIP |
| 你已经在当前平台买过 VIP 或某个解析器 | 恢复购买 |

单独买断某个解析器，不等于整个 app 变成 VIP。比如买断 Web Media Projection 后，这个解析器可以用；但 App Logs、Server Lock、投屏、更多 server、其他付费解析器和去广告仍然不会一起解锁。

## 打开 VIP 和解析器入口

打开 **Settings / 设置**。点击 **Unlock Zwind VIP / 解锁 Zwind VIP** 会打开 VIP 购买页。点击 **Projection Resolvers / 投影解析器** 会进入解析器列表；这一行有 **VIP** 标记，是因为 VIP 可以解锁全部解析器，但每个解析器仍然可以单独买断。

![Settings 的 General 分组中，框选 Unlock Zwind VIP 和 Projection Resolvers。](/assets/docs/webdav-server/vip-buy-once-rewarded-vip/boxed/settings-vip-entry.png)

如果当前设备支持奖励广告，并且你还没有 VIP，Settings 里还可能出现 **Watch Ad to get 1 day VIP / 看广告领取 1 天 VIP**。点击后会进入广告领取流程。本文不展示广告页，因为广告内容来自广告网络，不是 Zwind 自己的界面。

## VIP 解锁什么

点击 **Unlock Zwind VIP / 解锁 Zwind VIP** 后会看到 VIP 解锁页。已经买过时点 **Restore Purchases / 恢复购买**；只有准备购买时才点具体商品的 **Unlock / 解锁**。

![Zwind VIP 解锁页中，框选 Restore Purchases 和 VIP 商品。](/assets/docs/webdav-server/vip-buy-once-rewarded-vip/boxed/vip-paywall.png)

VIP 是范围最大的解锁。VIP 有效时，Zwind 会把 VIP 功能和付费解析器扩展都视为可用。主要包括：

| 范围 | VIP 后有什么变化 |
| --- | --- |
| Servers | 可以启动超过免费限制的 server。 |
| 解析器扩展 | 付费解析器可用，不需要逐个买断。 |
| Server 保护 | Server Lock、Face ID 启动验证、受保护访问控制可用。 |
| 媒体工具 | 播放器支持的投屏等 VIP 媒体控制可用。 |
| 诊断 | **App Logs / 应用日志** 会直接打开，而不是进入 VIP 页。 |
| 广告 | Zwind 内原本会出现的广告不再显示。 |

## 什么时候只买断一个解析器就够

进入 **Settings / 设置 > Projection Resolvers / 投影解析器**，再打开你要用的解析器。如果它还没解锁，详情页会显示解锁按钮，并显示类似 **Buy once or use VIP / 单独买断或使用 VIP** 的状态。

如果你只需要这一个解析器，可以选择单独买断。买断后，在同一受支持平台上，即使没有 VIP，这个解析器也可以继续用。如果你会用多个解析器，或者还需要 App Logs、Server Lock、投屏、更多 server，则直接开 VIP 更合适。

解析器买断按“单个解析器”计算。买断 RSS 不会解锁 Web Media Projection、Emby 或夸克搜索转存。买断一个解析器也不会去广告或解锁 server 保护功能。

## 看广告领取 1 天 VIP

当 Settings 里出现 **Watch Ad to get 1 day VIP / 看广告领取 1 天 VIP** 时，看完整个奖励广告后，会获得 24 小时 VIP。这个 24 小时内，Zwind 会按 VIP 处理付费功能，包括付费解析器。

如果广告中途退出，不会发放 VIP。如果入口不可点，或提示广告暂不可用，说明广告网络暂时没有给这台设备准备好奖励广告；稍后再试，或改用付费 VIP。

广告领取的 VIP 是临时的。过期后，VIP 功能会重新锁定；但如果你已经买过正式 VIP，或单独买断了正在用的解析器，对应权益仍然有效。

## 恢复购买

这些情况用 **Restore Purchases / 恢复购买**：

| 场景 | 恢复购买会检查什么 |
| --- | --- |
| 重装了 Zwind | 当前 App Store 账号下已有的购买。 |
| 换了同平台设备 | 同一个商店账号和受支持平台上的购买。 |
| 付费后某个 VIP 功能或解析器仍显示未解锁 | 刷新购买凭据和权益状态。 |

恢复购买不会新买东西。如果 Zwind 提示没有恢复到购买，先确认你登录的是同一个 App Store 账号，并且购买发生在当前平台支持的范围内。

## 被权限拦住后怎么继续

Zwind 因权限打开解锁页时，按你刚才要做的动作处理：

| 被拦住的动作 | 下一步 |
| --- | --- |
| 启动更多 server | 开通 VIP，或使用有效期内的广告 VIP。 |
| 打开 App Logs | 开通 VIP，或使用有效期内的广告 VIP。 |
| 启用 Server Lock 或 Face ID 启动保护 | 开通 VIP，或使用有效期内的广告 VIP。 |
| 使用锁定的解析器 | 单独买断该解析器、开通 VIP，或使用有效期内的广告 VIP。 |
| 使用你已经买过的解析器 | 恢复购买，然后重新打开解析器详情页。 |

解锁后，回到刚才被拦住的页面再操作一次。修改 server 设置或 resolver binding 后，如果页面提示正在运行的 server 需要重新加载配置，就重启对应 server。
