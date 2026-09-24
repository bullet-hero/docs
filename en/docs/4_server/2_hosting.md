---
title: Hosting a server for friends
date: 2026-09-24
tags: [server_host]
---

# Hosting a server for friends

What running a small community server will require, as far as it is known before the server exists

> [!warning] Warning
> The server tools are not released and the protocol is not designed. This page is a stub: it lists what is already decided and marks everything else as unknown

## What you will need

- **The server tools.** They will be open source under MIT, the same code the official server runs. They are not published yet
- **The full build of the game for everyone who connects.** Builds from Google Play and the App Store cannot connect to community servers, so your friends need the build from GitHub Releases or the project's site
- **A publishing profile.** A `PublishProfile` file decides which levels your server accepts: which licenses, how resources may be fetched, the size limits. You can start from the `standard` preset the official server uses and loosen or tighten it without changing any code. The fields are described in [[7_publish-profiles]]
- **A machine to run it on.** The system requirements, the runtime, the ports and the way to start the server are not known yet

## What you take on

- **Moderation is yours.** The developers do not moderate community servers, and the EULA of the full build tells every player so
- **No commercial use.** Levels are licensed under *CC BY-NC*: you may host and share them for free, but not charge for them or earn from them in any other way. The permission comes from each level's author, not from the game, so the developers cannot grant an exception
- **Rights to the resources.** A level can carry music and images from other people. How strict your server is about this is up to your profile, but a complaint about a work will come to you. The rules the official server follows are in [[ugc-licensing-policy]]

## What is not known

- how the game finds a server and connects to it
- whether a community server has accounts
- how levels are uploaded and listed
- whether a server for a few people will differ from a public one in setup

Once the tools are released this page will be rewritten with real steps. Until then, what already exists for a larger server is in [[3_advanced-hosting]]
