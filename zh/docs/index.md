---
title: 欢迎
date: 2026-09-24
---

# 欢迎

Bullet Hero的官方文档。它是节奏游戏与弹幕射击（bullet hell）的混合体，被打造为这一类型的引擎。Bullet Hero不只是一款游戏，而是由多个产品组成的软件体系

| 产品 | 文档 |
|---|---|
| 游戏 | [[1_game/index]] |
| 关卡编辑器 | [[2_editor/index]] |
| SDK | [[3_sdk/index]] |
| 服务器 | [[4_server/index]] |
| 文档 | [[5_contribute/index]] |

所有可下载的内容都在这里：[[download]]

想尽快开始游戏：[[0_quick-start]]

## 分类

不同的人关心文档的不同部分，这份文档为所有人而写

| 你是 | 从哪里开始 |
|---|---|
| [[player]]或[[advanced_player]] | [[1_game/index]] |
| [[level_author]] | [[2_editor/index]] |
| [[developer]] | [[3_sdk/index]] |
| [[server_host]] | 先看[[4_server/index]]，再看[[2_hosting]] |
| [[server_advanced]] | 先看[[4_server/index]]，再看[[3_advanced-hosting]] |
| [[contributor]] | [[5_contribute/index]] |

## 版本

每个产品都有自己的版本号，带一个字母前缀，格式都是major.minor.revision：

| 前缀 | 全称 | 产品 |
|---|---|---|
| `gv` | `game version` | 游戏（客户端） |
| `sv` | `sdk version` | SDK |
| `fv` | `frontend version` | 网站 |
| `bv` | `backend version` | 后端，即服务器 |

当前版本：`gv 1.0.0`、`sv 1.0.0`、`fv 1.0.0`。服务器尚未开发

各个版本号不必互相跟随，但大多数情况下是一致的。版本也会一起升级，共同的更新使用相同的版本号

关卡另有一个单独的版本`mg`（`model generation`）。它是每个存档中的一个普通数字，表示数据的版本。它比其他所有版本号都重要得多，更新和兼容处处都要用到它。更多：[[5_versioning]]

## 源代码

所有仓库都在[bullet-hero](https://github.com/bullet-hero)组织中

| 仓库 | 访问 | 内容 |
|---|---|---|
| [game](https://github.com/bullet-hero/game) | 闭源 | 游戏和编辑器 |
| [sdk](https://github.com/bullet-hero/sdk) | 开源 | SDK，关于SDK及其代码的issue |
| [releases](https://github.com/bullet-hero/releases) | 开源 | 游戏构建版本，玩家提交的issue |
| [docs](https://github.com/bullet-hero/docs) | 开源 | 本文档 |
| [backend](https://github.com/bullet-hero/backend) | 开源 | 服务器，目前为空 |
| [frontend](https://github.com/bullet-hero/frontend) | 闭源 | 网站 |

在游戏中发现了bug？请提交到[releases的issue](https://github.com/bullet-hero/releases/issues)。更多：[[11_help]]
