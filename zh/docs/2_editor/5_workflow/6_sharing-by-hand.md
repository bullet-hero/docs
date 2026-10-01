---
title: 如何手动分享关卡
date: 2026-10-01
tags: [level_author]
---

# 如何手动分享关卡

把关卡文件夹打包成zip或tar.gz，需要密码时用gpg加密。在另一台电脑上解包后的关卡可以直接游玩，游戏也能自己读取这类归档包

关卡就是一个装着文件的文件夹。归档包是为了传送而打包好的同一个文件夹。关卡用到的一切都随它一起传送：歌曲、图片、封面

接收方要把关卡放在哪里：[[2_metadata-and-sharing#现在如何分享关卡]]

## 不会进入归档包的内容

- 关卡通过链接获取的资源。链接保持原样
- 关卡中没有任何地方引用的文件

游戏的导出报告会列出这两类内容。更多：[[13_export-and-protection#导出关卡]]

## 五种形式

每一种都能用对方已有的工具打开：

| 文件 | 内容 | 打开方式 |
|---|---|---|
| `level.json.gpg` | 仅关卡文档，有密码保护，位于关卡文件夹中 | gpg |
| `LEVEL_FOLDER.tar.gz` | 整个文件夹打成一个归档包 | 7-Zip、Keka、Ark、资源管理器 |
| `LEVEL_FOLDER.tar.gz.gpg` | 同一个归档包，加了密码 | gpg |
| `LEVEL_FOLDER.zip` | 同一个文件夹，打成zip | Windows上双击即可，不需要安装任何东西 |
| `LEVEL_FOLDER.zip.gpg` | 同一个zip，加了密码 | gpg |

默认情况下，游戏用zip自身的手段为归档包设置密码，即AES-256。除资源管理器外，任何解压软件都能打开这样的归档包：它会要求输入密码。`.gpg`形式由游戏按需写出

## 运行命令之前

替换命令中的两处：
- `LEVEL_FOLDER`：关卡文件夹的名称，也就是它的ID。这是一个由数字和字母组成的长字符串，即`levels`中那个文件夹的名称
- `YOUR_PASSWORD`：密码本身

写在命令行里的密码会留在shell历史记录中。从命令中去掉`--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD`，gpg就会在屏幕上要求输入密码

## 用gpg处理关卡文档

加密会在原文件旁边放一个`level.json.gpg`。原文件留在原处：确认结果后自己删除它。解密会再次按原来的名字写出文档。加密文件不会消失：

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## tar.gz归档包

文件夹从内部打包：归档包里直接是关卡文件，外面没有套一层文件夹。解包时目标文件夹必须已经存在，tar不会创建它。`mkdir`在cmd、PowerShell以及Mac或Linux的终端中用法都一样：

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

一步完成打包和加密。未加密的归档包根本不会落到磁盘上。第二行把归档包解密并解包回同一个文件夹：

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## zip归档包

在Windows上用PowerShell，每台电脑上都有。星号打包的是文件夹的内容，而不是文件夹本身。`Expand-Archive`会自己创建文件夹，不需要提前`mkdir`：

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

在Mac或Linux上用zip和unzip：

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

7-Zip打开时会要求输入密码的zip，由7-Zip自己制作。它必须已经安装：

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## 游戏也能读回它们

所有形式都是双向的。游戏写出的文件，gpg、tar和zip都能打开。gpg、tar和zip制作的文件，游戏都能读取。正因如此才选择了标准工具，而不是自己的格式

> [!tip] 提示
> 游戏看的是文件实际是什么，而不是它叫什么。所以改过名的归档包照样能打开。游戏能识别`7z`，但不接受它：游戏会说出格式名称，而不是宣布文件已损坏。请把这样的归档包重新打包成zip

> [!caution] 注意
> **忘记的密码无法找回**。密钥不保存在任何地方：不在游戏里，不在文件里，也不在任何人手里。没有重置，没有恢复，也没有绕过的办法。密码丢失，关卡也随之丢失。关闭编辑器之前先把密码记下来

接下来：[[4_level-folder-and-backups|关卡文件夹与备份]]、[[4_not-losing-work|避免丢失工作]]
