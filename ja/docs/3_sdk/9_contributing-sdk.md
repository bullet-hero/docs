---
title: SDKへの貢献
date: 2026-10-02
tags: [developer]
---

# SDKへの貢献

SDKの問題はbullet-hero/sdkリポジトリのIssueに報告し、コードの変更はプルリクエストとして同じリポジトリに送ってください。コントリビューター向けのルールも、同じリポジトリのコードの隣にあります

リポジトリは[bullet-hero/sdk](https://github.com/bullet-hero/sdk)で、デフォルトブランチは`master`です

## 報告先

| 内容 | 報告先 |
|---|---|
| SDKとそのコード | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| ゲーム：プレイヤーのバグと要望 | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| ドキュメントの文章 | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## ルールの場所

コントリビューター向けのルールは、SDKリポジトリそのものの中で、説明対象のコードの隣にあります：

| ファイル | 内容 |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | 依存パッケージ、レベルパッケージ、DLLとパッケージのビルド、確認用サンプル |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | メンタルモデル、フォルダーの索引、ライブラリ全体の規約 |
| 各フォルダーの`CLAUDE.md` | そのフォルダー固有のルール。たとえば[Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md)、[Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md)、[Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | バージョンの軸、世代、マイグレーションと拒否 |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | モデルがエンティティをどう指定するか：Guid、int、フレーム、フィールドパス |
| [[ugc-licensing-policy]]（このサイト内） | ユーザーコンテンツのライセンスポリシー。`TrustedSourceCatalog`と一緒に編集される |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | スナップショットとマイグレーターの書き方 |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | ジェネレーターの契約 |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | アナライザーとモデルジェネレーター、そのリビルド方法 |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | 二重コンパイルの契約 |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | `sv`のバージョンごとの変更。新しいものが上 |

## ビルドとテスト

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- ここでは、Unityがコンパイルするのと同じソースをUnityなしでビルドします。エンジン非依存の契約を破るファイルがあると、このビルドが壊れます
- 出力先は`bin~`と`obj~`です
- packコマンドは`.nupkg`を作るだけです。nuget.orgへの公開は、`sv`タグがプッシュされたときにリポジトリの`release`ワークフローが行います

> [!caution] 注意
> アナライザーとモデルジェネレーターは、SDKのルートにあるビルド済みの`BH.SDK.Roslyn.dll`として同梱されています。`Roslyn/`の中を編集したら、これをリビルドして上書きコピーしてください。そうしないと、ソースが変わっていても古いジェネレーターが動き続けます

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Unityエディター内では、メニュー項目**Tools > BH.SDK.Roslyn > Build Analyzer**で同じことができます

## 前もって知っておくべき不変条件

- コアは`UnityEngine`の型を1つも参照しません。エンジンが必要なコードは、`UnityExtensions/`に置くか、エンジンなしの分岐を用意したうえで`#if BHSDK_UNITY`の内側として`UnityIntegration/`に置きます
- コードはファイルでもメモリ上のデータでも同じように動き、非同期処理はBCLのものだけを使います
- `netstandard2.1`とC# 9は、Unityプロジェクトがコンパイルに使う値です。引き上げることはありません
- モデルは`[GenerateModel] public sealed partial class`です。シリアライズされるフィールドはすべて、キーを`Names.cs`から取ります
- モデルの変更はどれも、スナップショットとマイグレーターを伴う新しい世代になります。詳細：[[5_versioning]]
- SDKのバージョンは3か所にあります：`SdkVersion.cs`、`package.json`、`BH.SDK.csproj`の`<Version>`。どれか1つだけが変わると`SdkVersionAgreementTests`が失敗します
