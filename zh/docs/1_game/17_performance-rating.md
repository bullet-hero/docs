---
title: 性能评分
date: 2026-10-15
tags: [player, level_author]
---

# 性能评分

开始游玩之前，游戏会显示关卡在你的设备上运行起来有多吃力。绿色表示运行流畅，黄色表示吃紧，红色表示过重，帧率会下降

评分是一个数字，`{{v:performance.score-limit}}` 正好等于在你的目标帧率下一帧可用的时间。档位由评分决定：

| 档位 | 评分 |
|---|---|
| `{{ui:level_performance_holds}}` | 低于 `{{v:performance.score-warning}}` |
| `{{ui:level_performance_tight}}` | 从 `{{v:performance.score-warning}}` 到 `{{v:performance.score-limit}}` |
| `{{ui:level_performance_does-not-hold}}` | 高于 `{{v:performance.score-limit}}` |
| `{{ui:level_performance_unknown}}` | 关卡或设备尚未测量 |

评分预测的是关卡最吃力的时刻，而不是平均情况。一个关卡轻松运行三分钟、卡住一秒钟，得到的就是那一秒的评分

## 在哪里看到

- 关卡浏览器：每张关卡卡片上的彩色圆点，以及筛选中的 `{{ui:root_level-filters_performance}}` 分组
- 菜单中的关卡页面：档位和评分
- 关卡编辑器中关卡的元数据：在你的设备和参考设备上的评分，以及关卡最吃力的时刻（时间戳）

## 评分的两半

**关卡的一半**在编辑器中保存关卡时测量，并存放在它的元数据里。它描述关卡的需求：有多少对象存活、它们覆盖了多少屏幕、运行了多少特效和后期处理通道。在此功能出现之前保存的关卡没有这条记录，在再次保存之前显示为 `{{ui:level_performance_unknown}}`。编辑器在打开关卡时会测量它，并保留结果直到关闭游戏，但不写入文件

**设备的一半**说明你的设备做这些事情的速度。在你测量设备之前，游戏使用你所在平台的参考设备。你的设置也会计入：渲染缩放、抗锯齿、特效和后期处理都会改变评分，无需重新测量

## 测量你的设备

1. 从主菜单打开 `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. 按下 `{{ui:settings_graphics-performance_measure}}`
3. 等待几分钟。设置界面会隐藏，游戏播放测试关卡。不要切换到其他应用

完成后，该部分会显示你的设备受什么限制（处理器或图形芯片），以及推荐哪个 `{{ui:settings_quick-setup_performance}}` 预设

如果测量不稳定（设备过热、其他应用占用资源），游戏会忽略它并继续使用参考设备。关闭其他应用后重新测量

## 换到另一台设备

测量结果属于进行测量的那台设备。档案转移（[[14_profile-transfer]]）和云存档都不会带上它，所以新设备会从它的参考设备开始，直到你重新测量
