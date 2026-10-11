---
title: 釋出
date: 2026-10-11
tags: [level_author]
---

# 釋出

關卡只能從關卡設定的“釋出”標籤頁傳送：以壓縮包形式或釋出到Steam創意工坊。報告會自動檢查關卡，其中的錯誤會阻止傳送

## “釋出”標籤頁

`釋出`是關卡設定中的一個標籤頁。這是關卡發往任何地方的唯一入口

頂部的`{{ui:editor_share_destination}}`顯示當前選擇的傳送方式。按下它會開啟`{{ui:editor_share_pick-title}}`：列出此版本在當前裝置上提供的方式，每種都有一行說明。預設選擇`{{ui:editor_share_archive}}`。上次的選擇會一直保留到關閉遊戲

下方有：
- 該方式自己的設定
- 它的報告
- 執行按鈕：`{{ui:editor_share_export}}`或`釋出`

如果此版本在當前裝置上沒有任何方式，標籤頁會顯示`{{ui:editor_share_none}}`

## 報告

報告會自動檢查：開啟某種方式時，以及它的任何設定發生變化時。沒有專門的檢查按鈕。報告以`錯誤：N，警告：N，建議：N`這一行開頭，之後每個發現一行

錯誤會阻止執行。警告和建議由你自己決定

評估關卡所用的規則由方式決定。`{{ui:editor_share_archive}}`按`{{ui:editor_publish_profile-local}}`規則檢查，`{{ui:editor_share_steam}}`按創意工坊規則檢查。每套規則的要求和每種結論的含義：[[5_publish-readiness]]

## 傳送方式

| 方式 | 在哪裡可用 | 傳送什麼 |
|---|---|---|
| `{{ui:editor_share_archive}}` | 任何有儲存對話方塊的裝置。iOS上沒有 | 關卡、合集或單個資源，作為一個檔案 |
| `{{ui:editor_share_steam}}` | 僅限Steam版本 | 關卡或你自己的合集 |

此版本或此裝置沒有的方式不會出現在列表中

## 壓縮包

對於關卡：

| 元素 | 作用 |
|---|---|
| `{{ui:editor_share_format}}` | 七種匯出模式之一，從普通資料夾到帶密碼的壓縮包 |
| `{{ui:editor_share_passphrase}}` | 只在受保護的模式下可見。密碼為空時，受保護的模式無法執行 |
| `{{ui:editor_share_export}}` | 把關卡寫到你指定的位置 |

