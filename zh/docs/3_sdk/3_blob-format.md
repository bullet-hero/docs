---
title: Blob格式
date: 2026-09-24
tags: [developer]
---

# Blob格式

.blob文件的字节布局：24字节的文件头、它的检查顺序以及其中的封套

`.blob`保存的数据与`.json`相同，只是二进制形式。它是与JSON平等的关卡格式，而不是缓存：关卡可以只保存为`.blob`

| 关卡`volcano`，19341个物体 | 大小 |
|---|---|
| `level.json` | 15.7 MB |
| `level.blob` | 5.1 MB，读取耗时203毫秒 |

`.blob`不保证的是可读性。它无法用眼睛读，也无法做diff，所以它在任何地方都不是默认格式

每个模型的编解码器都由Roslyn生成器产生

## 文件头

| 偏移 | 大小 | 字段 | 值 |
|---|---|---|---|
| 0 | 4 | magic | `uint` `0x4F424842`，字节为`42 48 42 4F`（`BHBO`） |
| 4 | 2 | 编解码器代 | `ushort`，`BlobFormat.Generation` = 1 |
| 6 | 2 | 标志 | `ushort`，第0位`FlagHashed` = 存在哈希。其余各位保留，必须为0 |
| 8 | 8 | 载荷长度 | `long` |
| 16 | 8 | 哈希 | `ulong`，载荷的xxHash64，以编解码器代作为种子 |

文件头长度为`BlobFormat.HeaderLength` = 24字节，载荷紧随其后

## 检查顺序

`BlobFormat.ReadHeader`按固定顺序检查文件头。文件头通过之前不分配任何内存：
1. magic
2. 编解码器代等于1
3. 没有设置未知标志
4. 声明的长度等于实际长度
5. 若设置了`FlagHashed`，哈希一致

每种失败都是带有各自消息的`BlobFormatException`。“文件已损坏”和“文件来自更新的构建”要求玩家做的事不同，所以从不合并为一个错误

哈希有意不采用加密哈希。它负责发现损坏，防伪造是OpenPGP层的职责。更多：[[4_archives]]

## 编码

- 小端序，定宽数字，不用varint
- 字符串是`int`字节数加上UTF-8内容
- `null`用长度`-1`表示。因此空列表和缺失的列表在往返之后仍能区分
- 多态值以一个字节的标签开头，`0xFF`保留给`null`。标签是模型的`GetModelType()`，与JSON在`[tag, payload]`中写入的判别值相同
- 从文件读出的数量先经`BlobReader.ReadCount`检查，然后才为它分配内存

## 封套和两种代

每个标有`[ModelGeneration]`的根都写入自己的封套：以字符串表示的域、`int`形式的模型代、内容长度，然后是内容本身。工具这样读取文件的代：

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

这里有两种不同的代：
- 文件头中的**编解码器代**描述字节布局。它一变，所有旧的`.blob`都整个无法读取：没有可回退的东西
- 每个封套中的**模型代**描述一个域的结构。旧的会迁移，新的会以`NewerGenerationException`拒绝。更多：[[5_versioning]]

两者不能合并成一个数字。模型代位于封套内部，而读取方只有在已经知道字节布局时才能找到封套。模型变化从不改变编解码器代

## 扩展文件头

文件头没有备用字节，也没有记录自身长度的字段。它有两种扩展方式：
- **标志**。还有15位空闲。旧的读取方遇到不认识的标志会拒绝文件，而不是错误地读取它
- **新的编解码器代**。新布局可以改变任何东西，包括文件头长度。新的读取方可以在支持新代的同时继续读取旧代

载荷之后不能追加任何内容。声明的长度必须等于实际长度，所以任何多余的尾部都会被拒绝。新的关卡数据放进载荷内部，通过模型代来实现

> [!info] 须知
> 内容没有恰好在声明的长度处结束，无论长了还是短了，都视为损坏。有时一个根通过了所有文件头检查，却仍然解析失败。这时按它的长度跳过它，并保留默认值。这次跳过会记录在`SerializationReport`中，绝不会悄无声息
