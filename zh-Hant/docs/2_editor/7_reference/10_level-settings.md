---
title: 關卡設定
date: 2026-10-15
tags: [level_author]
---

# 關卡設定

屬於關卡本身的一切都在這裡設定：長度、fps、種子、方向、後設資料、釋出。關卡也是從這裡啟動、按規則檢查和從副本恢復的

## 遊玩

啟動選項**只對這一次執行**有效。這裡的任何設定都不會儲存到關卡中

`{{ui:settings_level-settings_life-text}}`、`{{ui:field_common_speed}}`、`{{ui:settings_level-settings_checkpoints-toggle}}`和自動遊玩讓你無需編輯就能反覆練習某一段

> [!tip] 提示
> 這裡的`{{ui:settings_level-settings_seed}}`優先於關卡自己的種子，它是三層中的最高一層。想要重放剛剛看到的那一次執行時就用它。`0`表示使用關卡自己的種子，或每次執行都用新種子

更多：[[3_difficulty-curve]]

## 基本

幀長度、幀率和關卡的兩個種子

`{{ui:settings_level-settings_core-seed-value}}`是關卡自己的種子。它屬於內容的一部分，修改可以撤銷。`0`表示“每次執行都用新種子”。這是預設值，所以普通關卡每次玩起來都不一樣

> [!tip] 提示
> `{{ui:settings_level-settings_core-runtime-seed-value}}`只顯示當前編輯器會話實際得到的種子。`{{ui:settings_level-settings_core-runtime-seed-regenerate}}`只為本次會話換一個新的：不寫入任何內容，也不進入撤銷記錄。重新載入關卡時會再次確定種子

> [!info] 須知
> **幀是一個格子，時間是邊界**。幀從1開始計數。第*f*幀覆蓋從(*f*-1)/fps到*f*/fps的時間，不包括後者。一個N幀的關卡包含第1幀到第N幀。N+1是結束邊界，不是一幀

更多：[[4_frames-and-time]]

## 關卡方向

在這個關卡中，裝置以哪個方向握持

`{{ui:enum_level-orientation_horizontal}}`和`{{ui:enum_level-orientation_vertical}}`會在關卡進行期間轉動玩家的裝置方向。這個選擇優先於玩家的設定。顯示器無法轉動。所以在桌面上，垂直關卡會在兩側留黑邊的畫面中游玩，它本來就應該這樣顯示

`{{ui:enum_level-orientation_not-specified}}`把選擇留給玩家。它不是預設值，而是你對關卡的一個宣告：關卡在**兩種**方向下都能正確閱讀。遊戲不會為此做任何調整：不移動，不裁剪，也不縮放。超出水平邊緣的內容，在一種方向下位於螢幕之外，在另一種方向下則可見。只有在兩種方向下都檢查過關卡後，才選擇它

## 危險區域

會刪除或重寫檔案（而不是內容）的操作

> [!caution] 注意
> `{{ui:settings_level-settings_quot-level-quot-file-format}}`和`{{ui:settings_level-settings_quot-metadata-quot-file-format}}`下拉選單會重寫磁碟上的關卡及其後設資料。切換格式會**刪除舊格式的檔案**。除此之外什麼都不會發生：不重新載入，不重新模擬，你的選中項和撤銷歷史都會保留。寫入的內容與記憶體中已有的內容完全一致

> [!caution] 注意
> `{{ui:settings_level-settings_delete-level-open}}`會從磁碟上刪除關卡資料夾。這一步無法撤銷

更多：[[4_not-losing-work]]

## 規則

校驗在這個關卡中發現的問題：
- 失效的引用
- 重複的ID
- 父級迴圈
- 巢狀過深的預製件
- 重疊的節拍段

> [!info] 須知
> **部分問題可以修復，逐個修復或使用`{{ui:settings_level-settings_rules-fix-all}}`**。修復會先寫入草稿：`{{ui:editor_save_text}}`把它們作為一次可撤銷的操作應用，`{{ui:settings_level-settings_raw-discard}}`則丟棄它們。圖結構問題（ID、父級、預製件巢狀）沒有修復方案，這是有意為之：每一個都是隻有你能做的內容決定，自動修復會悄悄地從幾個有效答案中選一個

> [!tip] 提示
> 子物體的時段超出父級**不會**被報告。這是合法資料，其行為符合設計。如果你確實想讓生命週期相互適配，請從生成器中執行`{{ui:mod_span_fit}}`修改器。它會把子物體收進來，或者把父級向外擴充套件

更多：[[4_not-losing-work]]

## 後設資料

