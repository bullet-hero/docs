---
title: Publishing
date: 2026-09-29
tags: [level_author]
---

# Publishing

The Publication tab: checking a level against a service's rules, and publishing levels and collections to Steam Workshop

## The Publication tab

`Publication` is a level settings tab. It checks the open level in every build and publishes it in a Steam build

## Checking a level

`Check against` picks the rules the level is graded by:

| Profile | What it requires |
|---|---|
| `Steam Workshop` | the standard rules for sharing a level publicly |
| `Strict` | the standard rules plus attribution and hashes on every resource, smaller size limits, and resources only from inside the level or the game |
| `Sharing by hand` | nothing |

`Check` grades the open level. The report opens with the line `Errors: N, warnings: N, advice: N`, then one row per finding

Errors block publishing

The report is available in every build, with or without Steam. What each verdict means and what causes it - [[5_publish-readiness]]

## Publishing a level to Steam Workshop

Steam builds only. Below the report:

| Control | What it does |
|---|---|
| `Visible to` | who sees the item: `Everyone`, `Friends` or `Only me`. `Only me` is the default |
| `What changed` | the change note of this upload |
| `Publish` | uploads the level |

The Workshop item is filled from the level:
- the title and description are the level's name and description
- the preview is the level logo, png or jpg, at most 1 MB. Any other logo is skipped, and the item goes up without a picture

The first `Publish` creates the item. A later press updates the same item.
The game finds it by the level's own id among the items you published, so nothing is stored in the level

A protected level cannot be published. More - [[13_export-and-protection]]

> [!warning] Warning
> If you have not accepted the Steam Workshop legal agreement, the item uploads but stays hidden. Accept the agreement on the item's page. The game opens that page in the Steam overlay

## Builds without Steam

The tab shows the report only, with the line `This build cannot upload to the Workshop. Export the level as an archive to share it`.
Export - [[13_export-and-protection]]

## Publishing a collection

A collection of your own is published from its page in the Library tab, in the `Publish to the Workshop` section. It works the same way as a level

The check for a collection:
- it has a name
- it states a licence
- it is not empty
- every file it names is in it
- every resource its entries point at is included

Errors block publishing. More on collections - [[16_library-and-collections]]

## Workshop tags

The game sets the tags itself:

| Item | Tags |
|---|---|
| level | `level` |
| collection | `collection`, plus one per kind inside it: `prefabs`, `themes`, `shapes`, `effects`, `textures`, `fonts`, `audio` |

> [!info] Worth knowing
> Steam's own "Collections" are curated lists of Workshop items, a Valve feature. They have nothing to do with Bullet Hero collections

## Subscriptions

A Steam build reads what you subscribed to:
- levels appear in the level list under `Workshop`, [[2_playing-levels]]
- collections appear in the editor's Library under the `Workshop` chip, read only

Next: [[5_publish-readiness]], [[1_licensing-basics]], [[16_library-and-collections]]
