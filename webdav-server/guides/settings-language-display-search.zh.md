---
title: 设置语言、显示模式和默认搜索引擎
description: 在 Zwind 设置中切换 app 语言，选择经典、浅色、深色或跟随系统显示模式，并配置 Browser 默认搜索引擎和自定义搜索 URL。
seoTitle: 设置 Zwind 语言、显示模式和 Browser 默认搜索引擎 - Zwind 指南
keywords:
  - Zwind 语言设置
  - Zwind 显示模式
  - Zwind 默认搜索引擎
  - Zwind 自定义搜索 URL
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/settings-language-display-search
order: 54
tags:
  - guide
  - settings
  - browser
  - search
publishedAt: 2026-07-01
updatedAt: 2026-07-01
draft: false
---

如果你想让 Zwind 固定使用某种语言、固定在浅色或深色界面，或更换 app 把搜索词打开到 Browser 时使用的搜索服务，都在 **Settings / 设置** 里完成。

下面截图使用英文 UI。中文界面中，**Language** 对应 **语言**，**Appearance** 对应 **显示模式**，**Browser default search engine** 对应 **浏览器默认搜索引擎**。

## 打开这几个设置项

在首页点击齿轮进入 **Settings / 设置**。**General / 通用** 分组里有 **Language / 语言** 和 **Appearance / 显示模式**；继续往下到 **Configuration / 配置**，可以看到 **Browser default search engine / 浏览器默认搜索引擎**。

![Settings 中框选 Language、Appearance 和 Browser default search engine。](/assets/docs/webdav-server/settings-language-display-search/boxed/settings-preferences.png)

## 切换 app 语言

点击 **Language / 语言**，在弹出的菜单里选择语言。

![Language 菜单中有 Follow System、English 和中文，当前选项右侧有勾。](/assets/docs/webdav-server/settings-language-display-search/boxed/language-sheet.png)

| 选项 | 作用 |
| --- | --- |
| **Follow System / 跟随系统** | 设备系统语言是 Zwind 支持的语言时，Zwind 跟随系统显示。 |
| **English / 英语** | 不管设备系统语言是什么，Zwind 都固定显示英文。 |
| **中文 / Chinese** | 不管设备系统语言是什么，Zwind 都固定显示中文。 |

语言切换会立即作用在 Zwind 内部界面。iOS 系统界面仍跟随设备语言，例如分享页、文件选择器、权限弹窗和键盘。

## 切换显示模式

点击 **Appearance / 显示模式**。右侧有勾的选项就是当前模式。

![Appearance 菜单中有 Follow System、Classic、Light 和 Dark。](/assets/docs/webdav-server/settings-language-display-search/boxed/appearance-sheet.png)

| 选项 | 作用 |
| --- | --- |
| **Follow System / 跟随系统** | 跟随 iOS 的浅色或深色外观。 |
| **Classic / 经典** | 使用 Zwind 原来的浅色配色。 |
| **Light / 浅色** | 固定使用浅色界面。 |
| **Dark / 深色** | 固定使用深色界面。 |

想让 Zwind 随系统一起切换，就选 **Follow System / 跟随系统**。如果你希望 app 一直保持同一种观感，就选 **Classic / 经典**、**Light / 浅色** 或 **Dark / 深色**。

## 设置 Browser 默认搜索引擎

滚动到 **Configuration / 配置**，点击 **Browser default search engine / 浏览器默认搜索引擎**，可以选择 **Google**、**Bing**、**Baidu / 百度** 或 **Custom URL / 自定义 URL**。

![Default Search Engine 菜单中有 Google、Bing、Baidu 和 Custom URL。](/assets/docs/webdav-server/settings-language-display-search/boxed/search-engine-sheet.png)

这个设置用于 Zwind 需要把一段搜索词转换成网页搜索 URL 的场景，例如从 app 内的搜索动作打开内置 Web Browser。它不会改写你直接输入或打开的 URL：`https://example.com/video` 仍会作为完整 URL 打开，像 `example.com` 这样的域名输入也仍按网站地址处理。

搜索引擎偏好会包含在 Zwind 的配置导出、导入和 iCloud 配置同步里。语言和显示模式属于本机 app 偏好，不跟随这份配置文件迁移。

## 填写自定义搜索 URL

选择 **Custom URL / 自定义 URL** 后，输入一个搜索 URL 前缀。Zwind 会把搜索词做 URL 编码，然后直接拼在你填写的内容后面。

![Custom Search URL 弹窗提示搜索词会经过 URL 编码并追加到这个 URL 后面。](/assets/docs/webdav-server/settings-language-display-search/boxed/custom-search-url.png)

填写时要使用完整的 `http://` 或 `https://` URL，并把搜索词前面的查询参数也写进去：

| 搜索服务 | 自定义 URL 填写值 |
| --- | --- |
| Google | `https://www.google.com/search?q=` |
| Bing | `https://www.bing.com/search?q=` |
| 百度 | `https://www.baidu.com/s?wd=` |
| DuckDuckGo | `https://duckduckgo.com/?q=` |

不要写 `{q}` 或 `%s` 这类占位符；Zwind 不会替换占位符，只会把编码后的搜索词追加到末尾。比如自定义 URL 是 `https://duckduckgo.com/?q=`，搜索 `webdav server` 时会打开 `https://duckduckgo.com/?q=webdav%20server`。

如果没有写 `http://` 或 `https://`，或者 URL 的 host 无法解析，Zwind 会提示 **Invalid URL / URL 无效**。如果 URL 结构上有效但末尾没有查询分隔符，也可能保存成功，只是搜索词会直接粘到 URL 末尾；因此要按搜索服务要求补上最后的 `=`、`/` 或其他分隔符。
