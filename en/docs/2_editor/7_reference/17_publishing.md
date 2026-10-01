---
title: Publishing
date: 2026-10-01
tags: [level_author]
---

# Publishing

A level is sent only from the "Publication" tab in the level settings: as an archive, to Afterbeat or to Steam Workshop. The report checks the level by itself, and errors in it block sending

## The "Publication" tab

`Publication` is a level settings tab. It is the only place a level is sent anywhere from

At the top, `Share via` shows the chosen way of sending. Pressing it opens `How to share`: the ways this build offers on this device, each with a one-line description.
`Archive` is chosen by default. The last choice is remembered until the game is closed

Under it:
- the way's own settings
- its report
- the button that runs it: `Export` or `Publish`

If this build has no ways on this device, the tab shows `This build has no way to send this from here`

## The report

The report checks by itself: when a way opens and when any of its settings changes. There is no button for it.
It starts with the line `Errors: N, warnings: N, advice: N`, followed by one line per finding

Errors block the run. Warnings and advice are up to you

The way decides the rules the level is judged by. `Archive` checks against the `Sharing by hand` set, `Steam Workshop` against the Workshop rules. What each set requires and what each verdict means - [[5_publish-readiness]]

## Ways to send

| Way | Where it exists | What it sends |
|---|---|---|
| `Archive` | on any device with a save dialog. Not on iOS | a level, a collection or one resource, as a file |
| `Afterbeat` | Windows, macOS and Linux, in any build | a level, as an *Afterbeat* level folder |
| `Steam Workshop` | the Steam build only | a level or a collection of your own |

A way this build or this device does not have is simply not in the list

## Archive

For a level:

| Element | What it does |
|---|---|
| `Format` | one of seven export modes, from a plain folder to a password-protected archive |
| `Password` | visible only in protected modes. A protected mode with an empty password does not run |
| `Export` | writes the level where you point it |

