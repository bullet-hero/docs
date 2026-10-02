---
title: 帮助与错误报告
date: 2026-10-02
tags: [player, level_author]
---

# 帮助与错误报告

游戏错误提交到releases的issues，问题发到Discord。附上设置中的版本字符串，以及出现错误之前的操作步骤

先看看[[5_troubleshooting]]。关卡消失、“需要更新游戏”和归档包被拒绝都在那里有说明

## 发到哪里

| 内容 | 位置 |
|---|---|
| 游戏或编辑器的错误，对游戏的建议 | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| SDK或其代码中的错误 | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| 文档中的错误或过时的事实 | [bullet-hero/docs](https://github.com/bullet-hero/docs)，[[community]] |
| 提问、关卡求助、讨论 | [Discord](https://discord.gg/gkHQrp9NgS) |

GitHub上的消息是公开的。任何人都可以阅读并补充。可以向文档提交issue或pull request

不确定是不是错误？先在Discord里问一下

项目的所有链接：[[links]]

## 错误报告里写什么

能复现的错误会被修复。“它崩了”通常没法修复：不知道该重复什么

1. **版本字符串**。点击设置界面上的版本字符串，它会自动复制。格式如下：`gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`，[[4_settings]]
2. **平台和设备**：系统，如果是手机，还有型号
3. **步骤**：你做了什么，期望发生什么，实际发生了什么
4. **关卡**，如果错误与它有关：打包成归档包的关卡文件夹，或你打开过的归档包。如果关卡受保护，请注明
5. **错误报告**，如果出现过错误窗口。`{{ui:root_error_save}}`把它写入`reports`文件夹，`{{ui:root_error_open-reports-folder}}`打开该文件夹，[[1_installation]]

> [!tip] 提示
> 把文件作为附件添加到消息中，而不是粘贴到正文里。日志很长，放在正文里很难阅读

## 日志

游戏运行时会写日志。完全没有出现错误窗口时，它会有帮助

- **Windows**：游戏数据文件夹中的`Player.log`，`C:\Users\<你>\AppData\LocalLow\vertoker\Bullet Hero`（Unity的标准位置）
- **Android**：日志输出到logcat。设备连接到电脑时，用`adb logcat -s Unity`查看
- **其他系统**：暂无说明
