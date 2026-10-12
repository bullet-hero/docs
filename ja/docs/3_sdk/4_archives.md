---
title: アーカイブと保護
date: 2026-10-01
tags: [developer, level_author]
---

# アーカイブと保護

レベルはフォルダー、tar.gz、zipとしてエクスポートでき、パスワードもかけられます：AES-256のzipかOpenPGPです。受け取ったファイルのフォーマットは、SDKが名前ではなく先頭のバイトで判定します

## エクスポートモード

レベルは`LevelExportMode`のいずれかの形でデバイスを離れます：

| 値 | モード | 書き出されるもの | 保護 |
|---|---|---|---|
| 0 | `Folder` | ディスク上と同じ形の普通のフォルダー | なし |
| 1 | `FolderProtectedLevel` | `level.json.gpg`だけが暗号化されたフォルダー | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | なし |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | なし |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | エントリーがAES-256の`<name>.zip` | zip自体の暗号化 |

番号はモードの識別子で、決して変わりません。エディターのドロップダウンでの並び順は別に決められています（`DisplayOrder`）

**どのフォーマットもオープンな標準です**。`tar -xzf`、`gpg -d`、それに任意のアーカイバーで、ゲームなしで開けます：

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## 2つの保護方式

**パスワードでレベルを保護するデフォルトの方法は`ZipEncrypted`です**。受け取る側はアーカイバーを持っていても、gpgは持っていない可能性が高いからです

**OpenPGPは、ドキュメント、フォルダー、アーカイブを1つの方式で保護します**。フォルダーを保護できるのはOpenPGPだけです

`FolderProtectedLevel`では、メタデータ、カバー、メディアは読めるままです。そのため、レベルブラウザーには引き続きカードが表示されます

名前には内側の拡張子が残ります：`level.json.gpg`。`gpg -c level.json`が付ける名前とまったく同じなので、推測しなくてもフォーマットがわかります

## 中に入るもの

`LevelArchiveBuilder`は、フォルダー内のファイル一覧ではなく、モデルから中身を割り出します。レベルが参照していないファイルは外に残ります。そうしたファイルがいくつ残ったかはレポートに示されます

レベルの参照は次のように扱われます：
- `AbsolutePath`のリソースはアーカイブにコピーされます。その参照は`LevelPath`に書き換えられますが、書き換わるのはエクスポートしたコピーの中だけです
- `DirectUrl`はそのまま残り、レポートに載ります。URLはファイルの中に入れて運べないからです
- 見つからないファイルは、コード`archive.resource_missing`でレポートに載ります

## バイトによる判定

ファイル名は誰でも付けられます。そのため`ArchiveFormatSniffer`は先頭8バイトで判定します：

| 先頭のバイト | フォーマット |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`、`50 4B 05 06`、`50 4B 07 08`、`50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| OpenPGPのパケットタグ（最後にチェック） | `OpenPgp`：復号してから改めて判定 |

> [!warning] 警告
> `.7z`は読み込みも書き出しもできません。判定するのは、拒否のときにその名前を示すため（`Unsupported`）だけです。そうすれば、ファイルが壊れていると思い込まずに、レベルをzipに詰め直してもらえます

## 読み込み

`LevelArchiveReader.ReadAsync`は、フォルダーかシーク可能な`Stream`を受け取ります。返すのは`LevelArchiveContent`で、その`LevelArchiveOpenResult`は次のいずれかの値です：

| 結果 | 意味 |
|---|---|
| `Ok` | 読み込めた |
| `PassphraseRequired` | パスワードがないので、入力を求める必要がある |
| `WrongPassphrase` | パスワードはすでに入力されたが、間違っている |
| `Damaged` | ファイルが破損している |
| `NotAnArchive` | アーカイブではない |
| `Unsupported` | フォーマットは判定できたが、サポートされていない |

`PeekMetaAsync`は、カードやカタログのためにメタデータだけを読みます

サーバーは、誰かがアップロードすると決めたものを何でも読みます。そのため、読み込み側は`ArchiveLimits`の範囲内で動作します。デフォルトの値は次のとおりです：
- 4096エントリー
- エントリーあたり512 MiB
- 合計1 GiB

渡されたストレージの外には何も展開しません

エディター側から見たエクスポート：[[13_export-and-protection]]
