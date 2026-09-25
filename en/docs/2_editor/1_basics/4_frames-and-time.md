---
title: "Frames, time and the length of a level"
date: 2026-09-24
tags: [level_author]
---

# Frames, time and the length of a level

A level frame is not a screen frame. How a level counts time, where its length comes from and which fps to pick

## Level frames and screen frames

A level frame has nothing to do with a screen frame.
The screen draws as many frames per second as the hardware allows. A level counts time in its own frames, and how many there are per second is stored in the level itself. The default is `60`

So a level plays identically at 60 Hz, at 144 Hz and on a phone that dropped to 30. Hit accuracy does not depend on the graphics card

A frame is a cell, not a moment. If one object ends on frame 100 and another starts on frame 100, they do not overlap

More precisely: frames count from 1, and frame f covers the time from (f-1)/fps to f/fps, left edge included, right edge not. So frame 1 starts at the very beginning of the track

## The length of a level

You set the level's length. The track's length comes from the file. They do not have to match

Content past the end of the level is allowed. It simply never plays, and validation says nothing about it

A child that sticks out of its parent's span works the same way. The level keeps what you wrote, and the effective lifetime is computed separately

To fit the lifetimes of children and parents to each other, run the `span-fit` modifier in `Generators`. It either clamps the children in or expands the parents out

## The level's fps

The higher the fps, the more precisely you land on the beat. And the more frames the same length takes.
The range is 1 to 1000, the default is `60`

> [!tip] Recommendation
> Leave the fps at the default. At 60 the ear does not hear a one-frame shift, and the number of keys grows with the fps

The timeline is capped at `1000000` frames. That is about 4.6 hours at 60 fps and about 17 minutes at 1000

> [!warning] Warning
> Changing the fps of a finished level means recomputing every key in it. The `framerate-remap` modifier does that, doing it by hand is not realistic

Next: [[5_keyframes-and-easing]], [[2_rhythm-and-structure]], [[1_order-of-work]]
