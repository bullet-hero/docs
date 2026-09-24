---
title: Servers
date: 2026-09-24
tags: [player, server_host, server_advanced]
---

# Servers

The official server OWS and community servers NOWS: what is decided about them, which builds can connect and what the SDK already does for them

> [!warning] Warning
> There is no server yet, official or community. This section describes only what the developers have already decided, and it will be rewritten once the backend exists. The protocol between the game and a server has not been designed

The section is written for three readers: a player who wants to know which servers a build can reach and what a third-party one can cost, someone planning a server for themselves and friends, and a large host ready to extend or write a server. This page holds what is common to all three

## Two kinds of server

A server in Bullet Hero is a web service that hosts levels. The developers plan two kinds:

| | OWS | NOWS |
|---|---|---|
| Full name | Official Web Services | Non-official web services |
| Who runs it | the developers | anyone |
| Code | open source, MIT | the same open tools, or anything built on them |
| Publishing policy | the `standard` profile, set in the server config | the operator's own profile |
| Moderation | the developers | the operator. The developers neither control nor moderate a community server |
| Builds that can connect | every build, it is the default server | the full build only |

**Steam Workshop** is a third channel for levels, planned for the PC version. It is not a server of this kind: Valve hosts the files, and the developers can only grade them afterwards and decide what the game loads

## Status

- No server exists, and no build of the game can connect to one yet
- The planned order is Steam Workshop first, then OWS, then the Google Play build, then the App Store build
- There are no dates. Publishing levels to any service is planned no earlier than the update after `gv 1.0.0`, because the data the check relies on has to be recorded in levels before they are published
- Playing together on a server is only planned. The developers have worked out how a player's avatar appears and disappears on a network message, but transport, authority, level synchronisation and lobbies are not designed

## Which builds can connect

| Build | Where it comes from | OWS | NOWS |
|---|---|---|---|
| Store build | Google Play, App Store | yes | no |
| Full build | GitHub Releases and the project's site | yes | yes |

**Store builds cannot connect to community servers at all.** Support for them is removed from the program when it is compiled, not hidden behind a setting, because a store judges what the program can do, not which buttons it shows. A community server is a service nobody has moderated for the store, and the store rules require moderation of content shown to other people

The full build is published under its own application id, so on Android it can be installed next to the store version

## EULA

The full build ships with an EULA that states plainly: community servers are third-party services, the developers neither control nor moderate them. Store builds will ask you to accept an EULA before you publish a level. Neither text is written yet

## The SDK and PublishProfile

The server relies on the same open SDK as the game. It is MIT-licensed and builds without Unity, so the client and the server run the same checks over the same models and reach the same verdict. More in the [[3_sdk/index]] section

What a service accepts is described by a file, `PublishProfile`, not by code. Every service has its own:

| Preset | Key | For whom |
|---|---|---|
| `CreateOpen()` | `local` | levels on your own device, nothing is required |
| `CreateStandard()` | `standard` | a public server, the policy from [[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | store builds, no direct URLs, a hash on every resource |

**Nothing is checked on a level that stays on your device.** The profile matters only at the moment a level is offered to a service. How an author prepares a level for that moment is in [[5_publish-readiness]], the fields of the profile are in [[7_publish-profiles]]
