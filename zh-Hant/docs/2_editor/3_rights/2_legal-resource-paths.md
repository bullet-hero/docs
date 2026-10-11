---
title: 合法資源的兩種途徑
date: 2026-09-25
tags: [level_author]
---

# 合法資源的兩種途徑

資源要麼有合適的許可證，要麼有權利人的許可，才算合格。沒有第三種方式

外部資源是關卡自帶的一切：音樂、圖片、字型、文本和任何檔案。每個資源都必須滿足**兩種方式之一**

## 方式A：開放許可證

資源本身的分發條款已經不比`CC BY-NC`更嚴格。它保留自己的條款，不會變成`CC BY-NC`

標準配置接受：
- [CC0](https://creativecommons.org/publicdomain/zero/1.0/)：公有領域
- [CC BY](https://creativecommons.org/licenses/by/4.0/)，4.0和3.0版
- [CC BY-NC](https://creativecommons.org/licenses/by-nc/4.0/)，4.0和3.0版
- [MIT](https://choosealicense.com/licenses/mit/)和[Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)：用於文本和程式碼
- [SIL OFL 1.1](https://openfontlicense.org/open-font-license-official-text/)：用於字型，必須在後設資料中註明
- [Unlicense](https://choosealicense.com/licenses/unlicense/)

> [!tip] 建議
> 如果由你來選，就選`CC0`。它是唯一對關卡沒有任何要求的許可證

## 配置拒絕什麼

- **專有許可**，即“保留所有權利”
- [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/)：關卡就得以CC BY-NC-SA釋出，而關卡不是以它分發的
- [CC BY-ND](https://creativecommons.org/licenses/by-nd/4.0/)：它禁止修改，這一點遊戲不支援
- [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/)和[CC BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/)：同樣是這兩個原因

GPL系列不在列表中，儘管它比CC BY-NC更自由。GPL程式碼無法通過App Store分發而不與Apple的條款衝突。所以凡是會進入iOS版本的內容，都必須保持MIT或Apache的形式

## 配置取決於服務

接受哪些許可證由服務決定，而不是由許可證決定。上面的列表是標準配置。商店版本接受的更少，社群伺服器可能接受別的

## 方式B：權利人的許可

私下一句“行，拿去用吧”是不夠的。`CC BY-NC`的關卡會被公開分發，許可必須恰好覆蓋這一點，而不是你的個人使用

有效的許可同時給出以下三點：
1. 在Bullet Hero關卡中使用該資源的權利
2. 允許第三方通過遊戲的服務，自由、非商業地分發這個包含該資源的關卡，並署名
3. 明確限定為僅限非商業用途

如何請求許可：[[6_asking-permission]]

> [!caution] 注意
> 許可不會把拒絕變成通過。如果資源的許可證屬於被拒絕的那些，許可會把它送去人工稽核，但不會讓它變成“允許”

## 許可的範圍和期限

沒有寫明範圍或沒有證據的許可視為不完整。過期的許可完全不算數

**範圍會被記錄下來**，而且很重要：
- 針對某一個具體關卡的許可，一旦資源被複制到另一個關卡就失效
- 針對任意關卡的許可，在任何複用中都有效

接下來：[[6_asking-permission]]、[[4_resource-record]]
