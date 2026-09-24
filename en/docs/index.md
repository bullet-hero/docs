---
title: Documentation
date: 2026-09-24
---

# Documentation

What Bullet Hero consists of, which part of the documentation is for you and how the products are versioned

Bullet Hero is a rhythm game and *bullet hell* hybrid built as an engine for the genre rather than as one game. It is a set of products that share one open level format, and the documentation is split by product first and by reader second

## What Bullet Hero consists of

| Product | What it is | Status | Documentation |
|---|---|---|---|
| Game | the client you play in, on Windows, Linux and Android | released, post-alpha | [[1_game/index]] |
| Level editor | built into the game, the same client | released with the game | [[2_editor/index]] |
| SDK | the open data model of levels and saves, MIT | released | [[3_sdk/index]] |
| Server | the official server OWS and community servers NOWS | planned, not built | [[4_server/index]] |
| This documentation | open markdown pages anyone can fix or translate | open | [[5_contribute/index]] |

The website that shows these pages is a separate, closed product and is not documented here

## Who are you?

| You are | Tag on the pages | Start here |
|---|---|---|
| a player who wants to install the game and play | `player` | [[1_game/index]] |
| a player who wants to know how the mechanics work | `advanced_player` | [[1_game/index]], then [[7_damage]] and [[8_determinism]] |
| someone who makes levels | `level_author` | [[2_editor/index]] |
| a developer building a tool, a mod or a service on the SDK | `developer` | [[3_sdk/index]] |
| someone who wants a server for yourself and friends | `server_host` | [[4_server/index]], then [[2_hosting]] |
| a host ready to run a public server or extend one | `server_advanced` | [[4_server/index]], then [[3_advanced-hosting]] |
| someone who wants to fix a text or add a translation | `contributor` | [[5_contribute/index]] |

Every page shows its tags, so you can tell at a glance whether it was written for you

## How to read the documentation

New to the game? Start with [[0_quick-start]]: six steps from installing the game to your first level, each with a link to the full page

- **The menu on the left** follows the folders of the documentation. A folder has its own landing page: click its name to open it. The arrow opens or closes the folder without leaving the page. The folder of the page you are reading opens by itself, and a folder you opened by hand stays open while the tab is open
- **On a phone** the same menu is a collapsible `Documentation` block above the page. It closes itself after you pick a page
- **The search box** is at the top of this page. It looks through titles, section headings, tags and the full text of every documentation page
- **Tags** at the top of a page name the readers it is written for. The table above says which tag is yours
- **A page not translated yet** is shown in English, with a notice at the top that says so
- **Links between pages** show the title of the page they lead to. Every section heading is a link to that section, so you can copy the address of one section and send it
- **The language switch** keeps you on the same page

These pages are open: a typo, an outdated fact or a missing translation can be fixed by anyone, see [[5_contribute/index]]

## Status

- **The game and the editor** are playable today. The builds are post-alpha: they are unsigned, and a level made now may not load in a later version
- **The SDK** is open under MIT at [github.com/vertoker/bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk)
- **There is no server yet,** official or community. Its section describes only what has been decided
- **These pages** are open at [github.com/vertoker/bullet-hero-docs](https://github.com/vertoker/bullet-hero-docs)

## Versions

Every product of the complex has its own version with a letter prefix, each in the form major.minor.revision:

| Prefix | Product |
|---|---|
| `gv` | the game (the client) |
| `sv` | the SDK |
| `fv` | the website |
| `bv` | the backend, the server |

The numbers do not follow each other. `gv` and `sv` once started equal and are now free to diverge: an SDK change does not have to move the game version, and a game update does not have to move the SDK version. The game's Settings screen shows `gv`, `sv` and `mg` (the generation of the level format) on one line, and clicking the line copies it. More in [[5_versioning]]
