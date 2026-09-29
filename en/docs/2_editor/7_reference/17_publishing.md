---
title: Publishing
date: 2026-09-29
tags: [level_author]
---

# Publishing

The Publication tab and the Share button: sending a level, a collection or one resource as an archive, to Afterbeat or to Steam Workshop

## The Publication tab

`Publication` is a level settings tab. It is the one place a level is sent anywhere

At the top, `Share via` shows the chosen destination. Pressing it opens `How to share`: the destinations this build offers on this device, each with a one-line description.
`Archive` is the default. The last choice is remembered until the game is closed

Under it:
- the destination's own controls
- its report
- the button that runs it: `Export` or `Publish`

If this build has no destination on this device, the tab shows `This build has no way to send this from here`

## The report

The report checks by itself: when the destination opens and whenever one of its controls changes. There is no button for it.
It opens with the line `Errors: N, warnings: N, advice: N`, then one row per finding

Errors block the run. Warnings and advice are left to you

The destination decides the rules the level is graded by. `Archive` uses the `Sharing by hand` set, `Steam Workshop` the standard Workshop one. What each set requires and what each verdict means - [[5_publish-readiness]]

## Destinations

| Destination | Where it exists | What it sends |
|---|---|---|
| `Archive` | every device with a save dialog. iOS has none | a level, a collection or a single resource, as a file |
| `Afterbeat` | Windows, macOS and Linux, in any build | a level, as an *Afterbeat* level folder |
| `Steam Workshop` | the Steam build only | a level or a collection of your own |

A destination this build or device does not have is simply not listed

## Archive

For a level:

| Control | What it does |
|---|---|
| `Format` | one of seven export modes, from a plain folder to an archive behind a password |
| `Password` | shown only for a protected mode. A protected mode with an empty password does not run |
| `Export` | writes the level where you pick |

What each mode writes and who can open it - [[13_export-and-protection#Export level]]

For a collection or a single resource, `Format` offers five of those modes, all of them archives. There is no folder mode:

| `Format` | What you get | Opened with |
|---|---|---|
| `Archive .zip` | one file | a double click in Windows Explorer, nothing to install |
| `Archive .zip + password` | a zip with its own AES-256 encryption | 7-Zip or any other archiver, which asks for the password |
| `Archive .zip + password (gpg)` | the whole zip wrapped in OpenPGP | gpg |
| `Archive .tar.gz` | one file | any archiver |
| `Archive .tar.gz + password (gpg)` | the tar.gz wrapped in OpenPGP | gpg |

`Password` appears for the three password modes. With an empty password nothing is exported.
The collection check below applies, under the same `Sharing by hand` rules

## Afterbeat

A level only, and on a computer only: Windows, macOS or Linux, not only in the Steam build. Not on Android or iOS

`Export` writes `level.vgd` and the metadata into a folder you pick. The song is not copied: put it beside the level yourself

The report converts the level in memory before anything is written. It shows either `Everything converts, nothing is lost`, or the summary of the conversion with a `What is lost` button. That button opens the full loss report. More - [[3_afterbeat-import]]

## Steam Workshop

Steam builds only. The controls:

| Control | What it does |
|---|---|
| `Visible to` | who sees the item: `Everyone`, `Friends` or `Only me`. `Only me` is the default |
| `What changed` | the change note of this upload |
| `Tags` | the tags the item gets, shown as chips after the label. The game sets them itself |
| `Publish` | uploads the level |

The level is always checked against the standard Workshop rules. There is no choice of rules here

The Workshop item is filled from the level:
- the title and description are the level's name and description
- the preview is the level logo, png or jpg, at most 1 MB. Any other logo is skipped, and the item goes up without a picture

The first `Publish` creates the item. A later press updates the same item.
The game finds it by the level's own id among the items you published, so nothing is stored in the level

A protected level cannot be published. More - [[13_export-and-protection]]

> [!warning] Warning
> If you have not accepted the Steam Workshop legal agreement, the item uploads but stays hidden. Accept the agreement on the item's page. The game opens that page in the Steam overlay

## Builds without Steam

A build without Steam does not list `Steam Workshop`. `Archive` stays, and on a computer `Afterbeat` stays too

## Sharing a collection

A collection is shared from its page in the Library tab. `Share` opens the same surface in a window: `Archive`, plus `Steam Workshop` in a Steam build for a collection of your own

The check for a collection:
- it has a name
- it states a licence
- it is not empty
- every file it names is in it
- every resource its entries point at is included

A missing licence depends on the destination. Under `Archive` it is a warning and the export runs. Under `Steam Workshop` it is an error.
Errors block the run. More on collections - [[16_library-and-collections]]

## Sharing a single resource

Every theme, shape, effect and prefab row in the Library has a `Share` button too.
It packs that resource with everything it needs (a prefab's shapes, textures and nested prefabs, for example) as a collection of one entry

Only `Archive` is offered, with the same five formats as a collection, password ones included. The receiver imports the file with `Import archive`, like any collection

## Workshop tags

The game sets the tags itself:

| Item | Tags |
|---|---|
| level | `level` |
| collection | `collection`, plus one per kind inside it: `prefabs`, `themes`, `shapes`, `effects` |

Textures, fonts and audio get no tag and never go to the Workshop on their own. They go up inside a collection as what its prefabs, themes, shapes and effects use. A collection holding nothing but media is refused with a line saying so; share it as an archive instead

> [!info] Worth knowing
> Steam's own "Collections" are curated lists of Workshop items, a Valve feature. They have nothing to do with Bullet Hero collections

## Subscriptions

A Steam build reads what you subscribed to:
- levels appear in the level list under `Workshop`, [[2_playing-levels]]
- collections appear in the editor's Library under the `Workshop` chip, read only

Next: [[5_publish-readiness]], [[1_licensing-basics]], [[16_library-and-collections]]
