---
title: 釋出配置
date: 2026-10-01
tags: [developer, level_author]
---

# 釋出配置

服務用PublishProfile檔案描述自己接受哪些關卡：許可證、資源來源、必填欄位、大小限制。新增一個服務就是寫一個檔案，而不是修改分析器

## 配置就是資料

釋出配置（`PublishProfile`）是一個模型，與其他任何根一樣序列化，有自己的代

關卡可以進入Steam創意工坊、官方伺服器、社群伺服器、商店版的目錄。每個地方對同樣的問題都有自己的回答。這些回答會隨著年份變化，而程式碼不會

配置決定的內容：

| 欄位 | 含義 |
|---|---|
| `ProfileKey` | 這是哪個服務，在每份報告中重複出現 |
| `AllowedLicenses` | 服務接受的`TypicalLicenseType`值 |
| `AllowedUriTypes` | 資源可以通過哪些方式獲取。空列表表示任何方式 |
| `AllowUnknownLicense`、`AllowPermissionInstead` | 未知許可證或書面許可是否足夠 |
| `RequireResourceMeta`、`RequireResourceUrl`、`RequireAttribution`、`RequireAgeRating`、`RequireLevelAuthors`、`RequireHashes` | 哪些內容必須填寫 |
| `MaxResourceBytes`、`MaxDataFileBytes`、`MaxTotalBytes` | 大小限制，0表示不限制 |
| `Sources`、`UnknownSourceTrust` | 網站列表，以及對列表之外網站的評級 |

哪些許可證可以接受，只由配置決定。這看起來像許可證的屬性，實際上是接收方服務的屬性

## 四個內建配置

| 工廠方法 | `ProfileKey` | 用途 |
|---|---|---|
| `CreateOpen()` | `local` | 你裝置上的關卡。沒有任何要求 |
| `CreateStandard()` | `standard` | 公共伺服器 |
| `CreateWorkshop()` | `workshop` | Steam創意工坊。任何CC BY變體都能通過，缺少文件只會給出警告 |
| `CreateStrict()` | `strict` | 商店版，比`standard`更嚴格 |

| 專案 | `standard` | `strict` |
|---|---|---|
| 許可證 | CC0 1.0、CC BY 4.0和3.0、CC BY-NC 4.0和3.0、SIL OFL 1.1、MIT、Apache 2.0、the Unlicense | 同`standard` |
| 資源來源 | 關卡資料夾、遊戲內或直接連結 | 不允許連結 |
| 署名和雜湊 | - | 必需 |
| 每個資源的限制 | 64MiB | 32MiB |
| 每個資料檔案的限制 | 32MiB | 16MiB |
| 每個關卡的限制 | 256MiB | 128MiB |

> [!tip] 建議
> 不要為你的服務添加工廠方法。取四個配置之一，修改需要的欄位，然後以JSON檔案的形式提供

### 為什麼是這些許可證和大小

- GPL系列許可證不在`standard`中。通過App Store分發的GPL作品與Apple的條款衝突
- 排除CC BY-SA：ShareAlike會迫使關卡本身更換許可證
- 排除CC BY-ND：NoDerivatives禁止編輯，而遊戲正是建立在編輯之上的
- 嚴格的大小限制就是手機通過行動網路能下載的量

## 資源從哪裡來

許可證欄位說明作者聲稱了什麼。`SourceTrust`說明結合資源來源網站來看，這個宣告有多可信：

| 評級 | 結果 | 示例 |
|---|---|---|
| `Approved` | 釋出 | Kenney、ccMixter、Incompetech |
| `PartiallyApproved` | 釋出，但值得看一下這條記錄 | Pixabay、SoundImage |
| `RequiresLicenseCheck` | 對照真實頁面核對許可證 | OpenGameArt、Free Music Archive、Wikimedia Commons |
| `RequiresResourceCheck` | 先確認作品本身 | Rawpixel、itch.io |
| `NotAllowed` | 拒絕 | YouTube、SoundCloud、Spotify |
| `Unknown` | 沒有記錄，由`UnknownSourceTrust`決定 | - |

`TrustedSourceCatalog.CreateDefault()`返回25個網站。這是一份起始列表。預計每個運營者都會修改它。所以任何東西都不能依賴某條記錄一定存在

`Sources`列表為空時關閉來源評級

流媒體平臺被明確列為`NotAllowed`，而不是省略。缺失的網站通過`UnknownSourceTrust`評級，在`standard`和`strict`中這個評級要求檢查，而不是拒絕

目錄和[[ugc-licensing-policy]]描述的是同一件事，需要一起修改

## 如何處理結果

呼叫的是`ValidationFacade.ValidateForPublish`。更多：[[6_validation]]

`PublishReadinessReport`包含：
- `HasErrors`：`Error`組的問題
- `NeedsManualReview`：`Warning`組的問題
- `IsReady`

接下來怎麼做，配置不決定。客戶端在有錯誤時阻止上傳。伺服器把關卡放入稽核佇列，而不是直接釋出

作者一側的同一項檢查：[[5_publish-readiness]]
