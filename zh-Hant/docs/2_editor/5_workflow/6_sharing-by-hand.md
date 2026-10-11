---
title: 如何手動分享關卡
date: 2026-10-01
tags: [level_author]
---

# 如何手動分享關卡

把關卡資料夾打包成zip或tar.gz，需要密碼時用gpg加密。在另一臺電腦上解包後的關卡可以直接遊玩，遊戲也能自己讀取這類歸檔包

關卡就是一個裝著檔案的資料夾。歸檔包是為了傳送而打包好的同一個資料夾。關卡用到的一切都隨它一起傳送：歌曲、圖片、封面

接收方要把關卡放在哪裡：[[2_metadata-and-sharing#現在如何分享關卡]]

## 不會進入歸檔包的內容

- 關卡通過連結獲取的資源。連結保持原樣
- 關卡中沒有任何地方引用的檔案

遊戲的匯出報告會列出這兩類內容。更多：[[13_export-and-protection#匯出關卡]]

## 五種形式

每一種都能用對方已有的工具開啟：

| 檔案 | 內容 | 開啟方式 |
|---|---|---|
| `level.json.gpg` | 僅關卡文件，有密碼保護，位於關卡資料夾中 | gpg |
| `LEVEL_FOLDER.tar.gz` | 整個資料夾打成一個歸檔包 | 7-Zip、Keka、Ark、資源管理器 |
| `LEVEL_FOLDER.tar.gz.gpg` | 同一個歸檔包，加了密碼 | gpg |
| `LEVEL_FOLDER.zip` | 同一個資料夾，打成zip | Windows上雙擊即可，不需要安裝任何東西 |
| `LEVEL_FOLDER.zip.gpg` | 同一個zip，加了密碼 | gpg |

預設情況下，遊戲用zip自身的手段為歸檔包設定密碼，即AES-256。除資源管理器外，任何解壓軟體都能開啟這樣的歸檔包：它會要求輸入密碼。`.gpg`形式由遊戲按需寫出

## 執行命令之前

替換命令中的兩處：
- `LEVEL_FOLDER`：關卡資料夾的名稱，也就是它的ID。這是一個由數字和字母組成的長字串，即`levels`中那個資料夾的名稱
- `YOUR_PASSWORD`：密碼本身

寫在命令列裡的密碼會留在shell歷史記錄中。從命令中去掉`--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD`，gpg就會在螢幕上要求輸入密碼

## 用gpg處理關卡文件

加密會在原檔案旁邊放一個`level.json.gpg`。原檔案留在原處：確認結果後自己刪除它。解密會再次按原來的名字寫出文件。加密檔案不會消失：

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## tar.gz歸檔包

資料夾從內部打包：歸檔包裡直接是關卡檔案，外面沒有套一層資料夾。解包時目標資料夾必須已經存在，tar不會建立它。`mkdir`在cmd、PowerShell以及Mac或Linux的終端中用法都一樣：

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

一步完成打包和加密。未加密的歸檔包根本不會落到磁碟上。第二行把歸檔包解密並解包回同一個資料夾：

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## zip歸檔包

在Windows上用PowerShell，每臺電腦上都有。星號打包的是資料夾的內容，而不是資料夾本身。`Expand-Archive`會自己建立資料夾，不需要提前`mkdir`：

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

在Mac或Linux上用zip和unzip：

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

7-Zip開啟時會要求輸入密碼的zip，由7-Zip自己製作。它必須已經安裝：

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## 遊戲也能讀回它們

所有形式都是雙向的。遊戲寫出的檔案，gpg、tar和zip都能開啟。gpg、tar和zip製作的檔案，遊戲都能讀取。正因如此才選擇了標準工具，而不是自己的格式

> [!tip] 提示
> 遊戲看的是檔案實際是什麼，而不是它叫什麼。所以改過名的歸檔包照樣能開啟。遊戲能識別`7z`，但不接受它：遊戲會說出格式名稱，而不是宣佈檔案已損壞。請把這樣的歸檔包重新打包成zip

> [!caution] 注意
> **忘記的密碼無法找回**。金鑰不儲存在任何地方：不在遊戲裡，不在檔案裡，也不在任何人手裡。沒有重置，沒有恢復，也沒有繞過的辦法。密碼丟失，關卡也隨之丟失。關閉編輯器之前先把密碼記下來

接下來：[[4_level-folder-and-backups|關卡資料夾與備份]]、[[4_not-losing-work|避免丟失工作]]
