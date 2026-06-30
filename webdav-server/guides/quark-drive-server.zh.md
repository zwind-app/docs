---
title: 配置夸克云盘 server
description: 在 Zwind 中创建 QuarkDrive server，粘贴夸克 Cookie，启动后用 Browser 浏览云盘目录。
seoTitle: 配置夸克云盘 WebDAV server - Zwind iPhone 指南
keywords:
  - 夸克云盘 WebDAV
  - QuarkDrive server
  - Zwind 夸克云盘
  - iPhone 夸克 WebDAV
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/quark-drive-server
order: 33
tags:
  - guide
  - quark
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

要把夸克云盘账号里的文件作为 Zwind server 来源时，storage 类型选择 **QuarkDrive / 夸克云盘**。Zwind 会把你填入的夸克 Cookie 保存在这个 server 配置里，并用这份会话信息读取云盘目录。

## 准备夸克 Cookie

**Quark Cookie / 夸克 Cookie** 是账号会话凭据。拿到可用 Cookie 的人可以使用这次登录会话访问账号内容，所以只使用你信任的工具或流程获取自己账号的 Cookie，然后只把 Cookie 值粘贴进 Zwind。

Cookie 通常是用分号分隔的片段，例如 `__puus=...; kps=...`。不要把 `Cookie:` 这个请求头名字、请求 URL、浏览器命令或其他说明文字一起粘贴进去。

Cookie 过期后，不需要重建 server。重新获取一份 Cookie，回到 server 配置里替换 **Quark Cookie / 夸克 Cookie** 即可。

## 选择 QuarkDrive 类型

首次首页的 server 卡片里，点击 **使用夸克云盘 / Use Quark Drive**。如果已经有 server，点左下角 **+** 新建一个 server，再把 storage 类型选成 **QuarkDrive / 夸克云盘**。

![在第一个 server 卡片中选择 Use Quark Drive。](/assets/docs/webdav-server/quark-drive-server/use-quark-drive.png)

进入配置页后，确认 **Storage Type / 存储类型** 显示为 **QuarkDrive**。这个类型会在通用 server 字段里显示 **Quark Cookie / 夸克 Cookie**。

![QuarkDrive 配置页包含 Quark Cookie 字段。](/assets/docs/webdav-server/quark-drive-server/quark-drive-form.png)

## 粘贴 Cookie 并保存

把 Cookie 粘贴到 **Quark Cookie / 夸克 Cookie**。截图里是短占位值；实际使用时填你自己夸克登录会话对应的 Cookie。

![Quark Cookie 字段已填入占位值。](/assets/docs/webdav-server/quark-drive-server/quark-cookie-filled.png)

**Port / 端口** 保持 `0` 时，Zwind 会在启动 server 时自动选择可用端口。点 **保存 / Save**。如果 **保存 / Save** 仍是灰色，先检查 **Quark Cookie / 夸克 Cookie** 是否为空。

## 启动 server 并浏览云盘目录

保存后，首页会出现这个 QuarkDrive server，并显示一个虚拟根目录 **/QuarkDrive**。点击 **启动 Server / Start Server** 启动。

![保存后的 QuarkDrive server 会显示 QuarkDrive 根目录。](/assets/docs/webdav-server/quark-drive-server/quark-server-card.png)

server 运行后，打开右下角 server 菜单，选择 **浏览文件 / Browse Files**。Browser 会打开这个 server 的根目录；进入 **/QuarkDrive** 后，就能浏览这份 Cookie 对应夸克账号可访问的云盘文件夹和文件。

![从 server 菜单选择 Browse Files，在 Browser 中打开 server。](/assets/docs/webdav-server/quark-drive-server/browser-menu.png)

如果填的是占位 Cookie，或 Cookie 已过期，配置页仍可能保存成功，但 Browser 不能列出真实夸克云盘内容。

## Cookie 过期后替换

夸克登录会话失效或 Cookie 过期后，在首页选中这个 QuarkDrive server，点击 **编辑 / Edit**。把 **Quark Cookie / 夸克 Cookie** 里的旧值替换成新 Cookie，再点 **保存 / Save**。

如果 server 正在运行，先停止再重新启动。然后重新进入 **浏览文件 / Browse Files**，在 Browser 里刷新目录。

## 无法访问时检查什么

按现象区分处理：

| 现象 | 检查项 |
| --- | --- |
| **保存 / Save** 是灰色 | **Quark Cookie / 夸克 Cookie** 为空。粘贴 Cookie 值，不要只填空格或字段名。 |
| server 能启动，但 Browser 无法列出 **/QuarkDrive** | Cookie 过期、不完整，或来自已经退出登录的会话。重新获取 Cookie 后替换。 |
| Browser 一直等待或提示连接、网络错误 | 当前网络访问不到夸克服务。换到能正常打开夸克云盘的网络后再试。 |
| Browser 能打开，但看不到预期文件夹 | 这份 Cookie 对应的夸克账号没有这些文件的权限，或该账号云盘目录为空。到夸克 App 或网页确认同一个账号下是否能看到这些内容。 |
