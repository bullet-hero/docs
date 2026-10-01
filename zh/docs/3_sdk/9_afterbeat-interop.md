---
title: Afterbeat互通
date: 2026-10-01
tags: [developer, level_author]
---

# Afterbeat互通

SDK通过ABInterop类把Afterbeat的关卡、元数据、主题和预制件转换为Bullet Hero格式，也能反向转换。途中丢失或近似处理的一切都会记入报告

*Afterbeat*（原名*Project Arrhythmia*，由Vitamin Games开发）把一个关卡存放在四个JSON文档中，`ABInterop`可以双向转换全部四个

| 文档 | 扩展名 | 导入 | 导出 |
|---|---|---|---|
| 关卡 | `.vgd` | `ImportLevel(levelJson, metaJson, options)` | `ExportLevel(level, meta, options)` |
| 元数据 | `.vgm` | 与关卡一起 | 与关卡一起 |
| 主题 | `.vgt` | `ImportTheme(themeJson, report)` | `ExportTheme(theme, report)` |
| 预制件 | `.vgp` | `ImportPrefab(prefabJson, options, ...)` | `ExportPrefab(prefab, options, ...)` |

`ExportLevel`返回`ExportedLevel`，其中包含`LevelJson`、`MetaJson`和`Report`

在编辑器中，导入被包装成生成器`gen_level_afterbeat`。它在作者眼中是什么样子：[[3_afterbeat-import]]

## 工作方式

- **输入是文本，输出也是文本**。互通层不读取文件，也不接受路径。文档从哪里来由宿主决定
- **宿主应当搜索文件，而不是依赖文件名**。Afterbeat关卡文件夹的说明很少：`level.vgd`、`cover.jpg`，以及`.ogg`、`.mp3`或`.wav`格式的歌曲
- **不经过`SerializationService`**。外来文档既不会套上`{"g", "v"}`封套，也不会使用本格式的转换器：两者都会损坏它。Afterbeat格式根本没有版本字段
- **未知的键会保留**。每个Afterbeat模型都会保存自己不认识的键（`[JsonExtensionData]`）。往返不会删除它们
- **标识符是推导出来的，而不是生成的**。Afterbeat用任意字符串命名主题和预制件，`ABIdMap`把它们哈希为稳定的Guid。先导入`.vgt`，再导入引用它的`.vgd`，两次得到的ID相同
- **每一处损失都记入报告**。`InteropReport`按原因归类所有丢失或近似处理的内容。每个原因都有发生次数和第一次发生的位置

`ABOptions`包含转换无法自行做出的决定：`Framerate`（默认60）、`ImportParallax`、`ImportPrefabs`、`LayerImport`、`OpacityHitThreshold`等

## 途中会改变什么

| 项目 | 在Afterbeat中 | 在Bullet Hero中 |
|---|---|---|
| 时间 | 秒 | 按关卡帧率计的帧 |
| 旋转 | 角度，每个关键帧相对于上一个 | 弧度，绝对值 |
| 相机缩放 | 可见高度的一半，默认20 | `Zoom`，整个可见高度，也就是两倍 |
| 绘制顺序 | 深度0-60，越小越近 | 相对于父级的`Layer`，越大越近 |
| 伤害 | 不透明度低于1的物体不造成伤害 | 物体类型决定`ColliderId`，不透明度决定该碰撞体何时存在 |
| 视差 | 独立的背景子系统 | 没有碰撞体的普通物体 |

主题双向都能精确转换。Afterbeat的34种颜色与`ThemeData`的槽位布局相同，只是没有Alpha

游戏自带的21个主题会在关卡中具体化为普通主题

## 限制

**不导入**：
- 触发器
- 屏幕渐变事件轨道
- 景深
- 按单独的轴继承父级，以及父级的时间偏移
- 预制件的预览和提前时间

玩家力和色相轨道在报告中标记为延后处理。它们等待的是实现工作，而不是决定

**不导出**：
- 音频：Afterbeat关卡只有一个歌曲文件，没有轨道列表、偏移和效果
- 在关卡中创建的几何形状
- 锚点
- 按角设置的颜色
- 按字符的文本效果
- 随机值
- 第一个之后的节拍段
- World以外的检查点空间
- 多个后期效果
- 单个预制件实例的覆盖
- 许可证、年龄分级和署名：`.vgm`中没有对应的字段

这对作者意味着什么：[[3_afterbeat-import]]

完整的对应关系：[Interop/AfterBeat/README.md](https://github.com/bullet-hero/sdk/blob/master/Interop/AfterBeat/README.md)
