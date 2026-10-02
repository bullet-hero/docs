---
title: 伤害与生命
date: 2026-10-02
tags: [advanced_player]
---

# 伤害与生命

每次命中消耗一条命，把化身击退{{v:avatar.knockback-time}}秒，并给予{{v:avatar.damage-timeout}}秒无敌时间。默认情况下，死亡会把关卡倒回到最后一个检查点并恢复生命

## 命中的三个阶段

1. **击退，`{{v:avatar.knockback-time}}`秒**。你以每秒`{{v:avatar.knockback-speed}}`单位的速度被推离命中你的东西。这大约是{{v:avatar.knockback-distance}}单位，一整次冲刺，默认屏幕高度的四分之三。期间不接受输入。无法用冲刺摆脱击退：击退优先于一切
2. **操控恢复**，在这{{v:avatar.knockback-time}}秒之后
3. **无法被命中**，从命中那一刻起整整`{{v:avatar.damage-timeout}}`秒。这一秒内的所有命中都会被忽略

如果你正好站在命中你的东西上，就没有方向可推。这时你完全不会被击退

出现期间（`{{v:avatar.spawn-time}}`秒）和冲刺保护的`{{v:avatar.dash-invulnerability}}`秒内你同样无法被命中，[[6_avatar]]

> [!info] 须知
> 待在危险区域里只消耗一条命，而不是十条。被推进第二个危险区域也能活下来。密集的弹幕看起来像是瞬间死亡，实际往往比一颗正好在保护秒结束时飞来的子弹代价更小

## 生命

生命数量在关卡画面中选择：`{{ui:menu_levelview_options-lifes_option-zen}}`、`{{ui:menu_levelview_options-lifes_option-one}}`、`{{ui:menu_levelview_options-lifes_option-three}}`或最多16条的`{{ui:menu_levelview_options-lifes_option-custom}}`，[[2_playing-levels]]

每次命中消耗一条命。拿走最后一条命的命中就是死亡

`{{ui:menu_levelview_options-lifes_option-zen}}`对命中的反应和其他任何一局都一样：击退、护盾圆环、粒子爆发和一秒保护照常生效，命中也计入统计。但它永远不会消耗生命，所以这一局永远不会结束

生命由化身周围的圆点圆环显示：亮着的点是剩余的命，熄灭的是已消耗的

结果窗口显示`{{ui:game_game-result_hits}}`和`{{ui:game_game-result_lives-left}}`

## 死亡会发生什么

默认情况下，死亡不会结束这一局：

1. 关卡时钟在现实时间`{{v:checkpoint.rewind-time}}`秒内平滑停下。音乐也随之下沉
2. 关卡跳回到最后到达的检查点。生命恢复
3. 时钟在另外`{{v:checkpoint.rewind-time}}`秒内平滑加速回这一局的速度。加速期间你无法被命中，否则危险位置旁边的检查点会在第一秒内拿走全部生命

暂停也会停止这次加速

如果在关卡画面中关闭了`检查点`，就会倒回到关卡开头

想让死亡打开结果窗口，请开启`{{ui:settings_common_title}}`→`{{ui:settings_interface_label}}`→`{{ui:settings_interface_open-menu-on-lose}}`。这样回放会停止

在该窗口中，`{{ui:game_game-result_restart-checkpoint}}`会从已到达的检查点开始新的尝试

## 检查点

检查点由关卡作者放置。是否计入由你通过`检查点`开关决定

已到达的检查点是关卡当前位置或之前的最后一个检查点。所以回到它不会撤销任何东西，只是倒回

作者可以让检查点恢复生命值。这样经过它时会在一局中途恢复一次生命

屏幕底部的进度条在每个检查点处有一个刻度。进度条在`{{ui:settings_interface_label}}`→`{{ui:settings_interface_show-game-progress}}`中开启

有检查点和没有检查点的记录分开保存，[[10_statistics]]

## 无碰撞

`{{ui:menu_levelview_options-no-collision_title}}`是独立于`{{ui:menu_levelview_options-lifes_option-zen}}`的开关，在关卡画面和编辑器的启动面板中位于`检查点`旁边。开启后化身会穿过一切：再也没有东西能碰到它

`{{ui:menu_levelview_options-no-collision_title}}`的一局保存自己的记录，与`{{ui:menu_levelview_options-lifes_option-zen}}`和普通的局分开，结果窗口会在`{{ui:menu_levelview_options-lifes_title}}`的值后面加上`· 无碰撞`来标记它，[[10_statistics]]
