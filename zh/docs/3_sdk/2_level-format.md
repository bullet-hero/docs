---
title: 关卡格式
date: 2026-09-24
tags: [developer, level_author]
---

# 关卡格式

关卡文件夹里有什么，哪些文件随关卡一起走，哪些留在设备上，以及其中的JSON如何组织

## 关卡文件夹

关卡就是一个文件夹。其中每个文件名都固定在`FileNames`中：

| 文件 | 模型 | 内容 |
|---|---|---|
| `level.json`或`level.blob` | `Level` | 内容：设置、物体和事件、音频、资源、提示 |
| `metadata.json`或`metadata.blob` | `LevelMeta` | 名称、描述、作者、许可证、每个资源的一条记录、封面引用 |
| `logo.png`或`logo.jpg` | - | 封面 |
| 音轨、图片、字体 | - | 关卡引用的媒体文件 |

**扩展名就是格式**。文件内部不记录它。读取方检查存在的是哪个文件：`level.json`还是`level.blob`

关卡和元数据各自独立选择格式。例如内置关卡`new-zero-demo`在`metadata.json`旁边存放的是`level.blob`

**`metadata.json`是有意单独存放的**。目录列出一千个关卡时，只读取一千个小的元数据文件，一个关卡都不用打开

## 资源

资源由`uri`和`uri_type`（`ResourceUriType`）定位：

| 值 | 类型 | 文件在哪里 |
|---|---|---|
| 1 | `LevelPath` | 在关卡文件夹内。只有这种类型能让关卡可移植 |
| 2 | `AbsolutePath` | 在本设备的其他位置 |
| 3 | `DirectUrl` | 通过网络下载 |
| 4 | `StreamingAssets` | 随游戏提供，而不是随关卡 |

围绕一首歌创建关卡时得到的就是`AbsolutePath`。导出归档包时会把这类文件复制进去。更多：[[4_archives]]

封面和其他资源一样，通过`LevelMeta.LevelLogo`引用。是`logo.png`还是`logo.jpg`由文件本身的字节决定，而不是源图片的名称

## 不随关卡走的内容

这些文件位于`levels`文件夹旁边，从不在关卡文件夹内。打包、分享或删除关卡都不会动它们：

| 文件夹或文件 | 是什么 | 为什么留下 |
|---|---|---|
| `backups/` | 编辑器自动保存，每个关卡ID一个文件夹，`backup_level_<timestamp>.<ext>` | 放在被保护文件夹里的备份会和它一起被删除 |
| `stats/` | 按`LevelId`记录的成绩和进度，以及`statistics.json` | 否则分享出去的关卡到对方手里时已经通关 |
| `settings.json` | `UserSettings`，整台设备通用的玩家选项 | 它们属于玩家，而不是关卡 |
| `resources/themes`、`effects`、`shapes`、`prefabs` | 整台设备的共享库 | 它们由设备上的所有关卡共用 |
| `reports/` | 诊断报告 | - |

## JSON键

JSON总是紧凑写入，没有缩进。想用眼睛读，请在文本编辑器里格式化

**键的长度取决于它在关卡中出现的频率**：
- 每个文件只出现一次的键用完整的`snake_case`：`level_id`、`min_generation`
- 重复成千上万次的键缩写成几个字母：`objs`、`f`、`e`、`v`

键占关卡文件字节数的52%，所以这是规则，而不是个人口味。所有键都声明在`Names.cs`中

**多态值写作`[tag, payload]`**。普通字符串是`[0,{"v":"Author"}]`，本地化字符串是`[1,{"strs":[...]}]`

`ObjectId`这类ID包装类型写成裸数字或字符串

## 标识符

**整数ID的符号有含义**。`0`始终表示未设置：

| ID | JSON键 | 正数 | 负数 |
|---|---|---|---|
| `ObjectId` | `id`，父级用`pid` | 关卡中的物体 | 游戏的物体：`-1`相机，`-2`本地玩家，`-3`预制件模板的根 |
| 资源ID | `txid`、`fnid`、`auid`、`byid`、`ttid` | 随游戏提供的资源 | 关卡自己的资源 |
| 音频轨道的`AudioId` | `aid` | 本关卡的一条轨道 | 从不使用 |

`pid`为`0`表示物体没有父级。小于`-3`的数字只在游戏运行时存在，从不出现在文件中

**`Marker`、`Checkpoint`和`BeatSegment`没有ID**。它们按时间位置定位：标记和检查点按帧`f`，节拍段按其时段`sp`的起始帧（节拍段从不重叠）。移动其中一个，它的地址就会改变

**预制件覆盖用编号而不是JSON键来指明字段**。一次放置把自己的覆盖保存在列表`mod`中。每个覆盖的`key`包含三个数字：
- `id`：模板内的物体，而不是它在关卡中的副本
- `f`：字段的固定编号
- `i`：列表字段中的元素，`-1`表示整个字段

编号永久属于该字段。重命名字段的JSON键不会破坏已保存在关卡中的覆盖

## 外层的“g”

每个序列化根都包在一个带两个键的封套里：

```json
{"g":1,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g`是模型的代（`Names.Generation`），`v`是载荷

封套可以嵌套。在`Level`内部，`LevelSettings`、`GameLevel`、`AudioLevel`、`LevelResources`和`LevelHints`各有自己的封套。代的工作方式：[[5_versioning]]

> [!caution] 注意
> `g`和`vrs`是不同的数字。`vrs`是作者给关卡定的版本（`LevelMeta.LevelVersion`），与格式无关。不要手动修改`g`：`g`高于当前构建所知的文件会被整个拒绝读取
