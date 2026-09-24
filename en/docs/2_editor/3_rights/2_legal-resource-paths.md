---
title: Two ways a resource qualifies
date: 2026-09-24
tags: [level_author]
---

# Two ways a resource qualifies

A resource qualifies if it has a suitable licence or the rights holder's permission. There is no third way

An external resource is everything the level brings with it: music, images, fonts, texts, any files.
Each resource has to satisfy **one of two** options

## Option A: an open licence

The resource already carries terms as free as `CC BY-NC` or freer.
It keeps its own terms. It is not converted into `CC BY-NC`

What the standard profile accepts:
- [CC0](https://creativecommons.org/publicdomain/zero/1.0/) - public domain
- [CC BY](https://creativecommons.org/licenses/by/4.0/), versions 4.0 and 3.0
- [CC BY-NC](https://creativecommons.org/licenses/by-nc/4.0/), versions 4.0 and 3.0
- [MIT](https://choosealicense.com/licenses/mit/) and [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) - for text and code
- [SIL OFL 1.1](https://openfontlicense.org/open-font-license-official-text/) - for fonts, it has to be named in the metadata
- [Unlicense](https://choosealicense.com/licenses/unlicense/)

> [!tip] Recommendation
> Take `CC0` whenever the choice is yours. It is the only licence that asks nothing of the level

## What the profile refuses

- **Proprietary**, "all rights reserved"
- [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/) - the level would have to become CC BY-NC-SA, which is not what levels are distributed under
- [CC BY-ND](https://creativecommons.org/licenses/by-nd/4.0/) - it forbids modification, which the game does not support
- [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) and [CC BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/) - for the same two reasons

The GPL family is not on the list, even though it is freer than CC BY-NC.
GPL code cannot be redistributed through the App Store without colliding with Apple's terms. So anything reaching an iOS build has to stay MIT or Apache shaped

## The profile depends on the service

Which licences are accepted is decided by the service, not by the licence.
The list above is the standard profile. A store build accepts less, and a community server can accept something else

## Option B: the rights holder's permission

A private "sure, go ahead" is not enough.
A level under `CC BY-NC` is redistributed publicly, and the permission has to cover exactly that, not your personal use

A valid permission grants all three of:
1. The right to use the resource inside a Bullet Hero level
2. The right for that level, the resource included, to be freely and non-commercially redistributed by third parties through the game's services, with attribution
3. Explicitly non-commercial use only

How to ask - [[6_asking-permission]]

> [!caution] Caution
> A permission does not turn a refusal into a pass. If the resource's licence is one of the refused ones, the permission sends it to a human review, but never makes it "allowed"

## Scope and validity

A permission with no stated scope or no evidence counts as incomplete.
An expired permission counts as nothing at all

**The scope is recorded**, and it matters:
- a permission for one named level is void the moment the resource is copied into another level
- a permission for any level survives every reuse

Next: [[6_asking-permission]], [[4_resource-record]]
