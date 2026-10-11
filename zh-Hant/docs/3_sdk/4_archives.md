---
title: 歸檔包與保護
date: 2026-10-01
tags: [developer, level_author]
---

# 歸檔包與保護

關卡可匯出為資料夾、tar.gz或zip，並可選擇加密碼：AES-256加密的zip或OpenPGP。SDK根據收到檔案的開頭位元組判斷格式，而不是根據檔名

## 匯出模式

關卡以`LevelExportMode`的某種形式離開裝置：

| 值 | 模式 | 寫出什麼 | 保護 |
|---|---|---|---|
| 0 | `Folder` | 普通資料夾，與磁碟上的結構相同 | 無 |
| 1 | `FolderProtectedLevel` | 只有`level.json.gpg`加密的資料夾 | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | 無 |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | 無 |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | 條目以AES-256加密的`<name>.zip` | zip自帶 |

數字是模式的身份，永遠不變。編輯器下拉式清單中的順序另行設定（`DisplayOrder`）

**每種格式都是開放標準**。`tar -xzf`、`gpg -d`和任何壓縮工具都能在沒有遊戲的情況下開啟它們：

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## 兩種保護方案

**`ZipEncrypted`是用密碼鎖住關卡的預設方式**。接收方有壓縮工具，但很可能沒有gpg

**OpenPGP用同一種方案鎖住文件、資料夾和歸檔包**。只有它能保護資料夾

在`FolderProtectedLevel`中，後設資料、封面和媒體檔案仍然可讀。所以關卡瀏覽器仍然能顯示卡片

內部副檔名保留在檔名中：`level.json.gpg`。`gpg -c level.json`正是這樣命名檔案的，所以無需猜測就能知道格式

## 裡面放什麼

`LevelArchiveBuilder`根據模型計算內容，而不是根據資料夾中的檔案列表。關卡沒有引用的檔案留在外面。報告會說明留下了多少這樣的檔案

關卡的引用這樣處理：
- 使用`AbsolutePath`的資源複製進歸檔包。它的引用改寫為`LevelPath`，但只在匯出的副本中改寫
- `DirectUrl`保持原樣並記入報告：URL無法放在檔案裡一起帶走
- 缺失的檔案以程式碼`archive.resource_missing`記入報告

## 按位元組識別

檔名誰都能寫。所以`ArchiveFormatSniffer`根據開頭的8個位元組判斷：

| 開頭位元組 | 格式 |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`、`50 4B 05 06`、`50 4B 07 08`、`50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| OpenPGP資料包標籤，最後檢查 | `OpenPgp`：解密後重新識別 |

> [!warning] 警告
> `.7z`既不讀取也不寫入。識別它只是為了讓拒絕資訊能說出它的名稱（`Unsupported`）。這樣使用者會把關卡重新打包成zip，而不是認為檔案壞了

## 讀取

`LevelArchiveReader.ReadAsync`接受資料夾或支援定位的`Stream`。它返回`LevelArchiveContent`，其中`LevelArchiveOpenResult`是以下值之一：

| 結果 | 含義 |
|---|---|
| `Ok` | 已讀取 |
| `PassphraseRequired` | 沒有密碼，需要詢問 |
| `WrongPassphrase` | 使用者已經輸入了密碼，但密碼錯誤 |
| `Damaged` | 檔案已損壞 |
| `NotAnArchive` | 這不是歸檔包 |
| `Unsupported` | 格式已識別，但不受支援 |

`PeekMetaAsync`只讀取後設資料，用於卡片或目錄

伺服器讀取的是別人決定上傳的任何東西。所以讀取器在`ArchiveLimits`的限制內工作。預設限制為：
- 4096個條目
- 每個條目512MiB
- 總計1GiB

任何內容都不會解壓到分配給它的儲存之外

編輯器一側的匯出：[[13_export-and-protection]]
