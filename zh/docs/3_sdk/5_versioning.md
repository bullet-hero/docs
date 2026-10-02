---
title: 版本与迁移
date: 2026-10-02
tags: [developer, level_author]
---

# 版本与迁移

版本有三种：gv对应游戏，sv对应SDK，mg对应模型格式的代。SDK依据mg迁移旧文件，并拒绝读取代比当前构建更新的文件

## 三种版本

| 标记 | 全称 | 给什么定版本 | 存放位置 |
|---|---|---|---|
| `gv` | `game version` | 游戏客户端 | Unity项目的`bundleVersion` |
| `sv` | `sdk version` | 作为库的SDK，按其公开API遵循semver | `SdkVersion.Value` |
| `mg` | `model generation` | 模型格式，每个域一个代 | 每个根上的`[ModelGeneration]`，`ModelGenerations.Current` |

当前版本：`gv 1.1.0`、`sv 1.1.0`、`mg 2`

`gv`和`sv`的数字不必互相跟随，但大多数情况下是一致的。版本会一起提升，共同的更新使用同一个版本号

各部分的含义：
- `gv`：major是全局更新（剧情、多人游戏），minor是普通的新功能，patch是紧急修复
- `sv`，在SDK开始承诺API稳定之后：major是破坏性的API变更（删除类型，或改变成员的签名或含义），minor是无需任何人应对的新增，patch是不改变签名的修复

**`mg`比其他两个更重要**。SDK根据它决定是迁移文件还是拒绝读取

设置界面按这个顺序并带标记显示全部三个：`gv 1.1.0, sv 1.1.0, mg 2`。没有标记的话，错误报告里两个相同的数字就无法区分

以`b`加数字结尾的版本，例如`gv 1.1.0b1`，是测试版：下一个版本的测试构建，通常在Steam的测试分支上发布。之后的正式版不带这个字母（`gv 1.1.0`）。测试版保存的文件可能无法在上一个正式版中打开

> [!warning] 警告
> 在SDK另行说明之前，`sv`跟随游戏，`sv 1.0.0`并不承诺API稳定。`sv`的major变化目前说明不了针对DLL编译的代码是否兼容

## 不是版本的数字

还有两个数字看起来像“版本”，但并不是：
- `LevelMeta.LevelVersion`（键`vrs`）：作者给关卡定的版本，是`"1.0"`这样的字符串
- `BlobFormat.Generation`：`.blob`的字节布局。更多：[[3_blob-format]]

## 代：每个域一个整数

域是作为一个整体迁移的根。一共有21个：`Level`、`LevelMeta`、`UserSettings`、`Prefab`、`ThemeData`、`PublishProfile`等。其中也包括`Level`内部的部分：`LevelSettings`、`GameLevel`、`AudioLevel`、`LevelResources`、`LevelHints`。每个域把自己的代写入自己封套的`g`键

| 常量 | 值 | 含义 |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | 完全没有代 |
| `ModelGenerations.Test` | 0 | 用于检验迁移路径的`Versions/V0`脚手架 |
| `ModelGenerations.V1_AlphaRelease` | 1 | `gv 1.0.0`发布时的代，大多数域仍处于这一代 |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`、`LevelMeta`、`LevelStatistics`、`GameStatistics`以及新增的`Collection` |
| `ModelGenerations.Current` | 最新 | 界面和报告显示的代 |

**代是一个数字，而不是`major.minor`**。文件结构的变化要么需要迁移，要么不需要，没有中间档

**编号来自同一个全局计数器**。发生变化的域取`ModelGenerations.Current + 1`，而不是自己的下一个空闲编号。正因如此，版本行中唯一的`mg`才有意义

## 新的被拒绝

每次模型变化都是新的一代。结构变化、新增字段和新的枚举值都一样算。因此，高于构建所知的代，就是这个构建确定从未见过的结构

例外只有一个：任何现有模型都没有提到的全新模型，例如放在单独文件中的化身皮肤。它是一个新域，没有可以迁移的来源，所以代不增加。增加的是开始引用它的那个现有模型的代

这样的文件完全不读取：没有默认值，也没有跳过的部分。`NewerGenerationException`带有`Domain`、`FileGeneration`和`BuildGeneration`，宿主会请玩家更新

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## 旧的迁移

改变结构的域会得到：
1. 来自全局计数器的新代
2. 旧结构的冻结快照，位于`Versions/V<old>/`：一个带有`[GenerateModel]`和`[ModelGeneration(domain, <old>)]`的类
3. 位于`Versions/V<old>/Migrations/`的`ModelMigration<TFrom, TTo>`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry`通过反射找到快照和迁移器，并沿着链一直走到当前的结构。读取时每一次有损的替换都会记入`SerializationReport`，而不是悄无声息

## 读取前拒绝

`LevelMeta.MinGeneration`（键`min_generation`）是关卡各个域中最高的代。它在保存时通过`LevelGenerations.Required()`计算，从不手动填写

客户端在打开`level.json`之前比较它。这样，来自未来的关卡无需读取几兆字节的内容就会被拒绝。什么都不声明的文件存储`-1`

完整的决策记录：SDK仓库中的[VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md)
