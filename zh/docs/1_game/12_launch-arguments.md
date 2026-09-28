---
title: 启动参数
date: 2026-09-25
tags: [advanced_player, developer]
---

# 启动参数

直接打开某个界面、关卡或开始一局的命令行参数，以及只改变本次启动的开关

启动参数告诉游戏启动时要打开什么。它们写在可执行文件之后：可以写在快捷方式、终端或Steam的启动选项中。没有参数时，游戏打开主菜单

## 语法

- 每个参数都以两个连字符开头：`--editor`
- 值写在空格或`=`之后：`--speed 1.5`和`--speed=1.5`是一样的
- 键不区分大小写：`--Editor`也可以
- 无论系统语言是什么，数字都用点作小数点：`1.5`，不能写`1,5`
- 含空格的值要放在双引号中：`--level "D:\My Levels\Volcano"`

**游戏无法使用的参数永远不会阻止启动**。它会被丢弃，日志中会写一行相关信息，游戏打开平常的界面。日志在哪里：[[11_help#日志]]

**未知参数会被忽略**。游戏只读取自己的参数，也就是带两个连字符的参数。Unity自己的单连字符参数，例如`-screen-width`，会原样通过。用它们设置分辨率和全屏

## 界面

| 参数 | 打开什么 |
|---|---|
| `--menu` | 主菜单，与不带参数相同 |
| `--editor` | 关卡编辑器 |
| `--game` | `--level`指定的关卡，并立即开始这一局 |
| `--settings` | 主菜单，并在其上打开设置界面 |

最多只能传一个界面参数。两个不同的界面参数会互相抵消，此时打开菜单，并在日志中写入警告

`--settings`可以指定标签页：`general`、`audio`、`controls`、`keybindings`、`graphics`、`interface`、`game-editor`、`profile`、`other`。不指定时，设置打开到你上次离开的标签页。游戏不认识的名称会被丢弃，设置照样打开

每次启动只打开一次设置。之后回到菜单时不会再次打开。每个标签页包含什么：[[4_settings]]

## 指定关卡

`--level`通过关卡的ID（`LevelId`）或关卡文件夹的路径来指定关卡。标题永远不行：标题会重复、会被翻译、会被修改。看起来像ID的值总是被当作ID

游戏只在它本来就会列出的关卡中查找。它不列出的文件夹是找不到的

| 与之搭配 | 结果 |
|---|---|
| 无 | 菜单打开到该关卡的界面，等待按`开始` |
| `--editor` | 编辑器打开该关卡 |
| `--game` | 立即开始这一局 |

密码永远不能作为参数。受保护的关卡会在屏幕上要求输入密码，你输入后才会打开

## 一局的选项

这些选项会填写关卡界面上的控件，然后像按下`开始`一样开始这一局。它们只能与`--game`一起使用。没有`--game`时它们会被忽略，并在日志中写入警告

| 参数 | 值 | 关卡界面上的控件 |
|---|---|---|
| `--speed` | 大于`0`且不超过`2`，四舍五入到`0.1` | `速度` |
| `--lives` | `0`到`16`，`0`表示`禅` | `生命` |
| `--seed` | `0`或正整数，`0`表示每局使用新的种子 | `玩家种子` |
| `--bot` | `none`、`reflex`、`warm` | `机器人` |
| `--checkpoints`、`--no-checkpoints` | 无 | `检查点` |
| `--no-collision` | 无 | `无碰撞` |

省略的选项使用默认值：3条命，速度`1.0`，检查点开启，无机器人，种子`0`，无碰撞关闭

这样开始的一局就是普通的一局。它和其他局一样计入你的统计，[[10_statistics]]

## 作用于整次启动的开关

这三个开关可以和任何界面一起使用，而且从不改变已保存的设置：

| 参数 | 作用 |
|---|---|
| `--autosave on`、`--autosave off` | 在本次启动中开启或关闭编辑器的自动保存。`编辑器`设置标签页会显示强制设定的值，且不允许修改 |
| `--suppress-game-saves` | 整次启动都处于匿名模式，无法在游戏中关闭，[[4_settings#匿名模式]] |
| `--frame-stats` | 把帧时间摘要写入日志，包括GPU和CPU时间。用于测量性能 |

`--frame-stats`每30秒为每个界面写一行，界面上层的窗口变化时也会写。界面的前3秒不计入

## 组合

| 命令 | 结果 |
|---|---|
| 无，或`--menu` | 菜单 |
| `--editor` | 编辑器，不打开关卡 |
| `--settings` | 菜单，设置打开到上次离开的标签页 |
| `--settings graphics` | 同上，打开到`图形`标签页 |
| `--level X` | 菜单，停在关卡X的界面，等待按`开始` |
| `--level X --game` | 关卡X，开始游玩 |
| `--level X --editor` | 编辑器，打开关卡X |
| `--game`但没有`--level` | 菜单和一条警告 |
| `--menu --editor` | 菜单和一条警告 |
| `--speed 2`但没有`--game` | 该选项被忽略，并有一条警告 |
| `--editor --autosave off` | 编辑器，仅本次启动关闭自动保存 |
| `--autosave maybe` | 被忽略并有一条警告，由你的设置决定 |
| `--suppress-game-saves` | 菜单。本次启动期间，游戏自己的任何数据都不会写入硬盘 |
| `--level X --game --suppress-game-saves` | 关卡X，开始游玩，这一局不留下任何统计 |
| `--editor --suppress-game-saves` | 编辑器。关卡保存、自动保存和备份照常写入，设置和统计不写入 |

## 示例

在Windows上，通过终端或快捷方式：

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

在Steam中，只把参数写进游戏的启动选项，不写可执行文件：`--editor --autosave off`

## Android

Android没有命令行。参数放在启动游戏的intent的字符串extra`bh`中，拆分方式与输入的命令行完全相同。在电脑上可以用`adb`来做：

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **引号很重要**。整个`am start`放在双引号中，`bh`的值放在单引号中。否则设备的shell会拆分这一行：`bh`只收到第一个参数，其余的会作为`am`自己的选项传给它
- **`-S`会先停止正在运行的游戏**。参数只在启动时读取一次。发给已经在运行的游戏不会改变任何东西

iOS完全没有启动参数
