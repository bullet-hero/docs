---
title: Contributing
date: 2026-09-24
tags: [contributor]
---

# Contributing

How the documentation repository works, where each kind of page goes and how a change reaches the site through a pull request

The documentation is open so anyone can fix a mistake, fill a gap or add a translation. The site's own code is closed, but every page it shows comes from the public repository [github.com/vertoker/bullet-hero-docs](https://github.com/vertoker/bullet-hero-docs)

## How the repository works

- **It is plain markdown and nothing else.** The repository has no build of its own and no scripts
- **It is an [Obsidian](https://obsidian.md/) vault.** Open the repository's root folder as a vault, and links, embeds and previews work the same way they do on the site. Any other markdown editor works too
- **It is a submodule of the site.** The site includes the repository as its `content/` folder, compiles the pages when it is built and prerenders every one of them
- **A merged change is not live at once.** The site picks it up when its pointer to this repository is moved forward, so the change appears on [bullethero.space](https://bullethero.space/) with the next site deploy

## What goes where

| Path | What it holds | Address on the site |
|---|---|---|
| `<lang>/docs/1_game/` | players: installing, playing, settings, the mechanics | `/<lang>/docs/game` |
| `<lang>/docs/2_editor/` | level authors: the editor guide and reference | `/<lang>/docs/editor` |
| `<lang>/docs/3_sdk/` | developers: the open SDK and the level format | `/<lang>/docs/sdk` |
| `<lang>/docs/4_server/` | server hosts: official and community servers | `/<lang>/docs/server` |
| `<lang>/docs/5_contribute/` | this section | `/<lang>/docs/contribute` |
| `<lang>/notes/` | articles, public documents and policies, sorted by date | `/<lang>/notes/<name>` |
| `<lang>/download.md` | the download page | `/<lang>/download` |
| `assets/` | images for every language | embedded in pages |

`<lang>` is a language folder: `en` or `ru`. A file outside `docs/`, `notes/` and `download.md` does not become a page. `notes/` has no subfolders

**Docs describe how things work now.** A story of how something changed, an opinion or an essay belongs in `notes/`

## The pull request process

1. Fork the repository and create a branch
2. Edit or add pages. Change every language version, or say in the pull request which languages still need the change
3. Follow the [[3_style-guide]]
4. Open a pull request with a short description of what changed and why

**Facts come from the game, the SDK or its documentation.** Numbers, field names, file names, shortcuts and addresses are never guessed. If you are not sure something is true, say so in the pull request, not in the page

> [!tip] Tip
> You cannot build the site yourself, since its code is closed. Obsidian is the closest preview: a link that Obsidian cannot resolve will not resolve on the site either

## Pages in this section

- [[1_writing-pages]] - file names, frontmatter, headings, links, images, callouts
- [[2_translating]] - how languages mirror each other and what to do when they differ
- [[3_style-guide]] - how a page should sound, with before and after examples
