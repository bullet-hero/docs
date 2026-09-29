---
title: 版本与迁移
date: 2026-09-24
tags: [developer, level_author]
---

# 版本与迁移

哪个数字给什么定版本，旧文件如何迁移，以及为什么拒绝读取来自更新构建的文件

## 三种版本

| 标记 | 全称 | 给什么定版本 | 存放位置 |
|---|---|---|---|
| `gv` | `game version` | 游戏客户端 | Unity项目的`bundleVersion` |
| `sv` | `sdk version` | 作为库的SDK，按其公开API遵循semver | `SdkVersion.Value` |
| `mg` | `model generation` | 模型格式，每个域一个代 | 每个根上的`[ModelGeneration]`，`ModelGenerations.Current` |

当前版本：`gv 1.0.0`、`sv 1.0.0`、`mg 1`

`gv`和`sv`的数字不必互相跟随，但大多数情况下是一致的。版本会一起提升，共同的更新使用同一个版本号

各部分的含义：
- `gv`：major是全局更新（剧情、多人游戏），minor是普通功能，patch是紧急修复
- `sv`，在SDK承诺API稳定之后：major是破坏性的API变更（删除类型，或改变签名或成员的含义），minor是无需任何人应对的新增，patch是不改变任何签名的修复

**`mg`比其他两个更重要**。SDK根据它决定是迁移文件还是拒绝读取

设置界面按这个顺序并带标记显示全部三个：`gv 1.0.0, sv 1.0.0, mg 1`。没有标记的话，错误报告里两个相同的数字就无法区分

以`b`加数字结尾的版本，例如`gv 1.1.0b1`，是测试版：下一个版本的测试构建，通常在Steam的测试分支上发布。之后的正式版去掉这个字母（`gv 1.1.0`）。测试版保存的文件可能无法在之前的正式版中打开

> [!warning] 警告
> 在SDK另行说明之前，`sv`跟随游戏，1.0.0并不承诺API稳定。`sv`的major变化目前也说明不了针对DLL编译的代码是否兼容

## 不是版本的数字

还有两个数字看起来像“版本”，但并不是：
- `LevelMeta.LevelVersion`（键`vrs`）：作者给关卡定的版本，是`"1.0"`这样的字符串
- `BlobFormat.Generation`：`.blob`的字节布局。更多：[[3_blob-format]]

## 代：每个域一个整数

域是作为一个整体迁移的根。一共有20个：`Level`、`LevelMeta`、`UserSettings`、`Prefab`、`ThemeData`、`PublishProfile`等。其中包括嵌套在`Level`内部的部分：`LevelSettings`、`GameLevel`、`AudioLevel`、`LevelResources`、`LevelHints`。每个域把自己的代写入封套的`g`键

| 常量 | 值 | 含义 |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | 完全没有代 |
| `ModelGenerations.Test` | 0 | 用于演练迁移路径的`Versions/V0`脚手架 |
| `ModelGenerations.Release` | 1 | 游戏目前写入的代，所有域都处于这一代 |
| `ModelGenerations.Current` | 最新 | 界面和报告显示的代 |

**代是一个数字，而不是`major.minor`**。文件结构的变化要么需要迁移，要么不需要，没有中间档

**代的编号来自同一个全局计数器**。发生变化的域取`ModelGenerations.Current + 1`，而不是自己的下一个空闲编号。正因如此，版本行中唯一的`mg`才有意义

## 更新的代被拒绝

每次模型变化都是新的一代。结构变化、新增成员和新的枚举值都一样算。因此，高于当前构建所知的代，就是这个构建确定从未见过的结构

一个例外：一个全新的、现有模型都没有提到的模型，例如单独存放在自己文件中的化身皮肤。它是一个新域，没有可迁移的来源，所以没有代发生变化。发生变化的是开始引用它的那个现有模型的代

这样的文件完全不读取：不填默认值，也不跳过部分内容。`NewerGenerationException`带有`Domain`、`FileGeneration`和`BuildGeneration`，宿主会请玩家更新

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## 更旧的代会迁移

结构发生变化的域会得到：
1. 来自全局计数器的新代
2. 放在`Versions/V<old>/`下的旧结构冻结快照：一个带`[ModelGeneration(domain, <old>)]`的`[GenerateModel]`类
3. 放在`Versions/V<old>/Migrations/`下的`ModelMigration<TFrom, TTo>`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry`通过反射找到快照和迁移器，并沿着链一路迁移到当前的结构。有损读取所做的每一次替换都记入`SerializationReport`，绝不悄无声息

## 读取前就拒绝

`LevelMeta.MinGeneration`（键`min_generation`）是关卡中所有域用到的最高代。它在保存时由`LevelGenerations.Required()`计算，从不手动填写

客户端在打开`level.json`之前先比较它。这样来自未来的关卡不用读取几兆字节的内容就能被拒绝。没有声明的文件在这里存`-1`

完整的设计记录是SDK仓库中的[VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md)
