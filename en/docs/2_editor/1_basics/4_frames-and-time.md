---
title: "Frames, time and the length of a level"
date: 2026-09-24
tags: [level_author]
---

# Frames, time and the length of a level

Why a level frame is not a screen frame, where the level's length comes from, and what happens to content past the end

**A level frame has nothing to do with a screen frame.** The game draws as many frames per second as the hardware allows. A level is measured in its own frames, and how many of those there are per second is fixed and stored in the level itself, `60` by default

> [!info] Worth knowing
> That exists so a level plays identically at 60 Hz, at 144 Hz and on a phone that dropped to 30. Content tied to rendered frames would play differently on different hardware, and hit accuracy would depend on the graphics card

**A frame is a cell, not a moment.** Frame f covers the time from f/fps to (f+1)/fps, left edge included, right edge not. One practical consequence: if one object ends on frame 100 and another starts on frame 100, they do not overlap

**The level's length and the track's length are different numbers.** You set the level's length, the track's comes out of the file. They are not required to match

**Content past the end of the level is legal.** It simply never plays, and validation says nothing about it. A child whose span sticks out of its parent's works the same way: the model keeps what you wrote and the effective lifetime is computed separately

> [!tip] Tip
> To fit lifetimes to each other, run the `span-fit` modifier in Generators. It either clamps the children in or expands the parents out

**The level's fps.** The higher it is, the more precisely you land on the beat, and the more frames the same length takes. The range is 1 to 1000, the default is `60`

> [!tip] Recommendation
> Leave the fps at the default. At 60 the ear does not hear a one-frame shift, and the number of keys grows linearly with it

The timeline is capped at `1000000` frames, which is about 4.6 hours at 60 fps and about 17 minutes at 1000

> [!warning] Warning
> Changing the fps of a level that already exists means recomputing every key in it. The `framerate-remap` modifier does that. Doing it by hand is not realistic

Next: [[2_rhythm-and-structure|Rhythm and structure]], [[1_order-of-work|The order of work]]
