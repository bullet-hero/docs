---
title: 參與SDK開發
date: 2026-10-02
tags: [developer]
---

# 參與SDK開發

SDK的問題請在bullet-hero/sdk倉庫的issues中報告，程式碼修改也以拉取請求的形式提交到那裡。貢獻者規則位於同一個倉庫中，就在程式碼旁邊

倉庫是[bullet-hero/sdk](https://github.com/bullet-hero/sdk)，預設分支為`master`

## 在哪裡報告

| 關於什麼 | 報告到哪裡 |
|---|---|
| SDK及其程式碼 | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| 遊戲：玩家的錯誤報告和建議 | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| 文件文本 | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## 規則在哪裡

貢獻者規則位於SDK倉庫本身，就在它們所描述的程式碼旁邊：

| 檔案 | 內容 |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | 依賴、關卡包、構建DLL和包、檢查示例 |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | 思維模型、資料夾索引以及整個庫的約定 |
| 每個資料夾中的`CLAUDE.md` | 該資料夾的區域性規則，例如[Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md)、[Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md)、[Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | 版本軸、代、遷移和拒絕 |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | 模型如何定址實體：Guid、int、幀、欄位路徑 |
| [[ugc-licensing-policy]]（在本網站上） | 使用者內容的許可政策，與`TrustedSourceCatalog`一起修改 |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | 如何編寫快照和遷移器 |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | 生成器約定 |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | 分析器和模型生成器，以及如何重新構建它們 |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | 雙重編譯約定 |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | 按`sv`版本列出的變更，最新的在頂部 |

## 構建和測試

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- 這裡在沒有Unity的情況下構建Unity所編譯的同一份原始碼。破壞無引擎約定的檔案會讓這次構建失敗
- 輸出到`bin~`和`obj~`
- 打包命令只生成`.nupkg`。釋出到nuget.org由倉庫的`release` workflow在推送`sv`標籤時完成

> [!caution] 注意
> 分析器和模型生成器以預先構建好的`BH.SDK.Roslyn.dll`形式放在SDK根目錄。修改`Roslyn/`中的任何內容後，請重新構建並複製它。否則舊的生成器會繼續執行，儘管原始碼已經不同

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

在Unity編輯器中，選單項**Tools > BH.SDK.Roslyn > Build Analyzer**完成同樣的操作

## 值得提前瞭解的不變數

- 核心不引用任何`UnityEngine`型別。需要引擎的程式碼放到`UnityExtensions/`，或放到`UnityIntegration/`中`#if BHSDK_UNITY`之後，並提供不依賴引擎的分支
- 程式碼對檔案和記憶體中的資料同樣適用，只使用BCL中的非同步機制
- `netstandard2.1`和C# 9是Unity專案編譯時使用的版本。不會提高它們
- 模型是`[GenerateModel] public sealed partial class`。每個可序列化欄位都從`Names.cs`中取得自己的鍵
- 任何模型變化都是帶有快照和遷移器的新一代。更多：[[5_versioning]]
- SDK版本存放在三個地方：`SdkVersion.cs`、`package.json`和`BH.SDK.csproj`中的`<Version>`。只要其中一個單獨變動，`SdkVersionAgreementTests`就會失敗
