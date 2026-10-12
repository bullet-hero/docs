---
title: ライブラリとコレクション
date: 2026-10-02
tags: [level_author]
---

# ライブラリとコレクション

コレクションには、複数のレベルで再利用するリソースを保存します。レベルがコレクションを参照することはありません：インポートでリソースがレベル内にコピーされるので、レベルはどこでもプレイできます

## コレクションとは

**コレクション**は、再利用できるリソースのフォルダーです。7種類のリソースを入れられます：

| 種類 | 保存方法 |
|---|---|
| プレハブ、テーマ、シェイプ、エフェクト | データ、エントリーごとに1ファイル |
| テクスチャ、フォント、オーディオ | メディアファイル |

コレクションはレベルに結び付いていません。デバイス上に置かれ、開いたどのレベルでも使えます

## ソース

ライブラリは3つのソースからリソースを表示します。それぞれがリストの上のフィルターチップです：

| チップ | 内容 | 変更 |
|---|---|---|
| `{{ui:editor_library-source_library}}` | このデバイスの共有ライブラリ：`resources/prefabs`、`themes`、`shapes`、`effects` | できる |
| `{{ui:editor_library-source_local}}` | 自分のコレクション、`resources/collections` | できる |
| `{{ui:editor_library-source_workshop}}` | Steamワークショップでサブスクライブしているコレクション。その場で読み込まれます。Steam版のみ | できない |

読み取り専用のコレクションを変更するには、そのエントリーを自分のコレクションにコピーします

## 「ライブラリ」タブ

`{{ui:settings_editor-settings_library}}`は、エディターのホーム画面の最後のタブで、`{{ui:settings_editor-settings_community}}`の次にあります

