---
title: 获取帮助
date: 2026-09-25
tags: [player, level_author]
---

# 获取帮助

去哪里报告bug或提问，以及怎么写才能让bug被复现

先看看[[5_troubleshooting]]。关卡不在列表中、“需要更新”和归档包被拒绝，那里都有说明

## 去哪里写

| 内容 | 位置 |
|---|---|
| 游戏或编辑器的bug，对游戏的需求 | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| SDK或其代码的bug | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| 文档中的错误或过时信息 | [bullet-hero/docs](https://github.com/bullet-hero/docs)，[[5_contribute/index]] |
| 提问、关卡制作求助、讨论 | [Discord](https://discord.gg/gkHQrp9NgS) |

GitHub上的报告是公开的，任何人都可以阅读和补充。文档接受issue或pull request

不确定是不是bug？先在Discord上问一问

## bug报告里写什么

开发者能复现的bug会被修复。“它崩溃了”通常不会：没人知道该重复什么操作

1. **版本信息行**。点击设置界面上的版本信息行，它会自动复制。格式是`gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`，[[4_settings]]
2. **平台和设备**：系统，如果是手机还要写型号
3. **步骤**：你做了什么，预期是什么，实际发生了什么
4. **关卡**，如果bug与某个关卡有关：压缩后的关卡文件夹，或你打开的归档包。如果是受保护的关卡，请说明它受保护
5. **错误报告**，如果出现了错误窗口。`保存报告`会把它写入`reports`文件夹，`打开报告文件夹`会打开这个文件夹，[[1_installation]]

> [!tip] 提示
> 把文件作为附件添加到报告中，而不是粘贴到正文里。日志很长，粘贴进去很难阅读

## 日志

游戏运行时会写日志。完全没有出现错误窗口时，日志很有帮助

- **Windows**：游戏数据文件夹中的`Player.log`，`C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero`（Unity的标准位置）
- **Android**：日志输出到logcat。设备连接到电脑时，`adb logcat -s Unity`会把它打印出来
- **其他系统**：尚无说明
