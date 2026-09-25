---
title: Licensing policy for user levels
date: 2026-09-24
tags: [legal]
---

# Licensing policy for user levels

The license every user level is shared under, the two ways an external resource may be used in it and the licenses that are accepted

Bullet Hero lets players create their own content (UGC, user-generated content), and that content has to be licensed. The approach is similar to *Geometry Dash*, with one difference: where *Geometry Dash* deals with one music track, this policy covers **all** external resources of a level

## The level license

Every user level is distributed under **CC BY-NC**:

- **CC** - a Creative Commons license
- **BY** - attribution is required: the authors are credited
- **NC** - non-commercial use only

This license covers the level's own original content: its layout, timing and keyframes, custom code and the creative work of arranging everything into a finished level. **It does not relicense the external resources embedded in the level**

Each external resource keeps its own license or permission, recorded separately for each resource (see below). CC BY-NC on the level is a wrapper around resources that each, on their own, may already be redistributed this way

**A level qualifies for CC BY-NC distribution only if every external resource in it meets Option A or Option B.** If even one does not, the level cannot be distributed through the official Bullet Hero web services (the official server, OWS)

The developers do not prevent free distribution of levels through unofficial channels. They are categorically against commercial use of levels

## External resources

External resources are a wide range of data:

- music and audio: `.mp3`, `.wav`, `.ogg`
- textures and images: `.png`, `.jpg`, `.jpeg`
- fonts: `.ttf`, `.otf`
- texts and bytes: any data

Each external resource must meet one of the two options below

### Option A - an open license

The resource is available under a license that is the same as CC BY-NC or more permissive (see the list of accepted licenses below). The resource keeps its **own** original license: it is not converted into CC BY-NC, it already permits the public non-commercial redistribution that CC BY-NC requires, so including it in a CC BY-NC level is consistent

The resource's original license and source must be recorded in the level's metadata file. SIL OFL already requires this for fonts, and here the requirement applies to every resource, so anyone who downloads the level can see under what terms each part was used

### Option B - the author's direct permission

The author of the resource gives permission to use it specifically in Bullet Hero. A private "sure, go ahead" is not enough on its own: a level marked CC BY-NC is redistributed publicly, so the permission must cover that explicitly, not only your personal use. A valid permission grants all three of:

1. The right to use the resource inside a Bullet Hero level
2. The right for the resulting level, this resource included, to be freely redistributed **non-commercially** by third parties through Bullet Hero's services (OWS, Steam Workshop, NOWS), with attribution to the author
3. Non-commercial use only, stated explicitly

The permission can be anything a moderator can check: an email, a direct message or a public statement (for example on Twitter/X). Use the template below as a starting point and keep the author's reply as proof

### Permission request template

Fill in the placeholders and adjust the tone as needed, but keep points 1 to 3 intact: they are what makes the permission valid for CC BY-NC distribution. If the author speaks another language, translate the template, keeping all three points

```
Subject: Permission to use "<TRACK/RESOURCE NAME>" in a Bullet Hero level

Hi <AUTHOR NAME>,

My name is <YOUR NAME / HANDLE>, I'm creating a level for Bullet Hero (a rhythm/
bullet-hell game - <link to game/project if available>) and I'd love to use your
work "<TRACK/RESOURCE NAME>" (<link to the original>) in it.

Specifically, I'm asking your permission to:
1. Use "<TRACK/RESOURCE NAME>" inside my Bullet Hero level.
2. Allow the level (including your work) to be shared/redistributed for FREE and
   NON-COMMERCIALLY by anyone who downloads it, through Bullet Hero's official and
   unofficial services (including its official server, Steam Workshop, and any
   community-run servers).
3. Credit you as "<HOW YOU WANT TO BE CREDITED>" wherever the level shows attribution.

To be clear, this permission is for non-commercial use only - the level will not be
sold, and no one (including me) will make money from it or from your work through it.

If you're fine with this, a simple reply confirming points 1-3 is all I need - I'll
keep this email/message as proof of permission. If you'd rather I credit you
differently, or you want to set any other condition, just let me know.

Thanks a lot either way!
<YOUR NAME / HANDLE>
```

