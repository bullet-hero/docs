---
title: Running and extending a public server
date: 2026-09-24
tags: [server_advanced]
---

# Running and extending a public server

What already exists for a public Bullet Hero server in the open SDK today, and what is still undecided: the protocol, the API, moderation tools

> [!warning] Warning
> There is no server code and no protocol yet. Everything below is the part of the SDK a server will run on, and it already works. No endpoint, message format or API of the server itself is described here, because none exists

## The SDK runs on the server

The SDK is the open data model of the game: models, JSON and binary serialization, validation rules, generators. The same sources that Unity compiles also build as a plain `netstandard2.1` library, with no engine inside, so a server or a tool can reference it:

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

The package is called `BulletHero.SDK`. The code is at [github.com/vertoker/bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk) under MIT. Until the SDK says otherwise, its version follows the game and is not a promise of API stability (see [[5_versioning]])

**This is the point of the design:** the client and the server run the same checks over the same models, so a level the editor calls ready is ready on the server too, and there is no second rule set to keep in sync

## ValidateForPublish

One call answers "can this level be published here": `ValidationFacade.ValidateForPublish(meta, profile, level, now, payload)`. It runs three passes at once:

1. the declarative rules over the level and its metadata
2. the graph checks over the level
3. the service's own conditions from its `PublishProfile`

**The level itself is optional.** `metadata.json` is a separate file so a catalogue can grade thousands of levels without opening one. That cheap pass covers most of the policy, but two things need `level.json`: a resource with no record at all, and how resources are fetched. A metadata-only report that comes back clean means "nothing wrong in what was read", and `IsReady` stays `false` until the level file was actually inspected

`payload` carries the measured sizes (each resource, `level.json`, `metadata.json`, the whole level). Without it the size limits of the profile cannot be checked

Nothing is repaired during this check, on purpose: a silent fix to content on its way out is the last thing a service wants. More about validation in [[6_validation]]

## Three verdicts

| Group | Meaning | What a server does |
|---|---|---|
| `Error` | the service refuses | rejects the upload (`HasErrors`) |
| `Warning` | publishable, but a person has to look | puts the level in the moderation queue (`NeedsManualReview`) |
| `Advice` | noted | nothing |

The client blocks an upload on the same errors before it starts, so a level refused by your server should rarely reach it at all

## Your own PublishProfile

A service's policy is a file, a serialized SDK model, so running a stricter or looser server means shipping a different file, not forking code. The main fields:

| Field | What it decides |
|---|---|
| `AllowedLicenses` | which typical licenses are accepted, empty accepts all |
| `AllowedUriTypes` | how resources may be fetched, empty allows all |
| `AllowUnknownLicense` | whether a resource may say nothing about its terms |
| `AllowPermissionInstead` | whether a rights holder's permission can carry a refused license (always sent to review) |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution` | what every resource record must contain |
| `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | what the level must declare |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | size limits, zero means no limit |
| `Sources`, `UnknownSourceTrust` | the roster of trusted sites and how an unlisted site is graded |

The two public presets:

| | `standard` | `strict` |
|---|---|---|
| Direct URLs for resources | allowed | forbidden |
| Attribution on every resource | not required | required |
| Content hash on every record | not required | required |
| Largest resource | 64 MB | 32 MB |
| Largest `level.json` or `metadata.json` | 32 MB | 16 MB |
| Largest level | 256 MB | 128 MB |
| Unlisted site | `RequiresLicenseCheck` | `RequiresResourceCheck` |

GPL-family licenses are absent from `standard` on purpose. A GPL work redistributed through the App Store collides with Apple's terms, and a catalogue that allowed them could not be served to iOS later. All presets are described in [[7_publish-profiles]]

> [!info] Worth knowing
> The trusted-site roster that ships with the SDK is a starting point. Sites change their terms, so every operator is expected to override it in their own profile, and nothing may assume that a particular site is in the list

## Moderation

What the official server is planned to add on top of the check, and what a public server will most likely need too:

- **A moderation queue** fed by `Warning` findings
- **Reports and blocking** of levels and users. The Google Play and App Store rules demand both for any content shown to other people
- **Takedowns by hash.** A resource record can carry the content hashes of its files as `sha256:<hex>`. A complaint names a work, and with hashes every level that carries it is found by lookup, not by guessing from names. The editor records the hash when a resource is imported
- **Terms of service** covering what a license does not: the author's claim to hold the rights, the operator's right to remove a level, the right to show its name and cover in listings

## Archive formats

A level is a folder of files, and a package makes it portable. What the SDK reads and writes:

| Format | Read | Write | Note |
|---|---|---|---|
| `.tar.gz` | yes | yes | the default |
| `.zip` | yes | yes | can be encrypted entry by entry with AES-256 |
| `.tar.gz.gpg`, `.zip.gpg` | yes | yes | an OpenPGP message behind a passphrase, the only protection a `.tar.gz` can take |
| `level.json.gpg` | yes | yes | a single protected level file |
| `.7z` | no | no | recognised so it can be refused by name |

The format is detected from the first bytes of the file, never from its extension, since the name is the one part of a file anyone can change. `tar -xzf` and `gpg -d` open every writable format, so a level does not depend on the game to be unpacked. Details in [[4_archives]]

## What is not decided

- the protocol between the game and a server, and whether it is one protocol for OWS and NOWS
- the server API: upload, catalogue, search, accounts
- how the game is pointed at a community server
- how the server itself is extended and in what language
- anything about playing together on a server

## Licensing limits for any server

Levels are licensed under *CC BY-NC*. The permission to share a level comes from its author directly to every recipient, so no server, official or community, may host levels commercially. A server with different code under a different license still inherits nothing about the content. The full rules for authors are in [[ugc-licensing-policy]]
