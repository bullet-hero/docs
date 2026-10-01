---
title: Two ways to a legal resource
date: 2026-09-25
tags: [level_author]
---

# Two ways to a legal resource

A resource qualifies if it has a suitable licence or the rights holder's permission. There is no third way

An external resource is everything the level brings with it: music, images, fonts, texts, any files.
Every resource has to fit **one of two** options

## Option A: an open licence

The resource is already distributed on terms no stricter than `CC BY-NC`.
It keeps its own terms. It does not turn into `CC BY-NC`

The standard profile accepts:
- [CC0](https://creativecommons.org/publicdomain/zero/1.0/) - public domain
- [CC BY](https://creativecommons.org/licenses/by/4.0/), versions 4.0 and 3.0
- [CC BY-NC](https://creativecommons.org/licenses/by-nc/4.0/), versions 4.0 and 3.0
- [MIT](https://choosealicense.com/licenses/mit/) and [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) - for text and code
- [SIL OFL 1.1](https://openfontlicense.org/open-font-license-official-text/) - for fonts, it has to be stated in the metadata
- [Unlicense](https://choosealicense.com/licenses/unlicense/)

> [!tip] Recommendation
> If the choice is yours, take `CC0`. It is the only licence that asks nothing of the level

## What the profile refuses

- **Proprietary**, also known as "all rights reserved"
- [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/) - the level would have to be released under CC BY-NC-SA, and levels are not distributed under it
- [CC BY-ND](https://creativecommons.org/licenses/by-nd/4.0/) - it forbids modification, which the game does not support
- [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) and [CC BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/) - for the same two reasons

The GPL family is not on the list, even though it is freer than CC BY-NC.
GPL code cannot be distributed through the App Store without a conflict with Apple's terms. So anything that reaches an iOS build has to stay in the form of MIT or Apache

## The profile depends on the service

Which licences are accepted is decided by the service, not by the licence.
The list above is the standard profile. A store build accepts less, and a community server may accept something else

## Option B: the rights holder's permission

A private "sure, take it" is not enough.
A level under `CC BY-NC` is distributed publicly, and the permission has to cover exactly that, not your personal use

A valid permission grants all three points:
1. The right to use the resource inside a Bullet Hero level
2. The right for the level, the resource included, to be freely and non-commercially distributed by third parties through the game's services, with attribution
3. Explicitly non-commercial use only

How to ask - [[6_asking-permission]]

> [!caution] Caution
> A permission does not turn a refusal into a pass. If the resource's licence is one of the refused ones, the permission sends it to a human review, but does not make it "allowed"

## Scope and term of a permission

A permission with no scope or no evidence counts as incomplete.
An expired permission does not count at all

**The scope is recorded**, and it matters:
- a permission for one specific level stops working when the resource is copied into another level
- a permission for any level survives any reuse

Next: [[6_asking-permission]], [[4_resource-record]]
