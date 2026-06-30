---
title: 使用 Web Media Projection 解析网页媒体
description: 将 Web Media Projection 绑定到 WebDAV 目录，创建和编辑 .wm 标记文件，刷新投影结果，并在 Zwind Browser 中打开解析出的媒体文件。
seoTitle: "使用 Zwind Web Media Projection 解析网页媒体"
keywords:
  - Web Media Projection
  - .wm 标记文件
  - 网页媒体 WebDAV
  - Zwind 网页媒体解析器
  - 重新解析 Web Media
productSlug: webdav-server
section: 指南
locale: zh
translationOf: webdav-server/guides/web-media-projection
parent: guides
order: 48
tags:
  - guide
  - web-media
  - wm-rule
  - projection
  - webdav
publishedAt: 2026-05-24
updatedAt: 2026-06-30
draft: false
---

Web Media Projection 可以把网页媒体列表投影成一个虚拟 WebDAV 目录。你把解析器绑定到 `/WebMedia` 这样的目录，在目录里放 `.wm` 标记文件，Zwind 就会根据文件里的规则解析列表页、条目页和媒体链接，并在 Browser 中显示为可浏览、可播放的文件结构。

截图使用英文界面和本地示例页面，不依赖外部网页广告或会变化的公开网站。

## 开始前检查权限

你需要拥有 **Web Media Projection** 权限。打开 **Explore Resolvers（探索解析器）**，进入 **Web Media Projection**，查看状态。如果显示 **Unlocked（已解锁）**，可以继续。只有当这里显示锁定时，才需要按锁定提示购买单独解析器或解锁 Zwind VIP。

![Web Media Projection 详情页，框选了解锁状态、支持的存储类型和使用摘要。](/assets/docs/webdav-server/web-media-projection/boxed/01-resolver-detail.png)

还需要有一个 server 能暴露目标目录。绑定路径必须落在这个 server 可以访问的 WebDAV 路径内。如果数据文件夹在 Browser 中显示为 `/Files`，可以绑定 `/Files/WebMedia`；如果数据文件夹本身就挂载为 `/WebMedia`，直接使用 `/WebMedia`。

## 绑定到 /WebMedia

进入 server 设置，在 **Resolver Bindings（解析器绑定）** 中点 **Add（添加）**，选择 **Web Media Projection**，保持启用，并把 **Path（路径）** 设为存放 `.wm` 文件的目录。常见路径是 `/WebMedia`。

![解析器绑定编辑器中，Web Media Projection 已启用并绑定到 /WebMedia。](/assets/docs/webdav-server/web-media-projection/boxed/02-binding-editor.png)

保存绑定后，再保存 server。修改解析器绑定后需要启动或重启 server，新的绑定才会被 native WebDAV server 读取。

## 创建并编辑 .wm 文件

在 Browser 中打开绑定目录。新建一个以 `.wm` 结尾的文本文件，例如 `sample-by-item.wm`、`shows.wm` 或 `gallery.wm`。

![Browser 中的 /WebMedia 目录，里面有两个 .wm 标记文件。](/assets/docs/webdav-server/web-media-projection/boxed/03-marker-files.png)

用 **Text Editor（文本编辑器）** 打开这个 `.wm` 文件，粘贴或修改 Web Media 规则，然后点 **Save（保存）**。文件内容决定 Zwind 从哪个网页开始解析以及如何找到媒体；本篇只把它当作已经准备好的规则使用，不逐项解释规则字段。具体字段会在单独的 `.wm` 规则文档中说明。

![Text Editor 中的本地 .wm 示例规则。](/assets/docs/webdav-server/web-media-projection/boxed/04-text-editor-wm-rule.png)

`.wm` 文件可以在 Browser 里创建，也可以从其他 WebDAV 客户端写入。Bilibili 来源还可以通过 Feed View 的 **Bilibili UP** 来源创建 `.wm` 文件；创建完成后仍然回到同一个流程：保存标记文件，回到 Browser，打开投影目录。

## 刷新并浏览投影结果

回到 Browser，刷新或重新进入绑定目录。`.wm` 标记文件会表现为一个投影目录，点进去即可查看解析结果。

![打开 .wm 后的投影目录，包含条目文件夹和 source.json。](/assets/docs/webdav-server/web-media-projection/boxed/05-projected-items.png)

如果规则输出的是 by-item 形态，每个网页条目会显示为一个文件夹。进入条目文件夹后，可以看到可播放的媒体文件，以及 `item.json`、`detail.url`、`media.url`、`thumbnail.url` 这类辅助文件。

![条目文件夹中显示解析出的 MP4 文件、条目元数据和 URL 辅助文件。](/assets/docs/webdav-server/web-media-projection/boxed/06-item-media-files.png)

有些规则会输出 flat 形态。flat 会把媒体文件直接放在 `.wm` 投影目录下，而不是每个条目一个文件夹。需要保留每个网页条目的上下文时用 by-item；媒体客户端只想看到一层文件列表时用 flat。

## 网页变化后重新解析

如果网站改版，已有规则可能无法继续找到条目或媒体。在 Web Media 路径中打开右下角操作菜单，点 **Re-parse（重新解析）**。这个操作会清掉当前范围的缓存，并让 Zwind 重新解析页面。

![Browser 操作菜单中显示当前 Web Media 路径可用的 Re-parse。](/assets/docs/webdav-server/web-media-projection/boxed/07-reparse-menu.png)

如果重新解析后仍然没有期望的文件，Browser 中可能会显示 **Web Media Debug（Web Media 调试）** 入口，也可以复制调试报告交给规则维护者。本篇只讲用户操作链路；selector 字段、browser runtime 选项和调试报告含义会放在 `.wm` 规则文档中。
