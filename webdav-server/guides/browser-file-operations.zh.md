---
title: 在 Browser 中创建、编辑和整理文件
description: 在 Zwind Browser 中新建文件和文件夹，重命名、复制、移动、创建副本、删除，并分享文件或链接。
seoTitle: 在 Zwind Browser 中管理 WebDAV 文件 - Zwind 指南
keywords:
  - Zwind Browser 文件操作
  - WebDAV 新建文件
  - WebDAV 重命名 移动 复制
  - iPhone WebDAV 文件管理
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/browser-file-operations
order: 37
tags:
  - guide
  - browser
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

当前来源支持 WebDAV 写操作时，Browser 可以在目录里写入内容。本地文件夹通常可以新建和编辑文件；SMB、夸克云盘和投影目录是否可写，取决于上游服务和这个路径背后的 resolver。

下面截图使用英文界面；中文界面里的按钮位置相同。

## 先进入可写目录

打开 Browser 后，进入你要操作的挂载文件夹。server 根目录通常显示的是挂载来源列表，所以新建或上传文件应在某个挂载文件夹里面进行，而不是直接在根目录进行。

![当前 Browser 文件夹里会显示悬浮加号按钮。](/assets/docs/webdav-server/browser-file-operations/writable-folder-actions.png)

悬浮 **+** 按钮用于在当前目录里新增内容。文件或文件夹行的长按菜单用于操作被选中的那个项目。

## 新建文件或文件夹

点击悬浮 **+** 按钮。菜单里选择 **新建目录 / New Directory** 可以创建文件夹，选择 **新建文件 / New File** 可以创建文本文件。

![加号菜单包含 New Directory 和 New File。](/assets/docs/webdav-server/browser-file-operations/new-item-menu.png)

新建文件时输入文件名，并保留需要的扩展名，例如 `.txt`、`.md`、`.json` 或 `.m3u`。扩展名会影响 Zwind 和其他 app 后续用什么方式打开它。

![New File 会先要求输入文件名。](/assets/docs/webdav-server/browser-file-operations/new-file-dialog.png)

创建完成后，新项目会出现在当前目录。如果同一目录也被其他客户端改动过，可以下拉刷新一次。

## 使用文件或文件夹操作菜单

长按一个文件或文件夹行，会打开这个项目的操作菜单。

![长按文件后可看到打开、分享、重命名、复制、移动、创建副本和删除等操作。](/assets/docs/webdav-server/browser-file-operations/file-actions-menu.png)

常用操作：

| 操作 | 作用 |
| --- | --- |
| **重命名 / Rename** | 修改当前项目在同一目录下的名字。除非要改变打开方式，否则保留原扩展名。 |
| **复制 / Copy** | 把项目复制到另一个 Browser 位置。 |
| **移动 / Move** | 把项目移动到另一个 Browser 位置，并从原目录移除。 |
| **创建副本 / Duplicate** | 在当前目录再创建一份副本。Zwind 会选择或要求一个不会覆盖原项目的名字。 |
| **删除 / Delete** | 确认后删除选中项目。 |
| **分享 / Share** | 用 iOS 分享面板分享文件或选中项目。 |
| **复制链接 / Copy Link** | 复制这个项目的 WebDAV URL。 |
| **分享链接 / Share Link** | 用 iOS 分享面板分享这个项目的 WebDAV URL。 |

部分操作只会在当前文件类型或来源支持时出现。

## 编辑文本文件

对文本类文件，长按文件并选择 **在文本编辑器中打开 / Open in Text Editor**。保存时，Zwind 会把修改写回同一个 WebDAV 项目；如果当前来源只读，或上游服务拒绝写入，编辑器不能把修改保存到这个路径。

## 分享文件或链接

对方需要文件内容时，用 **分享 / Share**。对方要通过 WebDAV 打开这个项目时，用 **复制链接 / Copy Link** 或 **分享链接 / Share Link**。

链接会包含 server 地址、端口和项目路径。如果关闭了匿名访问，接收方的客户端仍然需要填写这个 server 的 WebDAV 用户名和密码。如果 **Port / 端口** 是 `0`，请在 server 正在运行时复制链接，这样链接里会使用当前端口。

## 操作失败时检查什么

按失败位置定位：

| 失败项 | 检查项 |
| --- | --- |
| 找不到 **新建文件 / New File** 或 **新建目录 / New Directory** | 你可能在 server 根目录、只读投影目录，或当前来源不支持写入。先进入一个挂载的数据文件夹。 |
| 新建、重命名、复制、移动或创建副本失败 | 上游来源可能拒绝写入，目标目录可能已有同名项目，或当前账号没有写权限。 |
| 删除失败 | 来源可能只读，项目可能已经被其他客户端改动，或上游服务拒绝删除。刷新后再确认来源状态。 |
| 分享成功，但另一台设备打不开链接 | 检查 server 是否运行、URL 是否使用当前端口，以及对方客户端是否填写了所需的 WebDAV 凭据。 |
