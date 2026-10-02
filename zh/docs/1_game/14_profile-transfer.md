---
title: 转移档案
date: 2026-10-02
tags: [player]
---

# 转移档案

整个档案可以放进一个zip文件：关卡、统计、设置和库。重装或换设备前先导出，再到新设备上导入

按钮位于`{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`。支持Windows、Mac、Linux和Android。iOS不可用

## 文件里有什么

| 部分 | 在数据文件夹中 | 默认勾选 |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | 是 |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | 是 |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | 是 |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | 是 |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | 否 |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | 否 |

这个文件是普通的zip，任何解压工具都能打开。里面是和数据文件夹（[[1_installation]]）相同的文件夹，外加描述文件的`profile.json`

## 导出

1. 点击`{{ui:settings_profile-transfer_export}}`
2. 勾选需要的部分
3. 选择保存位置

在任何能打开设置的地方都可以导出：主菜单、游玩暂停时和编辑器中。统计会先写入磁盘，所以文件是最新的

## 导入

1. 从主菜单打开设置，点击`{{ui:settings_profile-transfer_import}}`
2. 选择zip文件
3. 勾选部分并选择模式
4. 确认

只能在主菜单中导入。正在运行的关卡或打开的编辑器占用着自己的文件，无法在使用中替换

| 模式 | 会发生什么 |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | 每个勾选的部分会被清空，并用文件中的内容填充 |
| `{{ui:settings_profile-transfer_mode-merge}}` | 关卡会被添加。两边都有的关卡整体替换为较新的副本。统计保留每个计数中较大的值和更好的记录。库文件、自动保存和报告只会添加，你的保持不变 |

每次导入在写入前都会再确认一次。替换会列出将被清空的部分，合并会说明将添加、替换和保留多少关卡

**来自另一类设备的设置。**在电脑上导入来自手机的档案（或反过来）时，会保留你自己的操作和画面设置，其余都取自文件

游戏会拒绝来自更新版本游戏的文件，请先更新游戏。也会拒绝不是zip的文件、不是档案的zip、有密码的zip以及损坏的文件。这些情况下都不会有任何改动

## 备份

每次导入前，游戏会把即将被替换的部分保存到一个备份中。它位于数据文件夹里的`profile-backups`文件夹。备份只有一个：下一次导入会覆盖它

- `{{ui:settings_profile-transfer_backup-restore}}`会恢复备份。被它替换的内容会成为新的备份，所以恢复也可以撤销
- `{{ui:settings_profile-transfer_backup-save-as}}`会把副本保存到你选择的位置
- `{{ui:settings_profile-transfer_backup-delete}}`会删除它
- `{{ui:settings_profile-transfer_clear-cache}}`会删除整个`profile-backups`文件夹：备份以及中断的转移留下的文件

导入时`{{ui:settings_profile-transfer_backup-to-folder}}`默认勾选：游戏会立即询问在游戏外保存副本的位置

> [!caution] 注意
> 在Android上，备份位于游戏的数据文件夹中，会随游戏一起被删除。卸载前请导出档案，或把备份保存到别处

如果游戏在导入中途关闭，下次启动时档案会恢复原状

## 在Android上切换版本

从文件安装的游戏（itch.io等）无法通过Google Play更新，反之亦然。两个版本的签名不同，所以Android会拒绝更新。切换步骤：

1. 导出档案并把文件保存到游戏之外
2. 卸载游戏
3. 安装另一个版本
4. 导入档案
