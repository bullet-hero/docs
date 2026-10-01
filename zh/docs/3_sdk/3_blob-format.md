---
title: Blob格式
date: 2026-10-01
tags: [developer]
---

# Blob格式

.blob文件以二进制形式保存与.json相同的数据：24字节的文件头，后面是数据。它是与JSON地位相同的关卡格式，而不是缓存

关卡可以只保存为`.blob`

| 关卡`volcano`，19341个物体 | 大小 |
|---|---|
| `level.json` | 15.7MB |
| `level.blob` | 5.1MB，读取用时203毫秒 |

`.blob`不保证可读性。它无法用眼睛阅读，也无法用diff比较，所以任何地方都不默认选择它

每个模型的编解码器由Roslyn生成器创建

## 文件头

| 偏移 | 大小 | 字段 | 值 |
|---|---|---|---|
| 0 | 4 | magic | `uint` `0x4F424842`，字节`42 48 42 4F`（`BHBO`） |
| 4 | 2 | 编解码器的代 | `ushort`，`BlobFormat.Generation` = 1 |
| 6 | 2 | 标志 | `ushort`，第0位`FlagHashed` = 有哈希。其余位保留，必须为0 |
| 8 | 8 | 数据长度 | `long` |
| 16 | 8 | 哈希 | `ulong`，以编解码器的代为种子计算的数据xxHash64 |

文件头长度`BlobFormat.HeaderLength`为24字节，后面是数据

## 检查顺序

`BlobFormat.ReadHeader`按严格的顺序检查文件头。文件头通过之前不分配任何内存：
1. magic
2. 编解码器的代等于1
3. 没有未知标志
4. 声明的长度等于实际长度
5. 设置了`FlagHashed`时哈希一致

每种失败都是带有自己消息的`BlobFormatException`。“文件已损坏”和“文件来自更新的构建”要求玩家做的事不同，所以不会合并为一个错误

哈希有意不使用密码学算法。它用来发现损坏，防篡改由OpenPGP层负责。更多：[[4_archives]]

## 编码

- 小端序，定宽数字，不用varint
- 字符串是`int`类型的字节数，后面跟UTF-8
- `null`是长度`-1`。因此空列表和缺失的列表在往返后仍然不同
- 多态值以一个字节的标签开头，`0xFF`保留给`null`。标签就是模型的`GetModelType()`，与JSON写在`[标签, 数据]`中的标记相同
- 从文件读取的数量在为它分配任何内存之前，先由`BlobReader.ReadCount`检查

## 封套和两种代

每个带有`[ModelGeneration]`的根都写入自己的封套：字符串形式的域、`int`形式的模型的代、内容长度，然后是内容本身。工具这样读取文件的代：

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

这里有两种不同的代：
- 文件头中的**编解码器的代**描述字节布局。它一旦改变，所有旧的`.blob`都会整体无法读取：没有可以回退的东西
- 每个封套中的**模型的代**描述一个域的结构。旧的会迁移，新的通过`NewerGenerationException`拒绝。更多：[[5_versioning]]

二者无法合并成一个数字。模型的代位于封套内部，而只有已经知道字节布局的读取方才能找到封套。模型变化从不改变编解码器的代

## 扩展文件头

文件头没有备用字节，也没有记录自身长度的字段。它有两种扩展方式：
- **标志**。还有15位空闲。旧的读取方会拒绝带有陌生标志的文件，而不是错误地读取它
- **新的编解码器的代**。新布局可以改变任何东西，包括文件头长度。更新的读取方可以在读取新代的同时读取旧代

数据之后不能追加任何内容。声明的长度必须与实际长度一致，所以任何多余的尾部都会被拒绝。新的关卡数据放进数据内部，通过模型的代来实现

> [!info] 须知
> 内容没有恰好在声明的长度处结束，无论长了还是短了，都算作损坏。有时一个根通过了文件头的全部检查，却仍然无法解析。这时按它的长度跳过它，它保留默认值。跳过会记录到`SerializationReport`中，从不悄无声息
