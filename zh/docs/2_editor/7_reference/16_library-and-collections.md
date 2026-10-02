---
title: 库与合集
date: 2026-10-02
tags: [level_author]
---

# 库与合集

合集存放你在关卡之间复用的资源。关卡从不引用合集：导入会把资源复制到关卡内部，关卡在哪里都能游玩

## 什么是合集

**合集**是一个存放可复用资源的文件夹。它可以包含七类资源：

| 类别 | 存储方式 |
|---|---|
| 预制件、主题、形状、特效 | 数据，每个条目一个文件 |
| 纹理、字体、音频 | 媒体文件 |

合集不绑定任何关卡。它保存在你的设备上，在你打开的任何关卡中都能使用

## 来源

库显示来自三个来源的资源。每个来源是列表上方的一个筛选标签：

| 标签 | 是什么 | 可修改 |
|---|---|---|
| `{{ui:editor_library-source_library}}` | 本设备的共享库：`resources/prefabs`、`themes`、`shapes`、`effects` | 是 |
| `{{ui:editor_library-source_local}}` | 你自己的合集，`resources/collections` | 是 |
| `{{ui:editor_library-source_workshop}}` | 你在Steam创意工坊订阅的合集，直接在原位置读取。仅限Steam版本 | 否 |

只读合集的修改方式是：把它的条目复制到你自己的合集中

## “库”标签页

`{{ui:settings_editor-settings_library}}`是编辑器主页上的最后一个标签页，位于`{{ui:settings_editor-settings_community}}`之后

