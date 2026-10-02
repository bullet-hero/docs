---
title: 设置
date: 2026-10-02
tags: [player]
---

# 设置

最重要的设置在第一次启动时完成：游戏会自动打开快速设置，包括语言、音量、性能和效果。重置只影响设置，关卡会保留

## 标签页

| 标签页 | 内容 |
|---|---|
| `{{ui:settings_general_title}}` | 语言，每种语言都用它自己的语言命名，如`Русский (ru)`。`系统 (zh)`跟随设备，并显示最终使用的语言。还有同时加载的关卡文件数量、网址文件的超时时间、`{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | 音量：`{{ui:settings_audio_volume}}`、`{{ui:settings_audio_game}}`、`{{ui:settings_audio_ui}}`、`{{ui:settings_audio_editor-ui}}`、`{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | 设备和操作方式，[[3_controls]] |
| `{{ui:settings_keybindings_label}}` | 快捷键，主要是编辑器的，[[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | 显示、帧率、抗锯齿、`{{ui:settings_graphics-colliders-mode_title}}`、纹理、特效、后期处理 |
| `{{ui:settings_interface_label}}` | 游戏界面、`{{ui:settings_interface_open-menu-on-lose}}`、`{{ui:settings_interface_menu-background}}`、`{{ui:settings_interface_levels-layout}}`、屏幕方向、统计叠加层 |
| `{{ui:settings_game-editor_title}}` | 编辑器自己的设置，包括它自己的`{{ui:settings_interface_levels-layout}}` |
| `{{ui:settings_profile_tab}}` | 你的统计，[[10_statistics]] |
| `{{ui:settings_other_title}}` | 清理存储空间、Android上的文件夹访问权限、匿名模式、`{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}`决定主菜单按钮后面显示什么：机器人躲避攻击的实时竞技场、一片旋转的形状，或者什么都不显示

`{{ui:settings_interface_levels-layout}}`决定关卡选择以什么方式打开：封面组成的`{{ui:enum_level-browser-layout_grid}}`，或带简介的`{{ui:enum_level-browser-layout_list}}`。它有两个：`{{ui:settings_interface_label}}`标签页中的用于菜单（默认`{{ui:enum_level-browser-layout_grid}}`），`{{ui:settings_game-editor_title}}`标签页中的用于编辑器（默认`{{ui:enum_level-browser-layout_list}}`）。在你离开这个界面之前，搜索框旁边的按钮仍然可以切换视图

## 快速设置

`{{ui:settings_quick-setup_title}}`是`{{ui:settings_general_title}}`标签页中位于`{{ui:settings_general-open_folder}}`上方的按钮。它会问几个最重要的问题，每页一个类别。第一次启动时它会自动打开，在教程邀请之前。每个选项都有一行说明它的作用。页面可以按任意顺序打开，`{{ui:settings_quick-setup_next}}`只是提示下一页

| 页面 | 问题 | 选项 | 改变什么 |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}`以及游戏的每种语言，各自用本语言命名 | 与`{{ui:settings_general_title}}`标签页中的相同 |
| | `{{ui:settings_audio_volume}}` | 滑块 | 与`{{ui:field_common_audio}}`标签页中的相同 |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`、`{{ui:settings_quick-setup_performance-economy}}`、`{{ui:settings_quick-setup_performance-recommended}}`、`{{ui:settings_quick-setup_performance-max}}` | 渲染缩放（PC）、抗锯齿、纹理尺寸、特效的帧率，但不包括帧率上限：任何选项都按屏幕刷新率运行。`{{ui:settings_quick-setup_performance-minimum}}`还会关闭粒子特效和后期处理，并把图像限制在512以内 |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`、`{{ui:settings_quick-setup_comfort-soft}}`、`{{ui:settings_quick-setup_comfort-minimal}}` | 每种后期效果以及化身的碎裂。`{{ui:settings_quick-setup_comfort-soft}}`会关闭故障、颗粒、模糊、镜头畸变和色差 |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | 这里不改变任何东西：教程让你试遍每种操作方案并选出自己的。它从主菜单或沙盒打开 |

标有`{{ui:settings_quick-setup_default-badge}}`的选项就是游戏在你的设备上开始时使用的设置。选择会立即生效，并在完整设置中可见。如果你的设置与任何选项都不符，就不会高亮任何选项，并有一行文字说明。这是你自己的设置，按下任一选项会替换它们

## 折叠的部分

较长的标签页被分成几个部分。经常修改的部分是展开的，细节调整是折叠的：点击标题即可展开。标签页重置按钮旁边的按钮可以一次折叠或展开所有部分

在`{{ui:settings_controls_title}}`标签页中，只有你手上正在用的设备是展开的

## 重置

每个标签页都有自己的重置。`{{ui:settings_other_title}}`中的`{{ui:settings_other_reset}}`会一次重置所有标签页

重置只影响设置。你的关卡会保留

## 版本行

设置界面上有一行版本信息。点击它即可复制

它的格式是：`gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`。报告错误时应该附上的就是这一行，[[11_help]]

## 图形

**抗锯齿**。PC上默认使用`{{ui:enum_anti-aliasing-type_msaa}}`。手机一开始不开抗锯齿。游戏中的所有形状都是真正的几何体，`{{ui:enum_anti-aliasing-type_msaa}}`在所有平台上都能让边缘平整而不发糊

`{{ui:enum_anti-aliasing-type_fxaa}}`适用于性能较弱的手机。它对整个屏幕只做一次处理，开销是固定的。当许多透明形状叠在一起绘制时，`{{ui:enum_anti-aliasing-type_msaa}}`的开销会增加

刻意没有提供TAA。它会在快速移动的子弹后面留下拖影，它的抖动还会干扰故障效果

**帧率**。目标帧率是手动设定的，而不是通过垂直同步。这样关卡的时间在60Hz和144Hz的屏幕上完全相同。开启`{{ui:settings_graphics_vsync}}`时（仅PC），帧率上限不起作用

> [!tip] 建议
> 在性能较弱的设备上，先把**渲染缩放**降到1以下。它只损失清晰度，界面仍保持完整尺寸。仅PC

更多：[[2_mobile-devices]]

## “仅碰撞体”模式

用于练习的模式，是`{{ui:settings_graphics_title}}`标签页中一个折叠的部分。开启`{{ui:settings_graphics-colliders-mode_active}}`后，游玩中的关卡会把每个判定框画成同一种颜色的平面填充，放在纯色背景上，此外什么都不画。消失的有：形状本身的外观、没有碰撞体的形状、特效、文本、后期处理和主题背景。不变的有：音乐、碰撞、相机及其震动、检查点、界面和统计，这种模式下的一局和其他任何一局一样计入统计。你的化身照常绘制

这个模式只在游玩关卡时生效。编辑器、沙盒和菜单背景照常绘制

| 选项 | 作用 |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | 开启（默认）：填充按颜色的Alpha半透明显示，重叠的障碍看起来更暗。Alpha不会低于0.15。关闭：每个填充都是实心的，颜色的Alpha被锁定 |
| `{{ui:settings_graphics-colliders-mode_color}}` | 填充的颜色，默认是Alpha为0.6的红色。编辑器中的碰撞体视图使用同样的色相，但有自己的不透明度 |
| `{{ui:settings_graphics-colliders-mode_background}}` | 填充后面绘制的颜色，默认是深灰色。不用黑色，是为了让相机画面的边缘在周围的黑边前仍然可见 |

两种颜色都折叠在各自的标签下：展开需要的那一个，就能看到色轮

## 匿名模式

在`{{ui:settings_other_title}}`→`{{ui:settings_other_suppress-game-saves}}`中开启

开启这个模式时，游戏不保存任何自己的数据。`settings.json`、总体统计和关卡统计在硬盘上保持原样。修改过的设置在关闭游戏之前仍然有效

关卡相关的操作照常保存：保存、导出、导入、复制和删除。编辑器的自动保存和备份也照常工作，它们有自己的开关

这个模式持续到关闭游戏为止，不会被记住

关闭这个模式时，当前设置会被保存。在此期间游玩的一切都会被丢弃

> [!info] 须知
> 这个模式也会自动开启。[[12_launch-arguments|启动参数]]`--suppress-game-saves`会在整个运行期间开启它，并且无法在游戏中关闭。来自更新版本游戏的设置或统计也会开启它。这时游戏会在每次启动时询问是保留它们，还是用默认值覆盖
