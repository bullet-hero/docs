---
title: Hosting a server for friends
date: 2026-09-24
tags: [server_host]
---

# Hosting a server for friends

What a small community server will require and what is already known about it

> [!warning] Warning
> The server tools are not released and the protocol is not designed. This page holds only what is already decided

## What you will need

- **The server tools.** They will be open source, under MIT. It is the same code the official server runs. You can build your server on these tools or on anything based on them
- **The full build of the game for everyone who connects.** Builds from Google Play and the App Store cannot connect to community servers. The full build is on [GitHub](https://github.com/bullet-hero/releases) and on the project's site
- **A publishing profile.** A `PublishProfile` file decides which levels your server accepts. More - [[7_publish-profiles]]
- **A machine for the server.** The system requirements, the runtime, the ports and the way to start it are not known yet

## The publishing profile

The profile sets which licenses are accepted, where a level may fetch files from and how large it may be.
No code has to change for that

The official server runs the `standard` preset, set in its server config. Start from it and loosen or tighten it to suit you

## What you take on

- **Moderation.** The developers do not moderate community servers. The EULA of the full build tells every player so
- **No commercial use.** A level is licensed under *CC BY-NC* by default, and its author may pick another license. Follow each level's own license. A *CC BY-NC* level may be hosted and shared for free, but you may not charge for it or earn from it in any other way
- **Rights to the resources.** A level can carry other people's music and images. How strictly to check that is up to your profile. But a complaint about someone's work will come to you. The rules of the official server - [[ugc-licensing-policy]]

The permission to share non-commercially comes from each level's author, not from the game. So the developers cannot grant an exception

## What is not known

- how the game finds a server and connects to it
- whether a community server has accounts
- how levels are uploaded and listed
- whether a server for a few people will be set up differently from a public one

What already exists for a larger server - [[3_advanced-hosting]]
