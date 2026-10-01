---
title: Connecting to a server
date: 2026-10-01
tags: [player]
---

# Connecting to a server

The game will have the official server OWS for all builds and community servers NOWS for the full build only. Bullet Hero does not moderate community servers, so connect to those whose owner you know

> [!warning] Warning
> There are no servers yet, and the game cannot connect to them. There is no address format, no connection screen and no accounts

## Which servers there will be

| | OWS | NOWS |
|---|---|---|
| Full name | Official Web Services | Non-official web services |
| Who runs it | Bullet Hero | anyone |
| Who moderates it | Bullet Hero | the server owner |
| Which builds connect | all | the full build only |

**OWS is the default server.** Every build of the game on every platform knows it, nothing needs to be set up

**NOWS are community servers.** Bullet Hero neither controls nor moderates them

**The Steam Workshop is a third channel for levels on PC.** Steam builds list and launch the items you are subscribed to, and publish levels and collections there from the editor - [[17_publishing]]

## Which builds connect

| Build | Where from | OWS | NOWS |
|---|---|---|---|
| Store build | Google Play, App Store | yes | no |
| Full build | [GitHub](https://github.com/bullet-hero/releases) and the project website | yes | yes |

A store build cannot connect to a community server in any way.
NOWS support is cut out of it at compile time, not hidden behind a setting

The reason is store rules. A store judges what a program can do, not which buttons it shows. And content that other people see must be moderated under their rules

The full build is planned to get its own application id, so that on Android it can be installed next to the store version. Right now all Android builds share one id, `com.vertoker.BulletHero`

## What OWS will have

- accounts and terms of use
- a check of every level before publication: a level with an error is rejected, a level with a warning goes to a moderator
- reports on levels and users, and blocking them

What an account stores is not decided yet. The server will have its own privacy policy, which will appear together with the server. It will describe the account and explain how to delete it. The game's and the site's policies do not cover the server - [[game-privacy-policy]], [[privacy-policy]]

## When

Publishing to the Steam Workshop already works in Steam builds. There are no dates for the rest. The order is: OWS, then the Google Play build, then the App Store build

There is no playing together on a server yet, it has not been designed

## Risks of other people's servers

A community server is run by a person you most likely do not know.
Bullet Hero neither controls nor moderates such servers. The full build's EULA says so directly

| Risk | Why |
|---|---|
| Levels with unchecked rights | the owner decides what to check and may check nothing. A level may contain music its author had no right to share |
| Nobody moderates the content | there is no guarantee that anyone looks at what is uploaded |
| Files from other sites | the standard policy lets a level fetch a file by a direct link. When you open such a level, the game downloads the file from a site the level's author chose. That is why store builds forbid it |
| The owner sees your traffic | there is no protocol yet, so it is unknown what exactly the server will receive. Assume the owner sees everything you send |
| The server can disappear | a level that exists only on that server disappears with it |

By default a level is distributed under *CC BY-NC*, and the author can choose another license in the level's metadata. A server must respect the license of every level. Under *CC BY-NC* nobody may host a level commercially, a community server included, and a server that charges money for such levels breaks the license of every one of their authors

> [!tip] Recommendation
> Connect only to servers whose owner you know. Keep your own copy of every level you care about: a level is a folder of files, and the copy on your disk does not depend on any server

## EULA

The full build ships with an EULA. It says: community servers are third-party services, Bullet Hero neither controls nor moderates them

Store builds will ask you to accept an EULA before publishing a level

None of these texts has been written yet

## What to read next

- [[ugc-licensing-policy]] - which rules a level must meet to be published
- [[2_hosting]] - if you want to run a server yourself
