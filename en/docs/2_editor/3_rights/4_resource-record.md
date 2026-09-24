---
title: "A resource's record"
date: 2026-09-24
tags: [level_author]
---

# A resource's record

What to fill in and why an empty field means "unknown" rather than "probably fine"

## What the record holds

Every user-defined resource in a level gets a record of its own, and the record travels inside the level. That is how attribution survives: a file taken from somewhere carries where it came from and under what terms, wherever the level goes

What is in it:
- **Title** and **description** of the original work, both localisable
- **Url** - the canonical page of the work, the artist's own post or store page
- **Licence** - the terms the work is distributed under
- **Permissions** - Option B, one record per rights holder, with scope, dates and evidence
- **Authors** - everyone credited for this one resource, separate from the level's own authors
- **Sources** - free-form provenance, for anything the url cannot express
- **Hashes** - the content hashes of the files behind the resource

**The url is the page that states the terms, not the direct download.** What a moderator has to open is the page, not the file

## An empty field means unknown

> [!caution] Caution
> An unfilled licence field means `NoSpecifiedLicense`, and unspecified is refused. It is not a claim that the terms are fine, it is a claim that nobody checked

The same rule runs through the whole model: an age rating of `Unrated` is zero, a permission scope of `Undefined` is zero. Zero always means "nothing was declared", never "everything is permitted"

`NoSpecifiedLicense` can additionally name where the file came from - YouTube, SoundCloud, Spotify. That changes no verdict, it tells a moderator which conversation to have

## When to fill it in

> [!tip] Recommendation
> Fill the record in at the moment you add the resource. That is the only moment you still remember where it came from

Fill hashes in from day one even where nothing requires them. A takedown names a work, and answering it means finding every level carrying that work. By name that is a guess, by hash it is a lookup

## Stale records and the level card

A record describing a resource the level no longer has is reported as advice rather than an error. It blocks nothing, and clearing it is still worth doing

A record can be marked to show on the level's card, and the music is what that is for. The card then names one resource in a line under the level's own authors, and everything else stays in the full credits

Next: [[5_publish-readiness]], [[2_metadata-and-sharing]]
