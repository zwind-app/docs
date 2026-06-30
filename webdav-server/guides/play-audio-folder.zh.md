---
title: 用 Music Player 播放音频目录
description: 从 Zwind Browser 打开音频文件或文件夹，生成 Music Player 播放队列，恢复最小化会话，控制播放顺序，并使用 iOS 后台控制。
seoTitle: 用 Zwind Music Player 播放 WebDAV 音频目录 - Zwind 指南
keywords:
  - Zwind Music Player
  - WebDAV 音频播放器
  - iPhone WebDAV 音乐
  - WebDAV 音乐播放队列
productSlug: webdav-server
section: 指南
parent: guides
locale: zh
translationOf: webdav-server/guides/play-audio-folder
order: 40
tags:
  - guide
  - browser
  - music
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Zwind 的 Music Player 可以直接播放 Browser 里的音频，也可以从单个音频文件或整个音频文件夹启动。想连续播放专辑、有声书目录、下载好的播客目录，或投影出来的音频文件夹时，直接把文件夹交给 Music Player。

下面截图使用英文界面；中文界面里的菜单位置相同。截图用于说明 Browser 长按菜单的位置，不同文件类型和文件夹会显示不同打开方式。

## 从 Browser 打开 Music Player

在 Browser 中点击音频文件，会使用 Zwind 的默认打开方式。`.mp3`、`.m4a`、`.aac`、`.wav`、`.flac`、`.ape`、`.ogg`、`.wma`、`.alac` 等音频文件默认会进入 **Music Player / 音乐播放器**。

想自己指定打开方式时，长按音频文件或文件夹，然后选择 **在音乐播放器中打开 / Open in Music Player**。

![在 Browser 中长按项目会打开操作菜单；音频文件和文件夹也在这个菜单位置显示 Music Player 相关选项。](/assets/docs/webdav-server/play-audio-folder/music-open-menu.png)

打开单个音频文件时，Zwind 会先播放这个文件，并可能把当前 Browser 列表中附近的可播放音频加入队列。打开文件夹时，Zwind 会先从找到的第一首可播放音频开始，然后继续加载整个文件夹队列。

## 把文件夹加载为播放队列

在 Browser 中长按文件夹，选择 **在音乐播放器中打开 / Open in Music Player**。Zwind 会扫描所选文件夹及其子文件夹，把可播放音频文件加载到 Music Player，不支持的文件会被跳过。

队列顺序会跟随当前 Browser 的排序字段和升降序，然后再应用 Music Player 的队列规则。如果已经有一个 Music Player 会话在播放，打开新的音频文件夹会把匹配音频追加到现有队列，避免重复项，并跳到这个文件夹中第一首可播放音频。

文件夹还在扫描时，Music Player 可以先从第一首找到的音频开始播放，并显示队列加载提示。扫描完成后，播放列表数量会更新为完整队列。如果文件夹里没有可播放音频，Zwind 会显示未找到媒体的结果，并保留当前播放会话，不会用空队列替换它。

## 在 Music Player 里继续添加音频

当有可用的运行中 server 时，Music Player 右上角会显示带加号的文件夹按钮。点击它会打开 Zwind 内置选择器，你可以再选一个文件夹或音频文件，把其中可播放的项目追加到当前队列。

这个入口使用和 Browser 相同的音频匹配规则：可播放音频会加入队列，不支持的文件会跳过，已经在队列里的项目不会重复加入。

## 恢复最小化的 Music Player

点击播放器左上角的向下箭头、向下滑动播放器，或使用 iOS 返回手势，都会最小化 Music Player。最小化只收起完整播放器界面，不会暂停播放。

Music Player 最小化后，Browser 底部附近会出现一条紧凑播放栏。点击标题区域或音乐图标区域可以恢复完整播放器。紧凑播放栏也提供上一首、播放或暂停、下一首和关闭按钮。关闭紧凑播放栏会结束 Music Player 会话，并清除 iOS 正在播放状态。

当 Music Player 已经最小化时，再打开另一个音频文件或文件夹，会恢复或更新同一个音乐会话，不会新建第二个播放器。

## 控制播放顺序

播放器主控制区提供上一首、播放或暂停、下一首。点击列表按钮会打开 **播放列表 / Playlist**，可以直接跳到某一首；当前播放项旁边会有勾选标记。

顺序按钮会在三种模式之间循环：

| 模式 | 播放行为 |
| --- | --- |
| **顺序 / Sequential** | 按队列顺序播放，最后一首结束后不再继续前进。 |
| **单曲重复 / Repeat One** | 当前曲目结束后重新播放当前曲目。 |
| **随机 / Shuffle** | 从队列中选择另一首播放；有随机播放历史时，上一首会按历史返回。 |

播放器会用 `当前/总数` 显示队列位置，例如 `3/18`。

## 后台播放和远程控制

播放开始后，Zwind 会激活 iOS 音频播放会话。切换到其他 app 或锁屏不会因为这个动作本身停止音频。

iOS 锁屏、控制中心、耳机控制、蓝牙控制和 AirPlay 控制可以显示当前标题，并把播放、暂停、上一首、下一首和拖动进度命令发送回 Music Player。远程控制作用于当前 Music Player 队列，并遵循应用内当前的播放顺序模式。

从 iOS 远程控制暂停后，Music Player 会话仍然保留。通过完整播放器或最小化播放栏关闭 Music Player 时，Zwind 会停用远程播放会话。
