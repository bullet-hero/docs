---
title: Writing pages
date: 2026-09-24
tags: [contributor]
---

# Writing pages

File names and order, frontmatter, the title and summary, audience tags, links, images, callouts and code blocks

## File names and order

- **The order in the sidebar is set by an `N_` prefix** on every file and folder inside `docs/`: `1_`, `2_`, and so on up to `10_` and beyond. The prefix never reaches the address: `1_game/3_controls.md` opens at `/<lang>/docs/game/controls`
- **`index.md` has no prefix.** It is the landing page of its folder, takes the folder's position and gives the sidebar group its name
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

- **On a page in any language, `title`, the H1 and the summary are written in that language.** The example above is from the English version
- **Frontmatter is `title`, `date` and `tags`.** Nothing else is read. `date` is `YYYY-MM-DD`, set when the page is created
- **`# H1` is required and equals `title`.** The site renders only the body, so the H1 is the visible title of the page
- **The first paragraph after the H1 is the description** shown in listings, search and link previews. It is cut at 200 characters, so keep it to one line with no links or formatting
- **Sections are `##`, subsections `###`.** They produce anchors and the table of contents. Deeper levels are not needed

## Audience tags

Every docs page has 1 to 3 tags from this list, written in `snake_case` without `#`. The site shows them on the page

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

The code in the frontmatter never reaches the reader. The label comes from the tag's own page `<lang>/tags/<code>.md`: its `title` is the label, its first paragraph describes the audience, and the site adds the list of tagged pages to it. A new tag needs such a page in every language. To mention a tag in a page's text, link its page, `[[level_author]]`: the link shows the label in the reader's language

## Links

| What | How |
|---|---|
| Another page | `[[3_difficulty-curve]]`, by the full file name with its prefix |
| A section of a page | `[[3_difficulty-curve#Anchor]]` |
| A folder landing | `[[2_editor/4_craft/index]]`, with the path, since every landing is called `index` |
| An external site | `[text](https://…)`, with the full address and scheme |

Links resolve to an address without a language, so the same source works in every language: `[[cookie-policy]]` sends an English reader to the English page and a Russian reader to the Russian one. Link only to pages that exist, since the site build reports every link it cannot resolve

## Images

Images live in `assets/` at the root of the repository and are embedded with `![[file.png]]`. One folder serves every language, so text drawn inside an image is not translated with the page

## Callouts

| Syntax | Colour | Use |
|---|---|---|
| `> [!note]`, `> [!info]`, `> [!tip]` | blue | context, a shortcut, a recommendation |
| `> [!warning]`, `> [!caution]` | amber | costs time or quality, destroys work |
| `> [!danger]`, `> [!bug]` | red | rendered, but the style guide does not use them |

Which callout to pick, its title and the limit of two per page are in [[3_style-guide]]

## Code and other markup

- **Code highlighting** exists only for `ts`, `tsx`, `js`, `json`, `csharp`, `bash`, `yaml`, `css` and `md`. Any other language renders as plain text
- **GFM tables, task lists, footnotes and `==highlights==`** work
- **No MDX and no JSX.** `{` and `<` are shown as they are
