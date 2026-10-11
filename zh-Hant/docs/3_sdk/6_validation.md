---
title: 校驗
date: 2026-10-01
tags: [developer, level_author]
---

# 校驗

校驗由你自己通過ValidationFacade呼叫，它沒有內建在儲存和載入中。問題分為Error、Warning和Advice，ValidateAndFix會修復能修復的部分

在哪裡執行校驗由遊戲決定。在編輯器中開啟關卡會報告問題，而遊玩時跳過檢查。所以等待校驗的是作者，玩家從不需要等待

關卡作者在把關卡提交給某個服務時會遇到校驗。更多：[[7_publish-profiles]]

## 如何呼叫

`ValidationFacade`是唯一的入口。呼叫方無需知道一共有幾遍檢查：

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| 方法 | 作用 |
|---|---|
| `Validate(root, settings)` | 檢查任何根：`Level`、`LevelMeta`、`UserSettings`、單獨的`Prefab`或`EffectData`。只有對`Level`才執行圖檢查 |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | 修復能修復的部分，並報告剩下的問題 |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | 同時執行全部三遍檢查，不修復任何東西。`level`可以是`null`，此時只評估後設資料 |

`ValidationReport`包含`RuleIssues`和`GraphIssues`：
- `IsValid`：完全沒有問題
- `HasErrors`：至少有一個`Error`組的問題

## 嚴重程度

每條規則都屬於一個`RuleGroup`：
- `Error`：檔案按寫入的樣子無法遊玩
- `Warning`：可以遊玩，但與預期不符（永遠不會出現的內容、有備用方案的失效引用）。或者唯一的修復是破壞性的
- `Advice`：遊玩效果不變

## 三遍檢查

| 檢查 | 問什麼 | 作用於 |
|---|---|---|
| `RuleAnalyzer` | 每個值是否在其範圍內、不為`null`、是已知的列舉成員 | 任何根 |
| `LevelGraphAnalyzer` | 物體之間是否相互一致 | 僅`Level` |
| `PublishReadinessAnalyzer` | 能否按給定的配置把關卡交給陌生人 | `LevelMeta`，可選`Level` |

## 規則

型別通過`[RuleContainer]`標記納入檢查。它的屬性帶有規則特性：
- `[RuleNotNull]`、`[RuleInRange]`、`[RuleMinValue]`、`[RuleEnumValid]`、`[RuleCollectionMaxCount]`等
- `[RuleEnumFlagsValid]`：用於標誌列舉
- `[RuleOptional]`：用於可以缺失的欄位

限制本身是`Rules/`表中的常量：`FrameRules`、`ValueRules`、`LevelRules`等。例如，`LevelRules.MaxObjects`等於262144

對所有規則容器的遍歷由`BH.SDK.Roslyn`生成，不使用反射。在大型關卡上，這讓遍歷時間大約減半

## 修復

每個規則特性都能修復自己的值（`Fix`）。`RuleFixer`按跟蹤路徑的逆序應用修復：一次修復可能移動更深層的問題。`ValidateAndFix`會重複檢查，直到結果不再變化

圖檢查在修復之後進行。修復本身可能在圖中製造問題，例如新ID與已有ID重複

**圖問題從不修復**：`DuplicateObjectId`、`MissingParent`、`ParentCycle`、`PrefabRemapBroken`、`IdCounterNearExhaustion`等。每一次這樣的修復都是關於內容的決定（兩個物體中哪個保留自己的ID）。靠猜測會改寫關卡

> [!caution] 注意
> `ValidateAndFix`會修改你傳入的物件。如果需要保留原件，請在副本上執行，例如為了向作者展示具體改了什麼
