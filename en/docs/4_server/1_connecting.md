---
title: Connecting to a server
date: 2026-09-24
tags: [player]
---

# Connecting to a server

Which servers the game will have, which builds can connect to them and what a player risks on someone else's server

> [!warning] Warning
> No server exists yet, and the game cannot connect to one. There is no address format, no connection screen and no accounts

## Which servers there will be

| | OWS | NOWS |
|---|---|---|
| Full name | Official Web Services | Non-official web services |
| Who runs it | the developers | anyone |
| Who moderates it | the developers | the operator |
| Builds that can connect | all | the full build only |

**OWS is the default server.** Every build of the game knows it on every platform, with nothing to set up

**NOWS are community servers.** The developers neither control nor moderate them

**Steam Workshop is a third channel for levels on PC.** Steam builds already list and play the items you subscribed to. Publishing a level there from the game is not possible yet

## Which builds can connect

| Build | Where it comes from | OWS | NOWS |
|---|---|---|---|
| Store build | Google Play, App Store | yes | no |
| Full build | [GitHub](https://github.com/bullet-hero/releases) and the project's site | yes | yes |

A store build cannot connect to a community server in any way.
NOWS support is cut out of it when it is compiled, not hidden behind a setting

The reason is the store rules. A store judges what a program can do, not which buttons it shows. And by their rules, content shown to other people has to be moderated

The full build is planned to get its own application id, so that on Android it can be installed next to the store version. Today every Android build shares one id, `com.vertoker.BulletHero`

## What OWS will have

- accounts and terms of service
- a check of every level before it is published: a level with an error is refused, a level with a warning goes to a moderator
- reports and blocking of levels and users

What an account holds is not decided yet. The server will have its own privacy policy, written when the server exists. It will describe the account and explain how to delete it. The game's and the site's policies do not cover the server - [[game-privacy-policy]], [[privacy-policy]]

## When

There are no dates. The order is: publishing to Steam Workshop, then OWS, then the Google Play build, then the App Store build

Publishing levels to any service will arrive no earlier than the update after `gv 1.0.0`

Playing together on a server does not exist yet and is not designed

## Risks of third-party servers

A community server is run by someone you most likely do not know.
The developers neither control nor moderate such servers. The EULA of the full build says so plainly

| Risk | Why |
|---|---|
| Levels with unchecked rights | the operator decides what to check and may check nothing. A level may carry music its author had no right to share |
| Nobody moderates the content | there is no guarantee that anyone looks at what is uploaded |
| Files from other sites | the standard policy lets a level fetch a file by a direct URL. Opening such a level makes the game download from a site chosen by the level's author. That is why store builds forbid it |
| The operator sees your traffic | there is no protocol yet, so it is unknown what exactly the server receives. Treat anything you send as visible to the operator |
| The server can disappear | a level that exists only on that server is gone with it |

A level is licensed under *CC BY-NC* by default, and its author may pick another license in the level's metadata. A server has to respect each level's own license. Under *CC BY-NC* nobody may host a level commercially, a community server included, and a server that charges for such levels breaks the license of every author on it

> [!tip] Recommendation
> Connect only to servers whose operator you know. Keep your own copy of every level you care about: a level is a folder of files, and a copy on your disk does not depend on any server

## EULA

The full build ships with an EULA. It says: community servers are third-party services, the developers neither control nor moderate them

Store builds will ask you to accept an EULA before you publish a level

Neither text is written yet

## Read next

- [[ugc-licensing-policy]] - the rules a level has to meet to be published
- [[2_hosting]] - if you want to run a server yourself
