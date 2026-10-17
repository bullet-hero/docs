---
title: Game privacy policy
date: 2026-10-17
tags: [legal]
---

# Game privacy policy

The developer of Bullet Hero does not collect, receive, sell or share any personal data. The game has no accounts of its own, no advertising, no analytics, no crash reporting, no tracking and no advertising identifier. Everything the game remembers about you stays on your own device, except what you let a store keep for you under your own account with that store

These things can leave your device, and none of them goes to the developer:

- a level you open may reference a file hosted on a third-party website, and loading it contacts that website ([[game-privacy-policy#Network access]])
- a level or a profile file you deliberately share with someone else travels wherever you send it ([[game-privacy-policy#Levels you share]])
- in the Steam builds, the game talks to the Steam Workshop through the Steam client ([[game-privacy-policy#Steam Workshop]])
- in the Steam builds, the game keeps a copy of your saves in Steam Cloud and reports your achievements to Steam ([[game-privacy-policy#Steam Cloud and achievements]])
- in the Steam builds, the game shows your current activity on Discord through the Discord client ([[game-privacy-policy#Discord Rich Presence]])
- in the Google Play build, the game reports your achievements to Google Play Games and asks Google Play about updates and ratings ([[game-privacy-policy#Google Play]])
- in the RuStore build, the game asks the RuStore app about updates and ratings ([[game-privacy-policy#RuStore]])
- on a computer, an AI program you connect to the level editor sees the level you have open ([[game-privacy-policy#AI assistant in the editor]])

| | |
|---|---|
| Effective date | 17 October 2026 |
| Policy version | 1.4 |
| Application | Bullet Hero: `com.vertoker.BulletHero` on Android, `com.vertoker.Bullet-Hero` on iOS, and the desktop builds for Windows, Linux and macOS |
| Developer | vertoker, an individual developer |
| Contact | [kostyachurakov@gmail.com](mailto:kostyachurakov@gmail.com) |

This policy covers the game only. The website has its own policy - [[privacy-policy]]. The server will have its own policy too, written when the server exists

## Who this policy applies to

This policy covers every build of Bullet Hero, on every platform and every storefront it is distributed through, and every version of the game to which no newer policy is attached

Where a store (Google Play, the App Store, Steam, RuStore, VK Play or any other) collects data of its own about your purchase, installation or use of the application, that collection is governed by that store's own privacy policy and not by this one. The developer receives from those stores only what they choose to show every developer: aggregate, anonymous statistics about installations, crashes and achievements that cannot be traced back to an individual player

## What is stored on your device

The game writes the following into its own application storage, and reads it back on the next launch:

- **Settings**: graphics, audio, controls, keybindings, interface and language preferences
- **Progress and statistics**: attempts, best results, deaths, time played and similar records, both device-wide and per level
- **Achievements**: which achievements you have unlocked and when
- **Levels**: the levels you create, import or download, including their audio, images and other media, plus their automatic backups and, if you use the AI assistant, its notes in the level's `ai` folder
- **Avatar skins**: the skins you make or import, and which one you wear
- **Device performance profile**: if you run the stress test, its timings together with the device model, the name of the graphics chip and the screen size. It is used only to rate how heavy a level is on this device and never leaves the device: neither a profile transfer nor Steam Cloud carries it
- **Local state**: the editor's AI assistant settings, the state of the last Steam Cloud sync, and on Android the time the game last asked you to rate it
- **Diagnostic logs**: the engine's own log file, written locally so that a problem can be investigated on the device where it happened

None of this is sent to the developer, and none of it is backed up to any service operated by the developer. Only Steam Cloud, in the Steam builds, keeps a copy under your Steam account ([[game-privacy-policy#Steam Cloud and achievements]]). Where it lives depends on the platform:

- **Android and iOS**: the game's private storage. Other applications cannot read it, and it is deleted together with the game when you uninstall it
- **Windows, Linux and macOS**: the application-data folder in your user profile, the engine's standard location. Other programs running under your account can read it, as they can any of your files, and it stays there after the game is uninstalled until you delete that folder. The uninstaller that comes with the free builds (`unins000`) removes only the game's own files and leaves this folder alone

The game also offers, in `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}`, explicit controls for deleting stored statistics and backups without uninstalling

The game does not request access to your contacts, photos, camera, microphone, location, calendar, call log, installed-application list, or any other sensitive resource, and it asks for no runtime permissions at all

## Network access

Bullet Hero has no server. The developer operates no service the game connects to, and therefore receives no data from it

A level is a folder of files, and its author may point one of those files at an internet address instead of shipping it inside the folder. When you open such a level, the game downloads that file from whatever website its author chose. That website then sees what any website sees when a file is requested from it, most notably your IP address and the technical details of the request. The developer neither controls nor observes those requests, and no record of them is kept

Apart from that, the game makes network requests only through the store or the application it came with, and only in that store's build:

- the Steam builds: the Steam Workshop, Steam Cloud and Steam achievements through the Steam client, and Discord Rich Presence through the Discord client
- the Google Play build: Google Play Games achievements, the update check and the rating request through Google Play on the phone
- the RuStore build: the update check and the rating request through the RuStore app on the phone

Every other build makes none of these requests: the code for each store is compiled into that store's build only. The AI assistant in the editor listens only on the computer's own loopback address and cannot be reached from the network ([[game-privacy-policy#AI assistant in the editor]])

## Steam Workshop

The Steam builds use the Steam Workshop through the Steam client running on your computer. Builds for every other store never start Steam: the code that talks to it is compiled into the Steam builds only

The game asks Steam which Workshop items your account is subscribed to, so that it can list them as levels and collections. The Steam client downloads them. When you choose to publish a level or a collection, the game hands it to the Steam client together with the title, description, preview image, content descriptors and visibility you set, and Steam stores it on its servers under your Steam account. A public item can be seen by anyone on Steam until you remove it there

All of this passes between the Steam client and Valve's servers and is governed by Steam's own privacy policy and the Steam Subscriber Agreement. The developer receives nothing from it beyond what Steam shows every developer about a Workshop item

## Steam Cloud and achievements

In the Steam builds the game keeps a copy of your settings, statistics, achievements, levels, library and avatar skins in Steam Cloud, under your Steam account. It reads that copy at launch and writes changes while you play and when you quit, through the Steam client. Graphics and controls settings, backups, error reports, recordings, the device performance profile and the editor's local state never go there. Steam Cloud can be turned off for the game in its properties in Steam, and the game then keeps everything on this computer only

Each achievement you unlock is also reported to Steam, which shows it on your Steam profile according to your Steam privacy settings

Both are stored on Valve's servers and are governed by Steam's own privacy policy and the Steam Subscriber Agreement. The developer receives nothing from them beyond what Steam shows every developer, such as the share of players who unlocked each achievement

## Discord Rich Presence

The Steam builds can show what you are doing in the game in your Discord profile: the menu, the level editor, the sandbox or the level you are playing, and for how long. A level is named, together with its authors, only when it is already public - a Steam Workshop item or a level that ships with the game. Any other level is shown only as a custom level, and the level you are editing is never named. This only works while the Discord app is running on the same computer. Builds for every other store have no Discord integration: the code that talks to Discord is compiled into the Steam builds only

The game hands that activity to the Discord client on your device, never to a server of its own. The Discord client then publishes it under your Discord account, and your Discord friends and servers can see it. The game does not sign in to Discord, does not read your messages, servers or friends list and sends nothing on your behalf

What happens to that activity on Discord's side is governed by the [Discord Privacy Policy](https://discord.com/privacy). The developer receives nothing from it. You can hide your activity at any time in Discord: `User Settings` -> `Activity Privacy`

## Google Play

The Google Play build uses three services of Google Play on your phone:

- **Google Play Games**: if you are signed in to Google Play Games, each achievement you unlock is also reported there, under your Google account, and shown in your Play Games profile. The game only asks Play Games whether you are signed in and which achievements are already unlocked. It does not read your name, your friends or anything else from your account. Signing in is handled by Google Play Games itself, and without it the achievements stay in the game alone
- **Updates**: when the main menu opens, the game asks Google Play whether a newer version is available, and Google Play downloads it in the background
- **Rating**: after a cleared level, from the third one and at most once in 60 days, the game asks Google Play to show its rating window. Whether the window appears, and what you write in it, is up to Google Play: the game never sees your rating or your review

What Google does with this data is governed by the [Google Privacy Policy](https://policies.google.com/privacy). The developer receives nothing from it beyond what Google Play shows every developer, such as published reviews and the share of players who unlocked each achievement

## RuStore

The RuStore build uses the RuStore app on your phone for two things, and only while that app is installed:

- **Updates**: when the main menu opens, the game asks RuStore whether a newer version is available, and RuStore downloads it in the background
- **Rating**: after a cleared level, from the third one and at most once in 60 days, the game asks RuStore to show its rating window. Whether the window appears, and what you write in it, is up to RuStore: the game never sees your rating or your review

What RuStore does with this data is governed by RuStore's own documents. The developer receives nothing from it beyond what RuStore shows every developer

## AI assistant in the editor

On Windows, Linux and macOS the level editor can let an AI assistant program edit the open level. It is off until you turn on `{{ui:settings_game-editor_mcp-enabled}}` in `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor_mcp_title}}`. While it is on, the game listens only on the computer's own loopback address, accepts one program at a time and lets it in only with a random token written to a file in the game's storage. Nothing outside this computer can connect

The program you connect is your own choice and is not part of the game. It can read the open level, its resources and music, and pictures of the playfield, and it may send them to whoever runs its AI model. What happens to them there is governed by that program's own terms and privacy policy. The developer receives nothing from it

## Levels you share

Levels are portable by design: a level can be exported as an ordinary archive file and sent to another person by any means you choose. Such a file travels directly between you and the recipient, or through whatever service you use to send it. It does not pass through the developer, and the developer keeps no copy of it

The same holds for the other files the game can write for you to move: a profile file made with `{{ui:settings_profile-transfer_title}}`, which holds your levels, statistics, settings, library and avatar skins, and an avatar skin exported on its own

A level you create may contain your own music, images and text, and, if you put them there, your name or nickname. Anything you place inside a level is visible to everyone you give that level to. Deciding what to include is yours alone. If you use the AI assistant, the notes it keeps in the level's `ai` folder go with the level's exports and Workshop uploads unless `{{ui:settings_level-settings_metadata-level-ai-share}}` is cleared, and a password-protected export never carries them

A level may optionally be protected with a passphrase. That passphrase is used to encrypt the level's content on your device and is never written to disk, never logged and never transmitted. If you lose it, neither the developer nor anyone else can recover the level's content

## Children

The game collects no personal data from anyone, and that includes children. It contains no advertising, no in-app purchases, no chat and no other communication feature, and no mechanism by which a child could disclose personal information to the developer or to another player through the game itself

Because levels may be shared as files and may contain arbitrary text, images and audio chosen by their author, parents and guardians remain responsible for the levels a child obtains from other people

## Third-party components

The game is built with the Unity engine. **Unity's own data-collecting services (Unity Analytics, Unity Ads, Unity In-App Purchasing, Unity Cloud Diagnostics, engine diagnostics, hardware statistics, crash reporting and performance reporting) are all disabled in this project**, and the packages providing them are not included in the build. No advertising, analytics, attribution or crash-reporting SDK of any kind is present

A store's build carries that store's own library, and no other build does: Steamworks (through Facepunch.Steamworks) and the Discord Social SDK in the Steam builds, Google Play Games Services and the Google Play review and in-app update libraries in the Google Play build, the RuStore review and app-update SDK in the RuStore build. Each of them talks only to its own service, as described above

## Your rights

Regulations such as the GDPR, the UK GDPR, the CCPA/CPRA and Russian Federal Law No. 152-FZ grant you rights of access to, correction of, deletion of, and objection to the processing of your personal data

Because the developer holds no personal data about you whatsoever, there is nothing to access, correct, export or delete on the developer's side, and no request is needed to exercise those rights. The data described in [[game-privacy-policy#What is stored on your device]] is under your own control: it can be inspected in the game's storage folder on your device, cleared from within the game, or removed entirely by uninstalling the application. A copy a store keeps under your account (Steam Cloud, achievements on Steam or in Google Play Games) is held by that store, and those rights over it are exercised with that store, under its own policy. You may still write to the contact address above with any question about this policy

## Data retention

The developer retains no personal data and therefore has no retention period to declare. Data stored on your device is kept for as long as you keep it there. A copy a store keeps under your account is retained by that store under its own policy

## Changes to this policy

This policy will change if the game does, most likely when the game's own server, player accounts or multiplayer are added, none of which exist today. When it changes, the effective date and the policy version at the top of this page are updated, and the previous text remains available in the public version history of this page. Continuing to use the game after a change means the updated policy applies to that use

## Contact

Questions about this policy, or about privacy in Bullet Hero generally, go to the contact address at the top of this page
