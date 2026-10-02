---
title: 关卡格式
date: 2026-10-02
tags: [developer, level_author]
---

# 关卡格式

关卡是一个文件夹：内容在level.json或level.blob中，元数据在metadata.json或metadata.blob中，另有封面和媒体文件。备份、记录和玩家设置留在设备上

## 关卡文件夹

关卡文件夹中的每个文件名都固定在`FileNames`中：

| 文件 | 模型 | 内容 |
|---|---|---|
| `level.json`或`level.blob` | `Level` | 内容：设置、物体和事件、音频、资源、提示 |
| `metadata.json`或`metadata.blob` | `LevelMeta` | 名称、描述、作者、许可证、每个资源的记录、对封面的引用 |
| `logo.png`或`logo.jpg` | - | 封面 |
| 音轨、图片、字体 | - | 关卡引用的媒体文件 |

**扩展名就是格式**。文件内部的任何地方都没有写它。读取方看哪个文件存在：`level.json`还是`level.blob`

关卡和元数据各自独立选择格式。例如，内置关卡`new-zero-demo`在`metadata.json`旁边存放的是`level.blob`

**`metadata.json`特意做成单独的文件**。目录用一千个小元数据文件展示一千个关卡，期间一个关卡也不打开

## 资源

资源通过`uri`和`uri_type`（`ResourceUriType`）这一对值寻址：

| 值 | 类型 | 文件位置 |
|---|---|---|
| 1 | `LevelPath` | 关卡文件夹内。只有这种类型能让关卡可移植 |
| 2 | `AbsolutePath` | 本设备上的其他位置 |
| 3 | `DirectUrl` | 通过网络下载 |
| 4 | `StreamingAssets` | 随游戏提供，而不是随关卡 |

围绕一首歌创建关卡时会出现`AbsolutePath`。导出归档包时会把这样的文件复制进去。更多：[[4_archives]]

封面和其他资源一样，通过`LevelMeta.LevelLogo`访问。是`logo.png`还是`logo.jpg`，由文件本身的字节决定，而不是由源图片的名称决定

封面的作者记录是一个`resource_type`为9（`LevelLogo`）的`ResourceMeta`。其中`resource_id`和`resource_guid`都不填：关卡只有一个封面，所以类型就是完整的地址

## AI声明

`LevelMeta`和每个`ResourceMeta`都带有`AiGeneration`类型的`ai_generated`：

| 值 | 名称 | 含义 |
|---|---|---|
| 0 | `NotSpecified` | 未声明，未知。这是默认值，缺少该键时也按此读取 |
| 1 | `No` | 声明为未使用AI生成 |
| 2 | `Yes` | 声明为AI生成 |

在`LevelMeta`中，它只针对关卡自己的内容。每个资源和封面在各自的记录中声明自己。关卡中是否有AI内容并不存储：由`LevelMeta.ContainsAiContent()`回答，只有`Yes`才算

## 不随关卡一起走的内容

这些文件位于`levels`文件夹旁边，从不在关卡文件夹里。打包、发送或删除关卡都不会动它们：

| 文件夹或文件 | 是什么 | 为什么留下 |
|---|---|---|
| `backups/` | 编辑器自动保存，每个关卡ID一个文件夹，`backup_level_<time>.<extension>` | 放在它所保护的文件夹里的副本会随该文件夹一起被删除 |
| `stats/` | 按`LevelId`记录的成绩和进度，以及`statistics.json` | 否则别人发来的关卡到手时就已经通关了 |
| `settings.json` | `UserSettings`，玩家对整个设备的设置 | 它们属于玩家，而不属于关卡 |
| `resources/themes`、`effects`、`shapes`、`prefabs` | 本设备的共享库 | 它们由设备上的所有关卡共用 |
| `reports/` | 诊断报告 | - |

## JSON键

JSON总是紧凑写入，没有缩进。想用眼睛阅读，请在文本编辑器中格式化

**键的长度取决于它在关卡中出现的次数**：
- 每个文件只出现一次的键用完整单词以`snake_case`书写：`level_id`、`min_generation`
- 重复上千次的键缩短为几个字母：`objs`、`f`、`e`、`v`

键占关卡文件字节数的52%，所以这是规则，而不是个人口味。所有键都声明在`Names.cs`中

**多态值写作`[标签, 数据]`**。普通字符串是`[0,{"v":"Author"}]`，本地化字符串是`[1,{"strs":[...]}]`

`ObjectId`之类的标识符包装写作裸数字或裸字符串

## 标识符

**整数标识符的符号有含义**。`0`始终表示“未设置”：

| 标识符 | JSON键 | 正数 | 负数 |
|---|---|---|---|
| `ObjectId` | `id`，父级用`pid` | 关卡物体 | 游戏物体：`-1`相机，`-2`本地玩家，`-3`预制件模板的根 |
| 资源标识符 | `txid`、`fnid`、`auid`、`byid`、`ttid` | 随游戏提供的资源 | 关卡自己的资源 |
| 音频轨道的`AudioId` | `aid` | 本关卡的轨道 | 不使用 |

`pid`等于`0`表示物体没有父级。小于`-3`的数字只在游戏运行时存在，不会写入文件

**`Marker`、`Checkpoint`和`BeatSegment`没有标识符**。它们的地址是时间上的位置：标记和检查点是帧`f`，节拍段是其时段`sp`的第一帧（节拍段互不重叠）。移动这样的对象，它的地址就会改变

**预制件覆盖用编号而不是JSON键来指明字段**。放置把自己的覆盖存放在`mod`列表中。每个覆盖的`key`包含三个数字：
- `id`：模板内部的物体，而不是它在关卡中的副本
- `f`：字段的永久编号
- `i`：列表字段的元素，整个字段则为`-1`

编号永久绑定到字段。重命名该字段的JSON键不会破坏已经保存在关卡中的覆盖

## 外层的“g”

每个序列化根都包在一个带两个键的封套里：

```json
{"g":2,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g`是模型的代（`Names.Generation`），`v`是数据

封套可以嵌套。在`Level`内部，`LevelSettings`、`GameLevel`、`AudioLevel`、`LevelResources`和`LevelHints`都有自己的封套。代如何运作：[[5_versioning]]

> [!caution] 注意
> `g`和`vrs`是不同的数字。`vrs`是作者给关卡定的版本（`LevelMeta.LevelVersion`），与格式无关。不要手动修改`g`：`g`高于构建所知的文件完全无法读取
