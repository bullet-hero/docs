---
title: ジェネレーターの書き方
date: 2026-10-02
tags: [developer]
---

# ジェネレーターの書き方

ジェネレーターは、SDKの基底クラスBaseLevelGenerator、BaseContentGenerator、BaseModifierのいずれかを継承した1つのクラスです。フォーム、見積もり、元に戻す処理は、ホストが契約から自動で作ります

ジェネレーターは、いくつかのパラメーターからレベルの内容を生成します。作者がすべてのオブジェクトを手で配置する必要はありません

ジェネレーター用のインターフェースを書く人はおらず、一覧を編集することもありません

組み込みジェネレーターができること：[[8_generators]]

## 3つの種類

| 種類 | 作成するもの | 基底クラス | エントリーポイント |
|---|---|---|---|
| `Level` | 新しい`Level`と`LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | アクティブなスコープ内の新しいオブジェクトとリソース | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | すでに存在するオブジェクトの編集 | `BaseModifier<TParams>` | `Run(context, parameters)` |

ContentとModifierはエントリーポイントが同じです。違うのは意図と`GeneratorRequirements`です。モディファイアーはデフォルトで選択を必要とします

オブジェクトを作成するジェネレーター向けには`BaseSpawnGenerator<TParams>`があります。これがすべてのオブジェクトを作成し、親を設定し、時間上に配置します。具体的なクラスに残るのは配置の計算だけです

## レジストリなし

`GeneratorRegistry`は、最初のアクセス時にリフレクションですべてのジェネレーターを見つけます。同じ`NameKey`を持つジェネレーターが2つあると、その時点で失敗します

スキャンされるのはSDK自身のアセンブリだけです。そのため、新しいジェネレーターはSDKリポジトリに置き、プルリクエストとして届けます。詳細：[[9_contributing-sdk]]

## 例

オブジェクトを1列に並べるジェネレーターです。組み込みの`RadialGenerator`と同じクラスの上に作っています：

```csharp
using BH.SDK.Generators;
using BH.SDK.Generators.Spawn;
using BH.SDK.Rules;

public class RowGenerator : BaseSpawnGenerator<RowGenerator.Parameters>
{
    public override string NameKey => "gen_geometry_row";

    public override GeneratorHints Hints { get; } = new GeneratorHints.Builder()
        .Section(GeneratorSections.Main, SpawnParameters.MainFields)
        .Section(GeneratorSections.Main, nameof(Parameters.Count), nameof(Parameters.Spacing))
        .Section(GeneratorSections.Additional, SpawnParameters.AdditionalFields)
        .Section(GeneratorSections.Additional, nameof(Parameters.StartX), nameof(Parameters.Y))
        .Range(nameof(Parameters.Count), 1, 256)
        .Range(nameof(Parameters.Spacing), 0f, ValueRules.MaxPos)
        .Range(nameof(Parameters.StartX), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(Parameters.Y), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(SpawnParameters.Size), ValueRules.MinSca, ValueRules.MaxSca)
        .Build();

    protected override void Generate(GeneratorContext context, Parameters parameters)
    {
        for (var i = 0; i < parameters.Count; i++)
        {
            var obj = Spawn(context, parameters, $"row_{i}", context.Span);
            AddPosition(obj, parameters.StartX + i * parameters.Spacing, parameters.Y, obj.Span.StartFrame);
        }
    }

    // Spawn adds a size key and a color key, AddPosition adds the third
    protected override GeneratorCost EstimateTyped(GeneratorContext context, Parameters parameters)
        => new GeneratorCost(parameters.Count, parameters.Count * 3);

    public class Parameters : SpawnParameters
    {
        public int Count = 8;
        public float Spacing = 2f;
        public float StartX;
        public float Y;
    }
}
```

`NameKey`はローカライズキーの形をしています。ホストは自分の文字列テーブルを通じて名前を表示します

## 必須のルール

- **レベルの変更は必ず`GeneratorContext`を通じて行います**（`Create`、`Edit`、`Delete`、`SetValue`など）。これがすべての変更を`GeneratorChangeLog`に記録し、元に戻す機能はすべてそれに依存しています。モデルを直接変更してもコンパイルは通りますが、元に戻す機能が黙って壊れます
- **すべてのフィールドをセクションに載せ、すべての数値に`Range`を付けます**。リフレクションによるフィールドの順序は保証されません。範囲のない数値では、ホストがクランプする基準がありません。範囲はテストでチェックされます
- **パラメーターはpublicで変更可能なフィールドとし、引数なしのコンストラクターを持たせます**。フォームはそれにバインドし、プリセットはそれをシリアライズします。継承したフィールドを隠さないでください：すべてがフィールド名で指定されます
- **見積もりは実行と一致させます**。ホストは実行前に見積もりを表示します。実行が`LevelRules.MaxObjects`を超えるなら、ホストは拒否します
- **ランダム性は`System.Random`ではなく`context.CreateRandom()`から得ます**。同じシードなら、どのプラットフォームでも同じレベルになります
- **作成したものの親は`context.Parent`にします**。ホストはそうやって1回の実行全体を1つのオブジェクトにまとめます
- `context.Game`や`context.Audio`に触れるなら、**`GeneratorRequirements.LevelScope`を宣言します**。アクティブなスコープがプレハブの間は、どちらも`null`です
- パラメーターの組み合わせによって、作者が見ている範囲の外の内容を削除したり書き換えたりするなら、**`IsDangerousTyped`をオーバーライドします**。そうすればホストが確認を求めます

## 外部データ

SDKには、オーディオデコーダーも、FFTも、画像ローダーもありません。そうしたデータが必要なジェネレーターは：
1. `GeneratorRequirements.ExternalAnalysis`を宣言します
2. `External/`のインターフェースを実装します：`IWaveformInput`、`IBeatFramesInput`、`IPixelTextureInput`など

ホストは実行前にデータを渡します。何も渡されなかったら、ジェネレーターは何も作成してはいけません

契約の全文：[Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
