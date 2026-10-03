---
title: Why Bullet Hero
date: 2026-10-03
tags: [player, level_author]
---

# Why Bullet Hero

Bullet Hero is free, runs on Windows and Android, and its SDK, docs and builds are open. The core holds thousands of objects on screen on phones and is covered by more than 8000 tests

## Free

The game is free and will stay free. There will be no purchases, ads or paid content in it

I do not rule out monetization through voluntary donations, but nothing beyond that

## Available everywhere, everything is universal

The game is everywhere I have been able to port it to
- Platforms: Windows, Android (later iOS, Linux, Mac)
- Stores: Steam, Google Play (later App Store)

Everything in the game works with any controls, levels are the same everywhere, and every part of the game (the editor, multiplayer, servers) works the same everywhere

## A high degree of open code

The SDK, the docs, the builds and the server are in open repositories. Only the game itself and the site are closed.
All repositories - [[links]]

## The fastest technical core

Thousands of objects on screen, hundreds of effects and texts at once. And all of it runs on phones with a target of 60 FPS (often more)

## A very stable technical core

The game has a large number of mechanisms that keep the game and its data models stable
- Versioning of everything (more here - [[5_versioning]])
- Multimodal versioning and data migration, level data will not break
- More than 8k tests across the whole game, literally every aspect of the game is covered by tests

And many other checks. Together with the fast core, this gives a very high ratio of stability to performance

## Multiplayer (in development)

Multiplayer in any form: on one device, local multiplayer, through a server, and many interesting interactions

## Open servers (in development)

An official server and community servers that anyone can run. The server code will be open. Level catalogs and basic communication will arrive together with the server.
More - [[4_server/index]]

## Many languages

The game aims to support most of the world's languages out of the box. I believe a game should have no language barrier at all

Of course, no one can know every language in the world, but thanks to advances in AI and the community this goal is quite achievable

## Open licensing policy

All game data comes with a flexible choice of licenses (mostly [Creative Commons](https://creativecommons.org/))
for your levels and the resources you use. This makes reusing other people's resources more open

More - [[ugc-licensing-policy]]

## Integration with every service where possible

The game has more than 10 build variants, and each of them has its own integrations depending on the store it is distributed through

More - [[download]]

## Determinism and stability

The game has deterministic randomness, and every factor of it is tied to the seed and the level's parameters.
This means randomness can always be repeated if you know the level and have the seed

More - [[8_determinism]]

## Editor

The game has a large and flexible level editor, in which you can create almost anything

The editor has a large number of unique features: [[8_generators]], debugging and more

## Open level format

The C# SDK reads and writes levels the same way the game does. The game and the server work through it, and so can you.
With it you can create your own unique levels or resources, or your own services built on top of it

More - [[3_sdk/index]]