細いボタンの列で種類を選びます：
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`、`{{ui:editor_library_kind-themes}}`、`{{ui:editor_library_kind-shapes}}`、`{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`、`{{ui:editor_library_kind-fonts}}`、`{{ui:field_common_audio}}`

その右側には、ページタイトル（左）とそのボタン（右）が1行に並びます。その下がリストです。リストが空の場合は、リストの中央にそう表示されます

7種類のページ（`{{ui:editor_library_kind-prefabs}}`から`{{ui:field_common_audio}}`まで）では、`{{ui:editor_library_copy-target}}`がタイトルの下で全幅の独立した行を占めます。ソースのチップはその下の行に並びます

ライブラリのウィンドウ（コレクションのカード、テクスチャの画像、共有ウィンドウ）は、隅の×で閉じます。`{{ui:editor_library_close}}`ボタンはありません

どの行もボタンです。押すと、その種類の主な操作が実行されます：

| 種類 | 行を押すと |
|---|---|
| コレクション | そのページを開きます |
| テーマ、シェイプ、エフェクト | エディターを開きます |
| テクスチャ | 画像とそのサイズを表示します |
| プレハブ、フォント、オーディオ | 何も起きません。オーディオの行には専用の再生ボタンがあります |

行の右側にある小さなボタンはその他の操作で、ゴミ箱アイコンは削除または除去を行います

`{{ui:editor_library_open-folder}}`は、現在のページのフォルダーをシステムのファイルマネージャーで表示します。Windows、macOS、Linuxでのみ使えます

### コレクション

`{{ui:editor_library_open-folder}}`と`{{ui:editor_library_refresh}}`はページタイトルの右にあります。`新規コレクション`と`{{ui:editor_library_import-archive}}`は、その下の別の行に右揃えで並びます

- `新規コレクション`は空のコレクションを作成し、そのカードを開きます
- `{{ui:editor_library_import-archive}}`は、`.zip`または`.tar.gz`ファイル、あるいはパスワード付きアーカイブ（独自のパスワード付きの`.zip`、`.zip.gpg`、`.tar.gz.gpg`）からコレクションを追加します。そのコレクションがすでにデバイスにある場合は、置き換えるかどうかをゲームが確認します

パスワード付きアーカイブを開くと`{{ui:editor_library_passphrase-title}}`ウィンドウが開きます：`{{ui:editor_library_passphrase-needed}}`。パスワードを入力して`{{ui:editor_library_open}}`を押します。パスワードが間違っていると`{{ui:editor_library_passphrase-wrong}}`と表示されます
- `{{ui:editor_library_open-folder}}`は`resources/collections`を開きます
- `{{ui:editor_library_refresh}}`はフォルダーを読み込み直します

自分のコレクションには`{{ui:editor_library_edit}}`とゴミ箱アイコンがあります。ゴミ箱は先に確認してから、コレクションをそのすべてのファイルごと削除します

### コレクションのカード

`{{ui:editor_library_edit}}`は、コレクションのカードのウィンドウを開きます：
- `{{ui:editor_library_field-name}}`、`{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`、カンマ区切り
- `{{ui:editor_library_field-license}}`：`{{ui:editor_library_license-unspecified}}`または代表的なライセンスのいずれか
- `{{ui:editor_library_set-cover}}`でpng画像を選びます。隣の行に、カバーがあるかどうかが表示されます

`{{ui:editor_save_text}}`でカードを書き込みます。`{{ui:editor_cancel_text}}`、×、またはウィンドウの外をクリックすると、変更は破棄されます

### コレクションのページ

| 要素 | 機能 |
|---|---|
| `{{ui:settings_common_back}}` | リストに戻ります |
| `{{ui:editor_library_edit}}` | カードを開きます。自分のコレクションのみ |
| `{{ui:editor_share_share}}` | 共有ウィンドウを開きます：`.zip`または`.tar.gz`での`{{ui:editor_share_archive}}`（パスワードの有無は選べます）、Steam版では自分のコレクションに`{{ui:editor_share_steam}}`も使えます |
| `{{ui:editor_library_open-folder}}` | コレクション自体のフォルダーを開きます |
| `{{ui:editor_library_delete}}` | 先に確認してから、コレクションを削除します |

その下が中身です。行を押すと、その種類のページと同じようにエントリーが開きます。ゴミ箱アイコンはエントリーをコレクションから除去します

読み取り専用のコレクションには`{{ui:editor_library_read-only}}`と表示されます

`{{ui:editor_share_share}}`の詳細：[[17_publishing]]

### プレハブ、テーマ、シェイプ、エフェクト

これらの各ページには、すべてのソースのすべてのエントリーが表示されます。チップでリストを絞り込めます

`{{ui:editor_library_copy-target}}`では自分のコレクションを1つ選びます。デフォルトは`{{ui:editor_library_copy-target-none}}`です。対象を選ぶと、ほかの場所から来たすべての行に`{{ui:editor_library_copy-to}}`が付きます

テーマ、シェイプ、エフェクトは、レベル設定と同じエディターで開きます。`{{ui:editor_save_text}}`は、エントリーがある場所に変更を書き込みます：`{{ui:editor_library-source_library}}`または自分のコレクションです。ワークショップのエントリーは読み取り専用で開き、`{{ui:editor_save_text}}`はオフになります。変更するには、自分のコレクションにコピーします

`{{ui:editor_library_new-entry}}`は、エディターで新しいテーマ、シェイプ、エフェクトを作ります。エントリーは対象コレクションに保存され、対象を選んでいなければ`{{ui:editor_library-source_library}}`に保存されます。プレハブはレベルの中で作るもので、`{{ui:editor_library_new-entry}}`はありません

変更できるエントリーにはゴミ箱アイコンがあり、先に確認します

すべての行に`{{ui:editor_share_share}}`があります。このボタンは、エントリーを必要なものすべて（たとえばプレハブのシェイプ、テクスチャ、入れ子のプレハブ）と一緒に、1エントリーのコレクションとして`.zip`または`.tar.gz`にまとめます。パスワードの有無は選べます。受け取った側は、ほかのコレクションと同じく`{{ui:editor_library_import-archive}}`でそのファイルをインポートします

`{{ui:editor_library_open-folder}}`は、その種類のこのデバイスの共有ライブラリのフォルダー（たとえば`resources/themes`）を開きます

### テクスチャ、フォント、オーディオ

これらのページには、すべてのコレクションのファイルが表示されます。ファイル用の個人ライブラリはないため、これらの種類はコレクションの中にだけ存在します

- テクスチャの行には画像が表示されます
- オーディオの行には再生ボタンがあります。同時に再生されるのは1曲だけで、ページを離れると停止します
- フォントの行にはプレビューがありません

`{{ui:editor_library_add-file}}`は、デバイス上のファイルを対象コレクションに入れます。そのため、対象がないとボタンはオフです。テクスチャはpngかjpg、フォントはttfかotf、オーディオはmp3、wav、oggです。コレクションにすでに同じバイト列のファイルがある場合は何も追加されず、ゲームがそれを知らせます

行には`{{ui:editor_library_copy-to}}`とゴミ箱アイコンがあります

### コピーで一緒に運ばれるもの

コピーには、エントリーが必要とするものすべてが含まれます：プレハブのシェイプ、テクスチャ、フォント、入れ子のプレハブ、エフェクトのパーティクルのシェイプ。それらのリソースの作者情報も一緒に移ります

## 「コレクション」タブ

`{{ui:editor_library_kind-collections}}`はレベル設定のタブで、`{{ui:editor_library_kind-prefabs}}`のすぐ後にあります。上部に2つのモードがあります：`インポート`と`{{ui:editor_collections_mode-build}}`

### インポート

1. タブにコレクションの一覧が表示されます。必要なものを押します
2. 必要なエントリーにチェックを入れます。`{{ui:editor_collections_select-all}}`と`{{ui:editor_collections_select-none}}`で、すべてにチェックを入れるか、すべてのチェックを外します
3. `選択：N、追加された依存関係：M`の行に、レベルに入るものが表示されます。依存関係は自動で追加されます
4. `インポート`を押します

インポート全体で、元に戻す操作の1ステップになります

テクスチャ、フォント、オーディオはレベル内で新しいIDを受け取り、そのファイルは一意の名前でレベルフォルダーにコピーされます。レベルにバイト単位で同じファイルがすでにある場合、2回目のコピーは行われません：インポートはレベル自身のテクスチャ、フォント、オーディオトラックを使います

### コレクションを作成

1. `{{ui:editor_collections_target}}`で`新しいコレクション`または自分のコレクションのいずれかを選びます。新しいコレクションの名前は`{{ui:editor_library_field-name}}`フィールドから取られます
2. レベルのリソースにチェックを入れます。7種類のどれでも選べます
3. `{{ui:editor_collections_build}}`を押します

新しいコレクションには、レベルの作者が設定されます

保護されたレベルからはコレクションを作成できません。詳細：[[13_export-and-protection]]

## リソースの選択と検索

検索とリソース選択ウィンドウには、プレハブ、テーマ、シェイプ、エフェクト用の`{{ui:settings_editor-settings_library}}`の階層があります。この階層はすべてのソースを表示します。選択ウィンドウとは、シェイプ、コライダー、エフェクト、テーマのフィールドと`{{ui:cmd_editor_place-prefab}}`のことです

ライブラリからエントリーを選ぶと、依存関係と一緒にレベルにインポートされ、割り当てられます。競合があると、「コレクション」タブと同じ確認が出ます

レベルのリソースタブ内にあるライブラリブラウザーも同じように動作し、ソースのチップを表示します。詳細：[[11_level-resources]]

## 競合

インポートするエントリーが、同じIDですでにレベルにある場合があります：
- 内容が同じ：何もする必要はありません
- 内容が違う：`{{ui:editor_resource-conflict_title}}`ウィンドウが開きます

ウィンドウにはすべての競合が並び、それぞれに`{{ui:editor_resource-conflict_copy}}`のトグルがあります：

| 選択 | 結果 |
|---|---|
| 維持（トグルがオフ） | レベルのバージョンが残り、使われます |
| `{{ui:editor_resource-conflict_copy}}` | コレクションのバージョンが新しいIDで追加されます。一緒にインポートされたものはすべてコピーを参照します |

`{{ui:editor_resource-conflict_all-keep}}`と`{{ui:editor_resource-conflict_all-copy}}`で、すべてのトグルを一度に設定します。`インポート`で選択が適用され、`{{ui:editor_cancel_text}}`では何もインポートされません

どのバージョンも、黙って優先されることはありません。内容が違う競合はすべてこのウィンドウで決めます

## 作者情報

レベルのリソースの記録は、テクスチャ、フォント、オーディオと同様に、テーマ、エフェクト、シェイプ、プレハブも対象にします。インポートで必要な記録がレベルにコピーされるので、作者情報はリソースと一緒に届きます

詳細：[[4_resource-record]]

## ディスク上の配置

コレクションは、ゲームのデータフォルダーの`resources/collections/<collection-guid>/`にあります。これは、このデバイスの共有ライブラリがある、`levels`の隣の同じ`resources`フォルダーです。詳細：[[4_level-folder-and-backups]]

| パス | 内容 |
|---|---|
| `collection.json`または`collection.blob` | マニフェスト：名前、説明、作者、ライセンス、テクスチャ・フォント・オーディオのエントリー、中にあるすべてのものの作者情報 |
| `cover.png` | カバー、任意 |
| `prefabs/`、`themes/`、`shapes/`、`effects/` | エントリーごとに`<guid>.json`または`<guid>.blob`が1つ。このデバイスの共有ライブラリと同じファイルです |
| `media/` | テクスチャ、フォント、オーディオのファイル |

コレクションはアーカイブとして受け渡します：ページの`{{ui:editor_share_share}}`と、リストの`{{ui:editor_library_import-archive}}`を使います。コレクションではないアーカイブは拒否されます

次へ：[[17_publishing]]、[[2_reuse]]、[[4_resource-record]]
