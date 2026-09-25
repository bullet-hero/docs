---
title: Publish profiles
date: 2026-09-24
tags: [developer, level_author]
---

# Publish profiles

How a service states which levels it accepts, written as a data file instead of code

## A profile is data

A publish profile (`PublishProfile`) describes which levels a service accepts. It is a model, serialized like any other root, with its own generation.
Adding a service means writing a file, not editing an analyzer

A level can go to Steam Workshop, the official server, a community server, a store build's catalogue. Each place answers the same questions differently. The answers change over the years, the code does not

What a profile decides:

| Field | Meaning |
|---|---|
| `ProfileKey` | which service this is, repeated in every report |
| `AllowedLicenses` | the `TypicalLicenseType` values the service accepts |
| `AllowedUriTypes` | how resources may be fetched. Empty means any way |
| `AllowUnknownLicense`, `AllowPermissionInstead` | whether an unknown license or a written permission is enough |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution`, `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | what must be filled in |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | size limits, 0 means none |
| `Sources`, `UnknownSourceTrust` | the site roster and the grade for a site missing from it |

Which licenses are acceptable is decided only by the profile. It looks like a property of the license, but it is a property of the receiving service

## Three built-in profiles

| Factory | `ProfileKey` | For what |
|---|---|---|
| `CreateOpen()` | `local` | a level on your own device. Nothing is required |
| `CreateStandard()` | `standard` | a public server |
| `CreateStrict()` | `strict` | a store build, stricter than `standard` |

| What | `standard` | `strict` |
|---|---|---|
| licenses | CC0 1.0, CC BY 4.0 and 3.0, CC BY-NC 4.0 and 3.0, SIL OFL 1.1, MIT, Apache 2.0, the Unlicense | as in `standard` |
| where resources come from | the level folder, the game or a direct URL | no URLs |
| attribution and hashes | - | required |
| limit per resource | 64 MiB | 32 MiB |
| limit per data file | 32 MiB | 16 MiB |
| limit per level | 256 MiB | 128 MiB |

> [!tip] Recommendation
> Do not add a factory for your own service. Take one of the three, change the fields you need and ship it as a JSON file

### Why these licenses and sizes

- GPL-family licenses are left out of `standard`. A GPL work redistributed through the App Store collides with Apple's terms
- CC BY-SA is left out: ShareAlike would force the level's own license to change
- CC BY-ND is left out: NoDerivatives forbids the editing the game is built around
- the strict sizes are what a phone can download over a mobile connection

## Where a resource came from

A license field says what the author claims. `SourceTrust` says how much that claim is worth, given the site the resource came from:

| Grade | Outcome | Examples |
|---|---|---|
| `Approved` | publish | Kenney, ccMixter, Incompetech |
| `PartiallyApproved` | publish, the record is worth a glance | Pixabay, SoundImage |
| `RequiresLicenseCheck` | read the license against the actual page | OpenGameArt, Free Music Archive, Wikimedia Commons |
| `RequiresResourceCheck` | identify the work itself first | Rawpixel, itch.io |
| `NotAllowed` | refuse | YouTube, SoundCloud, Spotify |
| `Unknown` | no record, `UnknownSourceTrust` decides | - |

`TrustedSourceCatalog.CreateDefault()` returns 25 sites. It is a starting roster. Every operator is expected to change it. So nothing may assume an entry is present

An empty `Sources` list turns source grading off

Streaming platforms are listed as `NotAllowed` rather than omitted. A missing site is graded by `UnknownSourceTrust`, and in `standard` and `strict` that grade asks for a check instead of refusing

The catalogue and [UGC-LICENSING-POLICY.md](https://github.com/bullet-hero/sdk/blob/master/Docs/UGC-LICENSING-POLICY.md) describe the same thing and are edited together

## What to do with the answer

The call is `ValidationFacade.ValidateForPublish`. More - [[6_validation]]

`PublishReadinessReport` has:
- `HasErrors` - findings of the `Error` group
- `NeedsManualReview` - findings of the `Warning` group
- `IsReady`

The profile does not decide what happens next. A client blocks the upload on errors. A server queues a level for review instead of publishing it

The author's side of the same check - [[5_publish-readiness]]
