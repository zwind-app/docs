---
title: 导出、导入和同步配置
description: 在 Zwind 设置中导出配置文件、导入 YAML、理解导入前自动备份，并确认 iCloud 配置同步的范围和边界。
seoTitle: 导出、导入和同步 Zwind WebDAV Server 配置 - Zwind 指南
keywords:
  - Zwind 导出配置
  - Zwind 导入配置
  - Zwind iCloud 同步
  - WebDAV server 配置备份
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/export-import-sync-config
order: 53
tags:
  - guide
  - configuration
  - sync
publishedAt: 2026-07-01
updatedAt: 2026-07-01
draft: false
---

Zwind 有两种方式迁移 WebDAV 配置：**Export Configuration / 导出配置** 会生成一个 YAML 文件；**Import Configuration / 导入配置** 会读取这个 YAML 并应用到当前 app；**iCloud Sync / iCloud 同步** 会在登录同一 iCloud 账号的 iOS 设备之间同步支持的配置字段。

下面截图里的 Zwind 界面是英文。iOS 系统分享页和文件选择器跟随设备系统语言，所以会看到 **存储到“文件” / Save to Files**、**取消 / Cancel**、**我的 iPhone / On My iPhone** 这类系统按钮。

## 打开配置设置

在首页点右上角齿轮进入 **Settings / 设置**，滚动到 **Configuration / 配置**。这里有 **Export Configuration / 导出配置**、**Import Configuration / 导入配置** 和 **iCloud Sync / iCloud 同步**。

![Settings 的 Configuration 分组中，框选 Export Configuration、Import Configuration 和 iCloud Sync。](/assets/docs/webdav-server/export-import-sync-config/boxed/settings-configuration.png)

## 导出配置文件

点击 **Export Configuration / 导出配置**。Zwind 会生成一个类似 `zwind_config_YYYYMMDD_HHMMSS.yaml` 的 YAML 文件，并打开 iOS 分享页。想把它保存下来供以后恢复或在另一台设备导入时，选择 **Save to Files / 存储到“文件”**。

![导出配置后打开 iOS 分享页，框选 Save to Files / 存储到“文件”。](/assets/docs/webdav-server/export-import-sync-config/boxed/export-share-sheet.png)

导出的 YAML 是一份配置快照。它适合用于迁移到另一台设备、在大幅调整设置前保留回滚文件，或让另一台 Zwind 使用同一组 server 和书签。

这份文件包含 server 配置、数据文件夹条目、resolver bindings、WebDAV 书签、Browser quick links，以及 Browser 默认搜索引擎。WebDAV 密码、SMB 密码、夸克 Cookie、Server Lock 密码、书签凭据、resolver secret 字段等可恢复信息会以编码形式写入文件。不要把它当成普通说明文档发送给别人；能导入这份 YAML 的人，可以把这些已保存凭据恢复到 Zwind 里。

导出文件不包含本地文件内容、媒体缓存、app 日志、购买权益、系统权限，也不包含某个 server 当前是否正在运行。

## 导入配置文件

点击 **Import Configuration / 导入配置**，在 iOS 文件选择器里选择 `.yaml` 或 `.yml` 文件。

![导入配置会打开 iOS 文件选择器，用来选择 YAML 配置文件。](/assets/docs/webdav-server/export-import-sync-config/boxed/import-file-picker.png)

导入时，Zwind 会先把当前配置写成一份自动备份，保存在 app support 目录。导入成功提示里会显示类似 `config_backups/zwind_config_backup_YYYYMMDD_HHMMSS.yaml` 的路径。这份备份记录的是“导入发生前”的当前配置。如果导入的 YAML 把 server 或书签替换成了不想要的状态，这份备份就是回滚来源；如果你需要一个自己能在 Files 里直接找到的回滚文件，在导入另一份 YAML 前先手动导出并保存到 Files。

导入是替换，不是合并：

| 导入范围 | 实际效果 |
| --- | --- |
| Servers / 服务器 | 当前 server 列表会被 YAML 里的 `servers` 列表替换。导入后的 server 初始状态是 stopped。 |
| Bookmarks / 书签 | 当前 WebDAV 书签会被 YAML 里的 `bookmarks` 列表替换。 |
| Browser quick links | 文件里包含 `browserQuickLinks` 时，会替换当前 quick links。 |
| Browser default search engine | 文件里包含 `browserSearchEngine` 时，会更新默认搜索引擎。 |

数据文件夹条目会恢复保存的路径和 iOS folder bookmark，但导入不会复制文件夹里的文件。如果恢复出来的本地文件夹、iCloud Drive 文件夹、SMB 共享、夸克账号或 Emby endpoint 在这台设备上不可访问，server 仍可能保存成功，但浏览对应来源时会失败，需要先恢复底层访问条件。

导入也不会恢复 iOS 本地网络权限、Files provider 授权弹窗、钥匙串状态、购买权益、缓存内容、日志，或 **iCloud Sync / iCloud 同步** 开关本身。

## 打开 iCloud 同步

在 **Settings > Configuration / 设置 > 配置** 中打开 **iCloud Sync / iCloud 同步**。每台要参与同步的 iOS 设备都要单独打开这个开关；非 iOS 平台会显示不可用。

iCloud Sync 打开后，Zwind 会通过 iCloud 同步支持的配置载荷。当前版本使用的载荷结构与导出配置相同，但不带生成时间戳。它覆盖 server 配置、WebDAV 书签、Browser quick links，以及 Browser 默认搜索引擎。

同步载荷不包含本地文件内容、媒体缓存、app 日志、server 运行状态、VIP 或 resolver 购买状态、系统权限、导出配置之外的钥匙串项目，也不保证另一台设备一定能访问同一个 SMB、夸克、Emby、RSS 或 Web Media 来源。

## 多设备同步的边界

iCloud Sync 适合同步能写进 Zwind YAML 的配置：server 条目、书签、quick links 和搜索引擎偏好。

多设备使用时按下面理解：

| 情况 | 预期行为 |
| --- | --- |
| 一台设备修改 server 或书签 | 其他已开启同步的设备可以收到更新后的配置载荷。 |
| 两台设备在同步完成前分别改了不同的 server 或书签列表 | 后到达的配置载荷可能替换先前的本地列表；Zwind 不会逐条合并 server 或书签。 |
| server 指向本地 Files 文件夹 | server 条目可以同步，但文件内容和 iOS 授权是设备相关的；接收设备可能需要选择自己的可访问文件夹。 |
| server 指向 SMB、夸克、Emby、RSS 或 Web Media 来源 | 配置可以同步，但网络可达性、账号状态、Cookie、endpoint 和上游规则会在每台设备使用时重新决定。 |
| server 在第一台设备上正在运行 | 运行状态不同步。到接收设备上确认来源可访问后，再手动启动这个 server。 |

如果要把一组配置稳定交给另一台设备，先在来源设备确认 server 和书签列表就是想要的状态，再导出 YAML 给目标设备导入；或者只在确实要共享同一组配置的设备上打开 iCloud Sync。
