---
title: 公開プロファイル
date: 2026-10-01
tags: [developer, level_author]
---

# 公開プロファイル

サービスは、受け付けるレベルの条件をPublishProfileファイルで記述します：ライセンス、リソースの入手元、必須フィールド、サイズの上限。サービスを追加するにはファイルを書けばよく、アナライザーを編集する必要はありません

## プロファイルはデータ

公開プロファイル（`PublishProfile`）は、他のルートと同じようにシリアライズされるモデルで、自分の世代を持ちます

レベルの行き先には、Steamワークショップ、公式サーバー、コミュニティサーバー、ストア版ビルドのカタログがあります。どの行き先も、同じ質問にそれぞれの答えを出します。答えは年月とともに変わりますが、コードは変わりません

プロファイルが決めること：

| フィールド | 意味 |
|---|---|
| `ProfileKey` | どのサービスか。すべてのレポートに繰り返し記載される |
| `AllowedLicenses` | サービスが受け付ける`TypicalLicenseType`の値 |
| `AllowedUriTypes` | リソースの取得方法。空のリストはどの方法でもよいという意味 |
| `AllowUnknownLicense`、`AllowPermissionInstead` | 不明なライセンスや書面の許可で足りるか |
| `RequireResourceMeta`、`RequireResourceUrl`、`RequireAttribution`、`RequireAgeRating`、`RequireLevelAuthors`、`RequireHashes` | 入力が必須の項目 |
| `MaxResourceBytes`、`MaxDataFileBytes`、`MaxTotalBytes` | サイズの上限。0は無制限 |
| `Sources`、`UnknownSourceTrust` | サイトの一覧と、一覧にないサイトの評価 |

許容できるライセンスを決めるのはプロファイルだけです。ライセンスの性質のように見えますが、実際には受け取る側のサービスの性質です

## 4つの組み込みプロファイル

| ファクトリー | `ProfileKey` | 用途 |
|---|---|---|
| `CreateOpen()` | `local` | デバイス上のレベル。何も必須ではない |
| `CreateStandard()` | `standard` | 公開サーバー |
| `CreateWorkshop()` | `workshop` | Steamワークショップ。CC BYの派生はどれも通り、書類の不足は警告だけ |
| `CreateStrict()` | `strict` | ストア版ビルド。`standard`より厳しい |

| 項目 | `standard` | `strict` |
|---|---|---|
| ライセンス | CC0 1.0、CC BY 4.0と3.0、CC BY-NC 4.0と3.0、SIL OFL 1.1、MIT、Apache 2.0、Unlicense | `standard`と同じ |
| リソースの入手元 | レベルフォルダー、ゲーム、または直接リンク | リンクは不可 |
| 作者表示とハッシュ | - | 必須 |
| リソースあたりの上限 | 64 MiB | 32 MiB |
| データファイルあたりの上限 | 32 MiB | 16 MiB |
| レベルあたりの上限 | 256 MiB | 128 MiB |

> [!tip] 推奨
> 自分のサービス用にファクトリーを追加するのではなく、4つのプロファイルのどれかを元に必要なフィールドを変更し、JSONファイルとして配布することをおすすめします

### これらのライセンスとサイズにした理由

- GPL系のライセンスは`standard`から除外されています。App Storeで配布されるGPLの作品は、Appleの規約と衝突します
- CC BY-SAは除外されています：ShareAlikeにより、レベル自体のライセンスの変更を強いられるためです
- CC BY-NDは除外されています：NoDerivativesは、ゲームの土台である編集を禁じるためです
- strictのサイズは、スマートフォンがモバイル回線でダウンロードできる量です

## リソースの入手元

ライセンスのフィールドは、作者が何を主張しているかを示します。`SourceTrust`は、リソースの入手元のサイトを踏まえて、その主張にどれだけの価値があるかを示します：

| 評価 | 結果 | 例 |
|---|---|---|
| `Approved` | 公開する | Kenney、ccMixter、Incompetech |
| `PartiallyApproved` | 公開する。記録は確認する価値がある | Pixabay、SoundImage |
| `RequiresLicenseCheck` | 実際のページでライセンスを確認する | OpenGameArt、Free Music Archive、Wikimedia Commons |
| `RequiresResourceCheck` | まず作品そのものを特定する | Rawpixel、itch.io |
| `NotAllowed` | 拒否する | YouTube、SoundCloud、Spotify |
| `Unknown` | 記録なし。`UnknownSourceTrust`で決まる | - |

`TrustedSourceCatalog.CreateDefault()`は25のサイトを返します。これは出発点となる一覧で、運営者がそれぞれ変更することが前提です。そのため、ある記録が存在することを当てにしてよいものは何もありません

`Sources`リストが空なら、入手元の評価はオフになります

ストリーミングプラットフォームは、一覧から外すのではなく`NotAllowed`として載せています。一覧にないサイトは`UnknownSourceTrust`で評価され、`standard`と`strict`ではその評価は拒否ではなく確認を求めるものになっているからです

カタログと[[ugc-licensing-policy]]は同じことを記述しており、一緒に編集されます

## 結果の扱い

呼び出すのは`ValidationFacade.ValidateForPublish`です。詳細：[[6_validation]]

`PublishReadinessReport`には次のものがあります：
- `HasErrors`：`Error`グループの問題
- `NeedsManualReview`：`Warning`グループの問題
- `IsReady`

その後どうするかは、プロファイルが決めるわけではありません。クライアントはエラーがあるとアップロードを止めます。サーバーはレベルを公開せず、審査キューに入れます

作者側から見た同じチェック：[[5_publish-readiness]]
