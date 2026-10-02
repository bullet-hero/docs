---
title: 编写页面
date: 2026-10-02
tags: [contributor]
---

# 编写页面

页面是开放仓库bullet-hero/docs中的markdown文件。修改以pull request的形式提交：fork、分支、在每种语言中修改、对照风格指南检查

## 仓库

项目的所有仓库都在[bullet-hero](https://github.com/bullet-hero)组织下。开放的仓库有：

| 仓库 | 内容 |
|---|---|
| [bullet-hero/releases](https://github.com/bullet-hero/releases) | releases中是游戏的每个公开构建版本，issues中是玩家反馈的关于游戏的错误和建议 |
| [bullet-hero/sdk](https://github.com/bullet-hero/sdk) | SDK代码，issues中是关于SDK的错误和建议 |
| [bullet-hero/docs](https://github.com/bullet-hero/docs) | 这些页面及其翻译 |
| [bullet-hero/backend](https://github.com/bullet-hero/backend) | 服务器，目前是空的 |

游戏（`bullet-hero/game`）和网站（`bullet-hero/frontend`）的代码是闭源的

本页讲的是bullet-hero/docs

## 如何提交修改

1. Fork [bullet-hero/docs](https://github.com/bullet-hero/docs)并创建一个分支
2. 按下面描述的格式编辑或添加页面
3. 在每种语言中修改该页面，或者在pull request中说明哪些语言仍需要这项修改。更多：[[translating]]
4. 对照[[style-guide]]检查文本
5. 发起pull request，简要说明改了什么以及为什么改

**事实来自游戏、SDK或它们的文档**。数字、字段名、文件名、快捷键和地址从不靠猜。不确定某件事是否正确？在pull request里说明，而不是写在页面上

被接受的修改会在几分钟内出现在[bullethero.space](https://bullethero.space/)上：每次推送到`master`都会重新构建网站

> [!tip] 提示
> 网站代码是闭源的，所以你无法自己构建网站。最接近的预览方式是Obsidian：Obsidian找不到的链接，在网站上同样找不到

## 仓库如何运作

- **只有markdown**。没有自己的构建流程，也没有脚本
- **它是一个[Obsidian](https://obsidian.md/)库**。把仓库的根文件夹作为库打开，链接、嵌入和预览的效果与网站上相同。其他任何markdown编辑器也可以使用
- **它是网站的子模块**。网站把这个仓库作为自己的`content/`文件夹引入，在构建时编译页面，并预渲染每一个页面。网站从本仓库最新的`master`构建

## 内容放在哪里

| 路径 | 内容 | 网站上的地址 |
|---|---|---|
| `<lang>/docs/1_game/` | 面向玩家：安装、游玩、设置、机制 | `/docs/game` |
| `<lang>/docs/2_editor/` | 面向关卡作者：编辑器指南和参考 | `/docs/editor` |
| `<lang>/docs/3_sdk/` | 面向开发者：开源SDK和关卡格式 | `/docs/sdk` |
| `<lang>/docs/4_server/` | 面向服务器运营者：官方服务器和社区服务器 | `/docs/server` |
| `<lang>/docs/5_changelog/` | 更新日志，每个游戏版本一页 | `/docs/changelog` |
| `<lang>/notes/` | 文章、社区、编辑规则、公开文件和政策，按日期排序 | `/notes/<name>` |
| `<lang>/tags/` | 标签页面 | `/tags/<tag>` |
| `<lang>/download.md` | 下载页面 | `/download` |
| `assets/` | 所有语言共用的图片 | 嵌入到页面中 |

`<lang>`是语言文件夹：`en`、`ru`或`zh`。`docs/`、`notes/`、`tags/`和`download.md`之外的文件不会成为页面

**文档描述的是事物现在如何运作**。变更的历史、个人观点或随笔是`notes/`中的笔记

## 文件名和顺序

- **侧边栏中的顺序由`N_`前缀决定**，`docs/`内的每个文件和文件夹都有这个前缀：`1_`、`2_`，依此类推，直到`10_`及以上
- **前缀不会出现在地址中**。`1_game/3_controls.md`的地址是`/docs/game/controls`
- **`index.md`没有前缀**。它是所在文件夹的首页，占据文件夹的位置，并为侧边栏中的分组命名
- **要调整顺序，就重命名文件**。在Obsidian中启用“Automatically update internal links”，它会自己修正所有链接
- **去掉前缀后的名称在同一语言内是唯一的**。如果两个文件对应到同一个地址，网站构建时会报告
- **带前缀的名称在所有语言中都相同**。`en/docs/2_editor/4_craft/3_difficulty-curve.md`和`ru/docs/2_editor/4_craft/3_difficulty-curve.md`是同一个页面
- **`notes/`没有前缀，也没有子文件夹**。永远不要重命名`notes/cookie-policy`：网站上的Cookie横幅链接到它

## Frontmatter、标题和描述

每个页面都以这样的内容开头：

```md
---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

One line that says what the page is, up to 200 characters, no markup
```

- **`title`、H1和描述用页面所属的语言书写**。上面的例子来自英文版
- **Frontmatter包括`title`、`date`和`tags`**。其他内容一概不读取。`date`的格式是`YYYY-MM-DD`，是最后一次更新的日期，而不是创建日期。修改文件时，把`date`设为修改当天
- **`# H1`是必需的，且与`title`相同**。网站只显示页面正文，所以H1就是可见的标题
- **H1之后的第一段是描述**，显示在列表、搜索和链接预览中。它会在200个字符处截断。把它写成一行，不带链接和格式。它简短地回答页面的问题，而不是描述页面上有什么，见[[style-guide#页面开头]]
- **章节用`##`，小节用`###`**。它们会生成锚点和目录。不需要更深的层级

## 受众标签

每个文档页面都有1到3个来自此列表的标签。标签用`snake_case`书写，不带`#`。网站会在页面上显示它们

| 标签 | 网站上显示为 | 对象 |
|---|---|---|
| `player` | [[player]] | 普通玩家 |
| `advanced_player` | [[advanced_player]] | 对机制感兴趣的玩家 |
| `level_author` | [[level_author]] | 在编辑器中制作关卡 |
| `developer` | [[developer]] | 基于SDK构建东西或扩展游戏 |
| `server_host` | [[server_host]] | 为自己和朋友运行服务器 |
| `server_advanced` | [[server_advanced]] | 大型服务器运营者，准备扩展或编写服务器 |
| `contributor` | [[contributor]] | 在本仓库中编辑文本和翻译 |

`notes/`中的笔记改用主题标签，目前是`legal`（[[legal]]）

读者看不到标签代码。显示的名称来自标签页面`<lang>/tags/<code>.md`：

- 它的`title`就是名称
- 它的第一段描述受众
- 带有该标签的页面列表由网站自动添加

新标签需要在每种语言中都有这样一个页面

要在正文中提到某个标签，就链接到它的页面：`[[level_author]]`。链接会以读者的语言显示名称

## 链接

| 目标 | 写法 |
|---|---|
| 另一个页面 | `[[3_difficulty-curve]]`，使用带前缀的完整文件名 |
| 页面中的某个章节 | `[[3_difficulty-curve#Anchor]]` |
| 文件夹首页 | `[[2_editor/4_craft/index]]`，要带路径，因为每个这样的页面都叫`index` |
| 外部网站 | `[text](https://…)`，使用带协议的完整地址 |

链接指向不带语言的地址，所以同一份源文本在所有语言中都能用。`[[cookie-policy]]`会把英文读者带到英文页面，把俄文读者带到俄文页面，把中文读者带到中文页面

只链接到已经存在的页面。网站构建会报告每一个无法解析的链接

## 图片

图片放在仓库根目录的`assets/`中，用`![[file.png]]`嵌入

所有语言共用一个文件夹。图片上绘制的文字不会随页面一起翻译

## 标注框

| 语法 | 颜色 | 用途 |
|---|---|---|
| `> [!note]`、`> [!info]`、`> [!tip]` | 蓝色 | 背景信息、捷径、建议 |
| `> [!warning]`、`> [!caution]` | 黄色 | 耗费时间或降低质量、毁掉成果 |
| `> [!danger]`、`> [!bug]` | 红色 | 可以显示，但风格指南不使用它们 |

选用哪种标注框、它的标题，以及每页最多两个的限制：[[style-guide]]

## 数字、版本和界面文字

由游戏决定的数字（化身的速度、设置的默认值、大小上限）以及当前版本不直接写进页面。它们存放在仓库根目录的`values.yaml`中，页面只写一个占位符，由网站在构建时填入：

- `\{{v:avatar.move-speed}}`是`values.yaml`中的值。网站按页面语言的写法输出数字：英文是`0.15`，俄文是`0,15`
- `\{{ui:menu_main_sandbox-btn}}`是`game/<lang>.yaml`中的界面文字，使用页面本身的语言
- `\{{`表示两个普通的花括号

不存在的键会让网站构建失败，所以新数字要先加进`values.yaml`。作为历史节点提到的版本（"从`gv 1.0.0`起"）保持为文本。Obsidian会按原样显示占位符

## 代码和其他标记

- **代码高亮**只支持`ts`、`tsx`、`js`、`json`、`csharp`、`bash`、`yaml`、`css`和`md`。其他语言显示为纯文本
- **GFM表格、任务列表、脚注和`==highlights==`**都可以使用
- **不支持MDX和JSX**。`{`和`<`会原样显示
