---
title: 公共伺服器及其擴充套件
date: 2026-10-02
tags: [server_advanced]
---

# 公共伺服器及其擴充套件

公共伺服器已經可以使用開源SDK：與客戶端相同的模型和檢查可以脫離Unity構建。協議、伺服器API和稽核工具目前尚未確定

> [!warning] 警告
> 目前還沒有伺服器程式碼和協議。下面介紹的是伺服器將要依託的那部分SDK，它已經可以工作。這裡沒有地址、訊息格式和伺服器本身的API，因為它們還不存在

## SDK可以在伺服器上執行

SDK是遊戲的開源資料模型：模型、序列化為JSON和二進位制格式、校驗規則、生成器。Unity編譯的同一份原始碼可以脫離引擎構建為普通的`netstandard2.1`庫。伺服器或工具程式可以引用它：

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

包名為`BulletHero.SDK`。程式碼位於[github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk)，採用MIT許可證

SDK的版本通常與遊戲版本一致，目前還不承諾API穩定。更多：[[5_versioning]]

**客戶端和伺服器在同樣的模型上執行同樣的檢查**。編輯器認為已就緒的關卡，對伺服器來說也已就緒。不存在需要保持一致的第二套規則

## ValidateForPublish

一次呼叫回答“這個關卡能否在這裡釋出”：

```csharp
new ValidationFacade().ValidateForPublish(meta, profile, level, now, payload)
```

它一次執行三遍檢查：

1. 針對關卡及其後設資料的宣告式規則
2. 關卡圖的檢查
3. 服務在自己的`PublishProfile`中設定的條件

**關卡本身可以不傳入**。`metadata.json`是單獨的檔案，這樣目錄無需開啟任何一個關卡就能評估成千上萬個關卡。這一遍低成本的檢查覆蓋了大部分策略

但有兩項檢查需要`level.json`：完全沒有記錄的資源，以及資源的獲取方式。只根據後設資料得到的乾淨報告意味著“已讀取的部分沒有錯誤”。在關卡檔案檢查之前，`IsReady`保持為`false`

`payload`攜帶測得的大小：每個資源、`level.json`、`metadata.json`以及整個關卡的大小。沒有它，就無法檢查配置的大小限制

檢查期間不修復任何東西，這是有意為之。在輸出端悄悄修改內容，是服務最不需要的。更多：[[6_validation]]

## 三種結論

| 組 | 含義 | 伺服器做什麼 |
|---|---|---|
| `Error` | 服務拒絕 | 拒絕上傳（`HasErrors`） |
| `Warning` | 可以釋出，但需要人工檢視 | 把關卡放入稽核佇列（`NeedsManualReview`） |
| `Advice` | 已記錄 | 不做任何事 |

客戶端在上傳開始之前就會因同樣的錯誤阻止上傳。會被你的伺服器拒絕的關卡很少能到達伺服器

## 自己的PublishProfile

服務的策略是一個檔案，即序列化的SDK模型。更嚴格或更寬鬆的伺服器只是另一個檔案，而不是程式碼的分支

**留在玩家裝置上的關卡完全不檢查**。配置只在關卡提交給服務的那一刻才起作用。作者如何為這一刻準備關卡：[[5_publish-readiness]]

預設：