一列窄按钮用来选择类别：
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`、`{{ui:editor_library_kind-themes}}`、`{{ui:editor_library_kind-shapes}}`、`{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`、`{{ui:editor_library_kind-fonts}}`、`{{ui:field_common_audio}}`

它的右侧，页面标题（左）和页面按钮（右）排成一行。下面是列表。空列表会在中间说明这一点

在七个类别的页面上，从`{{ui:editor_library_kind-prefabs}}`到`{{ui:field_common_audio}}`，`{{ui:editor_library_copy-target}}`在标题下方独占一整行。来源筛选标签位于它下面一行

库的窗口（合集信息卡、纹理图片、分享窗口）用角落的叉号关闭。没有`{{ui:editor_library_close}}`按钮

每一行都是一个按钮。按下它会执行该类别的主要操作：

| 类别 | 按下一行 |
|---|---|
| 合集 | 打开它的页面 |
| 主题、形状、特效 | 打开编辑器 |
| 纹理 | 显示图片及其尺寸 |
| 预制件、字体、音频 | 无操作。音频行有自己的播放按钮 |

行右侧的小按钮是其他操作，垃圾桶图标用于删除或移除

`{{ui:editor_library_open-folder}}`在系统文件管理器中显示当前页面的文件夹。仅在Windows、macOS和Linux上提供

### 合集

`{{ui:editor_library_open-folder}}`和`{{ui:editor_library_refresh}}`位于页面标题右侧。`新建合集`和`{{ui:editor_library_import-archive}}`在标题下方单独一行，靠右对齐

- `新建合集`创建一个空的合集并打开它的信息卡
- `{{ui:editor_library_import-archive}}`从`.zip`或`.tar.gz`文件添加合集，也可以从带密码的压缩包添加：自带密码的`.zip`、`.zip.gpg`或`.tar.gz.gpg`。如果设备上已有这个合集，游戏会询问是否替换

带密码的压缩包会打开`{{ui:editor_library_passphrase-title}}`窗口：`{{ui:editor_library_passphrase-needed}}`。输入密码后按`{{ui:editor_library_open}}`。密码错误时会显示`{{ui:editor_library_passphrase-wrong}}`
- `{{ui:editor_library_open-folder}}`打开`resources/collections`
- `{{ui:editor_library_refresh}}`重新读取文件夹

你自己的合集有`{{ui:editor_library_edit}}`和垃圾桶图标。垃圾桶会先询问，然后删除合集及其中的所有文件

### 合集信息卡

`{{ui:editor_library_edit}}`打开合集信息卡窗口：
- `{{ui:editor_library_field-name}}`、`{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`，用逗号分隔
- `{{ui:editor_library_field-license}}`：`{{ui:editor_library_license-unspecified}}`或某个常见许可证
- `{{ui:editor_library_set-cover}}`选择一张png图片。旁边的一行显示是否有封面

`{{ui:editor_save_text}}`写入信息卡。`{{ui:editor_cancel_text}}`、叉号或点击窗口外会丢弃改动

### 合集页面

| 元素 | 作用 |
|---|---|
| `{{ui:settings_common_back}}` | 回到列表 |
| `{{ui:editor_library_edit}}` | 打开信息卡。仅限你自己的合集 |
| `{{ui:editor_share_share}}` | 打开分享窗口：`{{ui:editor_share_archive}}`，格式为`.zip`或`.tar.gz`，可带密码也可不带，在Steam版本中，你自己的合集还有`{{ui:editor_share_steam}}` |
| `{{ui:editor_library_open-folder}}` | 打开合集自己的文件夹 |
| `{{ui:editor_library_delete}}` | 先询问，然后删除合集 |

下面是合集内容。按下一行会像在该类别页面一样打开条目，垃圾桶图标把条目从合集中移除

只读合集会显示`{{ui:editor_library_read-only}}`

关于`{{ui:editor_share_share}}`的更多内容：[[17_publishing]]

### 预制件、主题、形状、特效

这些页面各自显示所有来源中的全部条目。筛选标签可以缩小列表

`{{ui:editor_library_copy-target}}`从你自己的合集中选择一个。默认为`{{ui:editor_library_copy-target-none}}`。选好目标后，来自其他位置的每一行都会出现`{{ui:editor_library_copy-to}}`

主题、形状或特效会在与关卡设置相同的编辑器中打开。`{{ui:editor_save_text}}`把改动写到条目所在的位置：`{{ui:editor_library-source_library}}`或你的合集。来自创意工坊的条目以只读方式打开，`{{ui:editor_save_text}}`不可用。要修改它，请把它复制到你自己的合集

`{{ui:editor_library_new-entry}}`在编辑器中创建新的主题、形状或特效。条目会保存到目标合集，未选择目标时保存到`{{ui:editor_library-source_library}}`。预制件在关卡中制作，没有`{{ui:editor_library_new-entry}}`

可以修改的条目有垃圾桶图标，它会先询问

每一行都有`{{ui:editor_share_share}}`。这个按钮会把条目连同它需要的一切（例如预制件的形状、纹理和嵌套预制件）打包成`.zip`或`.tar.gz`，可带密码也可不带，作为只有一个条目的合集。接收者通过`{{ui:editor_library_import-archive}}`导入该文件，和导入任何合集一样

`{{ui:editor_library_open-folder}}`打开该类别的设备库文件夹，例如`resources/themes`

### 纹理、字体、音频

这些页面显示所有合集中的文件。文件没有个人库，所以这几类只存在于合集中

- 纹理行会显示图片
- 音频行有播放按钮。同一时间只播放一首，离开页面时停止
- 字体行没有预览

`{{ui:editor_library_add-file}}`把设备上的文件放入目标合集，所以没有目标时这个按钮不可用。纹理为png或jpg，字体为ttf或otf，音频为mp3、wav或ogg。如果合集中已有字节完全相同的文件，则什么都不会添加，游戏会给出提示

行上有`{{ui:editor_library_copy-to}}`和垃圾桶图标

### 复制会带上什么

复制会带上条目需要的一切：预制件的形状、纹理、字体和嵌套预制件，特效的粒子形状。这些资源的署名信息也会一并带上

## “合集”标签页

`{{ui:editor_library_kind-collections}}`是关卡设置中的一个标签页，紧跟在`{{ui:editor_library_kind-prefabs}}`之后。顶部有两种模式：`导入`和`{{ui:editor_collections_mode-build}}`

### 导入

1. 标签页显示合集列表。按下需要的合集
2. 勾选需要的条目。`{{ui:editor_collections_select-all}}`和`{{ui:editor_collections_select-none}}`勾选全部或取消全部勾选
3. `已选：N，将添加依赖：M`这一行显示将进入关卡的内容。依赖会自动添加
4. 按`导入`

整个导入是一次撤销步骤

纹理、字体和音频会在关卡中得到新的id，它们的文件以唯一的名称复制到关卡文件夹中。关卡中已有字节完全相同的文件时不会再次复制：导入会使用关卡自己的纹理、字体或音轨

### 生成合集

1. `{{ui:editor_collections_target}}`选择`新合集`或你自己的某个合集。新合集的名称取自`{{ui:editor_library_field-name}}`字段
2. 勾选关卡的资源，七类中任意一类都可以
3. 按`{{ui:editor_collections_build}}`

新合集会获得关卡的作者

受保护的关卡不能生成合集。更多：[[13_export-and-protection]]

## 资源选择与搜索

搜索和资源选择窗口中有一个`{{ui:settings_editor-settings_library}}`层级，用于预制件、主题、形状和特效。它显示所有来源。选择窗口指形状、碰撞体、特效和主题字段，以及`{{ui:cmd_editor_place-prefab}}`

从库中选择条目会把它连同依赖一起导入关卡，并完成指定。遇到冲突时，会提出与“合集”标签页相同的问题

关卡各资源标签页里的库浏览器也按同样的方式工作，并显示来源标签。更多：[[11_level-resources]]

## 冲突

要导入的条目可能已经以相同的id存在于关卡中：
- 内容相同：无需任何操作
- 内容不同：打开`{{ui:editor_resource-conflict_title}}`窗口

窗口列出所有冲突，每个冲突都有一个`{{ui:editor_resource-conflict_copy}}`开关：

| 选择 | 结果 |
|---|---|
| 保留（开关关闭） | 关卡的版本保留并被使用 |
| `{{ui:editor_resource-conflict_copy}}` | 合集的版本以新的id加入。与它一起导入的所有内容都指向这个副本 |

`{{ui:editor_resource-conflict_all-keep}}`和`{{ui:editor_resource-conflict_all-copy}}`一次设置所有开关。`导入`应用选择，`{{ui:editor_cancel_text}}`什么都不导入

没有哪个版本会悄悄胜出。每一个内容不同的冲突都在这个窗口中决定

## 署名

关卡的资源记录除了纹理、字体和音频，也涵盖主题、特效、形状和预制件。导入会把需要的记录复制到关卡中，所以署名会随资源一起到达

更多：[[4_resource-record]]

## 磁盘上的位置

合集存放在游戏数据文件夹的`resources/collections/<collection-guid>/`中。这就是`levels`旁边存放本设备共享库的那个`resources`文件夹。更多：[[4_level-folder-and-backups]]

| 路径 | 内容 |
|---|---|
| `collection.json`或`collection.blob` | 清单：名称、描述、作者、许可证、纹理、字体和音频条目，以及其中所有内容的署名信息 |
| `cover.png` | 封面，可选 |
| `prefabs/`、`themes/`、`shapes/`、`effects/` | 每个条目一个`<guid>.json`或`<guid>.blob`，与本设备共享库中的文件相同 |
| `media/` | 纹理、字体和音频文件 |

合集以压缩包的形式传递：在合集页面上用`{{ui:editor_share_share}}`，在列表中用`{{ui:editor_library_import-archive}}`。不是合集的压缩包会被拒绝

接下来：[[17_publishing]]、[[2_reuse]]、[[4_resource-record]]
