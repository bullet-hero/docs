---
title: Welcome
date: 2026-09-24
---

# Welcome

The official documentation of Bullet Hero, a hybrid of a rhythm game and *bullet hell*, built as an engine for the genre.
Bullet Hero is not only a game, it is a software complex of several products

| Product | Documentation |
|---|---|
| Game | [[1_game/index]] |
| Level editor | [[2_editor/index]] |
| SDK | [[3_sdk/index]] |
| Server | [[4_server/index]] |
| Documentation | [[5_contribute/index]] |

Everything you can download is here - [[download]]

If you want to start playing quickly - [[0_quick-start]]

## Categories

Different people care about different parts of the documentation, and it is written for all of them

| You are | Where to start |
|---|---|
| [[player]] or [[advanced_player]] | [[1_game/index]] |
| [[level_author]] | [[2_editor/index]] |
| [[developer]] | [[3_sdk/index]] |
| [[server_host]] | [[4_server/index]], then [[2_hosting]] |
| [[server_advanced]] | [[4_server/index]], then [[3_advanced-hosting]] |
| [[contributor]] | [[5_contribute/index]] |

## Versions

Every product has its own version with a letter prefix, each in the form major.minor.revision:

| Prefix | Stands for | Product |
|---|---|---|
| `gv` | `game version` | the game (the client) |
| `sv` | `sdk version` | the SDK |
| `fv` | `frontend version` | the website |
| `bv` | `backend version` | the backend, the server |

The version numbers do not have to follow each other, but in most cases they match.
Versions are also bumped together, and a shared update carries the same version

There is also a separate version of levels, `mg` (`model generation`). It is a plain number in every save that describes the version of the data.
It matters much more than all the others and is used everywhere for updating and support. More in [[5_versioning]]

## Source code

Every repository lives in the [bullet-hero](https://github.com/bullet-hero) organization

| Repository | Access | What it holds |
|---|---|---|
| [game](https://github.com/bullet-hero/game) | closed | the game and the editor |
| [sdk](https://github.com/bullet-hero/sdk) | open | the SDK, issues about the SDK and its code |
| [releases](https://github.com/bullet-hero/releases) | open | game builds, issues from players |
| [docs](https://github.com/bullet-hero/docs) | open | this documentation |
| [backend](https://github.com/bullet-hero/backend) | open | the server, empty for now |
| [frontend](https://github.com/bullet-hero/frontend) | closed | the website |

Found a bug in the game? Write to the [releases issues](https://github.com/bullet-hero/releases/issues). More - [[11_help]]
