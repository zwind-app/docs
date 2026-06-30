---
title: 管理 WebDAV 书签
description: 在 Zwind 中保存本机或外部 WebDAV URL，按需填写凭据，并从 Bookmarks 打开、编辑或删除书签。
seoTitle: 管理 Zwind WebDAV 书签 - Zwind 指南
keywords:
  - Zwind WebDAV 书签
  - WebDAV URL 书签
  - WebDAV 用户名密码
  - Zwind Bookmarks
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/webdav-bookmarks
order: 44
tags:
  - guide
  - bookmarks
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

WebDAV 书签适合保存之后还会再打开的位置：本机 Zwind server 上的某个目录、局域网里另一台设备的 Zwind 地址，或你能访问到的外部 WebDAV 服务。一个书签会保存 URL；如果这个 URL 需要认证，也可以一起保存 WebDAV 用户名和密码。

下面截图使用英文界面；中文界面位置相同。截图里的 **Bookmarks** 对应中文里的 **书签**，**Add Bookmark** 对应 **添加书签**，**Username (optional)** / **Password (optional)** 对应 **用户名（可选）** / **密码（可选）**。当前截图所用版本中，打开 Bookmarks 和保存书签没有出现 VIP 提示。

## 打开 Bookmarks

在首页点左上角的侧边栏按钮，然后在 **Builtin Apps / 内置工具** 里点 **Bookmarks / 书签**。

![首页侧边栏框选 Bookmarks 入口。](/assets/docs/webdav-server/webdav-bookmarks/boxed/home-bookmarks-entry.png)

进入 Bookmarks 后，会看到已经保存的 WebDAV 位置。点右上角 **+** 可以手动添加一个 URL。

## 添加 WebDAV URL

点 **+** 后填写书签表单。

![Add Bookmark 表单框选 URL、Username 和 Password 字段。](/assets/docs/webdav-server/webdav-bookmarks/boxed/add-bookmark-form.png)

各字段这样填写：

| 字段 | 填写方式 |
| --- | --- |
| **Bookmark name / 书签名称** | 可选显示名，例如 `Home NAS`、`Mac mini WebDAV`。不填时，Zwind 会用 URL 的主机名作为列表名称。 |
| **URL** | 完整的 `http://` WebDAV URL。可以是本机 Zwind 地址，例如 `http://127.0.0.1:8080/webdav/`，也可以是局域网地址或外部 WebDAV 服务地址。 |
| **Username (optional) / 用户名（可选）** | 只有当这个 URL 需要 WebDAV 认证时才填写。 |
| **Password (optional) / 密码（可选）** | URL 需要认证时，填写对应的 WebDAV 密码。 |

如果目标 WebDAV 可以匿名访问，**Username (optional) / 用户名（可选）** 和 **Password (optional) / 密码（可选）** 都可以留空。如果目标 WebDAV 要求登录，这里填的就是第三方 WebDAV 客户端里会填写的同一组用户名和密码。

确认后点 **Add / 添加** 保存书签。

## 保存当前 Browser 位置

如果你已经在 Zwind 的 Browser 里浏览某个 WebDAV server，可以长按文件或文件夹，在操作菜单里点 **Bookmark / 添加书签**。Zwind 会把当前位置的 URL 保存为书签，并打开 Bookmarks 页面。如果这个 server 本身配置了 WebDAV 用户名和密码，书签会一起保存这组凭据。

当目标 URL 不在当前 Browser 里，或者你想保存来自另一台设备、NAS、外部 WebDAV 服务的地址时，用右上角 **+** 手动添加更直接。

## 打开或编辑书签

在 Bookmarks 列表中，点书签这一行会用 Browser 打开这个 URL。如果 URL 指向文件夹，Browser 会进入该文件夹；如果 URL 指向文件，并且 Zwind 能识别它，会先进入父目录，再打开这个文件。

![已保存的书签行可以直接打开 URL，右侧铅笔按钮用于编辑。](/assets/docs/webdav-server/webdav-bookmarks/boxed/saved-bookmark-list.png)

点右侧铅笔按钮可以修改书签名称、URL、用户名或密码。当 WebDAV server 后来开启了认证，或服务器端密码已经更换时，就到这里更新凭据。

## 删除书签

在书签行上向左滑动，然后在 **Delete Bookmark / 删除书签** 确认框里点 **Delete / 删除**。

![向左滑动书签行后出现 Delete Bookmark 确认框。](/assets/docs/webdav-server/webdav-bookmarks/boxed/delete-bookmark-confirmation.png)

删除书签只会移除 Zwind 里保存的快捷入口，不会删除 WebDAV server 上的文件，也不会修改 server 配置。

## 和 VIP 权限的关系

当前截图所用版本中，Bookmarks 可以直接使用：侧边栏入口能打开，右上角 **+** 可以保存 URL，保存后的书签也能从列表打开。如果你的版本在打开或保存书签时出现 **Unlock Zwind VIP / 解锁 Zwind VIP** 提示，请先按提示解锁；解锁后书签的添加、打开和删除步骤不变。