關於關卡、但不屬於關卡本身的一切：名稱、描述、封面、許可證、年齡分級、難度和作者

名稱和描述按語言分別編寫，就在這裡。如果玩家的語言你沒有填寫，就會顯示你填寫的第一條

> [!info] 須知
> 這裡不需要任何翻譯鍵。關卡是內容，而不是遊戲介面的一部分

許可證和作者會隨關卡一起被分享到任何地方。正是這一點讓署名在重新上傳後依然保留

`{{ui:settings_level-settings_difficulty}}`顯示一個大的等級圖示，以及一個寫著已儲存數字和等級名稱的按鈕，例如`3 · {{ui:enum_difficulty-tier_rain}}`。按下按鈕會開啟一個選單，列出每個等級的數字和圖示：`0`是`{{ui:enum_difficulty-tier_undefined}}`，`1`到`{{v:difficulty.scale-max}}`是從`{{ui:enum_difficulty-tier_auto}}`到`{{ui:enum_difficulty-tier_singularity}}`的各個等級

預設值是`{{ui:enum_difficulty-tier_undefined}}`，此時玩家看不到圖示。重新發布關卡的稽核員可以覆蓋這個等級。它始終只是一個值，而不是兩個。大於`{{v:difficulty.scale-max}}`的值會在按鈕上顯示它自己的數字和`{{ui:enum_difficulty-tier_singularity}}`，並按原樣保留，直到你選擇其他等級

更多：[[2_metadata-and-sharing]]

## 關卡標籤

標籤是你自己的詞語。它們按你寫的樣子原樣顯示，從不翻譯。玩家在關卡瀏覽器中按標籤篩選關卡

用逗號分隔標籤。保持簡短而通用：一種型別、一種氛圍、一種機制。只有其他關卡也在用的標籤才有幫助。沒有別人會輸入的標籤什麼也篩選不出來

## 合集

把合集中的資源匯入關卡，或用關卡自己的資源生成合集。這個標籤頁緊跟在`{{ui:editor_library_kind-prefabs}}`之後

- `匯入`：開啟一個合集，勾選條目，按`匯入`。依賴會一併帶上，整個匯入是一次撤銷步驟
- `{{ui:editor_collections_mode-build}}`：勾選關卡的資源，按`{{ui:editor_collections_build}}`，目標是`{{ui:editor_collections_target-new}}`或你自己的某個合集

如果關卡中已有某個條目的不同版本，會開啟`{{ui:editor_resource-conflict_title}}`視窗。不會悄悄覆蓋任何內容

更多：[[16_library-and-collections]]

## 釋出

關卡發往任何地方的唯一入口：壓縮包或Steam創意工坊

`{{ui:editor_share_destination}}`選擇傳送去向。下方是該方式自己的控制元件、它的報告和執行按鈕。報告會自動檢查關卡，沒有專門的檢查按鈕。錯誤會阻止執行，警告和建議不會

更多：[[17_publishing]]

## 歷史

本次會話中的每次編輯都是這裡的一行。最新的在最上面，就像`git log`

最左邊一列是主線。單獨的一列是分支。它是你撤銷某次編輯後換了另一條路時留下的那條線

圓環標出你當前的位置。綠色圓點標出上次儲存

點選某一行，關卡會回到那個確切的狀態。回退每幀執行一個操作。所以你能看著關卡變化，而不是對著一個卡住的螢幕等待

> [!warning] 警告
> 回退進行期間編輯器處於只讀狀態。你仍然可以移動相機和拖動播放頭，但不能編輯。取消會讓回退停在當前位置，而那始終是關卡的一個真實狀態

> [!tip] 提示
> 歷史只存在於當前會話中。它從不寫入磁碟，重新開啟關卡時會從頭開始。它的大小有限：最先丟棄最舊的廢棄分支，然後是最舊的編輯

## 原始資料

整個儲存的關卡模型，呈現為一棵欄位樹。它就是檔案本身，在編輯器處理之前的樣子

> [!caution] 注意
> **這裡的任何內容都不做校驗**。這是其他介面還沒有覆蓋到的內容的應急出口。它會寫入編輯器其他部分認為不可能的值

欄位旁邊的實心圓點表示你在本次會話中修改了它。空心圓點表示它內部有內容被修改。沒有它，一個摺疊分支中深三層的修改就無法被看到

沒有可應用的內容時，`{{ui:settings_level-settings_raw-apply}}`按鈕會被隱藏，而不是停用。空的應用會毫無理由地把一次關卡替換推入撤銷棧

更多：[[4_not-losing-work]]
