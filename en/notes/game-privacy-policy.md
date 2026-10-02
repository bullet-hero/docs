---
title: Game privacy policy
date: 2026-10-02
tags: [legal]
---

# Game privacy policy

Bullet Hero does not collect, transmit, store on any server, sell or share any personal data. There are no accounts, no sign-in, no advertising, no analytics, no crash reporting, no tracking and no advertising identifier. Everything the game remembers about you stays on your own device

Four things can leave your device, and none of them goes to the developer:

- a level you open may reference a file hosted on a third-party website, and loading it contacts that website ([[game-privacy-policy#Network access]])
- a level you deliberately share with someone else travels wherever you send it ([[game-privacy-policy#Levels you share]])
- in the Steam builds, the game talks to the Steam Workshop through the Steam client ([[game-privacy-policy#Steam Workshop]])
- in the desktop builds, the game shows your current activity on Discord through the Discord client ([[game-privacy-policy#Discord Rich Presence]])

| | |
|---|---|
| Effective date | 2 October 2026 |
| Policy version | 1.2 |
| Application | Bullet Hero: `com.vertoker.BulletHero` on Android, `com.vertoker.Bullet-Hero` on iOS, and the desktop builds for Windows, Linux and macOS |
| Developer | vertoker, an individual developer |
| Contact | [kostyachurakov@gmail.com](mailto:kostyachurakov@gmail.com) |

This policy covers the game only. The website has its own policy - [[privacy-policy]]. The server will have its own policy too, written when the server exists

## Who this policy applies to

This policy covers every build of Bullet Hero, on every platform and every storefront it is distributed through, and every version of the game to which no newer policy is attached

Where a store (Google Play, the App Store, Steam, RuStore, VK Play or any other) collects data of its own about your purchase, installation or use of the application, that collection is governed by that store's own privacy policy and not by this one. The developer receives from those stores only what they choose to show every developer: aggregate, anonymous statistics about installations and crashes that cannot be traced back to an individual player

## What is stored on your device

The game writes the following into its own application storage, and reads it back on the next launch:

- **Settings**: graphics, audio, controls, keybindings, interface and language preferences
- **Progress and statistics**: attempts, best results, deaths, time played and similar records, both device-wide and per level
- **Levels**: the levels you create, import or download, including their audio, images and other media, plus their automatic backups
- **Diagnostic logs**: the engine's own log file, written locally so that a problem can be investigated on the device where it happened

None of this is transmitted anywhere, and none of it is backed up to any service operated by the developer. Where it lives depends on the platform:

- **Android and iOS**: the game's private storage. Other applications cannot read it, and it is deleted together with the game when you uninstall it
- **Windows, Linux and macOS**: the application-data folder in your user profile, the engine's standard location. Other programs running under your account can read it, as they can any of your files, and it stays there after the game is uninstalled until you delete that folder

The game also offers, in `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}`, explicit controls for deleting stored statistics and backups without uninstalling

The game does not request access to your contacts, photos, camera, microphone, location, calendar, call log, installed-application list, or any other sensitive resource, and it asks for no runtime permissions at all

## Network access

Bullet Hero has no server. The developer operates no service the game connects to, and therefore receives no data from it

A level is a folder of files, and its author may point one of those files at an internet address instead of shipping it inside the folder. When you open such a level, the game downloads that file from whatever website its author chose. That website then sees what any website sees when a file is requested from it, most notably your IP address and the technical details of the request. The developer neither controls nor observes those requests, and no record of them is kept

Apart from that, the Steam Workshop in the Steam builds ([[game-privacy-policy#Steam Workshop]]) and Discord Rich Presence in the desktop builds ([[game-privacy-policy#Discord Rich Presence]]), the game makes no network requests of its own

## Steam Workshop

The Steam builds use the Steam Workshop through the Steam client running on your computer. Builds for every other store never start Steam: the code that talks to it is compiled into the Steam builds only

The game asks Steam which Workshop items your account is subscribed to, so that it can list them as levels and collections. The Steam client downloads them. When you choose to publish a level or a collection, the game hands it to the Steam client together with the title, description, preview image, content descriptors and visibility you set, and Steam stores it on its servers under your Steam account. A public item can be seen by anyone on Steam until you remove it there

All of this passes between the Steam client and Valve's servers and is governed by Steam's own privacy policy and the Steam Subscriber Agreement. The developer receives nothing from it beyond what Steam shows every developer about a Workshop item

## Discord Rich Presence

The desktop builds can show what you are doing in the game in your Discord profile: for example the menu you are in or the level you are playing, and for how long. This only works while the Discord app is running on the same computer. The mobile builds have no Discord integration

The game hands that activity to the Discord client on your device, never to a server of its own. The Discord client then publishes it under your Discord account, and your Discord friends and servers can see it. The game does not sign in to Discord, does not read your messages, servers or friends list and sends nothing on your behalf

What happens to that activity on Discord's side is governed by the [Discord Privacy Policy](https://discord.com/privacy). The developer receives nothing from it. You can hide your activity at any time in Discord: `User Settings` -> `Activity Privacy`

## Levels you share

Levels are portable by design: a level can be exported as an ordinary archive file and sent to another person by any means you choose. Such a file travels directly between you and the recipient, or through whatever service you use to send it. It does not pass through the developer, and the developer keeps no copy of it

A level you create may contain your own music, images and text, and, if you put them there, your name or nickname. Anything you place inside a level is visible to everyone you give that level to. Deciding what to include is yours alone

A level may optionally be protected with a passphrase. That passphrase is used to encrypt the level's content on your device and is never written to disk, never logged and never transmitted. If you lose it, neither the developer nor anyone else can recover the level's content

## Children

The game collects no personal data from anyone, and that includes children. It contains no advertising, no in-app purchases, no chat and no other communication feature, and no mechanism by which a child could disclose personal information to the developer or to another player through the game itself

Because levels may be shared as files and may contain arbitrary text, images and audio chosen by their author, parents and guardians remain responsible for the levels a child obtains from other people

## Third-party components

The game is built with the Unity engine. **Unity's own data-collecting services (Unity Analytics, Unity Ads, Unity In-App Purchasing, Unity Cloud Diagnostics, engine diagnostics, hardware statistics, crash reporting and performance reporting) are all disabled in this project**, and the packages providing them are not included in the build. No advertising, analytics, attribution or crash-reporting SDK of any kind is present

## Your rights

Regulations such as the GDPR, the UK GDPR, the CCPA/CPRA and Russian Federal Law No. 152-FZ grant you rights of access to, correction of, deletion of, and objection to the processing of your personal data

Because the developer holds no personal data about you whatsoever, there is nothing to access, correct, export or delete on the developer's side, and no request is needed to exercise those rights. The data described in [[game-privacy-policy#What is stored on your device]] is under your own control: it can be inspected in the game's storage folder on your device, cleared from within the game, or removed entirely by uninstalling the application. You may still write to the contact address above with any question about this policy

## Data retention

The developer retains no personal data and therefore has no retention period to declare. Data stored on your device is kept for as long as you keep it there

## Changes to this policy

This policy will change if the game does, most likely when the game's own server, player accounts or multiplayer are added, none of which exist today. When it changes, the effective date and the policy version at the top of this page are updated, and the previous text remains available in the public version history of this page. Continuing to use the game after a change means the updated policy applies to that use

## Contact

Questions about this policy, or about privacy in Bullet Hero generally, go to the contact address at the top of this page
