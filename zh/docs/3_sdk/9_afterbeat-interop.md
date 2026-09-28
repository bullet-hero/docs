---
title: Afterbeat互通
date: 2026-09-24
tags: [developer, level_author]
---

# Afterbeat互通

在Afterbeat与Bullet Hero格式之间双向转换关卡、主题和预制件，以及转换中会丢失什么

*Afterbeat*（原名*Project Arrhythmia*，由Vitamin Games制作）用四个JSON文档保存一个关卡。SDK通过一个类`ABInterop`对这四种文档做双向转换

| 文档 | 扩展名 | 导入 | 导出 |
|---|---|---|---|
| 关卡 | `.vgd` | `ImportLevel(levelJson, metaJson, options)` | `ExportLevel(level, meta, options)` |
| 元数据 | `.vgm` | 与关卡一起 | 与关卡一起 |
| 主题 | `.vgt` | `ImportTheme(themeJson, report)` | `ExportTheme(theme, report)` |
| 预制件 | `.vgp` | `ImportPrefab(prefabJson, options, ...)` | `ExportPrefab(prefab, options, ...)` |

`ExportLevel`返回带有`LevelJson`、`MetaJson`和`Report`的`ExportedLevel`

在编辑器中，导入被包装成生成器`gen_level_afterbeat`。它在作者眼中的样子：[[3_afterbeat-import]]

## 工作方式

- **输入文本，输出文本**。互通层不读取文件，也不接受路径。文档从哪里来是宿主的事
- **宿主应当查找文件，而不是假定文件名**。Afterbeat的关卡文件夹没有完善的文档：`level.vgd`、`cover.jpg`，歌曲为`.ogg`、`.mp3`或`.wav`
- **不经过`SerializationService`**。外来文档不加`{"g", "v"}`封套，也不使用本格式的任何转换器：两者都会破坏它。Afterbeat格式根本没有版本字段
- **未知键会保留**。每个Afterbeat模型都保留自己不认识的键（`[JsonExtensionData]`）。往返转换不会删除它们
- **ID是推导出来的，不是生成的**。Afterbeat用任意字符串命名主题和预制件，`ABIdMap`把它们哈希成稳定的Guid。先导入一个`.vgt`，再导入引用它的`.vgd`，两次得到的ID相同
- **每一处损失都会报告**。`InteropReport`把所有丢失或近似处理的内容按原因分组。每个原因都有计数和第一次出现的位置

`ABOptions`保存转换无法自行决定的选择：`Framerate`（默认60）、`ImportParallax`、`ImportPrefabs`、`LayerImport`、`OpacityHitThreshold`等

## 转换中的变化

| 内容 | 在Afterbeat中 | 在Bullet Hero中 |
|---|---|---|
| 时间 | 秒 | 按关卡帧率计的帧 |
| 旋转 | 角度制，每个关键帧相对于上一个 | 弧度制，绝对值 |
| 相机缩放 | 可见高度的一半，默认20 | `Zoom`，整个可见高度，因此翻倍 |
| 绘制顺序 | 深度0-60，越小越靠前 | 相对于父级的`Layer`，越大越靠前 |
| 伤害 | 不透明度低于1的物体不造成伤害 | 物体类型决定`ColliderId`，不透明度决定该碰撞体何时存在 |
| 视差 | 一个背景子系统 | 没有碰撞体的普通物体 |

主题在两个方向上都能精确转换。Afterbeat的34种颜色与`ThemeData`使用的槽位布局相同，只是没有Alpha

游戏自带的21个主题会作为普通主题写入关卡

## 限制

**不导入的内容**：
- 触发器
- 屏幕渐变事件轨道
- 景深
- 按轴继承父级和父级时间偏移
- 预制件预览图和提前时间

玩家推力和色相轨道会被报告为暂缓。它们等的是开发工作，而不是决策

**不导出的内容**：
- 音频：Afterbeat关卡只有一个歌曲文件，没有轨道列表、偏移和音频效果
- 关卡自定义的几何形状
- 锚点
- 逐角颜色
- 逐字符文本效果
- 随机值
- 第一个之后的节拍段
- World以外的检查点空间
- 部分后期效果
- 逐个放置的预制件覆盖
- 许可、年龄分级和署名：`.vgm`没有对应的字段

这对作者意味着什么：[[3_afterbeat-import]]

完整的映射见[Interop/AfterBeat/README.md](https://github.com/bullet-hero/sdk/blob/master/Interop/AfterBeat/README.md)
