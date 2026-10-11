---
title: 安裝
date: 2026-10-02
tags: [developer, level_author]
---

# 安裝

SDK就是nuget.org上的BulletHero.SDK包，也可以從原始碼構建。在Unity中以git submodule接入，ConsoleSmoke示例用來確認你的關卡能被讀取

SDK的程式碼位於[github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk)。許可證為MIT

## .NET

`BulletHero.SDK`包已釋出到nuget.org：`dotnet add package BulletHero.SDK`。三個依賴會隨它一起到位。如需從原始碼構建：

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

然後二選一接入：
- 從本地資料夾引用`.nupkg`：`dotnet add package BulletHero.SDK --source <folder>`。三個依賴會隨它一起到位
- 直接引用`BH.SDK.dll`。這時下面三個包需要自己新增：對DLL的引用不會帶上它的依賴

依賴全部來自NuGet：

| 包 | 版本 | 用途 |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | 為帶密碼的關卡提供OpenPGP |
| `SharpZipLib` | 1.4.2 | tar和zip（gzip來自BCL） |

### 構建細節

- 程式集名為`BH.SDK.dll`，旁邊附有XML文件
- 目標框架是`netstandard2.1`，語言是C# 9。這與Unity專案的版本相同，所以同一份原始碼既能在Unity中構建，也能脫離Unity構建
- 輸出資料夾是`bin~`和`obj~`。需要波浪號，是因為Unity不匯入名稱以波浪號結尾的資料夾

## Unity

遊戲以git submodule的方式接入SDK：

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

移除用`git rm -r -f Assets/Plugins/BH.SDK`

Unity專案需要自己提供：
- `Newtonsoft.Json`，通過`com.unity.nuget.newtonsoft-json`包
- 來自NuGet的`BouncyCastle.Cryptography`和`SharpZipLib`（遊戲用NuGetForUnity安裝它們）
- Player Settings中的指令碼宏`BHSDK_UNITY`。沒有它，`UnityIntegration`會選擇不依賴引擎的分支
- 位於SDK根目錄的`BH.SDK.Roslyn.dll`。Unity只把分析器應用到它所在資料夾的程式集以及引用該程式集的程式集。挪到別處後，它什麼也不分析

倉庫根目錄有一個`package.json`，名稱為`com.vertoker.bullet-hero-sdk`，最低Unity版本為`6000.0`。因此Package Manager也能通過git URL新增SDK。這種方式沒有使用，這裡也不介紹

## 檢查：ConsoleSmoke示例

`Samples~/ConsoleSmoke`是一個`net8.0`控制台應用。它引用構建好的`BH.SDK.dll`，和第三方工具的做法完全一樣。該應用讀取一個關卡資料夾，輸出名稱、物體數量和代。然後讓關卡經JSON和`.blob`各往返一次

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| 退出碼 | 含義 |
|---|---|
| 0 | 全部一致 |
| 1 | 引數錯誤 |
| 2 | 找不到`level.*`或`metadata.*` |
| 3 | 往返結果不一致 |
| 4 | 檔案比當前SDK新 |

在遊戲內建關卡`new-zero-demo`上的輸出（用`sv 1.0.0`錄製）：

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

下一步：[[2_level-format]]

## SDK的組成

| 部分 | 是什麼 | 是否需要Unity |
|---|---|---|
| `BH.SDK` | 核心：模型、序列化、版本、規則、校驗、歸檔包、釋出、生成器 | 否 |
| `UnityIntegration` | 一個薄層，其中每個檔案在有無Unity時都能編譯（`#if BHSDK_UNITY`），例如`Cat`日誌器 | 否：在Unity之外它直接編譯進核心 |
| `UnityExtensions` | 到Unity型別的轉換、2D變換、化身移動 | 是，始終需要 |
| `BH.SDK.Roslyn` | 分析器和原始碼生成器。它為每個帶有`[GenerateModel]`的模型編寫`Equals`、複製、JSON與`.blob`編解碼器以及校驗遍歷 | 在編譯期執行 |

模型檔案只包含它的欄位和建構函式。所有重複的部分都由生成器編寫。所以不會在七個生成的方法體中的某一個裡漏掉欄位

## 為什麼是獨立的庫

- **關卡比遊戲活得久**。關卡是一個由開放格式檔案組成的資料夾（JSON、tar.gz、zip、OpenPGP）。讀取它們的程式碼也是開源的。即使寫出關卡的遊戲不在了，關卡依然可讀
- **與其他節奏遊戲互通**。格式是公開描述的，所以可以據此編寫與其他遊戲格式之間的轉換器
- **修復更快**。格式的缺陷從外部就能看到。任何讀程式碼的人都能報告它或提交修復
- **第三方工具**。轉換器、校驗器、關卡生成器或模組使用與遊戲相同的模型。不需要從檔案中還原它們
- **伺服器**。核心不依賴Unity，以`netstandard2.1`構建。所以伺服器能在同樣的模型上執行與客戶端相同的檢查
