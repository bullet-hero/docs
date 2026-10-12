---
title: 検証
date: 2026-10-01
tags: [developer, level_author]
---

# 検証

検証はValidationFacadeを通じて自分で呼び出すもので、保存や読み込みには組み込まれていません。問題はError、Warning、Adviceに分かれ、ValidateAndFixは直せるものを修正します

どこで実行するかはゲームが決めます。エディターでレベルを開くと問題が報告されますが、プレイ時にはチェックを省きます。つまり、検証を待つのは作者で、プレイヤーが待つことはありません

レベルの作者が検証に出会うのは、レベルをサービスに提出するときです。詳細：[[7_publish-profiles]]

## 呼び出し方

`ValidationFacade`が唯一の入り口です。呼び出し側は、パスがいくつあるかを知る必要はありません：

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| メソッド | 何をするか |
|---|---|
| `Validate(root, settings)` | 任意のルートをチェックする：`Level`、`LevelMeta`、`UserSettings`、単体の`Prefab`や`EffectData`。グラフのパスは`Level`の場合だけ実行される |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | 直せるものを修正し、残ったものを報告する |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | 3つのパスを一度に実行し、何も修正しない。メタデータだけを評価するなら`level`は`null`でよい |

`ValidationReport`は`RuleIssues`と`GraphIssues`を持ちます：
- `IsValid`：問題がまったくない
- `HasErrors`：`Error`グループの問題が少なくとも1つある

## 重大度

ルールはそれぞれ`RuleGroup`に属します：
- `Error`：書かれたとおりにはファイルをプレイできない
- `Warning`：プレイはできるが、意図どおりにならない（決して現れない内容、フォールバックのある壊れた参照）。または、唯一の修正方法が破壊的
- `Advice`：プレイには影響しない

## 3つのパス

| パス | 何を確かめるか | 対象 |
|---|---|---|
| `RuleAnalyzer` | すべての値が範囲内にあり、`null`でなく、既知のenumメンバーか | 任意のルート |
| `LevelGraphAnalyzer` | オブジェクト同士が矛盾していないか | `Level`のみ |
| `PublishReadinessAnalyzer` | 指定したプロファイルのもとで、レベルを見知らぬ人に渡せるか | `LevelMeta`、任意で`Level` |

## ルール

型は`[RuleContainer]`マーカーによってチェックの対象になります。そのプロパティにルールの属性を付けます：
- `[RuleNotNull]`、`[RuleInRange]`、`[RuleMinValue]`、`[RuleEnumValid]`、`[RuleCollectionMaxCount]`など
- `[RuleEnumFlagsValid]`：フラグのenum用
- `[RuleOptional]`：なくてもよいフィールド用

制限値そのものは、`Rules/`のテーブルにある定数です：`FrameRules`、`ValueRules`、`LevelRules`など。たとえば`LevelRules.MaxObjects`は262,144です

すべてのルールコンテナーの走査は、リフレクションを使わずに`BH.SDK.Roslyn`が生成します。大きなレベルでは、これで所要時間がおよそ半分になります

## 修正

ルールの属性はどれも、自分の値を修正できます（`Fix`）。`RuleFixer`は修正をトレースの逆順に適用します。修正によって、より深い場所の問題がずれることがあるからです。`ValidateAndFix`は、結果が変わらなくなるまでパスを繰り返します

グラフのパスは修正の後に実行されます。修正そのものがグラフに問題を生むことがあるからです。たとえば、新しいIDが既存のIDと重なる場合です

**グラフの問題は決して修正されません**：`DuplicateObjectId`、`MissingParent`、`ParentCycle`、`PrefabRemapBroken`、`IdCounterNearExhaustion`など。こうした修正はどれも、内容についての判断（2つのオブジェクトのどちらがIDを残すか）になります。推測で直すとレベルを書き換えてしまいます

> [!caution] 注意
> `ValidateAndFix`は渡したオブジェクトを変更します。元の状態が必要なら（たとえば何が変わったかを作者に正確に見せるため）、コピーに対して実行してください
