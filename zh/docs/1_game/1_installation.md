---
title: 安装
date: 2026-10-14
tags: [player]
---

# 安装

游戏把关卡、设置和统计保存在同一个数据文件夹中。更新是安全的：新版本能读取所有旧数据。在Android上，卸载游戏也会清除关卡

在这里下载：[[download]]

## 你的文件在哪里

| 系统 | 文件夹 |
|---|---|
| Windows | `C:\Users\<你>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

最快的打开方式是在游戏中：`{{ui:settings_common_title}}`→`{{ui:settings_general_title}}`→`{{ui:settings_general-open_folder}}`

里面有什么：

| 文件夹 | 内容 |
|---|---|
| `levels` | 你的关卡，每个关卡一个文件夹 |
| `backups` | 编辑器的自动保存 |
| `stats` | 统计数据 |
| `settings.json` | 设置 |
| `reports` | 错误报告 |

## 卸载

在Windows、Linux和Mac上，免费版在游戏旁边附带卸载程序：Windows上是`unins000.exe`，Linux上是`unins000`，Mac上是`Bullet Hero.app`旁边的`unins000`。运行它，它会自动删除游戏，不会询问任何问题。你的关卡、设置和统计数据留在数据文件夹中

它只删除游戏自身的文件。你自己放进游戏文件夹的东西会保留，文件夹只有在清空后才会被删除。如果游戏正在运行，卸载程序会先关闭它，就像点击窗口的关闭按钮一样，并同时关闭AI的MCP服务器。关卡中未保存的更改会丢失，所以请在卸载前先保存关卡

用Windows安装程序安装的游戏，像卸载其他程序一样，在Windows设置的“应用”中卸载

商店版本由商店自己卸载

## 更新

新版本的游戏能顺利读取所有旧数据，无论经过什么更新、有什么变化

旧版本不会打开新版本的关卡。如果游戏要求你更新，就更新

在 Google Play 版和 RuStore 版中，主菜单会提示新的更新，并在后台下载。更新就绪后，主菜单会显示 `{{ui:menu_update-ready_text}}`，点击 `{{ui:menu_update-ready_install-btn}}` 即可。通关一个关卡后，它可能会请你为游戏评分

> [!caution] 注意
> 在Android上，卸载游戏也会删除你所有的关卡。卸载前请导出档案，[[14_profile-transfer]]
