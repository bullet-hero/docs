---
title: 用户关卡许可政策
date: 2026-09-24
tags: [legal]
---

# 用户关卡许可政策

每个用户关卡所采用的许可证、在关卡中使用外部资源的两种方式，以及可接受的许可证

Bullet Hero允许玩家创作自己的内容（UGC，user-generated content，用户生成内容），这些内容必须有许可证。做法与*Geometry Dash*类似，但有一点不同：*Geometry Dash*只涉及一首音乐曲目，而本政策涵盖关卡的**全部**外部资源

## 关卡许可证

每个用户关卡都以**CC BY-NC**分发：

- **CC**：Creative Commons许可证
- **BY**：必须署名，即注明作者
- **NC**：仅限非商业用途

该许可证涵盖关卡自身的原创内容：布局、时间安排和关键帧、自定义代码，以及把这一切组织成完整关卡的创作工作。**它不会对嵌入关卡的外部资源重新授权**

每个外部资源都保留自己的许可证或许可，并为每个资源单独记录（见下文）。关卡上的CC BY-NC是一层包装，包在其中的每个资源本身就已经允许以这种方式再分发

**只有当关卡中的每个外部资源都符合方案A或方案B时，关卡才能以CC BY-NC分发**。只要有一个资源不符合，该关卡就不能通过Bullet Hero官方网络服务（官方服务器OWS）分发

开发者不阻止通过非官方渠道免费分发关卡。开发者坚决反对对关卡进行商业使用

## 外部资源

外部资源涵盖范围很广的数据：

- 音乐和音频：`.mp3`、`.wav`、`.ogg`
- 纹理和图片：`.png`、`.jpg`、`.jpeg`
- 字体：`.ttf`、`.otf`
- 文本和字节：任何数据

每个外部资源都必须符合下面两个方案之一

### 方案A：开放许可证

资源采用与CC BY-NC相同或比它更宽松的许可证（见下方可接受的许可证列表）。资源保留**自己的**原始许可证：它不会被转换为CC BY-NC，它本身已经允许CC BY-NC所要求的公开非商业再分发，因此把它放进CC BY-NC关卡是一致的

资源的原始许可证和来源必须记录在关卡的元数据文件中。SIL OFL本来就对字体有此要求，这里把要求扩展到每个资源，这样任何下载关卡的人都能看到每个部分是在什么条件下使用的

### 方案B：作者的直接许可

资源的作者许可你专门在Bullet Hero中使用它。私下一句“当然，用吧”本身是不够的：标记为CC BY-NC的关卡会被公开再分发，所以许可必须明确涵盖这一点，而不只是你个人的使用。有效的许可必须同时授予以下三项：

1. 在Bullet Hero关卡中使用该资源的权利
2. 由此产生的关卡（包括该资源）可由第三方通过Bullet Hero的服务（OWS、Steam创意工坊、NOWS）**非商业地**自由再分发的权利，并注明作者
3. 仅限非商业用途，且明确说明

许可可以是审核员能够核实的任何形式：电子邮件、私信或公开声明（例如在Twitter/X上）。以下面的模板为基础，并保存作者的回复作为证明

### 许可请求模板

填写占位符，并根据需要调整语气，但第1到3点必须保持完整：正是这三点使许可对CC BY-NC分发有效。模板保持英文，与原始政策一致。如果作者使用其他语言，请翻译模板，并保留全部三点

```
Subject: Permission to use "<TRACK/RESOURCE NAME>" in a Bullet Hero level

Hi <AUTHOR NAME>,

My name is <YOUR NAME / HANDLE>, I'm creating a level for Bullet Hero (a rhythm/
bullet-hell game - <link to game/project if available>) and I'd love to use your
work "<TRACK/RESOURCE NAME>" (<link to the original>) in it.

Specifically, I'm asking your permission to:
1. Use "<TRACK/RESOURCE NAME>" inside my Bullet Hero level.
2. Allow the level (including your work) to be shared/redistributed for FREE and
   NON-COMMERCIALLY by anyone who downloads it, through Bullet Hero's official and
   unofficial services (including its official server, Steam Workshop, and any
   community-run servers).
3. Credit you as "<HOW YOU WANT TO BE CREDITED>" wherever the level shows attribution.

To be clear, this permission is for non-commercial use only - the level will not be
sold, and no one (including me) will make money from it or from your work through it.

If you're fine with this, a simple reply confirming points 1-3 is all I need - I'll
keep this email/message as proof of permission. If you'd rather I credit you
differently, or you want to set any other condition, just let me know.

Thanks a lot either way!
<YOUR NAME / HANDLE>
```

