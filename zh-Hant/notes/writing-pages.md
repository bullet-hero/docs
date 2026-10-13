---
title: 編寫頁面
date: 2026-10-13
tags: [contributor]
---

# 編寫頁面

頁面是開放倉庫bullet-hero/docs中的markdown檔案。修改以pull request的形式提交：fork、分支、在每種語言中修改、對照風格指南檢查

## 倉庫

專案的所有倉庫都在[bullet-hero](https://github.com/bullet-hero)組織下。開放的倉庫有：

| 倉庫 | 內容 |
|---|---|
| [bullet-hero/releases](https://github.com/bullet-hero/releases) | releases中是遊戲的每個公開構建版本，issues中是玩家反饋的關於遊戲的錯誤和建議 |
| [bullet-hero/sdk](https://github.com/bullet-hero/sdk) | SDK程式碼，issues中是關於SDK的錯誤和建議 |
| [bullet-hero/docs](https://github.com/bullet-hero/docs) | 這些頁面及其翻譯 |
| [bullet-hero/backend](https://github.com/bullet-hero/backend) | 伺服器，目前是空的 |

遊戲（`bullet-hero/game`）和網站（`bullet-hero/frontend`）的程式碼是閉源的

本頁講的是bullet-hero/docs

## 如何提交修改

1. Fork [bullet-hero/docs](https://github.com/bullet-hero/docs)並建立一個分支
2. 按下面描述的格式編輯或新增頁面
3. 在每種語言中修改該頁面，或者在pull request中說明哪些語言仍需要這項修改。更多：[[translating]]
4. 對照[[style-guide]]檢查文本
5. 發起pull request，簡要說明改了什麼以及為什麼改

**事實來自遊戲、SDK或它們的文件**。數字、欄位名、檔名、快捷鍵和地址從不靠猜。不確定某件事是否正確？在pull request裡說明，而不是寫在頁面上

被接受的修改會在幾分鐘內出現在[bullethero.space](https://bullethero.space/)上：每次推送到`master`都會重新構建網站

> [!tip] 提示
> 網站程式碼是閉源的，所以你無法自己構建網站。最接近的預覽方式是Obsidian：Obsidian找不到的連結，在網站上同樣找不到

## 倉庫如何運作

- **只有markdown**。沒有自己的構建流程，也沒有指令碼
- **它是一個[Obsidian](https://obsidian.md/)庫**。把倉庫的根資料夾作為庫開啟，連結、嵌入和預覽的效果與網站上相同。其他任何markdown編輯器也可以使用
- **它是網站的子模組**。網站把這個倉庫作為自己的`content/`資料夾引入，在構建時編譯頁面，並預渲染每一個頁面。網站從本倉庫最新的`master`構建

## 內容放在哪裡

| 路徑 | 內容 | 網站上的地址 |
|---|---|---|
| `<lang>/docs/1_game/` | 面向玩家：安裝、遊玩、設定、機制 | `/docs/game` |
| `<lang>/docs/2_editor/` | 面向關卡作者：編輯器指南和參考 | `/docs/editor` |
| `<lang>/docs/3_sdk/` | 面向開發者：開源SDK和關卡格式 | `/docs/sdk` |
| `<lang>/docs/4_server/` | 面向伺服器運營者：官方伺服器和社群伺服器 | `/docs/server` |
| `<lang>/docs/5_changelog/` | 更新日誌，每個遊戲版本一頁 | `/docs/changelog` |
| `<lang>/notes/` | 文章、社群、編輯規則、公開檔案和政策，按日期排序 | `/notes/<name>` |
| `<lang>/tags/` | 標籤頁面 | `/tags/<tag>` |
| `<lang>/download.md` | 下載頁面 | `/download` |
| `assets/` | 所有語言共用的圖片 | 嵌入到頁面中 |

`<lang>`是語言資料夾：`en`、`ru`、`zh`、`zh-Hant`、`ja`、`ko`、`es`、`pt`或`fr`。`docs/`、`notes/`、`tags/`和`download.md`之外的檔案不會成為頁面

**文件描述的是事物現在如何運作**。變更的歷史、個人觀點或隨筆是`notes/`中的筆記

## 檔名和順序

- **側邊欄中的順序由`N_`字首決定**，`docs/`內的每個檔案和資料夾都有這個字首：`1_`、`2_`，依此類推，直到`10_`及以上
- **字首不會出現在地址中**。`1_game/3_controls.md`的地址是`/docs/game/controls`
- **`index.md`沒有字首**。它是所在資料夾的首頁，佔據資料夾的位置，併為側邊欄中的分組命名
- **要調整順序，就重新命名檔案**。在Obsidian中啟用“Automatically update internal links”，它會自己修正所有連結
- **去掉字首後的名稱在同一語言內是唯一的**。如果兩個檔案對應到同一個地址，網站構建時會報告
- **帶字首的名稱在所有語言中都相同**。`en/docs/2_editor/4_craft/3_difficulty-curve.md`和`ru/docs/2_editor/4_craft/3_difficulty-curve.md`是同一個頁面
- **`notes/`沒有字首，也沒有子資料夾**。永遠不要重新命名`notes/cookie-policy`：網站上的Cookie橫幅連結到它

## Frontmatter、標題和描述

每個頁面都以這樣的內容開頭：

```md
---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

One line that says what the page is, up to 200 characters, no markup
```

- **`title`、H1和描述用頁面所屬的語言書寫**。上面的例子來自英文版
- **Frontmatter包括`title`、`date`和`tags`**。其他內容一概不讀取。`date`的格式是`YYYY-MM-DD`，是最後一次更新的日期，而不是建立日期。修改檔案時，把`date`設為修改當天
- **`# H1`是必需的，且與`title`相同**。網站只顯示頁面正文，所以H1就是可見的標題
- **H1之後的第一段是描述**，顯示在列表、搜尋和連結預覽中。它會在200個字元處截斷。把它寫成一行，不帶連結和格式。它簡短地回答頁面的問題，而不是描述頁面上有什麼，見[[style-guide#頁面開頭]]
- **章節用`##`，小節用`###`**。它們會生成錨點和目錄。不需要更深的層級

## 受眾標籤

每個文件頁面都有1到3個來自此列表的標籤。標籤用`snake_case`書寫，不帶`#`。網站會在頁面上顯示它們

| 標籤 | 網站上顯示為 | 物件 |
|---|---|---|
| `player` | [[player]] | 普通玩家 |
| `advanced_player` | [[advanced_player]] | 對機制感興趣的玩家 |
| `level_author` | [[level_author]] | 在編輯器中製作關卡 |
| `developer` | [[developer]] | 基於SDK構建東西或擴充套件遊戲 |
| `server_host` | [[server_host]] | 為自己和朋友執行伺服器 |
| `server_advanced` | [[server_advanced]] | 大型伺服器運營者，準備擴充套件或編寫伺服器 |
| `contributor` | [[contributor]] | 在本倉庫中編輯文本和翻譯 |

`notes/`中的筆記改用主題標籤，目前是`legal`（[[legal]]）

讀者看不到標籤程式碼。顯示的名稱來自標籤頁面`<lang>/tags/<code>.md`：

- 它的`title`就是名稱
- 它的第一段描述受眾
- 帶有該標籤的頁面列表由網站自動新增

新標籤需要在每種語言中都有這樣一個頁面

要在正文中提到某個標籤，就連結到它的頁面：`[[level_author]]`。連結會以讀者的語言顯示名稱

## 連結

| 目標 | 寫法 |
|---|---|
| 另一個頁面 | `[[3_difficulty-curve]]`，使用帶字首的完整檔名 |
| 頁面中的某個章節 | `[[3_difficulty-curve#Anchor]]` |
| 資料夾首頁 | `[[2_editor/4_craft/index]]`，要帶路徑，因為每個這樣的頁面都叫`index` |
| 外部網站 | `[text](https://…)`，使用帶協議的完整地址 |

連結指向不帶語言的地址，所以同一份源文本在所有語言中都能用。`[[cookie-policy]]`會把英文讀者帶到英文頁面，把俄文讀者帶到俄文頁面，把中文讀者帶到中文頁面，把日文讀者帶到日文頁面，把韓文讀者帶到韓文頁面，把西班牙文讀者帶到西班牙文頁面，把葡萄牙文讀者帶到葡萄牙文頁面，把法文讀者帶到法文頁面

只連結到已經存在的頁面。網站構建會報告每一個無法解析的連結

## 圖片

圖片放在倉庫根目錄的`assets/`中，用`![[file.png]]`嵌入

所有語言共用一個資料夾。圖片上繪製的文字不會隨頁面一起翻譯

## 標註框

| 語法 | 顏色 | 用途 |
|---|---|---|
| `> [!note]`、`> [!info]`、`> [!tip]` | 藍色 | 背景資訊、捷徑、建議 |
| `> [!warning]`、`> [!caution]` | 黃色 | 耗費時間或降低質量、毀掉成果 |
| `> [!danger]`、`> [!bug]` | 紅色 | 可以顯示，但風格指南不使用它們 |

選用哪種標註框、它的標題，以及每頁最多兩個的限制：[[style-guide]]

## 數字、版本和介面文字

由遊戲決定的數字（化身的速度、設定的預設值、大小上限）以及當前版本不直接寫進頁面。它們存放在倉庫根目錄的`values.yaml`中，頁面只寫一個佔位符，由網站在構建時填入：

- `\{{v:avatar.move-speed}}`是`values.yaml`中的值。網站按頁面語言的寫法輸出數字：英文是`0.15`，俄文是`0,15`
- `\{{ui:menu_main_sandbox-btn}}`是`game/<lang>.yaml`中的介面文字，使用頁面本身的語言
- `\{{`表示兩個普通的花括號

不存在的鍵會讓網站構建失敗，所以新數字要先加進`values.yaml`。作為歷史節點提到的版本（"從`gv 1.0.0`起"）保持為文本。Obsidian會按原樣顯示佔位符

## 程式碼和其他標記

- **程式碼高亮**只支援`ts`、`tsx`、`js`、`json`、`csharp`、`bash`、`yaml`、`css`和`md`。其他語言顯示為純文本
- **GFM表格、任務列表、腳註和`==highlights==`**都可以使用
- **不支援MDX和JSX**。`{`和`<`會原樣顯示
