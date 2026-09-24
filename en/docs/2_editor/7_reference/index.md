---
title: Reference
date: 2026-09-24
tags: [level_author]
---

# Reference

Every panel, property, generator and effect of the editor, one section each

The reference describes the editor as it looks on screen, one panel, tab or tool at a time. The guide in the other sections of the editor docs explains how to work and why, the reference says what a given field or button does. It is not meant to be read through: the usual way in is a search, a link from a guide article or the sidebar

## How a page is built

Every `##` section corresponds to one hint window of the game and stands on its own, so a section opened straight from a search makes sense without the rest of its page. A section says what the panel shows, marks what is easy to get wrong, and ends with a "More" link to the guide article that explains the idea behind it. When a section tells you what a field does but not why it works that way, follow that link

## What it covers

Three groups of things, roughly:
- the surfaces you author on: the timelines and the beat grid, the hierarchy, the object and keyframe inspectors
- the tools that make or change content: effects, audio effects, generators, modifiers and prefab mode
- the level around its content: its settings, metadata, resources and licences, export, and the editor's own settings

## Words mean one thing

The reference uses the editor's terms in their exact sense, and several of them differ from what other editors mean by the same word. A span is a start and a length, never an end frame. A layer is relative to the parent and adds up along the chain. A frame is a cell of time, not a moment. When a word is unfamiliar, start with the [[1_glossary]], which keeps every term in one table

## Facts that hold on every page

- a generator or a modifier runs as one undoable operation, and anything that rewrites or deletes existing content asks for confirmation first
- options in the Play tab of the level settings apply to one run only and are never saved into the level
- autosave is configured in the editor settings but does not run yet, so saving is entirely yours

> [!caution] Caution
> The official server does not exist yet. Until it arrives, a level reaches another person as a folder or an archive, which is how the pages on metadata and export describe sharing
