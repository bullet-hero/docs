---
title: 效率与快捷键
date: 2026-10-02
tags: [level_author]
---

# 效率与快捷键

最省时间的是命令面板（Ctrl+Shift+P）、内容搜索（Ctrl+F）、“定位”按钮和时间轴上的方向键。任何按键都可以在设置中重新绑定

## 最省时间的四样东西

- **`{{ui:editor_search-title_command}}`**（`Ctrl+Shift+P`）：编辑器能做的一切，都能按名称搜索。比记住某个按钮在哪个面板上更快
- **`搜索内容`**（`Ctrl+F`）：按名称跳转到物体或音频轨道，播放头会跟着一起跳过去
- **`{{ui:cmd_editor_ping}}`**：视口把选中项框入画面，时间轴和层级同时滚动到它的位置。再按一次会跳到多选中的下一个物体
- **时间轴上的方向键**：按方向移动，而不是按列表顺序。在相邻关键帧之间切换不需要鼠标

## 默认快捷键

下面的分组和名称与`{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`中显示的一致

### 播放

| 按键 | 设置中的名称 | 作用 |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | 播放和暂停 |

### 编辑

| 按键 | 设置中的名称 | 作用 |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | 撤销 |
| `Ctrl+Y`或`Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | 重做 |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | 保存 |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | 复制 |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | 粘贴 |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | 创建副本 |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | 从选中项创建预制件 |

### 选中项

| 按键 | 设置中的名称 | 作用 |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | 删除选中项 |
| 按住`Ctrl` | `{{ui:settings_keybindings_editor_multi_select}}` | 多选 |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | 一次清除所有选中：物体、关键帧、音频和节拍 |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | 退出预制件模式，回到关卡 |

### 视图

| 按键 | 设置中的名称 | 作用 |
|---|---|---|
| `Ctrl+F` | `搜索内容` | 搜索内容 |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | 运行命令 |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | 显示或隐藏左侧面板 |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | 显示或隐藏右侧面板 |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | 显示或隐藏底部面板 |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | 显示或隐藏视口上方的工具组 |
| 按住`` ` `` | `{{ui:settings_keybindings_editor_preview}}` | 预览：按住期间隐藏编辑器界面 |

### 时间轴

| 按键 | 设置中的名称 | 作用 |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | 循环切换折叠：全部子树、仅选定的类型、不折叠 |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | 开启或关闭吸附 |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | 选择工具 |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | 框选工具 |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | 剪刀工具 |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | 边缘工具 |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | 在时间轴上折叠选中的物体 |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | 打开关卡时间轴 |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | 打开局部时间轴 |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | 打开音频时间轴 |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | 打开事件时间轴 |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | 打开预制件时间轴 |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | 节拍网格窗口，在这里敲出速度。`{{ui:settings_keybindings_editor_beat_tap}}`本身默认没有按键，需要的话自己绑定一个 |
| 按住`Ctrl`并滚动滚轮 | `{{ui:settings_keybindings_timeline_pan_modifier}}` | 平移 |
| 按住`Shift`并滚动滚轮 | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | 缩放 |

`Z X C V B N`从左到右对应时间轴工具栏，`Q W E R T`对应标签页栏。工具较少的时间轴从右边开始缺少：局部时间轴只有`Z X C V`。当前时间轴没有对应工具的字母键不起作用

### 控制柄

| 按键 | 设置中的名称 | 作用 |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | 选择 |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | 位置 |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | 旋转 |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | 缩放 |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | 尺寸 |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | 锚点 |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | 轴心 |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | 隐藏：选中状态保留，但不绘制手柄和边框 |

### 窗口

| 按键 | 设置中的名称 | 作用 |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | 开启或关闭全屏。在任何屏幕上都有效，仅限桌面端 |
| `Ctrl+S` | `{{ui:settings_keybindings_window_settings_save}}` | 设置打开时立即把设置写入磁盘。在编辑器中`Ctrl+S`保存关卡 |

### 导航

| 按键 | 设置中的名称 | 作用 |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | 在你最后点击进入的区域中向上移动 |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | 在你最后点击进入的区域中向下移动 |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | 在你最后点击进入的区域中向左移动 |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | 在你最后点击进入的区域中向右移动 |

在文本框中输入时，不带修饰键的单键，例如控制柄数字键、时间轴字母键和`Space`，都不起作用。在帧数输入框里输入`2`不会切换控制柄

## 时间轴上的方向键

方向键会选中屏幕上该方向最近的项目。无论缩放到什么程度，同样的按键都会找到同一个项目

- 在多选状态下，方向键从沿按键方向最远的那个项目出发，永远不会退回到你选中的那一块里
- 方向键移动总是替换选中项，从不追加
- 时间轴只滚动到刚好能显示新项目的程度。点击播放头读数仍然会让视图居中
- 试玩玩家开启时，方向键控制的是它，而不是时间轴。层级和`{{ui:settings_level-settings_raw}}`标签页在你点击进入后会保留方向键的控制权

## 查看关卡

**预览**。按住`` ` ``可以隐藏编辑器界面，只看关卡本身。这是按住生效，不是开关：松开按键，一切都会恢复。关卡、黑边（letterbox）、玩家和相机边界仍然可见。它没有对应的按钮或设置。这个按键可以在`{{ui:settings_keybindings_editor_preview}}`中重新绑定

**视口网格**通过工具栏上的按钮或`{{ui:cmd_editor_viewport-grid}}`命令切换，默认关闭。`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}`可以改变这一点，而你手动开启网格这件事不会在会话之间被记住

**控制柄吸附**会把控制柄拖动的内容吸附到网格上。它默认开启，与控制柄模式无关。用工具栏按钮或`{{ui:cmd_editor_gizmo-magnet}}`命令切换

**暂停是查看的常态**。播放暂停时，网格、碰撞体、机器人叠加层、控制柄手柄和选中边框都会继续绘制。抓住控制柄手柄时，播放会暂停

## 重新绑定

任何按键都可以重新绑定：`{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

只保存你改过的按键，其余的都取自默认值。所以如果你没有动过某个按键，它的默认值改进后会直接生效。`{{ui:settings_keybindings_reset}}`只是删除你的修改，所有按键都回到默认值

> [!tip] 提示
> 按键标签没有写死在界面里。重新绑定后，命令面板和所有右键菜单会立即显示新的按键

## 按下型和按住型按键

按下型按键只在修饰键完全一致时触发。`Ctrl+Shift+P`不会顺带触发`Ctrl+P`的功能，按住`Ctrl`时单独的`T`也不会触发

按住型按键在它的修饰键包含在当前按住的修饰键中时触发。它用来细化一个已经在进行中的操作

> [!info] 须知
> 所以两个按住型按键可以故意共用同一个键。多选和时间轴平移都在`Ctrl`上，两者互不冲突

接下来：[[1_order-of-work|工作顺序]]、[[2_reuse|复用：预制件、复制、生成器]]