| 預設 | 鍵 | 用途 |
|---|---|---|
| `CreateOpen()` | `local` | 裝置上的關卡，沒有任何要求 |
| `CreateStandard()` | `standard` | 公共伺服器，策略來自[[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | 商店版，不允許直接連結，每個資源都要有雜湊 |

主要欄位：

| 欄位 | 決定什麼 |
|---|---|
| `AllowedLicenses` | 接受哪些典型許可證，空列表表示全部接受 |
| `AllowedUriTypes` | 資源可以通過哪些方式獲取，空列表表示允許所有方式 |
| `AllowUnknownLicense` | 資源能否對自己的條款什麼都不說明 |
| `AllowPermissionInstead` | 權利人的許可能否代替被拒絕的許可證（總是送去稽核） |
| `RequireResourceMeta`、`RequireResourceUrl`、`RequireAttribution` | 每個資源的記錄必須包含什麼 |
| `RequireAgeRating`、`RequireLevelAuthors`、`RequireHashes` | 關卡必須宣告什麼 |
| `MaxResourceBytes`、`MaxDataFileBytes`、`MaxTotalBytes` | 大小限制，零表示不限制 |
| `Sources`、`UnknownSourceTrust` | 可信網站列表，以及如何評級列表之外的網站 |

兩個公共預設：

| | `standard` | `strict` |
|---|---|---|
| 資源的直接連結 | 允許 | 禁止 |
| 每個資源註明作者 | 不要求 | 要求 |
| 每條記錄中的內容雜湊 | 不要求 | 要求 |
| 最大的資源 | {{v:publish.standard.max-resource-mb}}MB | {{v:publish.strict.max-resource-mb}}MB |
| 最大的`level.json`或`metadata.json` | {{v:publish.standard.max-data-file-mb}}MB | {{v:publish.strict.max-data-file-mb}}MB |
| 最大的關卡 | {{v:publish.standard.max-level-mb}}MB | {{v:publish.strict.max-level-mb}}MB |
| 列表之外的網站 | `RequiresLicenseCheck` | `RequiresResourceCheck` |

全部預設和欄位：[[7_publish-profiles]]

### 為什麼standard中沒有GPL

`standard`中特意不包含GPL系列許可證。通過App Store分發的GPL作品與Apple的條款衝突。允許它們的目錄以後就無法在iOS上提供

> [!info] 須知
> SDK自帶的可信網站列表只是一個起點。網站會改變自己的條款，所以每個伺服器所有者都應當在自己的配置中覆蓋它。任何東西都不能指望某個特定網站一定在列表中

## 稽核

官方伺服器計劃在檢查之上增加的內容。公共伺服器很可能也需要這些：

- **稽核佇列**。由`Warning`組的問題填充
- **舉報和封禁**關卡與使用者。Google Play和App Store的規則對任何其他人能看到的內容都要求這兩項
- **按雜湊刪除**。資源記錄可以以`sha256:<hex>`的形式儲存其檔案的內容雜湊。舉報會指明某件作品，有了雜湊，包含它的每個關卡都能通過搜尋找到，而不是靠名稱猜測。編輯器在匯入資源時記錄雜湊
- **使用條款**。它們涵蓋許可證沒有涵蓋的內容：作者宣告自己擁有權利，伺服器所有者刪除關卡的權利，在列表中顯示關卡名稱和封面的權利

**Steam創意工坊的方式不同**。檔案由Valve儲存，Bullet Hero一側沒有稽核佇列。遊戲在上傳前檢查關卡或合集，出現錯誤就阻止上傳：[[17_publishing]]。釋出之後，遊戲只決定從中下載哪些內容

## 歸檔包格式

關卡是一個裝有檔案的資料夾，歸檔包讓它便於攜帶。SDK讀取和寫入的格式：

| 格式 | 讀取 | 寫入 | 說明 |
|---|---|---|---|
| `.tar.gz` | 是 | 是 | 預設 |
| `.zip` | 是 | 是 | 可以按條目用AES-256加密 |
| `.tar.gz.gpg`、`.zip.gpg` | 是 | 是 | 帶密碼的OpenPGP訊息，是`.tar.gz`唯一可用的保護方式 |
| `level.json.gpg` | 是 | 是 | 單個受保護的關卡檔案 |
| `.7z` | 否 | 否 | 識別它是為了用清楚的名稱拒絕 |

格式根據檔案開頭的位元組判斷，而不是根據副檔名。名稱是檔案中唯一任何人都能修改的部分

`tar -xzf`、`gpg -d`和任何zip壓縮工具都能開啟所有寫入的格式。解壓關卡不需要遊戲。更多：[[4_archives]]

## 尚未確定的事

- 遊戲與伺服器之間的協議，以及OWS和NOWS是否使用同一個協議
- 伺服器API：上傳、目錄、搜尋、賬號
- 如何讓遊戲指向社群伺服器
- 伺服器本身如何擴充套件，用什麼語言擴充套件
- 在伺服器上一起遊玩：傳輸、權威、關卡同步和大廳

關於一起遊玩，只想清楚了一件事：玩家的化身如何根據網路訊息出現和消失

向任何服務釋出關卡的功能最早也要在`gv 1.0.0`之後的更新中出現。檢查所依賴的資料必須在關卡釋出之前就進入關卡

## 關卡許可證與任何伺服器

關卡預設以*CC BY-NC*釋出，作者可以在關卡後設資料中選擇其他許可證。分享關卡的許可直接從作者授予每位接收者。所以任何伺服器，無論官方還是社群，都不能以商業方式託管*CC BY-NC*下的關卡

採用不同程式碼和不同許可證的伺服器，不會改變內容的任何權利。面向作者的完整規則：[[ugc-licensing-policy]]
