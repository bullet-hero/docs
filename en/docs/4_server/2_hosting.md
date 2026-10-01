---
title: Server for friends
date: 2026-10-01
tags: [server_host]
---

# Server for friends

You will need the open server tools, the full build of the game for every player and a PublishProfile file. Moderation and respecting level licenses are on the server owner

> [!warning] Warning
> The server tools are not released, the protocol is not designed. This page holds only what has already been decided

## What you will need

- **Server tools.** They will be open, under MIT. This is the same code the official server runs on. You can build your own server on these tools or on anything based on them
- **The full build of the game for everyone who connects.** Builds from Google Play and the App Store do not connect to community servers. The full build is on [GitHub](https://github.com/bullet-hero/releases) and on the project website
- **A publish profile.** The `PublishProfile` file decides which levels your server accepts. More - [[7_publish-profiles]]
- **A machine for the server.** System requirements, runtime, ports and the way to launch it are not known yet

## Publish profile

The profile sets which licenses are accepted, where a level may fetch files from and what its size limit is.
No code needs to change for that

The official server runs on the `standard` preset, set in the server config. Start from it and loosen or tighten it to suit you

## What you take on

- **Moderation.** Bullet Hero does not moderate community servers. The full build's EULA tells every player so
- **No commerce.** By default a level is distributed under *CC BY-NC*, and the author can choose another license. Respect the license of every level. A level under *CC BY-NC* may be hosted and shared for free, but you may not charge money for it or earn from it in any other way
- **Rights to resources.** A level may contain someone else's music and graphics. How strictly to check this is decided by your profile. But a complaint about someone else's work will come to you. The official server's rules - [[ugc-licensing-policy]]

Permission for non-commercial distribution is given by the author of each level, not by the game. So only the author can make an exception

## What is unknown

- how the game finds a server and connects to it
- whether a community server will have accounts
- how levels are uploaded and get into the list
- whether a server for a few people will be configured differently from a public one

What already exists for a large server - [[3_advanced-hosting]]
