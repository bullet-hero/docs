---
title: 游玩关卡
date: 2026-10-02
tags: [player]
---

# 游玩关卡

在关卡列表中选择关卡，设定这一局的条件，然后开始。别人的关卡就是一个普通的文件夹：把它复制到levels文件夹，再刷新列表

## 主菜单

| 按钮 | 作用 |
|---|---|
| `{{ui:menu_main_levels-btn}}` | 关卡列表，见下文 |
| `{{ui:menu_main_editor-btn}}` | 关卡编辑器，[[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | 不需要关卡的竞技场和教程，[[13_sandbox]] |
| `{{ui:settings_common_title}}` | 所有设置，[[4_settings]] |
| `{{ui:menu_main_story-btn}}` | 暂时还不能用 |
| `{{ui:menu_main_multiplayer-btn}}` | 暂时还不能用 |

## 关卡列表

主菜单中的`{{ui:menu_main_levels-btn}}`会打开关卡列表。关卡有三个来源：

- `{{ui:root_level-source_local}}`：`levels`文件夹，[[1_installation]]
- `{{ui:root_level-source_builtin}}`：游戏自带的关卡
- `创意工坊`：仅限Steam版本。这里显示你订阅的关卡。你订阅的资源合集不是关卡，它们出现在编辑器的库中，[[16_library-and-collections]]

顶部有搜索框、`{{ui:root_level-browser_sort}}`和`{{ui:root_level-browser_layout}}`（网格或列表）。列表默认以网格显示。可以按`{{ui:root_level-browser_sort-relevance}}`、`{{ui:root_level-browser_sort-title}}`、`{{ui:root_level-browser_sort-duration}}`、`进度`和`{{ui:root_level-browser_sort-recent}}`排序

把关卡复制进了文件夹？按`{{ui:root_level-browser_refresh}}`，列表就会更新

卡片上有锁，表示这个关卡受密码保护

长按或右键点击卡片会打开菜单：`{{ui:level_passphrase_open}}`和`{{ui:root_level-browser_delete}}`。对`创意工坊`关卡使用`{{ui:root_level-browser_delete}}`会取消订阅该物品并删除其文件。这需要Steam正在运行，否则Steam会重新下载该关卡。内置关卡无法删除

## 添加别人的关卡

关卡就是一个普通的文件夹。你可以把它打包后发给朋友

**文件夹**。把关卡文件夹复制到`levels`，然后按`{{ui:root_level-browser_refresh}}`。要复制的是关卡文件夹本身：里面有`level.json`（或`level.blob`）和`metadata.json`的那个文件夹

**归档包**。打开编辑器，用`{{ui:gen_level_archive}}`生成器创建一个新关卡。然后用`{{ui:editor_create-level_archive-choose}}`按钮选择文件

| 文件 | 结果 |
|---|---|
| `.zip`、`.tar.gz` | 可以打开 |
| 自带密码的`.zip`、`.zip.gpg`、`.tar.gz.gpg` | 出现`{{ui:editor_create-level_archive-protected}}`后可以打开 |
| `.7z` | 暂时拒绝。请重新打包为zip |
| 其他任何文件 | 拒绝，[[5_troubleshooting]] |

改过名字的归档包照样能打开：游戏根据文件的字节识别格式。旧版本游戏的归档包会在导入时更新

默认情况下，导入的关卡会获得自己的ID。所以它不会覆盖设备上已有的关卡

更多：[[6_sharing-by-hand]]。*Afterbeat*的关卡：[[3_afterbeat-import]]

## 关卡界面

关卡界面显示封面、作者、简介和音乐作者。界面上还有`{{ui:level_level-view_authors}}`和`{{ui:level_level-view_licenses}}`按钮

如果关卡元数据里写有链接，点击作者名字和音乐那一行会打开对应的链接

年龄分级由关卡作者标注，游戏不做检查

当作者声明关卡、其封面或其中某个资源由AI生成时，会显示“含有AI生成的内容”。这同样是作者自己的声明。没有这一行并不代表“没有AI”：作者可能只是什么都没有标注

开始之前你可以选择条件：

| 条件 | 可选值 |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}`（这一局不会结束）、`{{ui:menu_levelview_options-lifes_option-one}}`、`{{ui:menu_levelview_options-lifes_option-three}}`、`{{ui:menu_levelview_options-lifes_option-custom}}`（滑块，最多16） |
| `{{ui:field_common_speed}}` | `0.5`、`1.0`、`2.0`、`{{ui:menu_levelview_options-lifes_option-custom}}`（滑块，最多2）。关卡和音乐会一起变速 |
| `检查点` | 开或关，[[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | 开或关。化身会穿过一切，[[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`、`{{ui:enum_bot-kind_reflex}}`、`{{ui:enum_bot-kind_warm}}`，[[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | 一个数字、`{{ui:level_level-view_seed-randomize}}`、`{{ui:level_level-view_seed-clear}}`。`0`表示每局使用新的种子，[[8_determinism]] |

按`开始`开始这一局

暂停时有`{{ui:game_pause-window_continue-btn}}`、`{{ui:game_pause-window_restart-btn}}`、`{{ui:game_game-result_restart-checkpoint}}`（到达检查点之后）、`{{ui:settings_common_title}}`、`{{ui:game_game-result_back-to-options}}`和`{{ui:game_game-result_back-to-menu}}`。`{{ui:game_game-result_back-to-options}}`会回到关卡界面，并保留这一局开始时的条件。如果这一局是从编辑器开始的，则回到编辑器的`游玩`标签页

## 结果窗口

窗口显示`通过`或`{{ui:game_game-result_lose}}`，以及三个部分：`进度`、`{{ui:game_game-result_section-damage}}`和`{{ui:game_game-result_section-conditions}}`

- 各行：`完成度`、`{{ui:game_game-result_checkpoint}}`、`{{ui:field_common_time}}`、`{{ui:game_game-result_length}}`、`{{ui:game_game-result_hits}}`、`{{ui:game_game-result_lives-left}}`、`{{ui:game_game-result_streak}}`
- 本局条件：`{{ui:field_common_speed}}`、`{{ui:menu_levelview_options-lifes_title}}`、`{{ui:menu_levelview_options-bot}}`、`{{ui:game_game-result_seed}}`、`检查点`。开启`{{ui:menu_levelview_options-no-collision_title}}`的一局会在`{{ui:menu_levelview_options-lifes_title}}`后面加上`· 无碰撞`
- 按钮：`{{ui:game_pause-window_restart-btn}}`、`{{ui:game_game-result_restart-checkpoint}}`、`{{ui:settings_common_title}}`、`{{ui:game_game-result_back-to-options}}`、`{{ui:game_game-result_back-to-menu}}`

默认情况下，失败时不会打开这个窗口，而是把这一局倒回到上一个检查点。要改变这一点：`{{ui:settings_common_title}}`→`{{ui:settings_interface_label}}`→`{{ui:settings_interface_open-menu-on-lose}}`

## 纪录

关卡界面上有一个纪录区：`{{ui:menu_levelview_record-best}}`、`{{ui:menu_levelview_record-attempts}}`和`{{ui:menu_levelview_record-clears}}`（或`{{ui:menu_levelview_record-none}}`）

每一组条件都有自己的纪录：生命、速度、检查点、碰撞和机器人。纪录区显示当前所选条件下的纪录。尝试次数和通关次数对任何一局都会统计

纪录是怎么选出来的：[[10_statistics]]

## 卡片标记

| 标记 | 含义 |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | 硬盘上有这个创意工坊文件夹，但你没有订阅它。只有打开`{{ui:settings_common_title}}`→`{{ui:settings_general_title}}`→`{{ui:settings_general_show-all-found-content}}`时才可见 |
| `{{ui:root_level-entry_unverified}}` | 关卡来源没有响应 |
| `{{ui:root_level-entry_newer-version}}`、`{{ui:root_level-entry_newer-file}}` | 这个版本的游戏无法打开该关卡，[[5_troubleshooting]] |

## 删除关卡

长按或右键点击卡片→`{{ui:root_level-browser_delete}}`。游戏会先要求确认

你可以同时删除关卡的统计数据（`{{ui:root_level-delete_statistics}}`）和备份（`{{ui:root_level-delete_backups}}`）

删除受保护的关卡不需要密码
