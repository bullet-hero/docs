---
title: インストール
date: 2026-10-02
tags: [developer, level_author]
---

# インストール

SDKはnuget.orgのBulletHero.SDKパッケージとして入手するか、ソースからビルドします。Unityにはgit submoduleとして組み込み、ConsoleSmokeサンプルで手元のレベルが読めることを確認できます

SDKのコードは[github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk)にあります。ライセンスはMITです

## .NET

`BulletHero.SDK`パッケージはnuget.orgで公開されています：`dotnet add package BulletHero.SDK`。3つの依存パッケージも一緒に入ります。ソースからビルドする場合は次のとおりです：

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

続いて、次のどちらかを参照に追加します：
- ローカルフォルダーの`.nupkg`：`dotnet add package BulletHero.SDK --source <folder>`。3つの依存パッケージも一緒に入ります
- `BH.SDK.dll`を直接。この場合、下の3つのパッケージは自分で追加します。DLLへの参照は、その依存パッケージを連れてきません

依存パッケージ（すべてNuGetから）：

| パッケージ | バージョン | 用途 |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | パスワード保護されたレベル用のOpenPGP |
| `SharpZipLib` | 1.4.2 | tarとzip（gzipはBCLのものを使用） |

### ビルドの詳細

- アセンブリは`BH.SDK.dll`で、XMLドキュメントがその隣に置かれます
- ターゲットは`netstandard2.1`、言語はC# 9です。Unityプロジェクトと同じ値なので、同じソースがUnityの中でも外でもビルドできます
- 出力フォルダーは`bin~`と`obj~`です。チルダが必要なのは、名前がチルダで終わるフォルダーをUnityがインポートしないためです

## Unity

ゲームはSDKをgit submoduleとして組み込んでいます：

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

削除は`git rm -r -f Assets/Plugins/BH.SDK`です

Unityプロジェクト側で用意するもの：
- `com.unity.nuget.newtonsoft-json`パッケージ経由の`Newtonsoft.Json`
- NuGetからの`BouncyCastle.Cryptography`と`SharpZipLib`（ゲームはNuGetForUnityでインストールしています）
- Player Settingsのスクリプトシンボル`BHSDK_UNITY`。これがないと、`UnityIntegration`はエンジンを使わない分岐を選びます
- SDKのルートにある`BH.SDK.Roslyn.dll`。Unityはアナライザーを、それが置かれたフォルダーのアセンブリと、そのアセンブリを参照するアセンブリにだけ適用します。別の場所に移すと何も解析しません

リポジトリのルートには、名前が`com.vertoker.bullet-hero-sdk`、Unityの最小バージョンが`6000.0`の`package.json`があります。そのためPackage ManagerからgitのURLでSDKを追加することもできます。この方法は使われておらず、ここでは説明しません

## 確認：ConsoleSmokeサンプル

`Samples~/ConsoleSmoke`は`net8.0`のコンソールアプリケーションです。サードパーティーのツールとまったく同じように、ビルド済みの`BH.SDK.dll`を参照します。アプリケーションはレベルフォルダーを読み込み、名前、オブジェクト数、世代を出力します。続いて、レベルをJSONと`.blob`でそれぞれ往復変換します

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| 終了コード | 意味 |
|---|---|
| 0 | すべて一致した |
| 1 | 引数が正しくない |
| 2 | `level.*`または`metadata.*`が見つからない |
| 3 | 往復変換の結果が一致しなかった |
| 4 | ファイルがこのSDKより新しい |

ゲームの組み込みレベル`new-zero-demo`での出力（`sv 1.0.0`で記録）：

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

次へ：[[2_level-format]]

## SDKの構成

| 部分 | 内容 | Unityが必要か |
|---|---|---|
| `BH.SDK` | コア：モデル、シリアライズ、バージョン、ルール、検証、アーカイブ、公開、ジェネレーター | いいえ |
| `UnityIntegration` | すべてのファイルがUnityありでもなしでもコンパイルされる薄い層（`#if BHSDK_UNITY`）。たとえば`Cat`ロガー | いいえ：Unityの外ではコアに直接コンパイルされる |
| `UnityExtensions` | Unityの型への変換、2Dトランスフォーム、アバターの移動 | はい、常に |
| `BH.SDK.Roslyn` | アナライザーとソースジェネレーター。`[GenerateModel]`の付いたモデルごとに、`Equals`、コピー、JSONと`.blob`のコーデック、検証の走査を書き出す | コンパイル時に動作 |

モデルのファイルには、フィールドとコンストラクターだけが書かれています。繰り返しになる部分はすべてジェネレーターが書きます。そのため、生成される7つの本体のどれかでフィールドを書き忘れることがありません

## 独立したライブラリにした理由

- **レベルはゲームより長く残ります**。レベルはオープンなフォーマット（JSON、tar.gz、zip、OpenPGP）のファイルが入ったフォルダーです。それを読むコードもオープンです。書き出したゲームがなくなっても、レベルは読めるまま残ります
- **他のリズムゲームとの連携**。フォーマットが公開されているので、他のゲームとの相互変換ツールをそれに基づいて書けます
- **素早い修正**。フォーマットの欠陥は外から見えます。コードを読んだ人なら誰でも、報告したり修正を送ったりできます
- **サードパーティーのツール**。コンバーター、バリデーター、レベルジェネレーター、MODは、ゲームと同じモデルで動きます。ファイルからモデルを再構築する必要はありません
- **サーバー**。コアはUnityなしで`netstandard2.1`としてビルドされます。そのため、サーバーはクライアントと同じモデルに対して同じチェックを実行します
