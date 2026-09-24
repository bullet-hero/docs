---
title: Images and fonts
date: 2026-09-24
tags: [level_author]
---

# Images and fonts

What loads, what size is sensible, and why a built-in shape nearly always beats an image

**Images.** Anything the engine can decode from a file's bytes loads, which in practice means `png` and `jpg`. The game imposes no limit on the FILE - the hardware does. On Android the guaranteed floor is 4096, in practice it is usually 8192 to 16384, and a desktop PC can report 32768

**The real limit is memory, not that number.** An image is decoded into raw pixels, so a `png` occupies width times height times 4 bytes, and a `jpg`, which cannot carry transparency at all, three:
- 512 by 512 - 1 MB
- 1024 by 1024 - 4 MB
- 2048 by 2048 - 16 MB
- 4096 by 4096 - 64 MB
- 8192 by 8192 - 256 MB

> [!caution] Caution
> An 8192 texture is a quarter of a gigabyte for one picture. On a phone that is not slow, it is a crash

> [!tip] Recommendation
> Treat 2048 as the ceiling for a mobile level and 4096 as the ceiling at all

**What the device does with those numbers is the player's setting, not yours.** Every player's graphics settings carry three of them: whether images are packed into a compressed format as they load, the largest side one may occupy in memory, and whether reduced copies are built for drawing small. Compression divides the numbers above by four to eight, and the size cap divides them by the square of every step down. A phone compresses and caps at 2048 by default, a desktop keeps the full image and caps at 4096

**Your own half of that decision is one field on the image: what KIND of picture it is.** A photograph survives scaling and compression better than anything else, a drawing with hard edges survives them less well, and `pixel art` refuses both - it is never compressed, never mip-mapped and never smoothed, whatever the device would have preferred. The field sits beside the image in the resources list, and it says what the picture IS rather than what to do with it - the doing is the player's

**Mip-maps are what stop a small image from shimmering.** They are reduced copies the device draws instead of the full picture while it is small on screen, and they cost a third more memory. Without them - a player can turn them off, and pixel art never gets any - an image scaled down does not smooth, it crawls. A 4096 image occupying 200 pixels on screen still costs 256 times the memory of one resized to 256 beforehand

> [!tip] Recommendation
> Make the image roughly the size it will be on screen, rounded up to the next power of two

**A shape is cheaper than an image in every way.** Built-in shapes are real geometry rather than a picture on a rectangle, so they carry no transparent padding that gets drawn and thrown away, no file, no memory and no rights question

> [!info] Worth knowing
> On a mid-range mobile chip a 1000-object scene spends 95 to 97 percent of its GPU time shading pixels, and a shape covers 29.4 percent of its own rectangle. The rest of a textured quad is transparent waste

An image earns its place when what you need really is an image - a logo, a photograph, hand-drawn art. For a geometric form, take a shape, and if the form does not exist, draw it in the shape editor

**Fonts:** `ttf`, `otf`, `ttc`. With no font of its own, text is drawn with whatever the system happens to have, which differs between devices

> [!tip] Tip
> Text also has a font cache - the set of characters prepared for drawing in advance. A generator rebuilds it from the text the level actually contains. Run it once the text stops changing

Next: [[1_level-budget|The level's budget]], [[2_mobile-devices|Mobile devices]]
