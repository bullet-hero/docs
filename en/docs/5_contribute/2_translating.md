---
title: Translating
date: 2026-09-24
tags: [contributor]
---

# Translating

How language versions mirror each other, what the site shows without a translation and how to keep every language complete

## Mirrored paths

Every page exists at the same path, with the same file name, in every language folder:

```
en/docs/2_editor/4_craft/3_difficulty-curve.md
ru/docs/2_editor/4_craft/3_difficulty-curve.md
```

To translate a missing page, copy the English file to the same path under your language folder and translate the text

What stays unchanged:

- the file name and every folder name, prefixes included
- `date` and `tags` in the frontmatter (`title` is translated)
- `[[wiki-links]]`: their targets are file names, identical in every language
- external links, image names, code blocks and inline code: files, fields, keys, values, commands
- the structure: the same headings in the same order, the same lists, tables and callouts

Callout titles are translated into the page's language. More - [[3_style-guide]]

## English is the fallback

When a page is missing in a language, the site shows the English page with a notice.
The reverse does not work: a page that exists only in `ru/` gives an English reader a 404

> [!caution] Caution
> Never add a page to another language before it exists in `en/`. Readers of every other language will get a broken link

## Every language carries every fact

English leads only for addresses, not for content.
A fact may be added in any language first, and then it is carried to all the others. After a change, every version holds everything all versions know

- **Add, never remove.** Missing information is written into every language that lacks it
- **Contradictions are not resolved by guessing.** Two versions give different numbers or opposite claims? Check the source (the game, the SDK) and raise it in the pull request
- **Nothing is deleted without asking,** including text that looks outdated

A difference in wording is not a problem. A difference in what the reader learns is

## Comparing versions

The repository ships a skill for Claude Code, `compare-translations` (in `.claude/skills/`). It does this comparison. Without it, go through the same two passes by hand

**The structural pass** compares the versions element by element: frontmatter, the H1, the first paragraph, the headings, the number of paragraphs, list items, table rows and callouts, the link targets, images, code

**The meaning pass** reads each section side by side and looks for facts one version has and another lacks: numbers and units, names of fields, buttons and keys, conditions and exceptions, warnings, the steps of a procedure and their order, examples

## Adding a new language

A new language needs two changes: its folder in this repository and a change on the site side, whose code is closed.
Open an issue in [bullet-hero/docs](https://github.com/bullet-hero/docs) before you start translating. Then the site can be prepared to show the new language
