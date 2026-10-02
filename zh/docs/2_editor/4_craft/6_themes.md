---
title: 主题
date: 2026-10-02
tags: [level_author]
---

# 主题

主题是由64种颜色组成的调色板，物体按槽位编号引用这些颜色。更换主题，所有引用它的内容都会随之改变

类型为`主题`的颜色不保存自己的颜色，只保存一个槽位编号。它取当前帧上活动主题中该槽位的颜色

为什么这比手动输入的颜色更好，以及如何让关卡在任何主题下都保持可读：[[5_color-and-postprocessing]]

## 主题包含什么

- **名称**：显示在列表和选择窗口中
- **ID**，即`ThemeId`。主题关键帧按这个ID引用主题，而不是按名称
- **64种颜色**，排成8×8的网格，每种颜色都带透明度
- 每个槽位的**槽位名称**，可选。在你给任何一个槽位命名之前，文件中存储的是`null`而不是名称列表

主题是`level.json`中的数据，而不是关卡文件夹中的单独文件（见[[1_level-needs]]）。一个关卡可以包含任意数量的主题

8×8的布局沿用了*Afterbeat*的布局。游戏不给槽位分配任何固定用途：游戏自带的`Balanced`主题只是把它的64种颜色按色相分组

## 颜色如何找到自己的值

分两步：
1. 事件时间轴上的`主题`轨道决定这一帧哪个主题处于活动状态
2. 类型为`主题`的颜色指定活动主题中0到63之间的一个槽位

可以引用主题的有，例如形状的颜色（每个角单独设置）、文本的颜色和关卡背景

**槽位的位置就是它的身份**。把一种颜色移到另一个槽位，所有引用旧槽位的内容都会被重新着色

## 随时间切换主题

在两个主题关键帧之间，游戏会把整个调色板从一个主题平滑地混合到另一个主题。缓动取自较晚的关键帧（见[[5_keyframes-and-easing]]）

完全没有主题关键帧时，每个槽位都是白色

> [!warning] 警告
> 新关键帧使用`Linear`，所以调色板会在从上一个主题关键帧到这一个的整个区间内逐渐变化。要让主题恰好在drop处切换，把drop处的关键帧设为`Constant`

> [!caution] 注意
> 主题关键帧可能比主题本身存在得更久。删除一个仍被关键帧引用的主题，所有这些帧都会变成白色。关键帧本身会保留。删除这样的主题之前，编辑器会再次确认

## 如何创建和编辑主题

关卡资源中的`主题`标签页显示关卡的所有主题，上面有`{{ui:settings_level-settings_resources-themes-add}}`和`{{ui:settings_level-settings_resources-themes-import}}`。点击某一行会打开`{{ui:settings_level-settings_theme-editor}}`：
- 主题的`{{ui:field_common_name}}`
- `主题ID`和`{{ui:settings_level-settings_theme-editor-regenerate-id}}`
- 8×8的网格。点击一个格子会选中它，显示带编号的`颜色：`，并把颜色载入网格下方的色轮
- 选中格子的`{{ui:editor_theme-editor_color-name}}`

编辑器在副本上工作。保存之前，任何改动都不会进入关卡。保存本身是一个撤销步骤

## 如何选择槽位

把颜色切换为`主题`，然后打开`{{ui:editor_select-theme_color}}`

网格显示的是在正在编辑的关键帧所在帧上混合后的调色板，而不是播放头处的。旁边显示该帧前后的两个主题关键帧，以及选中的槽位在每个关键帧中的颜色。未命名的槽位显示为`{{ui:editor_search_unnamed}}`

## 如何分享和导入

- **本设备的共享库**。主题行上的`{{ui:editor_level-theme-item_export}}`会把主题保存到`resources/themes`，这是本设备的共享库，`resources`与`levels`位于同一目录下（见[[4_level-folder-and-backups]]）。`{{ui:settings_level-settings_theme-library}}`列出其中的主题，并标记已经`{{ui:editor_theme-library-item_in-level}}`的主题。`{{ui:editor_library_delete}}`会把主题从库中移除。导入会把主题复制到关卡中，所以关卡永远不依赖你的库。`{{ui:settings_level-settings_theme-library}}`也会列出合集中的主题，并显示来源标签：[[16_library-and-collections]]
- **游戏自带的主题**。`{{ui:editor_search-title_theme}}`会在关卡的主题旁边列出游戏自带的主题
- **Afterbeat**。`{{ui:settings_level-settings_resources-themes-import-afterbeat}}`把*Afterbeat*的主题文件转换为关卡主题。再次导入同一个文件会更新该主题，而不是创建副本。`{{ui:settings_level-settings_resources-themes-export-afterbeat}}`把关卡的所有主题写入你选择的文件夹，每个主题一个文件。此时透明度会丢失，因为*Afterbeat*的主题颜色不带透明度。这两个按钮在Android、iOS和WebGL上隐藏（见[[3_afterbeat-import]]）

接下来：[[5_color-and-postprocessing|颜色、主题与后期处理]]、[[1_readability-and-fairness|可读性与公平]]
