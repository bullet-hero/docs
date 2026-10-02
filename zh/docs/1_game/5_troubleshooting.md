---
title: 问题排查
date: 2026-10-02
tags: [player]
---

# 问题排查

手动复制的关卡在重新扫描后出现在列表中。来自更新版本的关卡需要更新游戏，.7z归档包需要重新打包为zip。忘记的密码无法找回

没有找到你的问题？在哪里报告：[[11_help]]

## 关卡不在列表中

- **手动复制的**。关卡文件夹必须直接放在`levels`中，[[1_installation]]。复制后点击`{{ui:root_level-browser_refresh}}`
- **创意工坊物品**。Steam版本只显示你的订阅。`{{ui:settings_common_title}}`→`{{ui:settings_general_title}}`→`{{ui:settings_general_show-all-found-content}}`会加入在硬盘上找到的文件夹。它们标有`{{ui:root_level-entry_not-listed}}`
- **什么都看不到**。关卡文件夹可能无法访问。此时`{{ui:settings_other_title}}`中的存储清理不会运行，并提示`关卡扫描没有找到任何内容，因此已拒绝此次清理`

## 关卡无法加载

加载画面会显示当前阶段：`{{ui:root_loading_reading}}`、`{{ui:root_loading_validating}}`、`{{ui:root_loading_resources}}`、`{{ui:root_loading_building}}`

- **来自网络地址的文件**。关卡可以通过链接获取文件，而不是把它放在文件夹里。`{{ui:settings_general_title}}`→`{{ui:settings_general_resource-web-timeout}}`是游戏等待这种文件的秒数
- **损坏的关卡**。`Json`格式的关卡是文本，可以直接用眼睛读。损坏的`Blob`会被整个拒绝。更多：[[4_level-folder-and-backups]]
- **错误窗口**。窗口中有`{{ui:root_error_copy}}`、`{{ui:root_error_save}}`和`{{ui:root_error_open-reports-folder}}`。报告保存在`reports`文件夹中。把它附在[bullet-hero/releases](https://github.com/bullet-hero/releases/issues)的错误报告里，[[11_help]]
- **`关卡每帧需要的物体数超过此设备的上限`**。这不是加载错误。关卡可以游玩，但其中一部分不会被绘制。更多：[[1_level-budget]]

## “需要更新”

旧版本的游戏不会打开来自新版本的文件。请更新游戏

| 消息 | 怎么办 |
|---|---|
| `这个关卡由更新版本的游戏制作，当前版本无法读取...` | 更新游戏 |
| `这个归档包中的关卡来自更新版本的游戏...` | 更新游戏 |
| `剪贴板中的编辑器内容是在更新版本的游戏中复制的...` | 更新游戏 |
| `你的设置或统计由更新版本的游戏保存...` | `{{ui:root_update-required_download}}`、`{{ui:root_update-required_keep}}`或`{{ui:root_update-required_overwrite}}` |

标有`{{ui:root_level-entry_newer-version}}`或`{{ui:root_level-entry_newer-file}}`的卡片是同一种拒绝。在打开关卡之前就能看到

### 来自更新版本的设置或统计

这种情况下游戏使用默认值运行。在关闭之前它不保存任何自己的数据，新文件保持不变。这就是匿名模式，[[4_settings]]

使用`--suppress-game-saves`时没有`{{ui:root_update-required_overwrite}}`按钮

来自更新版本的关卡统计不会显示。通关该关卡会覆盖它，除非存档已被关闭

### 游戏为什么拒绝

文件格式的每次变化都会获得一个新的代号。版本不读取更新代号的文件，以免读错

## 受保护的关卡

打开之前，游戏会要求输入`{{ui:level_passphrase_password}}`

每次会话只询问一次密码，并且只保存在内存中

只有内容会被加密：物体、关键帧、主题。名称、封面和媒体仍然可读，所以没有密码也能看到卡片

删除受保护的关卡不需要密码

> [!caution] 注意
> 忘记的密码无法找回。密钥不存放在任何地方：不在游戏中，不在文件中，也不在任何人手里

## 归档包被拒绝

| 消息 | 原因 |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | 这是`.7z`。请重新打包为`.zip` |
| `{{ui:editor_create-level_archive-wrong-password}}` | 密码不对 |
| `{{ui:editor_create-level_archive-damaged}}` | 归档包已损坏，请再要一次 |
| `{{ui:editor_create-level_archive-not-archive}}` | 这个文件根本不是关卡归档包 |

改过名的归档包不是问题：游戏根据文件的字节识别格式

接受哪些归档包：[[2_playing-levels]]
