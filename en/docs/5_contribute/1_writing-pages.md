---
title: Writing pages
date: 2026-09-24
tags: [contributor]
---

# Writing pages

Where the pages live, how to send a change and how to lay out a page: file names, frontmatter, tags, links, images, callouts

## Three repositories

| Repository | What it holds |
|---|---|
| [bullet-hero-releases](https://github.com/vertoker/bullet-hero-releases) | releases hold every public build of the game, issues hold bugs and requests about the game from players |
| [bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk) | the SDK code, issues hold bugs and requests about the SDK |
| [bullet-hero-docs](https://github.com/vertoker/bullet-hero-docs) | these pages and their translations |

This page is about the last one, bullet-hero-docs

## How to send a change

1. Fork [bullet-hero-docs](https://github.com/vertoker/bullet-hero-docs) and create a branch
2. Edit or add pages in the format described below
3. Change the page in every language, or say in the pull request which languages still need the change. More - [[2_translating]]
4. Check the text against the [[3_style-guide]]
5. Open a pull request with a short description of what changed and why

**Facts come from the game, the SDK or their documentation.** Numbers, field names, file names, shortcuts and addresses are never guessed. Not sure something is true? Say so in the pull request, not in the page

A merged change does not appear on [bullethero.space](https://bullethero.space/) at once, but with the next site update

> [!tip] Tip
> You cannot build the site yourself, since its code is closed. Obsidian is the closest preview: a link that Obsidian cannot resolve will not resolve on the site either

## How the repository works

- **Markdown only.** There is no build of its own and no scripts
- **It is an [Obsidian](https://obsidian.md/) vault.** Open the repository's root folder as a vault, and links, embeds and previews work the same way they do on the site. Any other markdown editor works too
- **It is a submodule of the site.** The site includes the repository as its `content/` folder, compiles the pages when it is built and prerenders every one. A change reaches the site when the site's pointer to this repository is moved forward

## What goes where

| Path | What it holds | Address on the site |
|---|---|---|
| `<lang>/docs/1_game/` | players: installing, playing, settings, the mechanics | `/<lang>/docs/game` |
| `<lang>/docs/2_editor/` | level authors: the editor guide and reference | `/<lang>/docs/editor` |
| `<lang>/docs/3_sdk/` | developers: the open SDK and the level format | `/<lang>/docs/sdk` |
| `<lang>/docs/4_server/` | server hosts: official and community servers | `/<lang>/docs/server` |
| `<lang>/docs/5_contribute/` | this section | `/<lang>/docs/contribute` |
| `<lang>/notes/` | articles, public documents and policies, sorted by date | `/<lang>/notes/<name>` |
| `<lang>/tags/` | tag pages | `/<lang>/tags/<tag>` |
| `<lang>/download.md` | the download page | `/<lang>/download` |
| `assets/` | images for every language | embedded in pages |

`<lang>` is a language folder: `en` or `ru`. A file outside `docs/`, `notes/`, `tags/` and `download.md` does not become a page

**Docs describe how things work now.** A story of how something changed, an opinion or an essay belongs in `notes/`

## File names and order

- **The order in the sidebar is set by an `N_` prefix** on every file and folder inside `docs/`: `1_`, `2_`, and so on, up to `10_` and beyond
- **The prefix never reaches the address.** `1_game/3_controls.md` opens at `/<lang>/docs/game/controls`
- **`index.md` has no prefix.** It is the landing page of its folder. It takes the folder's position and gives the sidebar group its name
- **To reorder pages, rename them.** Enable "Automatically update internal links" in Obsidian and it fixes every link for you
- **A name without its prefix is unique within a language.** If two files collapse to the same address, the site build reports it
- **A prefixed name is identical in every language.** `en/docs/2_editor/4_craft/3_difficulty-curve.md` and `ru/docs/2_editor/4_craft/3_difficulty-curve.md` are the same page
- **`notes/` has no prefixes and no subfolders.** Never rename `notes/cookie-policy`: the site's cookie banner links to it

## Frontmatter, title and summary

Every page starts like this:

```md
---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

One line that says what the page is, up to 200 characters, no markup
```

- **`title`, the H1 and the summary are written in the page's language.** The example above is from the English version
- **Frontmatter is `title`, `date` and `tags`.** Nothing else is read. `date` is `YYYY-MM-DD`, set when the page is created
- **`# H1` is required and equals `title`.** The site shows only the body, so the H1 is the visible title of the page
- **The first paragraph after the H1 is the description** shown in listings, search and link previews. It is cut at 200 characters. Write it as one line, with no links or formatting
- **Sections are `##`, subsections `###`.** They produce anchors and the table of contents. Deeper levels are not needed

## Audience tags

Every docs page has 1 to 3 tags from this list. Tags are written in `snake_case` without `#`. The site shows them on the page

| Tag | Shown as | Who |
|---|---|---|
| `player` | [[player]] | a regular player |
| `advanced_player` | [[advanced_player]] | a player who wants the mechanics |
| `level_author` | [[level_author]] | makes levels in the editor |
| `developer` | [[developer]] | builds on the SDK or extends the game |
| `server_host` | [[server_host]] | runs a server for themselves and friends |
| `server_advanced` | [[server_advanced]] | a large host, invested enough to extend or write a server |
| `contributor` | [[contributor]] | edits the texts and translations in this repository |

Notes in `notes/` use topic tags instead, currently `legal` ([[legal]])

The reader never sees the tag code. The label comes from the tag's page `<lang>/tags/<code>.md`:

- its `title` is the label
- its first paragraph describes the audience
- the site adds the list of tagged pages itself

A new tag needs such a page in every language

To mention a tag in the text, link its page: `[[level_author]]`. The link shows the label in the reader's language

## Links

| What | How |
|---|---|
| Another page | `[[3_difficulty-curve]]`, by the full file name with its prefix |
| A section of a page | `[[3_difficulty-curve#Anchor]]` |
| A folder landing | `[[2_editor/4_craft/index]]`, with the path, since every landing is called `index` |
| An external site | `[text](https://…)`, with the full address and scheme |

Links resolve to an address without a language, so one source works in every language. `[[cookie-policy]]` sends an English reader to the English page and a Russian reader to the Russian one

Link only to pages that exist. The site build reports every link it cannot resolve

## Images

Images live in `assets/` at the root of the repository and are embedded with `![[file.png]]`

One folder serves every language. Text drawn inside an image is not translated with the page

## Callouts

| Syntax | Colour | Use |
|---|---|---|
| `> [!note]`, `> [!info]`, `> [!tip]` | blue | context, a shortcut, a recommendation |
| `> [!warning]`, `> [!caution]` | amber | costs time or quality, destroys work |
| `> [!danger]`, `> [!bug]` | red | rendered, but the style guide does not use them |

Which callout to pick, its title and the limit of two per page - [[3_style-guide]]

## Code and other markup

- **Code highlighting** exists only for `ts`, `tsx`, `js`, `json`, `csharp`, `bash`, `yaml`, `css` and `md`. Any other language renders as plain text
- **GFM tables, task lists, footnotes and `==highlights==`** work
- **No MDX and no JSX.** `{` and `<` are shown as they are
