---
title: Blob格式
date: 2026-10-01
tags: [developer]
---

# Blob格式

.blob檔案以二進位制形式儲存與.json相同的資料：24位元組的檔案頭，後面是資料。它是與JSON地位相同的關卡格式，而不是快取

關卡可以只儲存為`.blob`

| 關卡`volcano`，19341個物體 | 大小 |
|---|---|
| `level.json` | 15.7MB |
| `level.blob` | 5.1MB，讀取用時203毫秒 |

`.blob`不保證可讀性。它無法用眼睛閱讀，也無法用diff比較，所以任何地方都不預設選擇它

每個模型的編解碼器由Roslyn生成器建立

## 檔案頭

| 偏移 | 大小 | 欄位 | 值 |
|---|---|---|---|
| 0 | 4 | magic | `uint` `0x4F424842`，位元組`42 48 42 4F`（`BHBO`） |
| 4 | 2 | 編解碼器的代 | `ushort`，`BlobFormat.Generation` = 1 |
| 6 | 2 | 標誌 | `ushort`，第0位`FlagHashed` = 有雜湊。其餘位保留，必須為0 |
| 8 | 8 | 資料長度 | `long` |
| 16 | 8 | 雜湊 | `ulong`，以編解碼器的代為種子計算的資料xxHash64 |

檔案頭長度`BlobFormat.HeaderLength`為24位元組，後面是資料

## 檢查順序

`BlobFormat.ReadHeader`按嚴格的順序檢查檔案頭。檔案頭通過之前不分配任何記憶體：
1. magic
2. 編解碼器的代等於1
3. 沒有未知標誌
4. 宣告的長度等於實際長度
5. 設定了`FlagHashed`時雜湊一致

每種失敗都是帶有自己訊息的`BlobFormatException`。“檔案已損壞”和“檔案來自更新的構建”要求玩家做的事不同，所以不會合併為一個錯誤

雜湊有意不使用密碼學演算法。它用來發現損壞，防篡改由OpenPGP層負責。更多：[[4_archives]]

## 編碼

- 小端序，定寬數字，不用varint
- 字串是`int`型別的位元組數，後面跟UTF-8
- `null`是長度`-1`。因此空列表和缺失的列表在往返後仍然不同
- 多型值以一個位元組的標籤開頭，`0xFF`保留給`null`。標籤就是模型的`GetModelType()`，與JSON寫在`[標籤, 資料]`中的標記相同
- 從檔案讀取的數量在為它分配任何記憶體之前，先由`BlobReader.ReadCount`檢查

## 封套和兩種代

每個帶有`[ModelGeneration]`的根都寫入自己的封套：字串形式的域、`int`形式的模型的代、內容長度，然後是內容本身。工具這樣讀取檔案的代：

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

這裡有兩種不同的代：
- 檔案頭中的**編解碼器的代**描述位元組佈局。它一旦改變，所有舊的`.blob`都會整體無法讀取：沒有可以回退的東西
- 每個封套中的**模型的代**描述一個域的結構。舊的會遷移，新的通過`NewerGenerationException`拒絕。更多：[[5_versioning]]

二者無法合併成一個數字。模型的代位於封套內部，而只有已經知道位元組佈局的讀取方才能找到封套。模型變化從不改變編解碼器的代

## 擴充套件檔案頭

檔案頭沒有備用位元組，也沒有記錄自身長度的欄位。它有兩種擴充套件方式：
- **標誌**。還有15位空閒。舊的讀取方會拒絕帶有陌生標誌的檔案，而不是錯誤地讀取它
- **新的編解碼器的代**。新佈局可以改變任何東西，包括檔案頭長度。更新的讀取方可以在讀取新代的同時讀取舊代

資料之後不能追加任何內容。宣告的長度必須與實際長度一致，所以任何多餘的尾部都會被拒絕。新的關卡資料放進資料內部，通過模型的代來實現

> [!info] 須知
> 內容沒有恰好在宣告的長度處結束，無論長了還是短了，都算作損壞。有時一個根通過了檔案頭的全部檢查，卻仍然無法解析。這時按它的長度跳過它，它保留預設值。跳過會記錄到`SerializationReport`中，從不悄無聲息
