---
title: Publish profiles
date: 2026-10-01
tags: [developer, level_author]
---

# Publish profiles

A service describes which levels it accepts with a PublishProfile file: licenses, resource sources, required fields, size limits. Adding a service means writing a file, not editing the analyzer

## A profile is data

A publish profile (`PublishProfile`) is a model that is serialized like any other root, with its own generation

A level can go to the Steam Workshop, the official server, a community server, the catalog of a store build. Each place answers the same questions in its own way. The answers change over the years, and the code does not

What a profile decides:

| Field | Meaning |
|---|---|
| `ProfileKey` | which service this is, repeated in every report |
| `AllowedLicenses` | the `TypicalLicenseType` values the service accepts |
| `AllowedUriTypes` | how resources may be fetched. An empty list means any way |
| `AllowUnknownLicense`, `AllowPermissionInstead` | whether an unknown license or a written permission is enough |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution`, `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | what must be filled in |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | size limits, 0 means no limit |
| `Sources`, `UnknownSourceTrust` | a list of sites and the rating for a site that is not on it |

Only the profile decides which licenses are acceptable. It looks like a property of the license, but in fact it is a property of the receiving service

## Four built-in profiles

| Factory | `ProfileKey` | What for |
|---|---|---|
| `CreateOpen()` | `local` | a level on your device. Nothing is required |
| `CreateStandard()` | `standard` | a public server |
| `CreateWorkshop()` | `workshop` | the Steam Workshop. Any CC BY variant passes, missing documents only warn |
| `CreateStrict()` | `strict` | a store build, stricter than `standard` |

| What | `standard` | `strict` |
|---|---|---|
| licenses | CC0 1.0, CC BY 4.0 and 3.0, CC BY-NC 4.0 and 3.0, SIL OFL 1.1, MIT, Apache 2.0, the Unlicense | as in `standard` |
| where resources come from | from the level folder, from the game or by a direct link | no links |
| attribution and hashes | - | required |
| limit per resource | 64 MiB | 32 MiB |
| limit per data file | 32 MiB | 16 MiB |
| limit per level | 256 MiB | 128 MiB |

> [!tip] Recommendation
> Do not add a factory for your service. Take one of the four profiles, change the fields you need and ship it as a JSON file

### Why these licenses and sizes

- GPL-family licenses are excluded from `standard`. A GPL work distributed through the App Store conflicts with Apple's terms
- CC BY-SA is excluded: ShareAlike would force a change of the license of the level itself
- CC BY-ND is excluded: NoDerivatives forbids the editing the game is built on
- the strict sizes are what a phone can download over a mobile network

## Where a resource came from

The license field says what the author claims. `SourceTrust` says what that claim is worth, given the site the resource came from:

| Rating | Outcome | Examples |
|---|---|---|
| `Approved` | publish | Kenney, ccMixter, Incompetech |
| `PartiallyApproved` | publish, the record is worth a look | Pixabay, SoundImage |
| `RequiresLicenseCheck` | check the license against the real page | OpenGameArt, Free Music Archive, Wikimedia Commons |
| `RequiresResourceCheck` | identify the work itself first | Rawpixel, itch.io |
| `NotAllowed` | refuse | YouTube, SoundCloud, Spotify |
| `Unknown` | no record, `UnknownSourceTrust` decides | - |

`TrustedSourceCatalog.CreateDefault()` returns 25 sites. This is a starting list. Every operator is expected to change it. So nothing is entitled to rely on a record being there

An empty `Sources` list turns source rating off

Streaming platforms are listed as `NotAllowed` rather than left out. A missing site is rated through `UnknownSourceTrust`, and in `standard` and `strict` that rating asks for a check rather than refusing

The catalog and [[ugc-licensing-policy]] describe the same thing and are edited together

## What to do with the answer

The call is `ValidationFacade.ValidateForPublish`. More - [[6_validation]]

`PublishReadinessReport` has:
- `HasErrors` - findings in the `Error` group
- `NeedsManualReview` - findings in the `Warning` group
- `IsReady`

The profile does not decide what happens next. The client blocks the upload on errors. The server puts the level in a review queue instead of publishing it

The same check from the author's side - [[5_publish-readiness]]