每種模式寫出什麼、用什麼開啟：[[13_export-and-protection#匯出關卡]]

對於合集或單個資源，`{{ui:editor_share_format}}`提供其中的五種模式，全部是歸檔包。沒有資料夾模式：

| `{{ui:editor_share_format}}` | 得到什麼 | 用什麼開啟 |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_zip}}` | 一個檔案 | 在Windows資源管理器中雙擊，無需安裝任何軟體 |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | 帶內建AES-256加密的zip | 7-Zip或其他壓縮軟體，它會要求輸入密碼 |
| `{{ui:settings_level-settings_export-mode_zip-protected}}` | 整個zip外面再包一層OpenPGP | gpg |
| `{{ui:settings_level-settings_export-mode_targz}}` | 一個檔案 | 任何壓縮軟體 |
| `{{ui:settings_level-settings_export-mode_targz-protected}}` | tar.gz外面再包一層OpenPGP | gpg |

三種帶密碼的模式會顯示`{{ui:editor_share_passphrase}}`。密碼為空時不會匯出任何內容。適用下文的合集檢查，同樣按`{{ui:editor_publish_profile-local}}`規則

## Steam創意工坊

僅限Steam版本。元素：

| 元素 | 作用 |
|---|---|
| `{{ui:editor_publish_visibility}}` | 誰能看到物品：`{{ui:editor_publish_visibility-public}}`、`{{ui:editor_publish_visibility-friends-only}}`或`{{ui:editor_publish_visibility-private}}`。預設是`{{ui:editor_publish_visibility-private}}` |
| `{{ui:editor_publish_changelog}}` | 這次上傳的更新說明。多行輸入框，標題單獨佔一行 |
| `標題和描述使用的語言` | 物品文本取自哪種語言（見下文） |
| `{{ui:editor_share_steam-descriptors}}` | 五個核取方塊，即Steam自己的內容描述符（見下文） |
| `釋出` | 上傳關卡 |

關卡始終按創意工坊規則檢查。這裡沒有規則可選

創意工坊物品的內容取自關卡：
- 標題和描述就是關卡的名稱和描述，使用同一種語言
- 預覽圖是關卡封面，png或jpg格式，不超過1 MB。其他任何封面都會被跳過，物品上傳時不帶圖片
- 標籤由遊戲自動設定，見下文“創意工坊標籤”

第一次按`釋出`會建立物品。之後再按會更新同一個物品。遊戲在你釋出過的物品中按關卡自己的id找到它，所以關卡里不儲存任何東西

受保護的關卡不能釋出。更多：[[13_export-and-protection]]

上傳內容包含關卡的`ai`資料夾（AI助手在其中儲存它對關卡的筆記），除非在關卡後設資料中取消勾選了`{{ui:settings_level-settings_metadata-level-ai-share}}`。每個訂閱者都會隨關卡一起得到它。更多：[[7_ai-assistant#ai資料夾]]

> [!warning] 警告
> 如果你還沒有接受Steam創意工坊法律協議，物品會上傳，但保持隱藏。請在物品頁面上接受協議。遊戲會在Steam疊加層中開啟該頁面

### 標題語言

Steam每個物品只顯示一個標題和一個描述。遊戲按以下順序查詢，取第一個找到的語言：
1. `{{ui:settings_game-editor_title}}`設定中的`{{ui:settings_game-editor_publish-language}}`：`{{ui:enum_publish-language_english}}`（預設）或`{{ui:enum_publish-language_system}}`，即裝置的語言。更多：[[14_editor-settings]]
2. 你自己的語言，即遊戲介面的語言
3. 英語
4. 文本最初編寫時使用的第一種語言

描述會先按標題的語言查詢，使兩者一致。未本地化的名稱（普通文本）會按原樣上傳，這一行顯示`{{ui:editor_share_steam-language-as-written}}`

### 內容描述符

`{{ui:editor_share_steam-descriptors}}`下有五個核取方塊，即Steam自己的內容描述符：
- `{{ui:editor_share_steam-descriptor-mature}}`
- `{{ui:editor_share_steam-descriptor-violence}}`
- `{{ui:editor_share_steam-descriptor-some-nudity}}`
- `{{ui:editor_share_steam-descriptor-frequent-nudity}}`
- `{{ui:editor_share_steam-descriptor-adult-only}}`

它們隨每次釋出一起傳送，從不儲存在關卡中。每次釋出都會發送完整的一組，所以取消勾選某一項，也會把該描述符從已釋出的物品上移除。它們在上傳完成後緊接著通過第二次更新發送。如果這一步失敗，物品仍然已釋出，結果會說明描述符沒有設定

### 釋出之後

成功時，表單顯示建立或更新了哪個物品，以及`{{ui:editor_publish_open-item}}`按鈕。它會在Steam中開啟該物品的頁面

失敗時，表單顯示：
- 用通俗語言說明的原因，`釋出失敗：...`
- `傳送的內容和 Steam 的回覆：...`，這是一行英文技術資訊。報告問題時值得把它原樣發給開發者
- 一個`?`，展開後說明Steam為什麼這樣拒絕，並附三個連結：`{{ui:editor_publish_help-docs}}`（本頁）、`{{ui:editor_publish_help-steam-support}}`和`{{ui:editor_publish_help-agreement}}`

遊戲自己關於釋出的日誌行始終是英文，與介面語言無關

| 原因 | 怎麼辦 |
|---|---|
| `{{ui:enum_workshop-failure_steam-not-running}}` | 啟動Steam，然後從Steam重新啟動遊戲 |
| `{{ui:enum_workshop-failure_not-owner}}` | 用那個賬戶釋出，或複製一份關卡，這樣它會作為新物品上傳 |
| `{{ui:enum_workshop-failure_access-denied}}` | 賬戶沒有這款遊戲、賬戶受限（還沒有在Steam消費過）或該賬戶無法使用創意工坊 |
| `{{ui:enum_workshop-failure_invalid-param}}` | 遊戲的創意工坊沒有設定為接受上傳，或Steam以另一款遊戲的id執行。請重啟Steam和遊戲 |
| `{{ui:enum_workshop-failure_limit-exceeded}}` | 刪除你的創意工坊檔案中的舊物品 |
| `{{ui:enum_workshop-failure_connection}}` | 檢查網路連線和Steam狀態 |
| `{{ui:enum_workshop-failure_invalid-request}}` | 標題最多128個字元，描述最多8000個字元，預覽圖為不超過1 MB的png或jpg |
| `{{ui:enum_workshop-failure_staging}}` | 檢查磁碟剩餘空間，並確認關卡檔案沒有被其他程式開啟 |

如果新物品已建立，但它的上傳被拒絕，遊戲會刪除這個空物品，不會在創意工坊留下被遺棄的物品

## 沒有Steam的版本

沒有Steam的版本不會在列表中顯示`{{ui:editor_share_steam}}`。`{{ui:editor_share_archive}}`仍然可用

## 如何分享合集

合集從“庫”標籤頁中它的頁面分享。`{{ui:editor_share_share}}`會在視窗中開啟同樣的面板：`{{ui:editor_share_archive}}`，在Steam版本中，你自己的合集還有`{{ui:editor_share_steam}}`

合集的檢查項：
- 有名稱
- 指定了許可證
- 不為空
- 它列出的每個檔案都在其中
- 它的條目引用的每個資源都已包含在內

缺少許可證的後果取決於方式。對`{{ui:editor_share_archive}}`來說這是警告，匯出照常進行。對`{{ui:editor_share_steam}}`來說這是錯誤。錯誤會阻止執行。關於合集的更多內容：[[16_library-and-collections]]

## 如何分享單個資源

“庫”中每一行主題、形狀、特效和預製件也都有`{{ui:editor_share_share}}`按鈕。它會把該資源連同它需要的一切（例如預製件的形狀、紋理和巢狀預製件）打包成只有一個條目的合集

只提供`{{ui:editor_share_archive}}`，格式與合集相同，共五種，包括帶密碼的格式。接收者通過`{{ui:editor_library_import-archive}}`匯入該檔案，和匯入任何合集一樣

## 創意工坊標籤

標籤由遊戲自動設定：

| 物品 | 標籤 |
|---|---|
| 關卡 | `level` |
| 合集 | `collection`，外加其中每一類各一個：`prefabs`、`themes`、`shapes`、`effects` |

紋理、字型和音訊沒有標籤，也不會單獨進入創意工坊。它們作為合集中預製件、主題、形狀和特效所使用的內容，隨合集一起上傳。只包含媒體的合集會被拒絕，並顯示原因，這種合集最好以壓縮包形式分享

> [!info] 須知
> Steam自己的“合集”是創意工坊物品的精選列表，是Valve的功能。它們與Bullet Hero的合集毫無關係

## 訂閱

Steam版本會讀取你訂閱的內容：
- 關卡出現在關卡列表的`{{ui:editor_library-source_workshop}}`中，[[2_playing-levels]]
- 合集出現在編輯器的庫中`{{ui:editor_library-source_workshop}}`標籤下，只讀

接下來：[[5_publish-readiness]]、[[1_licensing-basics]]、[[16_library-and-collections]]
