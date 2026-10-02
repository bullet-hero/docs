---
title: Public server and extending it
date: 2026-10-02
tags: [server_advanced]
---

# Public server and extending it

For a public server there is already the open SDK: the same models and checks as in the client build without Unity. The protocol, the server API and the moderation tools are not decided yet

> [!warning] Warning
> There is no server code and no protocol yet. Below is the part of the SDK the server will run on, and it already works. Addresses, the message format and the API of the server itself are not here, they do not exist

## The SDK runs on a server

The SDK is the game's open data model: models, serialization to JSON and to a binary format, validation rules, generators.
The same sources that Unity compiles build as an ordinary `netstandard2.1` library without the engine. A server or a utility can reference it:

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

The package is called `BulletHero.SDK`. The code is at [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk), under MIT

The SDK version usually matches the game version and promises no API stability yet. More - [[5_versioning]]

**The client and the server run the same checks over the same models.** A level the editor considers ready is ready for the server too. There is no second set of rules to keep in agreement

## ValidateForPublish

One call answers the question "can this level be published here":

```csharp
new ValidationFacade().ValidateForPublish(meta, profile, level, now, payload)
```

It runs three passes at once:

1. declarative rules over the level and its metadata
2. checks of the level graph
3. the service's own conditions from its `PublishProfile`

**Passing the level itself is optional.** `metadata.json` is a separate file so that a catalog can assess thousands of levels without opening a single one. This cheap pass covers most of the policy

But two checks need `level.json`: a resource with no record at all, and the way resources are fetched. A clean report from the metadata alone means "no errors in what was read". `IsReady` stays `false` until the level file is checked

`payload` carries the measured sizes: of each resource, of `level.json`, of `metadata.json`, of the whole level. Without it the profile's size limits cannot be checked

Nothing is fixed during the check, and that is deliberate. Silently editing content on the way out is the last thing a service needs. More - [[6_validation]]

## Three verdicts

| Group | Meaning | What the server does |
|---|---|---|
| `Error` | the service refuses | rejects the upload (`HasErrors`) |
| `Warning` | it can be published, but a human needs to look | puts the level in the moderation queue (`NeedsManualReview`) |
| `Advice` | noted | nothing |

The client blocks an upload on the same errors before it even starts. A level your server would reject rarely gets to it

## Your own PublishProfile

A service's policy is a file, a serialized SDK model. A stricter or a looser server is a different file, not a fork of the code

**A level that stays on the player's device is not checked at all.** The profile matters only at the moment the level is offered to a service. How an author prepares a level for that moment - [[5_publish-readiness]]

Presets:

| Preset | Key | What for |
|---|---|---|
| `CreateOpen()` | `local` | levels on the device, nothing is required |
| `CreateStandard()` | `standard` | a public server, the policy from [[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | store builds, no direct links, a hash on every resource |

The main fields:

| Field | What it decides |
|---|---|
| `AllowedLicenses` | which typical licenses are accepted, an empty list accepts all |
| `AllowedUriTypes` | how resources may be fetched, an empty list allows every way |
| `AllowUnknownLicense` | whether a resource may say nothing about its terms |
| `AllowPermissionInstead` | whether the rights holder's permission can replace a rejected license (always sent for review) |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution` | what the record of each resource must contain |
| `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | what the level must declare |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | size limits, zero means no limit |
| `Sources`, `UnknownSourceTrust` | the list of trusted sites and how a site off the list is rated |

The two public presets:

| | `standard` | `strict` |
|---|---|---|
| Direct links to resources | allowed | forbidden |
| Author credit on every resource | not required | required |
| Content hash in every record | not required | required |
| Largest resource | 64 MB | 32 MB |
| Largest `level.json` or `metadata.json` | 32 MB | 16 MB |
| Largest level | 256 MB | 128 MB |
| A site off the list | `RequiresLicenseCheck` | `RequiresResourceCheck` |

All presets and fields - [[7_publish-profiles]]

### Why standard has no GPL

GPL-family licenses are left out of `standard` on purpose. A GPL work distributed through the App Store conflicts with Apple's terms. A catalog that allowed them could not later be shipped on iOS

> [!info] Worth knowing
> The list of trusted sites that ships with the SDK is only a starting point. Sites change their terms, so every server owner should override it in their own profile. Nothing can count on a particular site being on the list

## Moderation

What the official server plans to add on top of the check. A public server will most likely need it too:

- **A moderation queue.** It is filled by `Warning` findings
- **Reports and blocking** of levels and users. Google Play and App Store rules require both for any content other people see
- **Removal by hash.** A resource record can store the content hashes of its files as `sha256:<hex>`. A report names a work, and with hashes every level containing it is found by search rather than by guessing from titles. The editor records the hash when a resource is imported
- **Terms of use.** They cover what the license does not: the author's statement that they hold the rights, the server owner's right to remove a level, the right to show its title and cover in lists

**The Steam Workshop works differently.** Valve stores the files, and there is no moderation queue on the Bullet Hero side. The game checks a level or a collection before upload, and an error blocks the upload - [[17_publishing]]. After publication the game only decides which of it to download

## Archive formats

A level is a folder of files, and an archive makes it portable. What the SDK reads and writes:

| Format | Read | Write | Note |
|---|---|---|---|
| `.tar.gz` | yes | yes | the default |
| `.zip` | yes | yes | can be encrypted per entry with AES-256 |
| `.tar.gz.gpg`, `.zip.gpg` | yes | yes | a password-protected OpenPGP message, the only protection available to `.tar.gz` |
| `level.json.gpg` | yes | yes | a single protected level file |
| `.7z` | no | no | detected so it can be refused with a clear name |

The format is detected by the file's first bytes, not by its extension. The name is the only part of a file anyone can change

`tar -xzf`, `gpg -d` and any zip archiver open every format that is written. The game is not needed to unpack a level. More - [[4_archives]]

## What is not decided

- the protocol between the game and a server, and whether it will be the same for OWS and NOWS
- the server API: upload, catalog, search, accounts
- how to point the game at a community server
- how the server itself is extended and in which language
- playing together on a server: transport, authority, level sync and lobbies

For playing together only one thing has been worked out: how a player's avatar appears and disappears on a network message

Publishing levels to any service will appear no earlier than the update after `gv 1.0.0`. The data the check relies on has to get into levels before they are published

## Level license and any server

By default a level is distributed under *CC BY-NC*, and the author can choose another license in the level's metadata. Permission to share a level goes from its author directly to each recipient. So no server, official or community, may host a level under *CC BY-NC* commercially

A server with different code under a different license changes nothing about the rights to the content. The full rules for authors - [[ugc-licensing-policy]]
