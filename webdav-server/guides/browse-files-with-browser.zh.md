---
title: 使用内置 Browser 浏览文件
description: 从 Zwind 首页打开 Browser，切换目录、返回上级、输入路径或 URL、刷新目录并调整排序。
seoTitle: 使用 Zwind Browser 浏览 WebDAV 文件 - Zwind 指南
keywords:
  - Zwind Browser
  - WebDAV 文件浏览
  - 浏览 WebDAV 文件
  - iPhone WebDAV Browser
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/browse-files-with-browser
order: 36
tags:
  - guide
  - browser
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Zwind Browser 可以在 app 内直接打开一个 server。你可以用它检查目录结构、打开文件、复制路径，或者确认第三方客户端要访问的 URL 在 Zwind 内是否可达。

下面截图使用英文界面；中文界面里的按钮位置相同。

## 从首页打开 Browser

在首页选中 server 卡片，打开右下角 server 菜单，选择 **浏览文件 / Browse Files**。

![从选中 server 的菜单里打开 Browse Files。](/assets/docs/webdav-server/browse-files-with-browser/home-browse-files-menu.png)

Browser 会用当前 server 地址打开这个 server。如果 server 还没有运行，Zwind 会先启动或解析本机 Browser 会话，然后进入目录。

## 看懂 Browser 顶部工具栏

顶部栏显示当前 WebDAV 地址和路径。下面的列表显示当前目录里的文件夹和文件。

![Browser 显示当前地址、路径、文件夹和文件。](/assets/docs/webdav-server/browse-files-with-browser/browser-root-list.png)

这些控件分别这样用：

| 控件 | 作用 |
| --- | --- |
| **返回 / Back** 箭头 | 回到上一个 Browser 位置；没有上一个位置时离开 Browser。 |
| **上级 / Up** 箭头 | 回到当前路径的父目录。 |
| 地址或路径输入框 | 手动输入路径或完整 URL。 |
| 排序按钮 | 调整当前列表排序；支持时长按可打开排序菜单。 |
| 悬浮 **+** 按钮 | 打开当前目录的文件和文件夹操作。 |
| 悬浮搜索按钮 | 在当前目录中搜索。 |

点击文件夹行会进入下一级目录。点击文件行时，Zwind 会根据文件类型打开预览、播放器、编辑器或操作菜单。

## 进入目录和返回上级

点击一个文件夹行即可进入。Browser 会在地址下方更新路径，让你看到当前正在浏览哪个目录。

![进入文件夹后，路径会显示在地址下方。](/assets/docs/webdav-server/browse-files-with-browser/browser-inside-folder.png)

点击工具栏里的 **上级 / Up** 箭头返回父目录。需要回到上一个 Browser 页面时，使用 **返回 / Back** 箭头；它不一定等同于“父目录”。

## 手动输入路径或 URL

想直接跳转时，点击顶部的地址或路径输入框。

已经在浏览同一个 server 时，可以输入路径：

```text
/Movies
```

想让 Browser 打开某个完整 WebDAV 地址时，输入完整 URL：

```text
http://192.168.50.49:52500/Movies
```

如果 server 的 **Port / 端口** 设置为 `0`，使用 server 运行时当前显示的地址和端口。如果 server 使用固定端口，并且能用这个端口启动，就继续填写这个固定端口。

## 刷新和排序目录

在文件列表上下拉可以刷新当前目录。另一台设备刚改过文件、投影结果刚更新，或者从外部 app 回到 Browser 后，可以刷新一次当前目录。

点击排序按钮会调整或应用当前排序方式。当前 Browser 视图支持更细选项时，长按排序按钮可以打开排序菜单。排序只影响当前列表显示顺序，不会重命名文件，也不会改动 server 里的数据。

## 列表显示不符合预期时

按现象检查：

| 现象 | 检查项 |
| --- | --- |
| Browser 打开根目录，但看不到某个挂载文件夹 | 确认数据文件夹仍然挂在这个 server 下，并且添加后保存过 server。 |
| 文件夹能打开，但里面是空的 | 源目录可能确实为空，或者上游来源还没返回条目。刷新当前目录。 |
| 手动 URL 打不开 | 检查协议、IP、端口、路径拼写；如果关闭匿名访问，还要检查 WebDAV 用户名和密码。 |
| 同一个 URL 在 Browser 能打开，另一台设备打不开 | server 在本机可达；重点检查另一台设备的网络、URL 字段和凭据。 |
