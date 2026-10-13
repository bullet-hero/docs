---
title: Pictures from shapes
date: 2026-10-13
tags: [level_author]
---

# Pictures from shapes

Build a picture from built-in shapes first and draw your own only where none fits. Lay light and shade over one base shape, make every repeated element a prefab, and check the result against the original picture laid over the level

## Built-in shapes first

A built-in shape is real geometry with clean edges, and it costs nothing to reuse.
A circle and a square stretch to any size: a stretched, turned square is any bar, line or stick, a stretched circle is an ellipse

Draw your own shape in the shape editor only where no built-in one fits: a coat, a hand, a sail.
Give it its real corners only, with straight edges between them. A dozen corners read better than a hundred traced along every pixel

> [!tip] Recommendation
> Detail is the price of clean edges. A ragged outline or a visible seam spoils a picture more than a lost notch

## One base, details on top

Light and shade are separate shapes lying on top of one base shape, cut along its edge.
Two shapes that only touch edge to edge leave a thin seam of the background between them, and it shows

A part that another part covers runs on under it. A neck goes a little under the coat and the head, a leg under the hem.
Then the parts still meet when one of them moves

## Repeats are prefabs

Anything that appears more than once is a prefab: an eye, a window, a petal.
Build one, make it a prefab, place the rest, and change on each copy only what differs: its position, size, colours. Each such change is an override of that copy

One edit to the template then reaches every copy, and the level stays small

## Layers

Give every object its own layer. Two objects on one layer at the same time draw in an order you did not choose.
Keep the base below its details and the details below whatever lies over them

## Checking against the original

Import the original picture as a texture and put it on a rectangle of exactly its size, on top of everything.
To compare, turn the rectangle on. Turn it off for the rest of the work instead of making it transparent: a switched-off object draws nothing at all

Check the picture as a whole, then zoomed in, part by part: the edges, where parts meet, the shades

Next: [[2_reuse]], [[4_composition-and-camera]]
