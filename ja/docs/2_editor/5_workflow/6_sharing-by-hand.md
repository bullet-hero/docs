---
title: レベルを手動で共有する方法
date: 2026-10-01
tags: [level_author]
---

# レベルを手動で共有する方法

レベルフォルダーをzipまたはtar.gzにまとめ、パスワードが必要ならgpgで暗号化します。別のマシンでは展開したレベルをすぐにプレイでき、ゲームはこうしたアーカイブを自分で読み込めます

レベルはファイルの入ったフォルダーです。アーカイブは、送るためにまとめた同じフォルダーです。レベルが使うものはすべて一緒に運ばれます：曲、画像、カバー

受け取った人がレベルを置く場所：[[2_metadata-and-sharing#今のレベルの共有方法]]

## アーカイブに含まれないもの

- レベルがリンクから取得するリソース。リンクはそのまま残ります
- レベル内のどこからも参照されていないファイル

ゲームのエクスポートレポートには、両方が一覧表示されます。詳細：[[13_export-and-protection#レベルのエクスポート]]

## 5つの形式

どれも、相手側がすでに持っているツールで開けます：

| ファイル | 中身 | 開くツール |
|---|---|---|
| `level.json.gpg` | レベルドキュメントだけをパスワード付きで。レベルフォルダー内に置かれます | gpg |
| `LEVEL_FOLDER.tar.gz` | フォルダー全体を1つのアーカイブに | 7-Zip、Keka、Ark、エクスプローラー |
| `LEVEL_FOLDER.tar.gz.gpg` | 同じアーカイブをパスワード付きで | gpg |
| `LEVEL_FOLDER.zip` | 同じフォルダーをzipで | Windowsならダブルクリックで開け、インストール不要 |
| `LEVEL_FOLDER.zip.gpg` | 同じzipをパスワード付きで | gpg |

デフォルトでは、ゲームはzip自体の機能（AES-256）でアーカイブにパスワードを設定します。このようなアーカイブは、エクスプローラー以外のどのアーカイバーでも開けます：パスワードを求められます。`.gpg`の形式は、指定したときにゲームが書き出します

## コマンドを実行する前に

コマンド内の2か所を置き換えてください：
- `LEVEL_FOLDER`：レベルフォルダーの名前、つまりレベルのIDです。数字と文字の長い文字列で、`levels`内のフォルダーの名前です
- `YOUR_PASSWORD`：パスワードそのもの

コマンドラインに入力したパスワードは、シェルの履歴に残ります。コマンドから`--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD`を取り除くと、gpgが画面上でパスワードを尋ねます

## gpgでレベルドキュメントを暗号化する

暗号化すると、元のファイルの隣に`level.json.gpg`ができます。元のファイルはそのまま残るので、結果を確認したら自分で削除してください。復号すると、ドキュメントが元の名前でもう一度書き出されます。暗号化したファイルはそのまま残ります：

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## tar.gzアーカイブ

フォルダーは内側からまとめられます：アーカイブにはレベルのファイルそのものが入り、それを囲むフォルダーはありません。展開するには展開先のフォルダーがすでに存在している必要があり、tarはフォルダーを作成しません。`mkdir`は、cmd、PowerShell、MacやLinuxのターミナルで同じように動作します：

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

まとめと暗号化を1回で行うこともできます。この場合、保護されていないアーカイブはディスクに一切書き込まれません。2行目は、アーカイブを復号して同じフォルダーに展開し直します：

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## zipアーカイブ

Windowsでは、どのマシンにもあるPowerShellを使います。アスタリスクは、フォルダーそのものではなくフォルダーの中身をまとめます。`Expand-Archive`はフォルダーを自分で作成するので、事前の`mkdir`は不要です：

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

MacやLinuxでは、zipとunzipを使います：

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

7-Zipがパスワードを尋ねるzipは、7-Zip自身で作ります。7-Zipをインストールしておく必要があります：

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## ゲームはそれらを読み込める

どの形式も双方向に使えます。ゲームが書き出したものは、gpg、tar、zipで開けます。gpg、tar、zipで作ったものは、ゲームが読み込みます。独自のフォーマットではなく標準のツールを選んだのは、そのためです

> [!tip] ヒント
> ゲームが見るのはファイルの中身が何であるかで、名前ではありません。そのため、名前を変えたアーカイブでも開けます。`7z`はゲームが認識しますが、受け付けません：ファイルが壊れていると判断する代わりに、そのフォーマット名を表示します。そのようなアーカイブは、zipにまとめ直してください

> [!caution] 注意
> **忘れたパスワードは復元できません**。鍵はどこにも保存されていません：ゲームにも、ファイルにも、誰の手元にもありません。リセットも、復元も、回避策もありません。パスワードを失ったレベルは、パスワードと一緒に失われます。エディターを閉じる前に、パスワードを書き留めてください

次へ：[[4_level-folder-and-backups|レベルフォルダーとバックアップ]]、[[4_not-losing-work|作業を失わないために]]
