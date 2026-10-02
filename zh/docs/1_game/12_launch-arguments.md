---
title: 启动参数
date: 2026-10-02
tags: [advanced_player, developer]
---

# 启动参数

启动参数可以直接打开某个界面、关卡或一次游玩，开关参数只改变游戏的这一次启动。参数写在可执行文件后面：快捷方式、终端或Steam的启动选项中

不带参数时，游戏打开主菜单

## 语法

- 每个参数以两个连字符开头：`--editor`
- 值用空格或`=`隔开：`--speed 1.5`和`--speed=1.5`是一样的
- 键不区分大小写：`--Editor`同样有效
- 无论系统语言是什么，数字都用小数点：`1.5`，不能写`1,5`
- 含空格的值放在双引号中：`--level "D:\My Levels\Volcano"`

**游戏无法使用的参数永远不会中止启动**。它会被丢弃，相关的一行写入日志，游戏打开平常的界面。日志的位置：[[11_help#日志]]

**不认识的参数会被忽略**。游戏只读取自己的、带两个连字符的参数。Unity自己的单连字符参数，例如`-screen-width`，会原样通过。分辨率和全屏模式用它们来设置

## 界面

| 参数 | 打开什么 |
|---|---|
| `--menu` | 主菜单，和不带参数相同 |
| `--editor` | 关卡编辑器 |
| `--game` | `--level`指定的关卡，并立即开始游玩 |
| `--settings` | 主菜单，上面覆盖设置界面 |

界面参数最多传一个。两个不同的界面参数会互相抵消，打开的是菜单，并在日志中留下警告

`--settings`可以指定标签页：`general`、`audio`、`controls`、`keybindings`、`graphics`、`interface`、`game-editor`、`profile`、`other`。不指定名称时，设置打开在你上次所在的标签页。不认识的名称会被丢弃，设置照常打开

每次启动设置只打开一次。之后回到菜单时不会再次打开。每个标签页里有什么：[[4_settings]]

## 选择关卡

`--level`用关卡的标识符（`LevelId`）或关卡文件夹的路径来指定关卡。名称永远无效：名称会重复、会被翻译、会被修改。看起来像标识符的值总是被当作标识符

只在游戏列表中已经显示的关卡里查找。不在列表中的文件夹，游戏找不到

| 搭配 | 结果 |
|---|---|
| 无 | 菜单打开在关卡界面，等待`{{ui:menu_levelview_play-btn}}` |
| `--editor` | 编辑器打开这个关卡 |
| `--game` | 立即开始游玩 |

密码永远不通过参数传递。受保护的关卡会在界面上询问密码，回答后打开

## 游玩条件

这些条件会填写关卡界面上的控件，游玩就像你按下了`{{ui:menu_levelview_play-btn}}`一样开始。它们只在搭配`--game`时生效。没有它时会被忽略，并在日志中留下警告

| 参数 | 值 | 关卡界面上的控件 |
|---|---|---|
| `--speed` | 大于`0`且不超过`2`，四舍五入到`0.1` | `{{ui:field_common_speed}}` |
| `--lives` | 从`0`到`16`，`0`即`{{ui:menu_levelview_options-lifes_option-zen}}` | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0`或正整数，`0`表示每次游玩使用新种子 | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`、`reflex`、`warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`、`--no-checkpoints` | 无 | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | 无 | `{{ui:menu_levelview_options-no-collision_title}}` |

省略的条件取默认值：3条生命，速度`1.0`，检查点开启，无机器人，种子`0`，碰撞开启

这样启动的游玩就是普通的游玩。它和其他游玩一样计入统计，[[10_statistics]]

## 作用于整次启动的开关

这三个参数适用于任何界面，永远不会修改已保存的设置：

| 参数 | 作用 |
|---|---|
| `--autosave on`、`--autosave off` | 在这次启动中开启或关闭编辑器的自动保存。设置的`{{ui:settings_game-editor_title}}`标签页显示强制的值，并且不允许修改 |
| `--suppress-game-saves` | 整次启动使用匿名模式。无法在游戏中关闭，[[4_settings#匿名模式]] |
| `--frame-stats` | 向日志写入帧时间汇总，包括GPU和CPU时间。用于性能测量 |

`--frame-stats`每30秒为每个界面写一行，界面上方的窗口每次变化时也会写一行。界面的前3秒不计入

## 组合

| 命令 | 结果 |
|---|---|
| 无或`--menu` | 菜单 |
| `--editor` | 未打开关卡的编辑器 |
| `--settings` | 菜单，设置打开在你上次所在的标签页 |
| `--settings graphics` | 同上，打开在`{{ui:settings_graphics_title}}`标签页 |
| `--level X` | 菜单显示关卡X的界面，等待`{{ui:menu_levelview_play-btn}}` |
| `--level X --game` | 关卡X，正在游玩 |
| `--level X --editor` | 打开了关卡X的编辑器 |
| `--game`但没有`--level` | 菜单和警告 |
| `--menu --editor` | 菜单和警告 |
| `--speed 2`但没有`--game` | 条件被忽略，并有警告 |
| `--editor --autosave off` | 编辑器，自动保存仅在这次启动中关闭 |
| `--autosave maybe` | 被忽略并有警告，由你的设置决定 |
| `--suppress-game-saves` | 菜单。这次启动中游戏自己的存档都不会写入磁盘 |
| `--level X --game --suppress-game-saves` | 关卡X，正在游玩，结束后不留下统计 |
| `--editor --suppress-game-saves` | 编辑器。关卡存档、自动保存和备份照常写入，设置和统计不写入 |

## 示例

在Windows上，从终端或快捷方式：

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

在Steam中，游戏的启动选项只写参数，不写可执行文件：`--editor --autosave off`

## Android

Android没有命令行。参数通过启动游戏的intent中的字符串附加数据`bh`传递，拆分方式和手动输入的命令行完全相同。从电脑上通过`adb`来完成：

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **引号很重要**。整个`am start`放在双引号中，`bh`的值放在单引号中。否则设备的shell会拆开这一行：`bh`只收到第一个参数，其余的会作为`am`自己的参数交给它
- **`-S`会先停止正在运行的游戏**。参数只在启动时读取一次。发送给已经在运行的游戏不会有任何变化

iOS完全没有启动参数
