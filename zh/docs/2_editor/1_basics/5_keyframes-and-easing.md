---
title: 关键帧与缓动
date: 2026-10-12
tags: [level_author]
---

# 关键帧与缓动

关键帧是某条轨道在某一帧上的数值，再加上到达这个数值时使用的缓动。关卡中所有会移动、变色或开关的东西，都是一串关键帧

基础概念：[[3_how-the-editor-thinks]]。关键帧检视器的每个字段：[[5_object-properties]]

## 哪些内容可以做动画

每条轨道都有自己的关键帧，与其他轨道互不影响：

| 所属 | 轨道 |
|---|---|
| 任意物体 | 位置、旋转、缩放、尺寸、锚点、轴心 |
| 形状 | 颜色、UV |
| 文本 | 颜色、字号、`{{ui:editor_dummy_text-11}}`（文本已写出的部分）、`{{ui:editor_dummy_text-12}}`（文本被遮罩隐藏的部分） |
| 相机 | 位置、旋转、缩放、轴心、震动 |
| 关卡 | 背景、主题、屏幕限制、12种后期效果中的每一种 |
| 玩家 | 尺寸、速度、可见性、控制、碰撞 |

物体的关键帧从它的时段起点开始计算。所以在时间上移动物体，它的整段动画会跟着一起移动

位置相对于父级设置。关键帧存储的是数值本身，而不是相对于上一个关键帧的增量

玩家的可见性、控制和碰撞只有开和关两种状态。这些关键帧没有缓动：没有什么可以混合

空的玩家轨道上的第一个关键帧不会改变画面：可见性、控制和碰撞为开启，大小和速度为玩家的常规值。控制关闭或玩家隐藏时无法操控玩家：光标消失，按下也不会被接收。隐藏的玩家仍会被击中：这只由碰撞决定

## 文本：填充与出现

两条文本轨道以不同方式隐藏字符。两者都取0到1之间的比例，按文本的字符计数

`{{ui:editor_dummy_text-11}}`是文本已写出的比例：0表示什么都没有，1表示全部。未写出的字符完全不绘制，所以这一行会变短。空轨道写出全部文本。方向由每个关键帧设置：
- `{{ui:enum_text-fill-direction_forward}}`（默认）：从第一个字符开始，像打字机一样
- `{{ui:enum_text-fill-direction_backward}}`：从最后一个字符开始
- `{{ui:enum_text-fill-direction_from-center}}`：从中间向外扩展
- `{{ui:enum_text-fill-direction_to-center}}`：从两端向内扩展，在中间会合

`{{ui:editor_dummy_text-12}}`是被遮罩隐藏的字符比例：0表示全部显示，1表示全部被遮罩。被隐藏的字符保留自己的位置，绘制成遮罩字符，默认为`{{v:text.appearing-mask-default}}`。遮罩是文本物体的`{{ui:editor_inspector-appearing_mask}}`字段，其中有多个字符时，每个被隐藏的字符取其中一个。空轨道不隐藏任何字符。模式由每个关键帧设置：
- `{{ui:enum_text-appearing-mode_random}}`（默认）：分散，但每次运行的分布都相同。在0.3时被隐藏的字符在0.6时仍被隐藏，所以文本是逐渐显现，而不是闪烁
- `{{ui:enum_text-appearing-mode_forward}}`：被隐藏的字符在末尾，文本从开头出现
- `{{ui:enum_text-appearing-mode_backward}}`：被隐藏的字符在开头

要让一行字逐字打出，把`{{ui:editor_dummy_text-11}}`从0做动画到1。要让它从噪点中显现，把`{{ui:editor_dummy_text-12}}`从1做动画到0

## 几条建议

- 只给会动的东西设置关键帧。没有关键帧的轨道取默认值
- 需要正好落在节拍上的变化，使用`Constant`，例如在drop处切换主题
- 旋转不会折回：0度的关键帧和720度的关键帧会让物体转两圈

## 两个关键帧之间

在第一个关键帧之前和最后一个关键帧之后，数值保持不变。在两个关键帧之间，游戏取已经过去的时间比例，让它经过缓动处理，再混合两个数值

这个比例按时间计算，而不是按绘制的帧计算。所以在30fps和144fps下曲线完全相同

**缓动属于一对关键帧中较晚的那个**。关键帧的缓动决定从上一个关键帧到达它的这一段。所以轨道上第一个关键帧的缓动永远不会显现出来。新关键帧使用`Linear`

`{{ui:hint_editor_inspector_ease_header}}`字段会打开`{{ui:editor_search-title_ease}}`窗口，每种缓动都画成各自的曲线。你可以选中多个关键帧，甚至是不同轨道上的关键帧，在一个撤销步骤内一起修改

## 29种缓动

`Linear`是一条直线。`Constant`保持上一个数值，到关键帧时直接跳变

其余27种分为九个系列，每个系列三种：`In`、`Out`和`InOut`。例如`InSine`、`OutSine`、`InOutSine`

| 系列 | 曲线形态 |
|---|---|
| `Sine` | 最柔和的曲线 |
| `Quad`、`Cubic`、`Quart`、`Quint` | 2、3、4、5次幂 |
| `Expo` | 指数 |
| `Circ` | 四分之一圆 |
| `Back` | 越过范围后返回 |
| `Elastic` | 在目标值附近振荡 |

`In`开始慢、结束快。`Out`开始快、然后放缓。`InOut`两端都慢。从`Sine`到`Expo`，每个系列都比前一个更陡

> [!caution] 注意
> `Back`和`Elastic`会超出范围：`Out`会冲过目标，`In`会先反向越过起点。碰撞体随物体一起移动。所以一颗本应停在安全区边缘的子弹，会有几帧进入安全区

## 随机数值

关键帧中的数值不一定是单个数字：
- 数字：`{{ui:field_common_value}}`、`{{ui:enum_color-type_random-min-max}}`、`{{ui:enum_float-type_random-min-max-step}}`
- 向量（位置、缩放等）：`{{ui:field_common_value}}`、`{{ui:enum_vector-type_random-rect}}`、`{{ui:enum_vector-type_random-rect-step}}`、`{{ui:enum_vector-type_random-circle}}`、`{{ui:enum_color-type_random-lerp}}`、`{{ui:enum_vector-type_random-lerp-step}}`
- 颜色：`{{ui:field_common_value}}`、`{{ui:editor_events-timeline_track_theme}}`、`{{ui:enum_color-type_random-min-max}}`、`{{ui:enum_color-type_random-lerp}}`

`{{ui:enum_vector-type_random-rect}}`对每个轴分别取值。`{{ui:enum_color-type_random-lerp}}`对所有轴取同一个数，所以点会落在A和B之间的连线上。带步长的变体会把结果向下取整到步长的倍数。步长为0时不使用网格，数值与不带步长的变体相同。之后，这个关键帧和其他关键帧一样进行混合

同一个种子得到同一个关卡。随机数由种子、关键帧所在的帧、图层、物体的起始帧、轨道和通道计算得出。更多：[[8_determinism]]

接下来：[[2_rhythm-and-structure|节奏与结构]]、[[6_themes|主题]]
