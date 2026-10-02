---
title: 沙盒与教程
date: 2026-10-02
tags: [player]
---

# 沙盒与教程

沙盒是主菜单中的一个竞技场，你可以在这里移动化身，向自己发射六种攻击中的任意一种，并完成六个步骤的教程。不需要任何关卡

首次启动时，游戏会提供一次教程：`{{ui:menu_tutorial-offer_confirm}}`在教程中打开沙盒，`{{ui:menu_tutorial-offer_cancel}}`永久关闭这个提示。无论如何，沙盒本身都会留在菜单中

## 面板

沙盒左侧有一个面板。点击面板的把手可以折叠面板，拖动把手可以把面板拉宽或拉窄。面板有五个标签页：

| 标签页 | 作用 |
|---|---|
| `{{ui:sandbox_tab_home}}` | 沙盒是什么，以及每个标签页的作用 |
| `{{ui:sandbox_tab_tutorial}}` | 教程的步骤，以及现在要做什么 |
| `{{ui:sandbox_tab_controls}}` | 你当前操控所用设备的模式、体感开关，以及前往全部操作设置的入口 |
| `{{ui:sandbox_tab_attacks}}` | 手动发射六种攻击中的任意一种，或让波次自动出现 |
| `{{ui:sandbox_tab_game}}` | 生命、攻击速度、机器人和自由相机 |

`{{ui:settings_common_title}}`在沙盒上方打开游戏设置。`{{ui:sandbox_panel_exit}}`返回主菜单

## 暂停

暂停按钮在屏幕右上角。`Esc`同样打开暂停，而不是退出沙盒。暂停会停止一切，和在关卡中一样：化身、攻击和教程。暂停窗口中有`{{ui:root_error_continue}}`、`{{ui:settings_common_title}}`和`{{ui:game_game-result_back-to-menu}}`

## 教程

六个步骤，按顺序：

1. `{{ui:sandbox_tutorial_move_title}}`：移动大约一个屏幕宽度的距离
2. `{{ui:sandbox_tutorial_dash_title}}`：冲刺三次
3. `{{ui:sandbox_tutorial_dodge_title}}`：在减速的齐射下坚持10秒不被击中。被击中会重新开始计时
4. `{{ui:sandbox_tutorial_dash-through_title}}`：圆环会扩大到屏幕边缘之外，所以只能通过冲刺穿过它的边缘离开。需要穿过两个圆环，失败的圆环不会取消已经穿过的圆环。冲刺期间什么都击不中你
5. `{{ui:sandbox_tutorial_choose-mode_title}}`：在`{{ui:sandbox_tab_controls}}`标签页上尝试各个模式，然后按`{{ui:sandbox_tutorial_confirm-mode}}`
6. `{{ui:sandbox_tutorial_done_title}}`：`{{ui:sandbox_tutorial_play-level}}`启动教程关卡

在竞技场上进行某个步骤时，面板会折叠，步骤以一张小卡片显示在屏幕上方。触摸会穿过卡片。把手依然可以打开面板。在`{{ui:sandbox_tutorial_choose-mode_title}}`和`{{ui:sandbox_tutorial_done_title}}`步骤中，面板会自动打开在`{{ui:sandbox_tab_tutorial}}`标签页上

被击中或死亡只会重新开始发生时所在的步骤，而不是整个教程，并且这个步骤会变成红色，直到完成为止。已完成的步骤是绿色的

点击列表中的步骤会开始该步骤，包括已经完成的步骤。完成一个步骤后，教程会转到下一个未完成的步骤。只有完成所有步骤，教程才算完成，也是在那时写入统计。同一标签页上的`{{ui:sandbox_tutorial_restart}}`可以随时重新开始教程

> [!warning] 警告
> 在`{{ui:sandbox_tab_game}}`标签页上开启`{{ui:sandbox_game_immortal}}`时，击中完全不计入，所以`{{ui:sandbox_tutorial_dodge_title}}`和`{{ui:sandbox_tutorial_dash-through_title}}`步骤也看不到击中。完成教程时请保留几条生命

## 操作

模式针对当前正在操控的设备更改，并立即保存。体感没有`{{ui:enum_control-mode_relative}}`模式。每种模式的含义：[[3_controls#操作模式]]

## 攻击与游戏

- `{{ui:sandbox_attacks_auto}}`以`{{ui:sandbox_attacks_gap}}`为间隔发射随机波次，和主菜单背景一样
- `{{ui:sandbox_attacks_clear}}`移除屏幕上的所有攻击
- `{{ui:sandbox_game_speed}}`只让攻击变慢或变快。化身始终以自己的速度移动
- 生命：`{{ui:sandbox_game_immortal}}`、1、3或5。生命耗尽后会恢复，沙盒不会结束
- `{{ui:sandbox_game_bot}}`把化身交给在主菜单背景中游玩的同一个机器人
- `{{ui:sandbox_game_free-camera}}`让你看到屏幕边缘之外：用鼠标中键或两根手指移动视图，用滚轮或双指捏合缩放。蓝色边框显示关卡相机看到的范围，`{{ui:sandbox_camera_back}}`把视图恢复到它。操作、冲刺和攻击与不使用它时完全相同
- 死亡的表现和在关卡中一样：攻击减速并消失，化身以满生命出现在中央
