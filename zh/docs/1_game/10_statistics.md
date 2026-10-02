---
title: 统计
date: 2026-10-02
tags: [advanced_player]
---

# 统计

游戏按每个关卡和整台设备统计尝试次数、死亡次数、受击次数和时间。所有数据都保存在本地的stats文件夹中。每一组游玩条件单独记录纪录

## 两个文件

| 文件 | 保存什么 |
|---|---|
| `stats/statistics.json` | 关于你的一切：涵盖所有关卡和界面 |
| `stats/<LevelId>.json` | 你对某一个关卡做过的一切 |

文件为JSON格式，时间为UTC。不会向任何地方发送任何数据

`stats`文件夹位于游戏文件夹中`levels`的旁边，[[1_installation]]。它永远不会位于关卡内部。这样发给朋友的关卡不会带着已通关的状态到达。你的进度也能在删除关卡并重新导入后保留下来

## “档案”标签页

`{{ui:settings_common_title}}`→`{{ui:settings_profile_tab}}`显示设备的共享文件：

| 分区 | 行 |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`、`{{ui:settings_profile_last-played}}`、`{{ui:settings_profile_launches}}`、`{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`、`{{ui:settings_profile_game-time}}`、`{{ui:settings_profile_editor-time}}`、`{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`、`{{ui:settings_profile_clears}}`、`{{ui:settings_profile_deaths}}`、`{{ui:settings_profile_hits}}`、`{{ui:settings_profile_levels-played}}`、`{{ui:settings_profile_levels-cleared}}`、`{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`、`{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`、`{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`、`{{ui:settings_profile_tutorial-first}}`、`{{ui:settings_profile_tutorial-last}}`，只有完成[[13_sandbox|沙盒教程]]的所有步骤才算一次完成 |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`、`{{ui:settings_profile_levels-deleted}}`、`{{ui:settings_profile_objects}}`、`{{ui:settings_profile_operations}}`、`{{ui:settings_profile_generators}}`、`{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`、`{{ui:settings_profile_device-touch}}`、`{{ui:settings_profile_device-gamepad}}`、`{{ui:settings_profile_device-gyro}}` |

时间按真实秒数计算，而不是关卡时间。检查点处的慢动作和半速游玩，按实际经过的时长计入

设备行显示游玩时由哪台设备操控化身。仅仅连接着的设备不计入

## 按关卡

关卡文件保存：

- 你第一次和最近一次游玩它的时间
- 在关卡中的真实时长和进入次数
- 尝试次数（每次重开都是新的一次）、通关次数、死亡次数、受击次数、冲刺次数
- 回到检查点的次数和放弃的游玩
- 到达过的最远位置和首次通关
- 你在关卡中的哪里死亡：按长度比例和按检查点

## 纪录

纪录按游玩条件记录：生命、速度、检查点开或关、碰撞开或关，以及机器人。速度精确到百分位，与界面上显示的完全一致

禅（0条生命）依然统计受击：每次碰撞都计入它的数据，免除的只有生命损失和游玩结束

一次游玩在以下情况下打破相同条件的纪录，按顺序比较：

1. 它走得更远
2. 它受击更少
3. 它结束时剩余生命更多
4. 它使用的冲刺更少

纪录还保存这次游玩的种子和当时的关卡版本。版本不属于条件。因此关卡重做之前创下的纪录依然可见，旁边会显示版本

**从编辑器开始的游玩会被统计，但不创造纪录**。它计入尝试次数、死亡次数和受击次数。它不产生纪录、最佳进度和首次通关，因为那个关卡只存在于内存中

## 写入、删除、冻结

游戏每30秒写入一次统计。游玩结束、切换界面和退出时也会立即写入。崩溃最多损失30秒的数据

- **删除**：`{{ui:settings_common_title}}`→`{{ui:settings_other_title}}`→`{{ui:settings_other_cache-title}}`。那里有`{{ui:settings_other_cache-orphan-statistics}}`和`{{ui:settings_other_cache-all-statistics}}`
- **随关卡删除**：删除关卡时会提供`{{ui:root_level-delete_statistics}}`
- **冻结**：匿名模式会停止一切写入，直到关闭游戏，[[4_settings]]

> [!warning] 警告
> 手动复制的关卡文件夹会保留关卡的ID。原件和副本共用同一个统计文件
