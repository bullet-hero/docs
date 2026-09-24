---
title: Readiness to publish
date: 2026-09-24
tags: [level_author]
---

# Readiness to publish

How a service grades a level before publishing, and why one service can accept a level another refuses

> [!warning] Warning
> The game has no button for this check yet. The check is written and tested, and it becomes a screen when the services arrive. Below is how it will grade a level

## Three verdicts

| Verdict | What happens |
|---|---|
| **`Error`** | the service refuses, the upload is blocked before it starts |
| **`Warning`** | publishable, but a person will look at it. The server queues it for moderation |
| **`Advice`** | a note, blocks nothing |

A level that stays on your own device is graded by nothing at all

## What gives an error

In the standard profile:
- the level's own licence is not accepted
- no age rating
- nobody credited for the level
- a resource with no record
- a resource whose licence is refused or unstated
- a resource with no url
- a resource fetched in a way the service does not accept
- a resource from a site nothing may be published from
- anything over the size limits

## What gives a warning

- a permission that names no scope or points at no evidence
- a permission that has lapsed
- a site that hosts more than one kind of terms

## What gives advice

- a record for a resource the level no longer has

## Size limits

| Limit | Standard profile | Store build |
|---|---|---|
| Per resource | `64 MB` | `32 MB` |
| Per data file | `32 MB` | `16 MB` |
| Per level | `256 MB` | `128 MB` |

A store build also requires attribution and hashes, and refuses arbitrary urls.
The tighter sizes are not a stricter opinion. They are what a phone can actually download over a mobile connection

## A clean report

> [!caution] Caution
> A clean report on metadata alone does not mean "ready". Two checks need the level file itself: a resource with no record, and where a resource is fetched from. A metadata-only pass means "nothing wrong in what was read"

## Why services grade differently

A service's rules are a data file, not code.
Every service asks the same handful of questions and answers them its own way:
- which licences are acceptable
- how resources may be fetched
- whether an unknown licence is tolerated
- what has to be filled in
- how large a level may be

One service carries its answers, another replaces them. That is why the same level can be ready for one service and refused by another

> [!info] Worth knowing
> The same check runs both automatically on your machine and in manual moderation on the server. A client with no network still grades a level correctly, because the rules it was built with travel with it

Next: [[4_resource-record]], [[2_metadata-and-sharing]]
