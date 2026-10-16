---
title: 性能评分
date: 2026-10-17
tags: [player, level_author]
---

# 性能评分

开始游玩之前，游戏会用一个五格的指示条显示关卡在你的设备上运行起来有多吃力：亮起的格越多，关卡越轻松。绿色的格表示运行流畅，黄色表示吃紧，红色表示帧率会下降

评分是一个数字，`{{v:performance.score-limit}}` 正好等于在你的目标帧率下一帧可用的时间。档位由评分决定：

| 格数 | 档位 | 评分 |
|---|---|---|
| 5 | `{{ui:level_performance_holds}}` | 低于 `{{v:performance.score-warning}}` |
| 4 | `{{ui:level_performance_tight}}` | 从 `{{v:performance.score-warning}}` 到 `{{v:performance.score-limit}}` |
| 3 | `{{ui:level_performance_drops}}` | 高于 `{{v:performance.score-limit}}`，最高到 `{{v:performance.score-heavy}}` |
| 2 | `{{ui:level_performance_severe-drops}}` | 高于 `{{v:performance.score-heavy}}`，最高到 `{{v:performance.score-severe}}` |
| 1 | `{{ui:level_performance_does-not-hold}}` | 高于 `{{v:performance.score-severe}}` |
| 无 | `{{ui:level_performance_unknown}}` | 关卡或设备尚未测量 |

评分预测的是关卡最吃力的时刻，而不是平均情况。一个关卡轻松运行三分钟、卡住一秒钟，得到的就是那一秒的评分

## 在哪里看到

- 关卡浏览器：每张关卡卡片上的指示条，以及筛选中的 `{{ui:root_level-filters_performance}}` 分组
- 菜单中的关卡页面：指示条、档位和评分
- 关卡编辑器中关卡的元数据：在你的设备和参考设备上的评分，以及关卡最吃力的时刻（时间戳）

## 评分的两半

**关卡的一半**在每次保存后的几秒内由编辑器测量（你可以继续工作），并存放在它的元数据里。如果在测量完成前离开编辑器，文件保留上一次的测量。它描述关卡的需求：有多少对象存活、它们覆盖了多少屏幕、运行了多少特效和后期处理通道。在此功能出现之前保存的关卡没有这条记录，在再次保存之前显示为 `{{ui:level_performance_unknown}}`。编辑器在打开关卡时会测量它，并保留结果直到离开编辑器，但不写入文件

**设备的一半**说明你的设备做这些事情的速度。在你测量设备之前，游戏使用你所在平台的参考设备。你的设置也会计入：渲染缩放、抗锯齿、特效和后期处理都会改变评分，无需重新测量

## 测量你的设备

1. 从主菜单打开 `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. 按下 `{{ui:settings_graphics-performance_measure}}`。一个窗口会说明哪些做法有助于测量：关闭其他应用和游戏，将手机或笔记本电脑接上充电器，不要触碰设备
3. 按下 `{{ui:settings_graphics-performance_start}}`，最多等待 {{v:performance.benchmark-max-seconds}} 秒。设置界面会隐藏，游戏播放测试关卡，并在上方两角显示正在测量的内容。不要切换到其他应用

`{{ui:settings_graphics-performance_stop}}` 可提前结束测量。被停止或超时的测量不会保存任何内容，之前的结果保持不变

完成后，窗口会显示结果：演示关卡在你的设备上的指示条、你的设备受什么限制（处理器或图形芯片）、推荐哪个 `{{ui:settings_quick-setup_performance}}` 预设，以及你的关卡在每个档位各有多少个。`{{ui:settings_graphics-performance_again}}` 会再测量一次

如果测量不稳定（设备过热、其他应用占用资源），游戏仍会使用它，因为它比任何参考设备都更接近你的设备，窗口也会对此提示。关闭其他应用后重新测量，评分会更准确

## 换到另一台设备

测量结果属于进行测量的那台设备。档案转移（[[14_profile-transfer]]）和云存档都不会带上它，所以新设备会从它的参考设备开始，直到你重新测量
