---
title: 校验
date: 2026-10-01
tags: [developer, level_author]
---

# 校验

校验由你自己通过ValidationFacade调用，它没有内置在保存和加载中。问题分为Error、Warning和Advice，ValidateAndFix会修复能修复的部分

在哪里运行校验由游戏决定。在编辑器中打开关卡会报告问题，而游玩时跳过检查。所以等待校验的是作者，玩家从不需要等待

关卡作者在把关卡提交给某个服务时会遇到校验。更多：[[7_publish-profiles]]

## 如何调用

`ValidationFacade`是唯一的入口。调用方无需知道一共有几遍检查：

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| 方法 | 作用 |
|---|---|
| `Validate(root, settings)` | 检查任何根：`Level`、`LevelMeta`、`UserSettings`、单独的`Prefab`或`EffectData`。只有对`Level`才运行图检查 |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | 修复能修复的部分，并报告剩下的问题 |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | 同时执行全部三遍检查，不修复任何东西。`level`可以是`null`，此时只评估元数据 |

`ValidationReport`包含`RuleIssues`和`GraphIssues`：
- `IsValid`：完全没有问题
- `HasErrors`：至少有一个`Error`组的问题

## 严重程度

每条规则都属于一个`RuleGroup`：
- `Error`：文件按写入的样子无法游玩
- `Warning`：可以游玩，但与预期不符（永远不会出现的内容、有备用方案的失效引用）。或者唯一的修复是破坏性的
- `Advice`：游玩效果不变

## 三遍检查

| 检查 | 问什么 | 作用于 |
|---|---|---|
| `RuleAnalyzer` | 每个值是否在其范围内、不为`null`、是已知的枚举成员 | 任何根 |
| `LevelGraphAnalyzer` | 物体之间是否相互一致 | 仅`Level` |
| `PublishReadinessAnalyzer` | 能否按给定的配置把关卡交给陌生人 | `LevelMeta`，可选`Level` |

## 规则

类型通过`[RuleContainer]`标记纳入检查。它的属性带有规则特性：
- `[RuleNotNull]`、`[RuleInRange]`、`[RuleMinValue]`、`[RuleEnumValid]`、`[RuleCollectionMaxCount]`等
- `[RuleEnumFlagsValid]`：用于标志枚举
- `[RuleOptional]`：用于可以缺失的字段

限制本身是`Rules/`表中的常量：`FrameRules`、`ValueRules`、`LevelRules`等。例如，`LevelRules.MaxObjects`等于262144

对所有规则容器的遍历由`BH.SDK.Roslyn`生成，不使用反射。在大型关卡上，这让遍历时间大约减半

## 修复

每个规则特性都能修复自己的值（`Fix`）。`RuleFixer`按跟踪路径的逆序应用修复：一次修复可能移动更深层的问题。`ValidateAndFix`会重复检查，直到结果不再变化

图检查在修复之后进行。修复本身可能在图中制造问题，例如新ID与已有ID重复

**图问题从不修复**：`DuplicateObjectId`、`MissingParent`、`ParentCycle`、`PrefabRemapBroken`、`IdCounterNearExhaustion`等。每一次这样的修复都是关于内容的决定（两个物体中哪个保留自己的ID）。靠猜测会改写关卡

> [!caution] 注意
> `ValidateAndFix`会修改你传入的对象。如果需要保留原件，请在副本上运行，例如为了向作者展示具体改了什么
