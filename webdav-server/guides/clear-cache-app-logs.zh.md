---
title: 清除缓存和查看应用日志
description: 在 Zwind 设置中清除媒体预览缓存，并使用 App Logs 查看 server、WebDAV、native bridge 和 app 诊断日志。
seoTitle: 清除 Zwind 媒体缓存和查看 App Logs - Zwind 指南
keywords:
  - Zwind 清除媒体缓存
  - Zwind 应用日志
  - Zwind App Logs
  - Zwind VIP 日志
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/clear-cache-app-logs
order: 55
tags:
  - guide
  - settings
  - cache
  - logs
  - vip
publishedAt: 2026-07-01
updatedAt: 2026-07-01
draft: false
---

如果 **Media General Search / 媒体通搜** 里的视频预览图不对、一直显示失败，或你想释放这部分本地缓存空间，可以用 **Clear media cache / 清除媒体缓存**。如果 server 启动、WebDAV 请求、解析器刷新、native WebDAV 引擎调用出问题，则看 **App Logs / 应用日志**。

下面截图使用英文 UI。中文界面中，**Clear media cache** 对应 **清除媒体缓存**，**App Logs** 对应 **应用日志**，**Share Logs** 对应 **分享日志**，**Copy Logs** 对应 **复制日志**，**Clear Logs** 对应 **清除日志**。

## 媒体预览缓存影响什么

这里的媒体缓存只针对 **Media General Search / 媒体通搜** 生成的视频预览帧。搜索结果里出现视频预览图时，Zwind 会把生成出的 JPEG 预览帧存到 app 的本地支持目录里；下次同一路径再次出现在结果中，就可以更快显示预览。

它不是原始视频文件，也不是解析器缓存。清除它不会删除 Emby 元数据缓存、RSS materialize 内容、夸克转存记录、resolver 结果、配置文件、书签、App Logs 或购买状态。

这些情况适合清除：

| 场景 | 为什么清除有用 |
| --- | --- |
| 视频内容换了，但 WebDAV 路径没变 | 旧预览帧可能仍然挂在同一个路径上。 |
| 媒体通搜里的预览格一直失败或空白 | 失败记录会被清掉，下次可以重新尝试生成。 |
| 预览缓存占用了较多本地空间 | 扫描大量视频后缓存会增长，自动清理只会在达到缓存上限后触发。 |
| 你调整了 server 来源、认证或投影结果，预览看起来和当前内容不一致 | 清除后，之后的预览会从当前来源重新生成。 |

## 清除媒体缓存

打开 **Settings / 设置**，滚动到 **Configuration / 配置**，点击 **Clear media cache / 清除媒体缓存**。

![Settings 的 Configuration 分组中，框选 Clear media cache。](/assets/docs/webdav-server/clear-cache-app-logs/boxed/settings-cache-row.png)

Zwind 会先弹出确认框，避免误删已经生成的预览帧。

![Clear media cache 确认框提示将删除所有已缓存预览。](/assets/docs/webdav-server/clear-cache-app-logs/boxed/clear-cache-confirm.png)

点击 **Confirm / 确认** 后，Zwind 会清空媒体预览缓存。已有 Browser 目录、server、resolver binding、书签、日志和配置都不会改变。下次媒体通搜需要视频预览时，Zwind 会重新生成。

## 打开 App Logs

在 **Settings / 设置** 中滚动到 **Support / 支持**，点击 **App Logs / 应用日志**。这一行带有 **VIP** 标记，表示日志功能需要 Zwind VIP。

![Settings 的 Support 分组中，框选带 VIP 标记的 App Logs。](/assets/docs/webdav-server/clear-cache-app-logs/boxed/app-logs-row.png)

如果当前没有 VIP，点击后会先进入 VIP 解锁页，而不是直接打开日志。付费 VIP 和观看广告领取到的 1 天 VIP 在有效期内都算 VIP；单独买断某个 resolver 只解锁对应解析器，不会单独解锁 App Logs。

## 看日志来源

App Logs 页面会按来源显示日志。点击顶部蓝色来源标签可以隐藏或显示对应日志；一条日志太长时，点击该条可以展开。

![App Logs 页面中显示来源筛选标签和近期诊断日志。](/assets/docs/webdav-server/clear-cache-app-logs/boxed/app-logs-screen.png)

常见来源含义如下：

| 来源 | 主要用来排查 |
| --- | --- |
| **App Logic** | app 级事件，例如 server 启动结果、广告领取 VIP 状态、导入或刷新结果、已捕获错误。 |
| **SwiftWebDAV** | WebDAV 请求和响应、状态码、路由错误、native server 行为。 |
| **Native Bridge** | Flutter 和 iOS native 层之间的调用结果，例如启动或停止 server。 |
| **Flutter SDK** | Flutter 框架层捕获到的错误。 |

某些构建或登记为测试设备的设备上，还可能看到 **Flutter UI**、**SwiftWebDAV Console** 等额外来源。这些日志更吵，主要给 copy review 或深度调试使用，普通设备默认不会显示。

App Logs 只保存在本机。Zwind 会保留较新的日志，列表数量和日志文件大小都有上限；如果后续产生了大量新日志，很早以前的记录可能会被移除。

## 分享、复制或清空日志

在 App Logs 页面点击右上角省略号按钮。

![App Logs 操作菜单中有 Share Logs、Copy Logs 和 Clear Logs。](/assets/docs/webdav-server/clear-cache-app-logs/boxed/app-log-actions.png)

| 操作 | 作用 |
| --- | --- |
| **Share Logs / 分享日志** | 打开 iOS 分享页，把当前保存的日志文本发给其他 app。 |
| **Copy Logs / 复制日志** | 把日志文本复制到剪贴板。 |
| **Clear Logs / 清除日志** | 删除本设备上保存的 App Log 条目。 |

日志里可能出现 server 名称、文件路径、WebDAV 路径、URL、请求状态、设备标识或外部服务返回的错误。发给别人之前，先看一遍文本内容。

清空日志不会清除媒体预览、resolver 缓存、配置、购买状态，也不会删除任何 WebDAV server 正在提供的文件。
