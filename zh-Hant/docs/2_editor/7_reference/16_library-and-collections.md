---
title: 庫與合集
date: 2026-10-02
tags: [level_author]
---

# 庫與合集

合集存放你在關卡之間複用的資源。關卡從不引用合集：匯入會把資源複製到關卡內部，關卡在哪裡都能遊玩

## 什麼是合集

**合集**是一個存放可複用資源的資料夾。它可以包含七類資源：

| 類別 | 儲存方式 |
|---|---|
| 預製件、主題、形狀、特效 | 資料，每個條目一個檔案 |
| 紋理、字型、音訊 | 媒體檔案 |

合集不繫結任何關卡。它儲存在你的裝置上，在你開啟的任何關卡中都能使用

## 來源

庫顯示來自三個來源的資源。每個來源是列表上方的一個篩選標籤：

| 標籤 | 是什麼 | 可修改 |
|---|---|---|
| `{{ui:editor_library-source_library}}` | 本裝置的共享庫：`resources/prefabs`、`themes`、`shapes`、`effects` | 是 |
| `{{ui:editor_library-source_local}}` | 你自己的合集，`resources/collections` | 是 |
| `{{ui:editor_library-source_workshop}}` | 你在Steam創意工坊訂閱的合集，直接在原位置讀取。僅限Steam版本 | 否 |

只讀合集的修改方式是：把它的條目複製到你自己的合集中

## “庫”標籤頁

`{{ui:settings_editor-settings_library}}`是編輯器主頁上的最後一個標籤頁，位於`{{ui:settings_editor-settings_community}}`之後

