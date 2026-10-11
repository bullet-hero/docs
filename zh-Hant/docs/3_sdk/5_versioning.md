---
title: 版本與遷移
date: 2026-10-02
tags: [developer, level_author]
---

# 版本與遷移

版本有三種：gv對應遊戲，sv對應SDK，mg對應模型格式的代。SDK依據mg遷移舊檔案，並拒絕讀取代比當前構建更新的檔案

## 三種版本

| 標記 | 全稱 | 給什麼定版本 | 存放位置 |
|---|---|---|---|
| `gv` | `game version` | 遊戲客戶端 | Unity專案的`bundleVersion` |
| `sv` | `sdk version` | 作為庫的SDK，按其公開API遵循semver | `SdkVersion.Value` |
| `mg` | `model generation` | 模型格式，每個域一個代 | 每個根上的`[ModelGeneration]`，`ModelGenerations.Current` |

當前版本：`gv {{v:version.gv}}`、`sv {{v:version.sv}}`、`mg {{v:version.mg}}`

`gv`和`sv`的數字不必互相跟隨，但大多數情況下是一致的。版本會一起提升，共同的更新使用同一個版本號

各部分的含義：
- `gv`：major是全域性更新（劇情、多人遊戲），minor是普通的新功能，patch是緊急修復
- `sv`，在SDK開始承諾API穩定之後：major是破壞性的API變更（刪除型別，或改變成員的簽名或含義），minor是無需任何人應對的新增，patch是不改變簽名的修復

**`mg`比其他兩個更重要**。SDK根據它決定是遷移檔案還是拒絕讀取

設定介面按這個順序並帶標記顯示全部三個：`gv {{v:version.gv}}, sv {{v:version.sv}}, mg {{v:version.mg}}`。沒有標記的話，錯誤報告裡兩個相同的數字就無法區分

以`b`加數字結尾的版本，例如`gv 1.1.0b1`，是測試版：下一個版本的測試構建，通常在Steam的測試分支上釋出。之後的正式版不帶這個字母（`gv 1.1.0`）。測試版儲存的檔案可能無法在上一個正式版中開啟

> [!warning] 警告
> 在SDK另行說明之前，`sv`跟隨遊戲，`sv 1.0.0`並不承諾API穩定。`sv`的major變化目前說明不了針對DLL編譯的程式碼是否相容

## 不是版本的數字

還有兩個數字看起來像“版本”，但並不是：
- `LevelMeta.LevelVersion`（鍵`vrs`）：作者給關卡定的版本，是`"1.0"`這樣的字串
- `BlobFormat.Generation`：`.blob`的位元組佈局。更多：[[3_blob-format]]

## 代：每個域一個整數

域是作為一個整體遷移的根。一共有21個：`Level`、`LevelMeta`、`UserSettings`、`Prefab`、`ThemeData`、`PublishProfile`等。其中也包括`Level`內部的部分：`LevelSettings`、`GameLevel`、`AudioLevel`、`LevelResources`、`LevelHints`。每個域把自己的代寫入自己封套的`g`鍵

| 常量 | 值 | 含義 |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | 完全沒有代 |
| `ModelGenerations.Test` | 0 | 用於檢驗遷移路徑的`Versions/V0`腳手架 |
| `ModelGenerations.V1_AlphaRelease` | 1 | `gv 1.0.0`釋出時的代，大多數域仍處於這一代 |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`、`LevelMeta`、`LevelStatistics`、`GameStatistics`以及新增的`Collection` |
| `ModelGenerations.Current` | 最新 | 介面和報告顯示的代 |

**代是一個數字，而不是`major.minor`**。檔案結構的變化要麼需要遷移，要麼不需要，沒有中間檔

**編號來自同一個全域性計數器**。發生變化的域取`ModelGenerations.Current + 1`，而不是自己的下一個空閒編號。正因如此，版本行中唯一的`mg`才有意義

## 新的被拒絕

每次模型變化都是新的一代。結構變化、新增欄位和新的列舉值都一樣算。因此，高於構建所知的代，就是這個構建確定從未見過的結構

例外只有一個：任何現有模型都沒有提到的全新模型，例如放在單獨檔案中的化身皮膚。它是一個新域，沒有可以遷移的來源，所以代不增加。增加的是開始引用它的那個現有模型的代

這樣的檔案完全不讀取：沒有預設值，也沒有跳過的部分。`NewerGenerationException`帶有`Domain`、`FileGeneration`和`BuildGeneration`，宿主會請玩家更新

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## 舊的遷移

改變結構的域會得到：
1. 來自全域性計數器的新代
2. 舊結構的凍結快照，位於`Versions/V<old>/`：一個帶有`[GenerateModel]`和`[ModelGeneration(domain, <old>)]`的類
3. 位於`Versions/V<old>/Migrations/`的`ModelMigration<TFrom, TTo>`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry`通過反射找到快照和遷移器，並沿著鏈一直走到當前的結構。讀取時每一次有損的替換都會記入`SerializationReport`，而不是悄無聲息

## 讀取前拒絕

`LevelMeta.MinGeneration`（鍵`min_generation`）是關卡各個域中最高的代。它在儲存時通過`LevelGenerations.Required()`計算，從不手動填寫

客戶端在開啟`level.json`之前比較它。這樣，來自未來的關卡無需讀取幾兆位元組的內容就會被拒絕。什麼都不宣告的檔案儲存`-1`

完整的決策記錄：SDK倉庫中的[VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md)
