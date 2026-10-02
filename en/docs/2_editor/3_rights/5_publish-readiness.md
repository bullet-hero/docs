---
title: Readiness to publish
date: 2026-10-02
tags: [level_author]
---

# Readiness to publish

Every service checks a level by its own rules, so one can accept it and another refuse it. Only an error blocks publishing, a warning sends the level to moderation

The check runs by itself on the `{{ui:settings_level-settings_publication}}` tab of the level settings, in any build. The destination picks the profile: `{{ui:editor_share_archive}}` is checked by `{{ui:editor_publish_profile-local}}`, the loosest one, `{{ui:editor_share_steam}}` by the Workshop profile. The standard profile is a public server's profile, and the store build profile is not offered in the game, its limits are below. More - [[17_publishing]]

## Three verdicts

| Verdict | What happens |
|---|---|
| **`Error`** | the service refuses, the upload is blocked before it starts |
| **`Warning`** | publishable, but a person will look at the level. The server puts it in the moderation queue |
| **`Advice`** | a note, blocks nothing |

A level that stays on your device is graded by nothing at all

## The Workshop profile

Looser than the standard one for now, because the licensing policy is still going to be rewritten:
- any CC BY licence passes, 3.0 and 4.0: BY, BY-SA, BY-NC, BY-NC-SA, BY-ND, BY-NC-ND. Also CC0, SIL OFL, MIT, Apache and the Unlicense
- still refused: all rights reserved, GPL-family licences and a custom licence text
- only a warning: no licence stated, a resource with no record, no link to the source page
- an age rating and level authors are not required
- the size limits are the same as in the standard profile

> [!caution] Caution
> CC BY-ND music is accepted, but under CC 4.0 music synced to a moving picture always counts as an adaptation, and ND forbids distributing adaptations. A level built on an ND track can be taken down at the rights holder's request. Better take another track

## What gives an error

In the standard profile:
- the level's own licence is not accepted
- no age rating
- nobody is credited for the level
- a resource has no record
- a resource's licence is refused or not stated
- a resource is fetched in a way the service does not accept
- a resource is taken from a site that is not allowed
- something exceeds the size limits

## What gives a warning

- a resource has no link to its source page. A work you made yourself has no such page, so this never blocks
- a permission with no scope or no evidence
- an expired permission
- a site with more than one kind of terms

## What gives advice

- a record of a resource the level no longer has

## Why, and what to do

Every line of the report names its resource: by file name or by the name you gave it. The `?` at the end of the line unfolds the details: which licence the resource has, which ones the service accepts instead, how much it weighs against the limit and where to fix it

## Size limits

| Limit | Standard profile | Store build |
|---|---|---|
| Per resource | `{{v:publish.standard.max-resource-mb}} MB` | `{{v:publish.strict.max-resource-mb}} MB` |
| Per data file | `{{v:publish.standard.max-data-file-mb}} MB` | `{{v:publish.strict.max-data-file-mb}} MB` |
| Per level | `{{v:publish.standard.max-level-mb}} MB` | `{{v:publish.strict.max-level-mb}} MB` |

A store build also requires attribution and hashes, and refuses arbitrary links.
The smaller sizes are not a stricter opinion. They are what a phone can actually download over a mobile network

## A clean report

> [!caution] Caution
> A clean report on metadata alone does not mean "ready". Two checks need the level file itself: a resource with no record, and where a resource is fetched from. A metadata-only pass means "nothing wrong in what was read"

## Why services grade differently

A service's rules are a data file, not code.
Every service asks the same dozen or so questions and answers them its own way:
- which licences are acceptable
- how resources may be fetched
- whether an unknown licence is tolerated
- what has to be filled in
- how large a level may be

One service carries its own answers, another replaces them. That is why the same level can be ready for one service and refused by another

> [!info] Worth knowing
> The same check runs both automatically on your machine and in manual moderation on the server. A client with no network still grades a level correctly, because the rules it was built with travel with it

Next: [[4_resource-record]], [[2_metadata-and-sharing]]
