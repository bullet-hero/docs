---
title: 发布
date: 2026-10-02
tags: [level_author]
---

# 发布

关卡只能从关卡设置的“发布”标签页发送：以压缩包形式或发布到Steam创意工坊。报告会自动检查关卡，其中的错误会阻止发送

## “发布”标签页

`发布`是关卡设置中的一个标签页。这是关卡发往任何地方的唯一入口

顶部的`{{ui:editor_share_destination}}`显示当前选择的发送方式。按下它会打开`{{ui:editor_share_pick-title}}`：列出此版本在当前设备上提供的方式，每种都有一行说明。默认选择`{{ui:editor_share_archive}}`。上次的选择会一直保留到关闭游戏

下方有：
- 该方式自己的设置
- 它的报告
- 执行按钮：`{{ui:editor_share_export}}`或`发布`

如果此版本在当前设备上没有任何方式，标签页会显示`{{ui:editor_share_none}}`

## 报告

报告会自动检查：打开某种方式时，以及它的任何设置发生变化时。没有专门的检查按钮。报告以`错误：N，警告：N，建议：N`这一行开头，之后每个发现一行

错误会阻止执行。警告和建议由你自己决定

评估关卡所用的规则由方式决定。`{{ui:editor_share_archive}}`按`{{ui:editor_publish_profile-local}}`规则检查，`{{ui:editor_share_steam}}`按创意工坊规则检查。每套规则的要求和每种结论的含义：[[5_publish-readiness]]

## 发送方式

| 方式 | 在哪里可用 | 发送什么 |
|---|---|---|
| `{{ui:editor_share_archive}}` | 任何有保存对话框的设备。iOS上没有 | 关卡、合集或单个资源，作为一个文件 |
| `{{ui:editor_share_steam}}` | 仅限Steam版本 | 关卡或你自己的合集 |

此版本或此设备没有的方式不会出现在列表中

## 压缩包

对于关卡：

| 元素 | 作用 |
|---|---|
| `{{ui:editor_share_format}}` | 七种导出模式之一，从普通文件夹到带密码的压缩包 |
| `{{ui:editor_share_passphrase}}` | 只在受保护的模式下可见。密码为空时，受保护的模式无法执行 |
| `{{ui:editor_share_export}}` | 把关卡写到你指定的位置 |

