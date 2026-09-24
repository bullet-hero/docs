---
title: Readiness to publish
date: 2026-09-24
tags: [level_author]
---

# Readiness to publish

Three verdicts, two enforcers, and why the same level can be ready for one service and refused by another

> [!caution] Caution
> None of this has a button in the game yet. The machinery is written and tested, and it arrives as a screen when the services do. What is below is how it will grade a level

**A policy is a file, not code.** Every service asks the same handful of questions and answers them differently. Which licences are acceptable, how resources may be fetched, whether an unknown licence is tolerated, what has to be filled in and how large a level may be - all of it is data one service carries and another replaces

**Three verdicts:**
- **** - the service refuses. The upload is blocked before it starts
- **** - publishable, but a person has to look. The server queues it for moderation
- **** - noted, blocks nothing

> [!info] Worth knowing
> That split is what lets one implementation serve both automatic checking on your machine and manual moderation on the server. A client with no network still grades a level correctly, because the policy it was built with travels with it

**Errors** in the standard profile: the level's own licence is not accepted, no age rating, nobody credited for the level, a resource with no record at all, a resource whose licence is refused or unstated, a resource with no url, a resource fetched in a way the service does not accept, a site nothing may be published from, or anything over the size limits

**Warnings:** a permission that names no scope or points at no evidence, a permission that has lapsed, a site that hosts more than one kind of terms

**Advice:** a record describing a resource the level no longer has

**The standard profile in numbers:** up to `64 MB` per resource, `32 MB` per data file, `256 MB` per level. A store build is tighter - `32 MB`, `16 MB` and `128 MB` - and additionally requires attribution and hashes, and refuses arbitrary urls

> [!info] Worth knowing
> The tighter sizes are not a stricter opinion about the same thing, they are what a phone can actually download over a mobile connection

> [!caution] Caution
> A clean report on metadata alone never means ready. Two findings need the level file itself - a resource with no record, and where a resource is fetched from - so a metadata-only pass means "nothing wrong in what was read"

> [!tip] Tip
> A level that stays on your own device is graded by nothing at all

Next: [[4_resource-record|A resource's record]], [[2_metadata-and-sharing|Metadata and sharing a level]]