How to write such a request and what counts as proof is explained in more detail in [[6_asking-permission]]

## External services

The game can work with several external services:

| Service | Description |
|---|---|
| Official Web Services (OWS) | the default server, available on every platform |
| Steam Workshop | available on PC |
| Non-official web services (NOWS) | services anyone may create and run as they see fit |

All tools for running your own server are planned to be open source under the MIT license. No server exists yet. More about servers in [[4_server/index]]

## Accepted licenses (Option A)

An accepted external resource carries one of these typical licenses, the same as the level's or more permissive:

- The Creative Commons family
  - CC BY-NC (Attribution-NonCommercial) - the same as the level
  - CC BY (Attribution) - more permissive than CC BY-NC
  - CC0 (public domain) - the best option, use it whenever you can
- Apache, MIT - meant for text and code, and more permissive than CC BY-NC
- GPL - meant for text and code, accepted only by a service whose profile allows it. The official server does not, see below
- SIL OFL (Open Font License) - must be stated in the metadata file

> [!info] Worth knowing
> The `standard` publishing profile the official server is built on accepts CC0, CC BY, CC BY-NC, SIL OFL, MIT, Apache 2.0 and the Unlicense, but not the GPL family. A GPL work redistributed through the App Store collides with Apple's terms, so a catalogue with such works could not be served to iOS later

Typical licenses that are **not** accepted:

- Proprietary ("All Rights Reserved") - obviously not accepted
- The Creative Commons family
  - CC BY-SA (Attribution-ShareAlike) - technically allowed, but it requires the level's license to change to CC BY-NC-SA, which OWS does not accept, so the answer is no
  - CC BY-ND (Attribution-NoDerivatives) - technically allowed, but it requires the level to be protected from modification, which the game does not support, so the answer is no
  - CC BY-NC-SA (Attribution-NonCommercial-ShareAlike)
  - CC BY-NC-ND (Attribution-NonCommercial-NoDerivatives)

## Where to find accepted resources

### Audio and music

Guaranteed free:

- [ccMixter](https://ccmixter.org/) - perfect, content under CC BY and CC BY-NC
- [Freesound](https://freesound.org/) - perfect, all content under CC0, CC BY and CC BY-NC
- [Incompetech](https://incompetech.com/) - perfect, all content under CC BY
- [Teknoaxe](https://teknoaxe.com/) - perfect, all content under CC BY
- [Kenney Assets](https://kenney.nl/) - all sounds under CC0

Free, but worth a glance at each record:

- [SoundImage](https://soundimage.org/)
- [Pixabay](https://pixabay.com)
- [GoodKid](https://goodkidofficial.com/creators/) - no license is declared, but judging by their FAQ it is CC BY without the author's mention. Use it as CC BY
- NCS - only if the level keeps the default CC BY-NC license

Require a manual license check:

- [OpenGameArt](https://opengameart.org/) - if the license cannot be identified, the resource cannot be used
- [FMA](https://freemusicarchive.org/home) - all kinds of CC licenses, check each one carefully
- SoundBible

Questionable:

- Zapsplat
- [Play On Loop](https://www.playonloop.com/music-licensing/) - one condition: the game must not be a commercial project

### Textures and images

Guaranteed free:

- [Poly Haven](https://polyhaven.com/)
- [AmbientCG](https://ambientcg.com/)
- [Kenney Assets](https://kenney.nl/)
- [Pexels](https://www.pexels.com/)
- [Unsplash](https://unsplash.com/)

Free, but worth a glance at each record:

- [Pixabay](https://pixabay.com)

Require a manual license check:

- [OpenGameArt](https://opengameart.org/)
- [Rawpixel](https://www.rawpixel.com/) - only the "Personal License" and the "Public Domain License", see [the license page](https://www.rawpixel.com/services/licenses)
- itch.io
- Wikimedia Commons

### Fonts

Guaranteed free:

- Google Fonts

## Closing words

Bullet Hero is not a big game. The developers try to stay human towards the community and ask you to do the same. A good community is built together
