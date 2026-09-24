---
title: Publish profiles
date: 2026-09-24
tags: [developer, level_author]
---

# Publish profiles

How a service states which levels it accepts, written as a data file instead of code

## A profile is data

Every place a level can go (Steam Workshop, the official server, a community server, a store build's catalogue) answers the same handful of questions differently, and those answers change over the years while the code does not. So the policy is a model, `PublishProfile`, serialized like any other root with its own generation. Adding a service means writing a file, not editing an analyzer

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

Which licenses are acceptable lives only in the profile. It looks like a property of the license, but it is a property of the receiving service

## Three built-in profiles

| Factory | `ProfileKey` | For what |
|---|---|---|
| `CreateOpen()` | `local` | a level on your own device. Nothing is required |
| `CreateStandard()` | `standard` | a public server. Licenses: CC0 1.0, CC BY 4.0 and 3.0, CC BY-NC 4.0 and 3.0, SIL OFL 1.1, MIT, Apache 2.0, the Unlicense. Resources from the level folder, the game or a direct URL. Limits of 64 MiB per resource, 32 MiB per data file and 256 MiB per level |
| `CreateStrict()` | `strict` | a store build. `standard` plus: no URLs, attribution and hashes required, limits of 32, 16 and 128 MiB |

GPL-family licenses are left out of `standard` because a GPL work redistributed through the App Store collides with Apple's terms. CC BY-SA and CC BY-ND are left out because ShareAlike would force the level's own license to change and NoDerivatives forbids the editing the game is built around. The strict sizes are what a phone can download over a mobile connection

> [!tip] Recommendation
> Do not add a factory for your own service. Take one of the three, change the fields you need and ship it as a JSON file

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

`TrustedSourceCatalog.CreateDefault()` returns 25 sites. It is a starting roster: every operator is expected to change it, and nothing may assume an entry is present. Streaming platforms are listed as `NotAllowed` rather than omitted, because a missing site is graded by `UnknownSourceTrust`, and in `standard` and `strict` that grade asks for a check instead of refusing. An empty `Sources` list turns source grading off. The catalogue and [UGC-LICENSING-POLICY.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Docs/UGC-LICENSING-POLICY.md) describe the same thing and are edited together

## What the caller does with the answer

`PublishReadinessReport` has `HasErrors` (findings of the `Error` group), `NeedsManualReview` (`Warning`) and `IsReady`. The profile does not decide what happens next: a client blocks the upload on errors, a server queues a level for review instead of publishing it. The call is `ValidationFacade.ValidateForPublish`, see [[6_validation]]. The author's side of the same check is on [[5_publish-readiness]]
