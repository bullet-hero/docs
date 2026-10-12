---
title: バージョン管理とマイグレーション
date: 2026-10-02
tags: [developer, level_author]
---

# バージョン管理とマイグレーション

バージョンは3つあります：ゲームのgv、SDKのsv、モデルフォーマットの世代を表すmgです。SDKはmgを見て、古いファイルはマイグレーションし、ビルドより新しい世代のファイルは読み込みを拒否します

## 3つのバージョン

| ラベル | 略称の元 | 何のバージョンか | どこにあるか |
|---|---|---|---|
| `gv` | `game version` | ゲームクライアント | Unityプロジェクトの`bundleVersion` |
| `sv` | `sdk version` | ライブラリとしてのSDK。公開APIに対するセマンティックバージョニング | `SdkVersion.Value` |
| `mg` | `model generation` | モデルフォーマット。ドメインごとに1つの世代 | 各ルートの`[ModelGeneration]`、`ModelGenerations.Current` |

現在のバージョンは`gv {{v:version.gv}}`、`sv {{v:version.sv}}`、`mg {{v:version.mg}}`です

`gv`と`sv`の番号は連動しなくてもかまいませんが、ほとんどの場合は一致します。バージョンは一緒に上げられ、共通のアップデートは同じバージョンになります

それぞれの部分の意味：
- `gv`：majorは大型アップデート（ストーリー、マルチプレイヤー）、minorは通常の新機能、patchはホットフィックス
- `sv`（SDKがAPIの安定性を約束するようになってから）：majorはAPIの破壊的変更（型の削除、メンバーのシグネチャーや意味の変更）、minorは誰も対応する必要のない追加、patchはシグネチャーを変えない修正

**`mg`は他より重要です**。SDKはこれを見て、ファイルをマイグレーションするか読み込みを拒否するかを決めます

設定画面には3つすべてが、この順序でラベル付きで表示されます：`gv {{v:version.gv}}, sv {{v:version.sv}}, mg {{v:version.mg}}`。ラベルがないと、バグ報告に並んだ同じ2つの数を見分けられません

末尾に`b`と番号の付いたバージョン（たとえば`gv 1.1.0b1`）はベータ版です：次のバージョンのテスト用ビルドで、通常はSteamのベータブランチで配布されます。その後のリリースは文字なし（`gv 1.1.0`）で出ます。ベータ版で保存したファイルは、1つ前のリリースでは開けないことがあります

> [!warning] 警告
> SDKが別途表明するまで、`sv`はゲームに合わせて上がり、`sv 1.0.0`はAPIの安定性を何も約束しません。DLLに対してビルドしたコードにとって、`sv`のmajorはまだ互換性について何も示しません

## バージョンではない数

「バージョン」のように見えて、実はバージョンではない数がさらに2つあります：
- `LevelMeta.LevelVersion`（キー`vrs`）：作者が付けるレベルのバージョン。`"1.0"`のような文字列
- `BlobFormat.Generation`：`.blob`のバイトのレイアウト。詳細：[[3_blob-format]]

## 世代：ドメインごとに1つの整数

ドメインとは、1つのまとまりとしてマイグレーションされるルートのことです。全部で21個あります：`Level`、`LevelMeta`、`UserSettings`、`Prefab`、`ThemeData`、`PublishProfile`など。`Level`の中の部分も含みます：`LevelSettings`、`GameLevel`、`AudioLevel`、`LevelResources`、`LevelHints`。各ドメインは、自分のエンベロープの`g`キーに世代を書きます

| 定数 | 値 | 意味 |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | 世代がまったくない |
| `ModelGenerations.Test` | 0 | マイグレーションの経路を試す`Versions/V0`の足場 |
| `ModelGenerations.V1_AlphaRelease` | 1 | `gv 1.0.0`で出荷されたもの。ほとんどのドメインはまだこれ |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`、`LevelMeta`、`LevelStatistics`、`GameStatistics`と新しい`Collection` |
| `ModelGenerations.Current` | 最新 | インターフェースとレポートに表示されるもの |

**世代は`major.minor`ではなく1つの数です**。ファイルの形の変更は、マイグレーションが必要か不要かのどちらかです。その中間の段階はありません

**番号は1つのグローバルなカウンターから取ります**。変更されたドメインは、自分の次の空き番号ではなく`ModelGenerations.Current + 1`を受け取ります。だからこそ、バージョン文字列の1つの`mg`が意味を持ち続けます

## 新しいものは拒否する

モデルの変更はすべて新しい世代になります。形の変更も、フィールドの追加も、enumの新しい値も同じ扱いです。そのため、ビルドが知っているより大きい世代は、ビルドが確実に見たことのない形です

例外が1つあります：既存のどのモデルからも参照されないまったく新しいモデル、たとえば別ファイルのアバタースキンです。マイグレーション元のない新しいドメインなので、世代は上がりません。上がるのは、それを参照し始めた既存のモデルの世代です

ビルドより新しい世代のファイルは一切読み込まれません：デフォルト値で埋めることも、一部を飛ばすこともしません。`NewerGenerationException`は`Domain`、`FileGeneration`、`BuildGeneration`を持ち、ホストはプレイヤーにアップデートを求めます

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## 古いものはマイグレーションする

形が変わるドメインには、次のものが加わります：
1. グローバルなカウンターからの新しい世代
2. `Versions/V<old>/`に置く古い形の凍結スナップショット：`[GenerateModel]`と`[ModelGeneration(domain, <old>)]`の付いたクラス
3. `Versions/V<old>/Migrations/`に置く`ModelMigration<TFrom, TTo>`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry`はリフレクションでスナップショットとマイグレーターを見つけ、今日の形までチェーンをたどります。読み込み中に情報が失われる置き換えはすべて、黙って捨てられずに`SerializationReport`に記録されます

## 読み込み前の拒否

`LevelMeta.MinGeneration`（キー`min_generation`）は、レベルのドメインの中で最も大きい世代です。保存時に`LevelGenerations.Required()`で計算され、手で入力することはありません

クライアントは`level.json`を開く前にこれを比較します。そのため、未来から来たレベルは、何MBもある内容を読まずに拒否されます。何も宣言していないファイルには`-1`が保存されます

判断の記録の全文：SDKリポジトリの[VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md)
