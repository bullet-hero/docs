---
title: Translating
date: 2026-10-01
tags: [contributor]
---

# Translating

A translation is a copy of the English file at the same path in your language's folder, where only the text is translated. A fact that appears in any language is carried to all the others

## Mirrored paths

Every page lies at the same path, with the same file name, in every language folder:

```
en/docs/2_editor/4_craft/3_difficulty-curve.md
ru/docs/2_editor/4_craft/3_difficulty-curve.md
zh/docs/2_editor/4_craft/3_difficulty-curve.md
```

What stays unchanged:

- the file name and every folder name, prefixes included
- `date` and `tags` in the frontmatter (`title` is translated)
- `[[wiki-links]]`: their targets are file names, identical in every language
- external links, image names, code blocks and inline code: files, fields, keys, values, commands
- the structure: the same headings in the same order, the same lists, tables and callouts

Callout titles are translated into the page's language. More - [[style-guide]]

## English is the fallback

When a page is missing in a language, the site shows the English page with a notice.
The reverse does not work: a page that exists only in `ru/` gives an English reader a 404

> [!caution] Caution
> Never add a page in another language before it appears in `en/`. Readers of every other language will get a broken link

## Every language carries every fact

English leads only for addresses, not for content.
A fact may appear in any language first, and then it is carried to all the others. After a change, every version holds everything all versions know

- **Add, never remove.** Missing information is written into every language that lacks it
- **Contradictions are not resolved by guessing.** Two versions give different numbers or opposite claims? Check the source (the game, the SDK) and raise the question in the pull request
- **Nothing is deleted without asking,** even text that looks outdated

A difference in wording is not a problem. A difference in what the reader learns is a problem

## Comparing versions

The repository has a skill for Claude Code, `compare-translations` (in `.claude/skills/`). It does this comparison. Without it, go through the same two passes by hand

**The structural pass** compares the versions element by element: frontmatter, the H1, the first paragraph, the headings, the number of paragraphs, list items, table rows and callouts, the link targets, images, code

**The meaning pass** reads each section side by side and looks for facts one version has and another lacks: numbers and units, names of fields, buttons and keys, conditions and exceptions, warnings, the steps of a procedure and their order, examples

## New language

A new language is added entirely in this repository, the site's code does not change:

1. Copy `frontend/en.yaml` to `frontend/<code>.yaml`, for example `frontend/de.yaml`, and translate the values. These are the site's own strings: the menu, buttons, search, the cookie banner. Keep the keys and every `{name}` as they are
2. Create the `<code>/` folder next to `en/`, `ru/` and `zh/` and translate pages into it. A page without a translation is shown in English with a notice

A key with `one` / `few` / `many` / `other` forms depends on a count. Give it every form your language needs, the build names the missing ones.
An untranslated key is shown in English. The build lists such keys as warnings

Before a large translation, open an issue in [bullet-hero/docs](https://github.com/bullet-hero/docs), so two people do not translate the same thing
