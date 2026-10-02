---
title: 安装
date: 2026-10-02
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

## 更新

新版本的游戏能顺利读取所有旧数据，无论经过什么更新、有什么变化

旧版本不会打开新版本的关卡。如果游戏要求你更新，就更新

> [!caution] 注意
> 在Android上，卸载游戏也会删除你所有的关卡。卸载前请导出档案，[[14_profile-transfer]]
