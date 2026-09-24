---
title: "A resource's record"
date: 2026-09-24
tags: [level_author]
---

# A resource's record

What to fill in a resource's record, and why an empty field means "unknown" rather than "probably fine"

> [!tip] Recommendation
> Fill the record in as soon as you add the resource. That is the only moment you still remember where it came from

## What the record holds

Every resource of yours in a level has its own record. It is stored inside the level and travels with it.
That is how attribution survives: wherever the level goes, the file carries where it came from and under what terms

The record's fields:
- **Title** and **description** of the original work, both translatable into other languages
- **Url** - the work's page: the artist's own post or page, a store page
- **Licence** - the terms the work is distributed under
- **Permissions** - [[2_legal-resource-paths|Option B]], one record per rights holder, with scope, dates and evidence
- **Authors** - everyone credited for this one resource, separate from the level's own authors
- **Sources** - free-form provenance, for anything the url cannot express
- **Hashes** - the content hashes of the files behind the resource

**The url is the page that states the terms, not the direct download.** A moderator needs the page, not the file

## An empty field means "unknown"

> [!caution] Caution
> An empty licence field is `NoSpecifiedLicense`, and such a resource is refused. It does not mean "the terms are fine". It means "nobody checked"

The whole model works this way: an empty value means "nothing was declared", never "everything is permitted".
An age rating of `Unrated` and a permission scope of `Undefined` work the same

`NoSpecifiedLicense` can additionally name where the file came from: YouTube, SoundCloud, Spotify.
That changes no verdict. It just tells a moderator which conversation to have

## Hashes

Fill hashes in from day one, even where nothing requires them.
A rights holder's takedown names a work. Answering it means finding every level carrying that work.
By name that is a guess, by hash it is an exact lookup

## Stale records

A record for a resource the level no longer has gives advice, not an error.
It blocks nothing, but clearing it is still worth doing

## A resource on the level card

A resource's record can be marked to show on the level's card. That is for the music.
The card then names this resource in a line under the level's authors. Everything else stays in the full credits

Next: [[5_publish-readiness]], [[2_metadata-and-sharing]]