What each mode writes and what opens it - [[13_export-and-protection#Export level]]

For a collection or one resource, `Format` offers five of those modes, and all of them are archives. There are no folder modes:

| `Format` | What you get | What opens it |
|---|---|---|
| `Archive .zip` | one file | a double click in Windows Explorer, nothing to install |
| `Archive .zip + password` | a zip with built-in AES-256 encryption | 7-Zip or another archiver, it asks for the password |
| `Archive .zip + password (gpg)` | the whole zip wrapped in OpenPGP | gpg |
| `Archive .tar.gz` | one file | any archiver |
| `Archive .tar.gz + password (gpg)` | a tar.gz wrapped in OpenPGP | gpg |

`Password` appears in the three password modes. With an empty password nothing is exported.
The collection check below applies, under the same `Sharing by hand` rules

## Afterbeat

A level only and on a computer only: Windows, macOS or Linux, not only in the Steam build. Not on Android or iOS

`Export` writes `level.vgd` and the metadata into the chosen folder. The song is not copied: put it next to the level yourself

The report converts the level in memory before anything is written. It shows either `Everything converts, nothing is lost` or a conversion summary with a `What is lost` button. That button opens the full loss report. More - [[3_afterbeat-import]]

## Steam Workshop

Steam builds only. The elements:

| Element | What it does |
|---|---|
| `Visible to` | who sees the item: `Everyone`, `Friends` or `Only me`. By default `Only me` |
| `What changed` | the change note for this upload. A multiline field, with its label on its own line |
| `Title and description go up in` | the language the item's text is taken in (see below) |
| `Content` | five tick boxes, Steam's own content descriptors (see below) |
| `Publish` | uploads the level |

The level is always checked against the Workshop rules. There is no choice of rules here

The Workshop item is filled from the level:
- the title and description are the level's name and description, in one language
- the preview is the level cover, png or jpg, no larger than 1 MB. Any other cover is skipped, and the item is uploaded without a picture
- the game sets the tags itself, see "Workshop tags" below

The first press of `Publish` creates the item. The next ones update the same item.
The game finds it by the level's own id among the items you published, so nothing is stored in the level

A protected level cannot be published. More - [[13_export-and-protection]]

> [!warning] Warning
> If you have not accepted the Steam Workshop legal agreement, the item uploads but stays hidden. Accept the agreement on the item's page. The game opens that page in the Steam overlay

### Title language

Steam shows one title and one description per item. The game takes the first language it finds, in this order:
1. `Publish Language` in the `Game Editor` settings: `English` (the default) or `System`, the device's language. More - [[14_editor-settings]]
2. your own language, i.e. the language of the game's interface
3. English
4. the first language the text was written in

The description is looked for in the title's language first, so that they match.
A name that is not localized (plain text) goes up exactly as written, and the line says `as written, the text is not localized`

### Content descriptors

`Content` has five tick boxes, Steam's own content descriptors:
- `General mature content`
- `Frequent violence or gore`
- `Some nudity or sexual content`
- `Frequent nudity or sexual content`
- `Adult-only sexual content`

They are sent with every publish and are never stored in the level. Every publish sends the whole set, so an unticked box removes the descriptor from an item that is already published too.
They go up in a second update right after the upload. If that part fails, the item is still published, and the result says the descriptors were not set

### After publishing

On success the form shows which item was created or updated, and an `Open in the Workshop` button. It opens the item's page in Steam

On failure the form shows:
- the reason in plain words, `Publishing failed: ...`
- `What was sent and what Steam answered: ...` - a technical line in English. It is worth quoting to the developer when you report a problem
- a `?` that unfolds why Steam refuses this way, and three links: `Publishing guide` (this page), `Steam Support` and `Workshop legal agreement`

The game's own log lines about publishing are always in English, whatever the interface language

| Reason | What to do |
|---|---|
| `Steam is not running` | start Steam and restart the game from Steam |
| `the item belongs to another account` | publish from that account, or make a copy of the level, then it goes up as a new item |
| `Steam denied access` | the account does not own the game, the account is limited (no purchases on Steam yet) or the Workshop is closed to it |
| `Steam did not accept the item` | the game's Workshop is not set up for uploads, or Steam is running under another game's id. Restart Steam and the game |
| `your Workshop storage is full` | delete old items in your Workshop files |
| `Steam could not be reached` | check the connection and the Steam status |
| `the item breaks a Steam limit` | a title up to 128 characters, a description up to 8000, a png or jpg preview up to 1 MB |
| `the files could not be prepared` | check the free disk space and that the level files are not open in another program |

If a new item is created but its upload is rejected, the game deletes that empty item, so that no abandoned item is left in the Workshop

## Builds without Steam

A build without Steam does not show `Steam Workshop` in the list. `Archive` stays, and on a computer `Afterbeat` stays too

## How to share a collection

A collection is shared from its page on the "Library" tab. `Share` opens the same panel in a window: `Archive`, and in the Steam build also `Steam Workshop` for a collection of your own

The collection check:
- it has a name
- it has a licence stated
- it is not empty
- every file it names is in it
- every resource its entries refer to is included in it

A missing licence depends on the way. For `Archive` it is a warning, and the export runs. For `Steam Workshop` it is an error.
Errors block the run. More on collections - [[16_library-and-collections]]

## How to share one resource

Every theme, shape, effect and prefab row in the Library also has a `Share` button.
It packs the resource with everything it needs (for example, a prefab's shapes, textures and nested prefabs) as a collection of one entry

Only `Archive` is available, with the same five formats as for a collection, password formats included. The recipient imports the file through `Import archive`, like any collection

## Workshop tags

The game sets the tags itself:

| Item | Tags |
|---|---|
| level | `level` |
| collection | `collection` and one for each kind inside: `prefabs`, `themes`, `shapes`, `effects` |

Textures, fonts and audio get no tags and do not go to the Workshop on their own. They go inside a collection as what its prefabs, themes, shapes and effects use. A collection of media alone is rejected with a line giving the reason, and such a collection is better shared as an archive

> [!info] Worth knowing
> Steam's own "Collections" are curated lists of Workshop items, a Valve feature. They have nothing to do with Bullet Hero collections

## Subscriptions

The Steam build reads what you are subscribed to:
- levels appear in the level list under `Workshop`, [[2_playing-levels]]
- collections appear in the editor's library under the `Workshop` chip, read only

Next: [[5_publish-readiness]], [[1_licensing-basics]], [[16_library-and-collections]]