每种模式写出什么、用什么打开：[[13_export-and-protection#导出关卡]]

对于合集或单个资源，`{{ui:editor_share_format}}`提供其中的五种模式，全部是归档包。没有文件夹模式：

| `{{ui:editor_share_format}}` | 得到什么 | 用什么打开 |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_zip}}` | 一个文件 | 在Windows资源管理器中双击，无需安装任何软件 |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | 带内置AES-256加密的zip | 7-Zip或其他压缩软件，它会要求输入密码 |
| `{{ui:settings_level-settings_export-mode_zip-protected}}` | 整个zip外面再包一层OpenPGP | gpg |
| `{{ui:settings_level-settings_export-mode_targz}}` | 一个文件 | 任何压缩软件 |
| `{{ui:settings_level-settings_export-mode_targz-protected}}` | tar.gz外面再包一层OpenPGP | gpg |

三种带密码的模式会显示`{{ui:editor_share_passphrase}}`。密码为空时不会导出任何内容。适用下文的合集检查，同样按`{{ui:editor_publish_profile-local}}`规则

## Steam创意工坊

仅限Steam版本。元素：

| 元素 | 作用 |
|---|---|
| `{{ui:editor_publish_visibility}}` | 谁能看到物品：`{{ui:editor_publish_visibility-public}}`、`{{ui:editor_publish_visibility-friends-only}}`或`{{ui:editor_publish_visibility-private}}`。默认是`{{ui:editor_publish_visibility-private}}` |
| `{{ui:editor_publish_changelog}}` | 这次上传的更新说明。多行输入框，标题单独占一行 |
| `标题和描述使用的语言` | 物品文本取自哪种语言（见下文） |
| `{{ui:editor_share_steam-descriptors}}` | 五个复选框，即Steam自己的内容描述符（见下文） |
| `发布` | 上传关卡 |

关卡始终按创意工坊规则检查。这里没有规则可选

创意工坊物品的内容取自关卡：
- 标题和描述就是关卡的名称和描述，使用同一种语言
- 预览图是关卡封面，png或jpg格式，不超过1 MB。其他任何封面都会被跳过，物品上传时不带图片
- 标签由游戏自动设置，见下文“创意工坊标签”

第一次按`发布`会创建物品。之后再按会更新同一个物品。游戏在你发布过的物品中按关卡自己的id找到它，所以关卡里不保存任何东西

受保护的关卡不能发布。更多：[[13_export-and-protection]]

> [!warning] 警告
> 如果你还没有接受Steam创意工坊法律协议，物品会上传，但保持隐藏。请在物品页面上接受协议。游戏会在Steam叠加层中打开该页面

### 标题语言

Steam每个物品只显示一个标题和一个描述。游戏按以下顺序查找，取第一个找到的语言：
1. `{{ui:settings_game-editor_title}}`设置中的`{{ui:settings_game-editor_publish-language}}`：`{{ui:enum_publish-language_english}}`（默认）或`{{ui:enum_publish-language_system}}`，即设备的语言。更多：[[14_editor-settings]]
2. 你自己的语言，即游戏界面的语言
3. 英语
4. 文本最初编写时使用的第一种语言

描述会先按标题的语言查找，使两者一致。未本地化的名称（普通文本）会按原样上传，这一行显示`{{ui:editor_share_steam-language-as-written}}`

### 内容描述符

`{{ui:editor_share_steam-descriptors}}`下有五个复选框，即Steam自己的内容描述符：
- `{{ui:editor_share_steam-descriptor-mature}}`
- `{{ui:editor_share_steam-descriptor-violence}}`
- `{{ui:editor_share_steam-descriptor-some-nudity}}`
- `{{ui:editor_share_steam-descriptor-frequent-nudity}}`
- `{{ui:editor_share_steam-descriptor-adult-only}}`

它们随每次发布一起发送，从不保存在关卡中。每次发布都会发送完整的一组，所以取消勾选某一项，也会把该描述符从已发布的物品上移除。它们在上传完成后紧接着通过第二次更新发送。如果这一步失败，物品仍然已发布，结果会说明描述符没有设置

### 发布之后

成功时，表单显示创建或更新了哪个物品，以及`{{ui:editor_publish_open-item}}`按钮。它会在Steam中打开该物品的页面

失败时，表单显示：
- 用通俗语言说明的原因，`发布失败：...`
- `发送的内容和 Steam 的回复：...`，这是一行英文技术信息。报告问题时值得把它原样发给开发者
- 一个`?`，展开后说明Steam为什么这样拒绝，并附三个链接：`{{ui:editor_publish_help-docs}}`（本页）、`{{ui:editor_publish_help-steam-support}}`和`{{ui:editor_publish_help-agreement}}`

游戏自己关于发布的日志行始终是英文，与界面语言无关

| 原因 | 怎么办 |
|---|---|
| `{{ui:enum_workshop-failure_steam-not-running}}` | 启动Steam，然后从Steam重新启动游戏 |
| `{{ui:enum_workshop-failure_not-owner}}` | 用那个账户发布，或复制一份关卡，这样它会作为新物品上传 |
| `{{ui:enum_workshop-failure_access-denied}}` | 账户没有这款游戏、账户受限（还没有在Steam消费过）或该账户无法使用创意工坊 |
| `{{ui:enum_workshop-failure_invalid-param}}` | 游戏的创意工坊没有设置为接受上传，或Steam以另一款游戏的id运行。请重启Steam和游戏 |
| `{{ui:enum_workshop-failure_limit-exceeded}}` | 删除你的创意工坊文件中的旧物品 |
| `{{ui:enum_workshop-failure_connection}}` | 检查网络连接和Steam状态 |
| `{{ui:enum_workshop-failure_invalid-request}}` | 标题最多128个字符，描述最多8000个字符，预览图为不超过1 MB的png或jpg |
| `{{ui:enum_workshop-failure_staging}}` | 检查磁盘剩余空间，并确认关卡文件没有被其他程序打开 |

如果新物品已创建，但它的上传被拒绝，游戏会删除这个空物品，不会在创意工坊留下被遗弃的物品

## 没有Steam的版本

没有Steam的版本不会在列表中显示`{{ui:editor_share_steam}}`。`{{ui:editor_share_archive}}`仍然可用

## 如何分享合集

合集从“库”标签页中它的页面分享。`{{ui:editor_share_share}}`会在窗口中打开同样的面板：`{{ui:editor_share_archive}}`，在Steam版本中，你自己的合集还有`{{ui:editor_share_steam}}`

合集的检查项：
- 有名称
- 指定了许可证
- 不为空
- 它列出的每个文件都在其中
- 它的条目引用的每个资源都已包含在内

缺少许可证的后果取决于方式。对`{{ui:editor_share_archive}}`来说这是警告，导出照常进行。对`{{ui:editor_share_steam}}`来说这是错误。错误会阻止执行。关于合集的更多内容：[[16_library-and-collections]]

## 如何分享单个资源

“库”中每一行主题、形状、特效和预制件也都有`{{ui:editor_share_share}}`按钮。它会把该资源连同它需要的一切（例如预制件的形状、纹理和嵌套预制件）打包成只有一个条目的合集

只提供`{{ui:editor_share_archive}}`，格式与合集相同，共五种，包括带密码的格式。接收者通过`{{ui:editor_library_import-archive}}`导入该文件，和导入任何合集一样

## 创意工坊标签

标签由游戏自动设置：

| 物品 | 标签 |
|---|---|
| 关卡 | `level` |
| 合集 | `collection`，外加其中每一类各一个：`prefabs`、`themes`、`shapes`、`effects` |

纹理、字体和音频没有标签，也不会单独进入创意工坊。它们作为合集中预制件、主题、形状和特效所使用的内容，随合集一起上传。只包含媒体的合集会被拒绝，并显示原因，这种合集最好以压缩包形式分享

> [!info] 须知
> Steam自己的“合集”是创意工坊物品的精选列表，是Valve的功能。它们与Bullet Hero的合集毫无关系

## 订阅

Steam版本会读取你订阅的内容：
- 关卡出现在关卡列表的`{{ui:editor_library-source_workshop}}`中，[[2_playing-levels]]
- 合集出现在编辑器的库中`{{ui:editor_library-source_workshop}}`标签下，只读

接下来：[[5_publish-readiness]]、[[1_licensing-basics]]、[[16_library-and-collections]]