一列窄按鈕用來選擇類別：
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`、`{{ui:editor_library_kind-themes}}`、`{{ui:editor_library_kind-shapes}}`、`{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`、`{{ui:editor_library_kind-fonts}}`、`{{ui:field_common_audio}}`

它的右側，頁面標題（左）和頁面按鈕（右）排成一行。下面是列表。空列表會在中間說明這一點

在七個類別的頁面上，從`{{ui:editor_library_kind-prefabs}}`到`{{ui:field_common_audio}}`，`{{ui:editor_library_copy-target}}`在標題下方獨佔一整行。來源篩選標籤位於它下面一行

庫的視窗（合集資訊卡、紋理圖片、分享視窗）用角落的叉號關閉。沒有`{{ui:editor_library_close}}`按鈕

每一行都是一個按鈕。按下它會執行該類別的主要操作：

| 類別 | 按下一行 |
|---|---|
| 合集 | 開啟它的頁面 |
| 主題、形狀、特效 | 開啟編輯器 |
| 紋理 | 顯示圖片及其尺寸 |
| 預製件、字型、音訊 | 無操作。音訊行有自己的播放按鈕 |

行右側的小按鈕是其他操作，垃圾桶圖示用於刪除或移除

`{{ui:editor_library_open-folder}}`在系統檔案管理器中顯示當前頁面的資料夾。僅在Windows、macOS和Linux上提供

### 合集

`{{ui:editor_library_open-folder}}`和`{{ui:editor_library_refresh}}`位於頁面標題右側。`新建合集`和`{{ui:editor_library_import-archive}}`在標題下方單獨一行，靠右對齊

- `新建合集`建立一個空的合集並開啟它的資訊卡
- `{{ui:editor_library_import-archive}}`從`.zip`或`.tar.gz`檔案新增合集，也可以從帶密碼的壓縮包新增：自帶密碼的`.zip`、`.zip.gpg`或`.tar.gz.gpg`。如果裝置上已有這個合集，遊戲會詢問是否替換

帶密碼的壓縮包會開啟`{{ui:editor_library_passphrase-title}}`視窗：`{{ui:editor_library_passphrase-needed}}`。輸入密碼後按`{{ui:editor_library_open}}`。密碼錯誤時會顯示`{{ui:editor_library_passphrase-wrong}}`
- `{{ui:editor_library_open-folder}}`開啟`resources/collections`
- `{{ui:editor_library_refresh}}`重新讀取資料夾

你自己的合集有`{{ui:editor_library_edit}}`和垃圾桶圖示。垃圾桶會先詢問，然後刪除合集及其中的所有檔案

### 合集資訊卡

`{{ui:editor_library_edit}}`開啟合集資訊卡視窗：
- `{{ui:editor_library_field-name}}`、`{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`，用逗號分隔
- `{{ui:editor_library_field-license}}`：`{{ui:editor_library_license-unspecified}}`或某個常見許可證
- `{{ui:editor_library_set-cover}}`選擇一張png圖片。旁邊的一行顯示是否有封面

`{{ui:editor_save_text}}`寫入資訊卡。`{{ui:editor_cancel_text}}`、叉號或點選視窗外會丟棄改動

### 合集頁面

| 元素 | 作用 |
|---|---|
| `{{ui:settings_common_back}}` | 回到列表 |
| `{{ui:editor_library_edit}}` | 開啟資訊卡。僅限你自己的合集 |
| `{{ui:editor_share_share}}` | 開啟分享視窗：`{{ui:editor_share_archive}}`，格式為`.zip`或`.tar.gz`，可帶密碼也可不帶，在Steam版本中，你自己的合集還有`{{ui:editor_share_steam}}` |
| `{{ui:editor_library_open-folder}}` | 開啟合集自己的資料夾 |
| `{{ui:editor_library_delete}}` | 先詢問，然後刪除合集 |

下面是合集內容。按下一行會像在該類別頁面一樣開啟條目，垃圾桶圖示把條目從合集中移除

只讀合集會顯示`{{ui:editor_library_read-only}}`

關於`{{ui:editor_share_share}}`的更多內容：[[17_publishing]]

### 預製件、主題、形狀、特效

這些頁面各自顯示所有來源中的全部條目。篩選標籤可以縮小列表

`{{ui:editor_library_copy-target}}`從你自己的合集中選擇一個。預設為`{{ui:editor_library_copy-target-none}}`。選好目標後，來自其他位置的每一行都會出現`{{ui:editor_library_copy-to}}`

主題、形狀或特效會在與關卡設定相同的編輯器中開啟。`{{ui:editor_save_text}}`把改動寫到條目所在的位置：`{{ui:editor_library-source_library}}`或你的合集。來自創意工坊的條目以只讀方式開啟，`{{ui:editor_save_text}}`不可用。要修改它，請把它複製到你自己的合集

`{{ui:editor_library_new-entry}}`在編輯器中建立新的主題、形狀或特效。條目會儲存到目標合集，未選擇目標時儲存到`{{ui:editor_library-source_library}}`。預製件在關卡中製作，沒有`{{ui:editor_library_new-entry}}`

可以修改的條目有垃圾桶圖示，它會先詢問

每一行都有`{{ui:editor_share_share}}`。這個按鈕會把條目連同它需要的一切（例如預製件的形狀、紋理和巢狀預製件）打包成`.zip`或`.tar.gz`，可帶密碼也可不帶，作為只有一個條目的合集。接收者通過`{{ui:editor_library_import-archive}}`匯入該檔案，和匯入任何合集一樣

`{{ui:editor_library_open-folder}}`開啟該類別的裝置庫資料夾，例如`resources/themes`

### 紋理、字型、音訊

這些頁面顯示所有合集中的檔案。檔案沒有個人庫，所以這幾類只存在於合集中

- 紋理行會顯示圖片
- 音訊行有播放按鈕。同一時間只播放一首，離開頁面時停止
- 字型行沒有預覽

`{{ui:editor_library_add-file}}`把裝置上的檔案放入目標合集，所以沒有目標時這個按鈕不可用。紋理為png或jpg，字型為ttf或otf，音訊為mp3、wav或ogg。如果合集中已有位元組完全相同的檔案，則什麼都不會新增，遊戲會給出提示

行上有`{{ui:editor_library_copy-to}}`和垃圾桶圖示

### 複製會帶上什麼

複製會帶上條目需要的一切：預製件的形狀、紋理、字型和巢狀預製件，特效的粒子形狀。這些資源的署名資訊也會一併帶上

## “合集”標籤頁

`{{ui:editor_library_kind-collections}}`是關卡設定中的一個標籤頁，緊跟在`{{ui:editor_library_kind-prefabs}}`之後。頂部有兩種模式：`匯入`和`{{ui:editor_collections_mode-build}}`

### 匯入

1. 標籤頁顯示合集列表。按下需要的合集
2. 勾選需要的條目。`{{ui:editor_collections_select-all}}`和`{{ui:editor_collections_select-none}}`勾選全部或取消全部勾選
3. `已選：N，將新增依賴：M`這一行顯示將進入關卡的內容。依賴會自動新增
4. 按`匯入`

整個匯入是一次撤銷步驟

紋理、字型和音訊會在關卡中得到新的id，它們的檔案以唯一的名稱複製到關卡資料夾中。關卡中已有位元組完全相同的檔案時不會再次複製：匯入會使用關卡自己的紋理、字型或音軌

### 生成合集

1. `{{ui:editor_collections_target}}`選擇`新合集`或你自己的某個合集。新合集的名稱取自`{{ui:editor_library_field-name}}`欄位
2. 勾選關卡的資源，七類中任意一類都可以
3. 按`{{ui:editor_collections_build}}`

新合集會獲得關卡的作者

受保護的關卡不能生成合集。更多：[[13_export-and-protection]]

## 資源選擇與搜尋

搜尋和資源選擇視窗中有一個`{{ui:settings_editor-settings_library}}`層級，用於預製件、主題、形狀和特效。它顯示所有來源。選擇視窗指形狀、碰撞體、特效和主題欄位，以及`{{ui:cmd_editor_place-prefab}}`

從庫中選擇條目會把它連同依賴一起匯入關卡，並完成指定。遇到衝突時，會提出與“合集”標籤頁相同的問題

關卡各資源標籤頁裡的庫瀏覽器也按同樣的方式工作，並顯示來源標籤。更多：[[11_level-resources]]

## 衝突

要匯入的條目可能已經以相同的id存在於關卡中：
- 內容相同：無需任何操作
- 內容不同：開啟`{{ui:editor_resource-conflict_title}}`視窗

視窗列出所有衝突，每個衝突都有一個`{{ui:editor_resource-conflict_copy}}`開關：

| 選擇 | 結果 |
|---|---|
| 保留（開關關閉） | 關卡的版本保留並被使用 |
| `{{ui:editor_resource-conflict_copy}}` | 合集的版本以新的id加入。與它一起匯入的所有內容都指向這個副本 |

`{{ui:editor_resource-conflict_all-keep}}`和`{{ui:editor_resource-conflict_all-copy}}`一次設定所有開關。`匯入`應用選擇，`{{ui:editor_cancel_text}}`什麼都不匯入

沒有哪個版本會悄悄勝出。每一個內容不同的衝突都在這個視窗中決定

## 署名

關卡的資源記錄除了紋理、字型和音訊，也涵蓋主題、特效、形狀和預製件。匯入會把需要的記錄複製到關卡中，所以署名會隨資源一起到達

更多：[[4_resource-record]]

## 磁碟上的位置

合集存放在遊戲資料資料夾的`resources/collections/<collection-guid>/`中。這就是`levels`旁邊存放本裝置共享庫的那個`resources`資料夾。更多：[[4_level-folder-and-backups]]

| 路徑 | 內容 |
|---|---|
| `collection.json`或`collection.blob` | 清單：名稱、描述、作者、許可證、紋理、字型和音訊條目，以及其中所有內容的署名資訊 |
| `cover.png` | 封面，可選 |
| `prefabs/`、`themes/`、`shapes/`、`effects/` | 每個條目一個`<guid>.json`或`<guid>.blob`，與本裝置共享庫中的檔案相同 |
| `media/` | 紋理、字型和音訊檔案 |

合集以壓縮包的形式傳遞：在合集頁面上用`{{ui:editor_share_share}}`，在列表中用`{{ui:editor_library_import-archive}}`。不是合集的壓縮包會被拒絕

接下來：[[17_publishing]]、[[2_reuse]]、[[4_resource-record]]
