---
title: 手动分享关卡
date: 2026-09-24
tags: [level_author]
---

# 手动分享关卡

归档包里有什么、它的五种形式，以及用tar、zip和gpg创建和打开每种形式的命令

关卡就是一个装着文件的文件夹，归档包是为了发送而打包好的这个文件夹。关卡用到的一切都随它一起传送：歌曲、图片、封面。在另一台电脑上解包后，关卡可以直接游玩

对方要把关卡放在哪里：[[2_metadata-and-sharing#现在如何分享关卡]]

## 不会进入归档包的内容

- 关卡通过链接获取的资源。链接保持原样
- 关卡中没有任何地方引用的文件

游戏的导出报告会列出这两类内容。更多：[[13_export-and-protection#导出关卡]]

## 五种形式

每一种都能用对方电脑上已有的工具打开：

| 文件 | 内容 | 打开方式 |
|---|---|---|
| `level.json.gpg` | 仅关卡文档，有密码保护，位于关卡文件夹中 | gpg |
| `LEVEL_FOLDER.tar.gz` | 整个文件夹打成一个归档包 | 7-Zip、Keka、Ark、资源管理器 |
| `LEVEL_FOLDER.tar.gz.gpg` | 同一个归档包，加了密码 | gpg |
| `LEVEL_FOLDER.zip` | 同一个文件夹，打成zip | Windows上双击即可，不需要安装任何东西 |
| `LEVEL_FOLDER.zip.gpg` | 这个zip加了密码 | gpg |

默认情况下，游戏用zip自带的AES-256为归档包设置密码。除资源管理器外，任何解压软件都能打开它，打开时会要求输入密码。`.gpg`形式由游戏按需写出

## 运行命令之前

替换命令中的两处：
- `LEVEL_FOLDER`：关卡自己的文件夹名，也就是它的ID。就是`levels`中那个由数字和字母组成的长字符串文件夹名
- `YOUR_PASSWORD`：密码本身

写在命令行里的密码会留在shell历史记录中。从命令中去掉`--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD`，gpg就会在屏幕上提示你输入密码

## 用gpg处理关卡文档

加密会在原文件旁边写出`level.json.gpg`。原文件留在原处：确认结果无误后自己删除它。解密会把文档按原来的名字重新写出，加密文件保留不动：

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## tar.gz归档包

文件夹从内部打包：归档包里是关卡自己的文件，外面没有套一层文件夹。解包时目标文件夹必须已经存在，tar不会创建它。`mkdir`在cmd、PowerShell以及Mac或Linux的终端中用法都一样：

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

一步完成打包和加密，未加密的归档包根本不会落到磁盘上。第二行把归档包解密并解包回同一个文件夹：

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## zip归档包

在Windows上使用PowerShell，每台Windows电脑都有。星号打包的是文件夹里的内容，而不是文件夹本身。`Expand-Archive`会自己创建文件夹，所以不需要先`mkdir`：

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

在Mac或Linux上使用zip和unzip：

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

要制作7-Zip打开时会要求输入密码的zip，需要用7-Zip本身来做，必须先安装它：

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## 游戏也能读回它们

所有形式都是双向的。游戏写出的文件，gpg、tar和zip都能打开。gpg、tar和zip制作的文件，游戏都能读取。正因如此才选择了标准工具，而不是游戏自己的格式

> [!tip] 提示
> 游戏识别的是文件的实际内容，而不是文件名。所以改过名的归档包照样能打开。`7z`是唯一一种游戏能识别但拒绝接受的格式：游戏会说出格式名称，而不是说文件已损坏。请把这样的归档包重新打包成zip

> [!caution] 注意
> **忘记的密码无法找回**。密钥不保存在任何地方：不在游戏里，不在文件里，开发者那里也没有。没有重置，没有恢复，也没有任何后门。密码丢失，关卡也就随之丢失。关闭编辑器之前先把密码记下来

接下来：[[4_level-folder-and-backups|关卡文件夹与备份]]、[[4_not-losing-work|避免丢失工作]]
