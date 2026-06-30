---
title: 添加和管理本地数据文件夹
description: 给本地 Zwind server 添加 iOS Files 文件夹，理解挂载名，重命名或移除映射，并区分 WebDAV 根目录和数据文件夹。
seoTitle: 添加和管理 Zwind WebDAV 本地数据文件夹 - Zwind 指南
keywords:
  - Zwind 数据文件夹
  - iPhone WebDAV 文件夹挂载
  - iOS 本地 WebDAV 文件夹
  - Zwind 挂载名
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/manage-local-data-folders
order: 32
tags:
  - guide
  - server
  - local-folders
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

本地文件系统 server 不会自动暴露整台 iPhone 或 iPad。你要先添加一个或多个数据文件夹，Zwind 才会把这些文件夹挂到 WebDAV 根目录下。

## 添加数据文件夹

创建或选中一个 **Local FileSystem / 本地文件系统** server。没有数据文件夹时，当前 server 卡片会显示 **Add Folder / 添加文件夹**。点它进入 iOS Files 选择器。

![在当前本地 server 卡片上点击 Add Folder。](/assets/docs/webdav-server/manage-local-data-folders/add-folder-entry.png)

在 Files 选择器里选择一个目录。可以来自 **On My iPhone / 我的 iPhone**、iCloud Drive，或其他支持目录选择的 Files provider。截图里的 Files 选择器跟随系统语言，所以会看到 **浏览 / Browse**、**我的 iPhone / On My iPhone**、**打开 / Open** 这类系统按钮。

![从 iOS Files 选择器里选择一个目录。](/assets/docs/webdav-server/manage-local-data-folders/files-picker.png)

确认后，Zwind 回到首页，并把这个目录显示在 server 行下面。

![选中的目录会出现在本地 server 下面。](/assets/docs/webdav-server/manage-local-data-folders/folder-mounted.png)

## 挂载名是什么

首页数据文件夹行显示的是文件夹名称。WebDAV 根目录里显示的是挂载名，也就是客户端在 `/` 下面看到和打开的入口名。

例如 Files 里的文件夹叫 `File Provider Storage`，WebDAV 根目录里可能显示为：

```text
/File_Provider_Storage/
```

这个挂载名不是 iPhone 或 iCloud Drive 里的原始路径。它只是 Zwind 对外提供 WebDAV 访问时使用的入口名。你在 Zwind 里重命名它，只会改变 WebDAV 入口，不会重命名或移动 Files 里的原始目录。

## 重命名或移除数据文件夹

在首页展开本地 server 行，然后把某个数据文件夹向左滑动。

![左滑数据文件夹行会显示 Rename 和 Delete。](/assets/docs/webdav-server/manage-local-data-folders/folder-actions.png)

点 **Rename / 重命名** 可以修改这个数据文件夹在 WebDAV 里的入口名。如果名称里有空格或不适合 URL 的字符，Zwind 会把它转换成适合 WebDAV 路径的形式。

点 **Delete / 删除** 是把这个数据文件夹从当前 server 中移除。确认弹窗会询问是否从 server 移除，因为这个操作只解除映射，不会删除原始目录里的文件。

## 根目录只列出挂载入口

启动 server 后，在 Zwind Browser 打开 `/`，根目录会列出已经挂载的数据文件夹入口。

![Browser 根目录显示已经挂载的数据文件夹入口。](/assets/docs/webdav-server/manage-local-data-folders/browser-root-mount.png)

WebDAV 根目录本身不是普通可写文件夹。它只用来列出 `/File_Provider_Storage/` 这类挂载入口。客户端如果直接在 `/` 下新建或上传，操作应该失败或不可用；先进入某个数据文件夹，再在里面写入文件。
