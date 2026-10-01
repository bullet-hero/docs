---
title: 归档包与保护
date: 2026-10-01
tags: [developer, level_author]
---

# 归档包与保护

关卡可导出为文件夹、tar.gz或zip，并可选择加密码：AES-256加密的zip或OpenPGP。SDK根据收到文件的开头字节判断格式，而不是根据文件名

## 导出模式

关卡以`LevelExportMode`的某种形式离开设备：

| 值 | 模式 | 写出什么 | 保护 |
|---|---|---|---|
| 0 | `Folder` | 普通文件夹，与磁盘上的结构相同 | 无 |
| 1 | `FolderProtectedLevel` | 只有`level.json.gpg`加密的文件夹 | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | 无 |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | 无 |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | 条目以AES-256加密的`<name>.zip` | zip自带 |

数字是模式的身份，永远不变。编辑器下拉列表中的顺序另行设定（`DisplayOrder`）

**每种格式都是开放标准**。`tar -xzf`、`gpg -d`和任何压缩工具都能在没有游戏的情况下打开它们：

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## 两种保护方案

**`ZipEncrypted`是用密码锁住关卡的默认方式**。接收方有压缩工具，但很可能没有gpg

**OpenPGP用同一种方案锁住文档、文件夹和归档包**。只有它能保护文件夹

在`FolderProtectedLevel`中，元数据、封面和媒体文件仍然可读。所以关卡浏览器仍然能显示卡片

内部扩展名保留在文件名中：`level.json.gpg`。`gpg -c level.json`正是这样命名文件的，所以无需猜测就能知道格式

## 里面放什么

`LevelArchiveBuilder`根据模型计算内容，而不是根据文件夹中的文件列表。关卡没有引用的文件留在外面。报告会说明留下了多少这样的文件

关卡的引用这样处理：
- 使用`AbsolutePath`的资源复制进归档包。它的引用改写为`LevelPath`，但只在导出的副本中改写
- `DirectUrl`保持原样并记入报告：URL无法放在文件里一起带走
- 缺失的文件以代码`archive.resource_missing`记入报告

## 按字节识别

文件名谁都能写。所以`ArchiveFormatSniffer`根据开头的8个字节判断：

| 开头字节 | 格式 |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`、`50 4B 05 06`、`50 4B 07 08`、`50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| OpenPGP数据包标签，最后检查 | `OpenPgp`：解密后重新识别 |

> [!warning] 警告
> `.7z`既不读取也不写入。识别它只是为了让拒绝信息能说出它的名称（`Unsupported`）。这样用户会把关卡重新打包成zip，而不是认为文件坏了

## 读取

`LevelArchiveReader.ReadAsync`接受文件夹或支持定位的`Stream`。它返回`LevelArchiveContent`，其中`LevelArchiveOpenResult`是以下值之一：

| 结果 | 含义 |
|---|---|
| `Ok` | 已读取 |
| `PassphraseRequired` | 没有密码，需要询问 |
| `WrongPassphrase` | 用户已经输入了密码，但密码错误 |
| `Damaged` | 文件已损坏 |
| `NotAnArchive` | 这不是归档包 |
| `Unsupported` | 格式已识别，但不受支持 |

`PeekMetaAsync`只读取元数据，用于卡片或目录

服务器读取的是别人决定上传的任何东西。所以读取器在`ArchiveLimits`的限制内工作。默认限制为：
- 4096个条目
- 每个条目512MiB
- 总计1GiB

任何内容都不会解压到分配给它的存储之外

编辑器一侧的导出：[[13_export-and-protection]]
