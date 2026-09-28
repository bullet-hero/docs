---
title: 归档包与保护
date: 2026-09-24
tags: [developer, level_author]
---

# 归档包与保护

SDK如何把关卡打包成一个文件或加上密码，以及如何识别交给它的是什么

## 导出模式

关卡以`LevelExportMode`中的某一种形式离开设备：

| 值 | 模式 | 写出什么 | 保护 |
|---|---|---|---|
| 0 | `Folder` | 普通文件夹，与磁盘上的结构相同 | 无 |
| 1 | `FolderProtectedLevel` | 文件夹，其中只有`level.json.gpg`被加密 | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | 无 |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | 无 |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | 条目用AES-256加密的`<name>.zip` | zip自带的加密 |

数字是模式的身份，永不改变。编辑器下拉列表中的顺序另行设定（`DisplayOrder`）

**每种格式都是开放标准**。`tar -xzf`、`gpg -d`和任何解压软件都能在没有游戏的情况下打开它们：

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## 两种保护方案

**`ZipEncrypted`是给关卡加密码的默认方式**。接收者有解压软件，但多半没有gpg

**OpenPGP用同一种方案保护文档、文件夹和归档包**。只有它能保护文件夹

在`FolderProtectedLevel`中，元数据、封面和媒体文件仍然可读。所以关卡浏览器依然能显示卡片

内层扩展名保留在文件名中：`level.json.gpg`。`gpg -c level.json`正是这样命名文件的，所以不用猜就能知道格式

## 包含哪些内容

`LevelArchiveBuilder`根据模型计算内容，而不是根据文件夹的文件列表。关卡没有引用的文件不会放进去。报告会说明有多少文件被留下

关卡的引用这样处理：
- 带`AbsolutePath`的资源会被复制进归档包。它的引用被改写为`LevelPath`，但仅限导出的副本
- `DirectUrl`保持原样并写入报告：URL无法放进文件里带走
- 缺失的文件以代码`archive.resource_missing`写入报告

## 按字节识别

文件名谁都能写。所以`ArchiveFormatSniffer`根据前8个字节判断：

| 起始字节 | 格式 |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`、`50 4B 05 06`、`50 4B 07 08`、`50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| OpenPGP数据包标签，最后检查 | `OpenPgp`：先解密，再重新识别 |

> [!warning] 警告
> `.7z`既不读取也不写入。识别它只是为了在拒绝时能说出它的名字（`Unsupported`）。这样用户会把关卡重新打包成zip，而不是认为文件坏了

## 读取

`LevelArchiveReader.ReadAsync`接受一个文件夹或可定位的`Stream`。它返回`LevelArchiveContent`，其中的`LevelArchiveOpenResult`是以下之一：

| 结果 | 含义 |
|---|---|
| `Ok` | 已读取 |
| `PassphraseRequired` | 没有密码，需要询问 |
| `WrongPassphrase` | 用户已经输入了密码，但密码错误 |
| `Damaged` | 文件已损坏 |
| `NotAnArchive` | 这不是归档包 |
| `Unsupported` | 格式已识别，但不受支持 |

`PeekMetaAsync`只读取元数据，用于卡片或目录

服务器读取的是别人选择上传的任何东西。所以读取器在`ArchiveLimits`的限制下工作。默认值为：
- 4096个条目
- 每个条目512 MiB
- 总计1 GiB

任何内容都不会解压到给定的存储位置之外

编辑器一侧的导出：[[13_export-and-protection]]
