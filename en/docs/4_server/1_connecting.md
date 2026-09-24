---
title: Connecting to a server
date: 2026-09-24
tags: [player]
---

# Connecting to a server

What is already decided about connecting the game to the official and community servers, and what a third-party server can cost you

> [!warning] Warning
> No server exists yet and the game has no way to connect to one. There is no address format, no connection screen and no account system. This page describes only what has been decided

## What is decided

- **OWS is the default server.** Every build of the game will know it without any setup, on every platform
- **Community servers (NOWS) work only in the full build** from GitHub Releases and the project's site. A build from Google Play or the App Store cannot connect to them, the code for it is not in the program
- **OWS will have accounts and terms of service.** What an account holds is not decided. When it is, the privacy policy on the site will describe it and explain how to delete an account
- **Levels on OWS pass a check before they appear.** A level with an error is refused, a level with a warning goes to a moderator. On OWS you will be able to report a level or a user and block them
- **Playing together is not designed.** The developers have worked out only how an avatar appears and disappears when a player connects or leaves. Transport, lobbies and level synchronisation have no design yet

More about the two kinds of server and the builds in [[4_server/index]]

## Risks of third-party servers

A community server is run by someone you most likely do not know. The developers neither control nor moderate such servers, and the EULA of the full build says so. What that means in practice:

| Risk | Why |
|---|---|
| Levels with unchecked rights | the operator sets their own publishing policy, and it may check nothing. A level may carry music its author had no right to share |
| Content nobody moderated | there is no guarantee that anyone looks at what is uploaded |
| Resources fetched from arbitrary addresses | the standard policy lets a level fetch a file by a direct URL, so opening such a level makes the game download from a site chosen by the level's author. Store builds forbid this for that reason |
| The operator sees your traffic | what a server receives from the game depends on the protocol, and the protocol does not exist yet. Treat anything you send as visible to the operator |
| The server can disappear | a level that exists only on one community server is gone with it |

Levels are licensed under *CC BY-NC*, so nobody may host them commercially, a community server included. A server that charges for levels breaks the license of every author on it

> [!tip] Recommendation
> Connect only to community servers whose operator you know, and keep your own copy of every level you care about. A level is a folder of files, and a copy on your disk does not depend on any server

## Read next

- [[ugc-licensing-policy]] - the rules a level has to meet to be published
- [[2_hosting]] - if you want to run a server yourself