如何撰写这类请求，以及什么可以作为证明，在[[6_asking-permission]]中有更详细的说明

## 外部服务

游戏可以与多个外部服务配合使用：

| 服务 | 说明 |
|---|---|
| Official Web Services（OWS） | 默认服务器，所有平台均可使用 |
| Steam创意工坊 | PC上可用 |
| Non-official web services（NOWS） | 任何人都可以创建并按自己的意愿运行的服务 |

所有用于运行自有服务器的工具计划以MIT许可证开源。目前还没有任何服务器。关于服务器的更多内容见[[4_server/index]]

## 可接受的许可证（方案A）

可接受的外部资源采用以下常见许可证之一，与关卡的许可证相同或更宽松：

- Creative Commons系列
  - CC BY-NC（Attribution-NonCommercial，署名-非商业性使用）：与关卡相同
  - CC BY（Attribution，署名）：比CC BY-NC更宽松
  - CC0（公有领域）：最佳选择，能用就用
- Apache、MIT：用于文本和代码，比CC BY-NC更宽松
- GPL：用于文本和代码，只有配置允许它的服务才接受。官方服务器不接受，见下文
- SIL OFL（Open Font License，开放字体许可证）：必须在元数据文件中注明

> [!info] 须知
> 官方服务器所基于的`standard`发布配置接受CC0、CC BY、CC BY-NC、SIL OFL、MIT、Apache 2.0和Unlicense，但不接受GPL系列。通过App Store再分发GPL作品会与Apple的条款冲突，因此包含这类作品的目录以后将无法提供给iOS

**不**被接受的常见许可证：

- 专有许可（“All Rights Reserved”，保留所有权利）：显然不被接受
- Creative Commons系列
  - CC BY-SA（Attribution-ShareAlike，署名-相同方式共享）：技术上允许，但它要求把关卡的许可证改为CC BY-NC-SA，而OWS不接受这种许可证，所以答案是否定的
  - CC BY-ND（Attribution-NoDerivatives，署名-禁止演绎）：技术上允许，但它要求关卡受到保护、不可修改，而游戏不支持这一点，所以答案是否定的
  - CC BY-NC-SA（Attribution-NonCommercial-ShareAlike，署名-非商业性使用-相同方式共享）
  - CC BY-NC-ND（Attribution-NonCommercial-NoDerivatives，署名-非商业性使用-禁止演绎）

## 在哪里找到可接受的资源

### 音频和音乐

保证免费：

- [ccMixter](https://ccmixter.org/)：非常合适，内容采用CC BY和CC BY-NC
- [Freesound](https://freesound.org/)：非常合适，所有内容采用CC0、CC BY和CC BY-NC
- [Incompetech](https://incompetech.com/)：非常合适，所有内容采用CC BY
- [Teknoaxe](https://teknoaxe.com/)：非常合适，所有内容采用CC BY
- [Kenney Assets](https://kenney.nl/)：所有音效采用CC0

免费，但值得逐条查看：

- [SoundImage](https://soundimage.org/)
- [Pixabay](https://pixabay.com)
- [GoodKid](https://goodkidofficial.com/creators/)：没有声明许可证，但从他们的FAQ来看，是不要求提及作者的CC BY。请按CC BY使用
- NCS：仅当关卡保留默认的CC BY-NC许可证时可用

需要手动检查许可证：

- [OpenGameArt](https://opengameart.org/)：如果无法确定许可证，就不能使用该资源
- [FMA](https://freemusicarchive.org/home)：各种CC许可证都有，请仔细逐一检查
- SoundBible

有疑问：

- Zapsplat
- [Play On Loop](https://www.playonloop.com/music-licensing/)：有一个条件，游戏不得是商业项目

### 纹理和图片

保证免费：

- [Poly Haven](https://polyhaven.com/)
- [AmbientCG](https://ambientcg.com/)
- [Kenney Assets](https://kenney.nl/)
- [Pexels](https://www.pexels.com/)
- [Unsplash](https://unsplash.com/)

免费，但值得逐条查看：

- [Pixabay](https://pixabay.com)

需要手动检查许可证：

- [OpenGameArt](https://opengameart.org/)
- [Rawpixel](https://www.rawpixel.com/)：仅限“Personal License”和“Public Domain License”，见[许可证页面](https://www.rawpixel.com/services/licenses)
- itch.io
- Wikimedia Commons

### 字体

保证免费：

- Google Fonts

## 结语

Bullet Hero不是一款大游戏。开发者努力以人与人的方式对待社区，也请你这样做。好的社区要靠大家一起建设
