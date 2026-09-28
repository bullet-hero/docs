---
title: 校验
date: 2026-09-24
tags: [developer, level_author]
---

# 校验

SDK如何按格式规则检查关卡，修复能修复的问题，并报告无法修复的问题

校验由你自己调用。它没有内置在保存或加载中

在哪里运行校验由游戏决定。在编辑器中打开关卡时会报告问题，播放时则跳过检查。所以作者需要等待校验，玩家从不需要

关卡作者在把关卡提交给某个服务时会遇到校验。更多：[[7_publish-profiles]]

## 如何调用

`ValidationFacade`是唯一的入口。调用方不需要知道有几遍检查：

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| 方法 | 作用 |
|---|---|
| `Validate(root, settings)` | 检查任意根：`Level`、`LevelMeta`、`UserSettings`、独立的`Prefab`或`EffectData`。图检查只对`Level`运行 |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | 修复能修复的内容，然后报告剩下的问题 |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | 一次运行全部三遍检查，不做任何修复。`level`可以为`null`，只评估元数据 |

`ValidationReport`包含`RuleIssues`和`GraphIssues`：
- `IsValid`：完全没有问题
- `HasErrors`：至少有一个`Error`组的问题

## 严重程度

每条规则都属于一个`RuleGroup`：
- `Error`：文件无法按原样播放
- `Warning`：可以播放，但与作者的设计不符（永远不会出现的内容、损坏的引用改用了后备值）。或者唯一的修复方式具有破坏性
- `Advice`：播放不受影响

## 三遍检查

| 检查 | 检查什么 | 适用对象 |
|---|---|---|
| `RuleAnalyzer` | 每个值是否在范围内、不为`null`、是已知的枚举成员 | 任意根 |
| `LevelGraphAnalyzer` | 物体之间是否彼此一致 | 仅`Level` |
| `PublishReadinessAnalyzer` | 在给定的发布配置下，关卡能否交给陌生人 | `LevelMeta`，可选`Level` |

## 规则

类型通过`[RuleContainer]`标记加入检查。它的属性带有规则特性：
- `[RuleNotNull]`、`[RuleInRange]`、`[RuleMinValue]`、`[RuleEnumValid]`、`[RuleCollectionMaxCount]`等
- `[RuleEnumFlagsValid]`：用于标志枚举
- `[RuleOptional]`：用于可以缺省的成员

限制值本身是`Rules/`表中的常量：`FrameRules`、`ValueRules`、`LevelRules`等。例如`LevelRules.MaxObjects`为262144

对所有规则容器的遍历由`BH.SDK.Roslyn`生成，不使用反射。这让它在大型关卡上的耗时大约减半

## 修复器

每个规则特性都知道如何修复自己的值（`Fix`）。`RuleFixer`按追踪的逆序应用修复：一次修复可能改变更深层的问题。`ValidateAndFix`会重复检查，直到结果不再变化

图检查在修复之后运行。修复本身也可能造成图的问题，例如新ID与已有ID冲突

**图检查的问题从不修复**：`DuplicateObjectId`、`MissingParent`、`ParentCycle`、`PrefabRemapBroken`、`IdCounterNearExhaustion`等。这类修复都是内容上的决定（两个物体中哪个保留ID）。靠猜测会改写关卡

> [!caution] 注意
> `ValidateAndFix`会修改你传入的对象。需要保留原始版本时，请在副本上运行，例如要向作者展示究竟改了什么
