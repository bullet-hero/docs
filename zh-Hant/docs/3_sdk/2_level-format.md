---
title: 關卡格式
date: 2026-10-02
tags: [developer, level_author]
---

# 關卡格式

關卡是一個資料夾：內容在level.json或level.blob中，後設資料在metadata.json或metadata.blob中，另有封面和媒體檔案。備份、記錄和玩家設定留在裝置上

## 關卡資料夾

關卡資料夾中的每個檔名都固定在`FileNames`中：

| 檔案 | 模型 | 內容 |
|---|---|---|
| `level.json`或`level.blob` | `Level` | 內容：設定、物體和事件、音訊、資源、提示 |
| `metadata.json`或`metadata.blob` | `LevelMeta` | 名稱、描述、作者、許可證、每個資源的記錄、對封面的引用 |
| `logo.png`或`logo.jpg` | - | 封面 |
| 音軌、圖片、字型 | - | 關卡引用的媒體檔案 |

**副檔名就是格式**。檔案內部的任何地方都沒有寫它。讀取方看哪個檔案存在：`level.json`還是`level.blob`

關卡和後設資料各自獨立選擇格式。例如，內建關卡`new-zero-demo`在`metadata.json`旁邊存放的是`level.blob`

**`metadata.json`特意做成單獨的檔案**。目錄用一千個小後設資料檔案展示一千個關卡，期間一個關卡也不開啟

## 資源

資源通過`uri`和`uri_type`（`ResourceUriType`）這一對值定址：

| 值 | 型別 | 檔案位置 |
|---|---|---|
| 1 | `LevelPath` | 關卡資料夾內。只有這種型別能讓關卡可移植 |
| 2 | `AbsolutePath` | 本裝置上的其他位置 |
| 3 | `DirectUrl` | 通過網路下載 |
| 4 | `StreamingAssets` | 隨遊戲提供，而不是隨關卡 |

圍繞一首歌建立關卡時會出現`AbsolutePath`。匯出歸檔包時會把這樣的檔案複製進去。更多：[[4_archives]]

封面和其他資源一樣，通過`LevelMeta.LevelLogo`訪問。是`logo.png`還是`logo.jpg`，由檔案本身的位元組決定，而不是由源圖片的名稱決定

封面的作者記錄是一個`resource_type`為9（`LevelLogo`）的`ResourceMeta`。其中`resource_id`和`resource_guid`都不填：關卡只有一個封面，所以型別就是完整的地址

## AI宣告

`LevelMeta`和每個`ResourceMeta`都帶有`AiGeneration`型別的`ai_generated`：

| 值 | 名稱 | 含義 |
|---|---|---|
| 0 | `NotSpecified` | 未宣告，未知。這是預設值，缺少該鍵時也按此讀取 |
| 1 | `No` | 宣告為未使用AI生成 |
| 2 | `Yes` | 宣告為AI生成 |

在`LevelMeta`中，它只針對關卡自己的內容。每個資源和封面在各自的記錄中宣告自己。關卡中是否有AI內容並不儲存：由`LevelMeta.ContainsAiContent()`回答，只有`Yes`才算

## 不隨關卡一起走的內容

這些檔案位於`levels`資料夾旁邊，從不在關卡資料夾裡。打包、傳送或刪除關卡都不會動它們：

| 資料夾或檔案 | 是什麼 | 為什麼留下 |
|---|---|---|
| `backups/` | 編輯器自動儲存，每個關卡ID一個資料夾，`backup_level_<time>.<extension>` | 放在它所保護的資料夾裡的副本會隨該資料夾一起被刪除 |
| `stats/` | 按`LevelId`記錄的成績和進度，以及`statistics.json` | 否則別人發來的關卡到手時就已經通關了 |
| `settings.json` | `UserSettings`，玩家對整個裝置的設定 | 它們屬於玩家，而不屬於關卡 |
| `resources/themes`、`effects`、`shapes`、`prefabs` | 本裝置的共享庫 | 它們由裝置上的所有關卡共用 |
| `reports/` | 診斷報告 | - |

## JSON鍵

JSON總是緊湊寫入，沒有縮排。想用眼睛閱讀，請在文本編輯器中格式化

**鍵的長度取決於它在關卡中出現的次數**：
- 每個檔案只出現一次的鍵用完整單詞以`snake_case`書寫：`level_id`、`min_generation`
- 重複上千次的鍵縮短為幾個字母：`objs`、`f`、`e`、`v`

鍵佔關卡檔案位元組數的52%，所以這是規則，而不是個人口味。所有鍵都宣告在`Names.cs`中

**多型值寫作`[標籤, 資料]`**。普通字串是`[0,{"v":"Author"}]`，本地化字串是`[1,{"strs":[...]}]`

`ObjectId`之類的識別符號包裝寫作裸數字或裸字串

## 識別符號

**整數識別符號的符號有含義**。`0`始終表示“未設定”：

| 識別符號 | JSON鍵 | 正數 | 負數 |
|---|---|---|---|
| `ObjectId` | `id`，父級用`pid` | 關卡物體 | 遊戲物體：`-1`相機，`-2`本地玩家，`-3`預製件模板的根 |
| 資源識別符號 | `txid`、`fnid`、`auid`、`byid`、`ttid` | 隨遊戲提供的資源 | 關卡自己的資源 |
| 音訊軌道的`AudioId` | `aid` | 本關卡的軌道 | 不使用 |

`pid`等於`0`表示物體沒有父級。小於`-3`的數字只在遊戲執行時存在，不會寫入檔案

**`Marker`、`Checkpoint`和`BeatSegment`沒有識別符號**。它們的地址是時間上的位置：標記和檢查點是幀`f`，節拍段是其時段`sp`的第一幀（節拍段互不重疊）。移動這樣的物件，它的地址就會改變

**預製件覆蓋用編號而不是JSON鍵來指明欄位**。放置把自己的覆蓋存放在`mod`列表中。每個覆蓋的`key`包含三個數字：
- `id`：模板內部的物體，而不是它在關卡中的副本
- `f`：欄位的永久編號
- `i`：列表欄位的元素，整個欄位則為`-1`

編號永久繫結到欄位。重新命名該欄位的JSON鍵不會破壞已經儲存在關卡中的覆蓋

## 外層的“g”

每個序列化根都包在一個帶兩個鍵的封套裡：

```json
{"g":2,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g`是模型的代（`Names.Generation`），`v`是資料

封套可以巢狀。在`Level`內部，`LevelSettings`、`GameLevel`、`AudioLevel`、`LevelResources`和`LevelHints`都有自己的封套。代如何運作：[[5_versioning]]

> [!caution] 注意
> `g`和`vrs`是不同的數字。`vrs`是作者給關卡定的版本（`LevelMeta.LevelVersion`），與格式無關。不要手動修改`g`：`g`高於構建所知的檔案完全無法讀取
