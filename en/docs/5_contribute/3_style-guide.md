---
title: Style guide
date: 2026-09-24
tags: [contributor]
---

# Style guide

How a Bullet Hero page should sound: simplicity, punctuation, voice, callouts and structure, with before and after examples

The text reports, it does not sell. Every emotion is turned into a list, a table or a number first.
A page that sounds like marketing, expert posturing or a friendly assistant has failed, even when every fact in it is right

## Simple first

This rule stands above all the others

A text can have no filler at all and still be hard to read. Every sentence is true, but they are chained into one dense argument, and the reader has to hold all of it at once

Beginner pages are written so they can be skimmed. These are the player pages, the first pages for level authors, the quick start, the FAQ, help and the landing page of every section. Reference and SDK pages may be denser, but the same rules apply to their sentences

1. **Only what the reader needs now.** Before each sentence ask: will the reader act differently after reading it? If not, cut it or move it to the detailed page. Edge cases, platform caveats, internal reasons, how the site itself works - not for a beginner page
2. **One sentence, one thought.** No chains of clauses joined by colons, "because", "so", "while", no parentheses inside parentheses. Two short sentences beat one long one. A sentence may stand on its own line inside a paragraph: with a full stop at the end, except the last one
3. **The general rule, not the exceptions.** "The numbers usually match" instead of three sentences on when they diverge. The exception lives on the detailed page, behind `More - [[page]]`
4. **Navigation before explanation.** A landing page is a short intro and a table of name -> link, or lines like `Everything you can download is here - [[download]]`. Descriptive columns such as "what it is" and "status" are not needed when the link already says it
5. **Say what matters, not how it works.** "This number matters more than all the others" plus a link, instead of the mechanism
6. **Status in a word.** `In development`, `Not available`, `Current version - gv 1.0.0`. No "at the time of writing", no "planned no earlier than"
7. **Expand an abbreviation where it first appears.** For example, a column `gv` -> `game version`
8. **Talk to the reader.** A question and an answer are fine: `Don't like the documentation? Then you can help write it`. `You may want to...` is fine too
9. **Plain words.** A term appears only when the reader will meet it in the game UI. Then it is in backticks, exactly as the game shows it

```
Before (correct, but heavy):
The numbers do not follow each other. `gv` and `sv` once started equal and are now free to diverge: an SDK change does not have to move the game version, and a game update does not have to move the SDK version

After:
The version numbers do not have to follow each other, but in most cases they match.
Versions are also bumped together, and a shared update carries the same version
```

## Punctuation

Punctuation follows the norms of the language, with two deliberate departures. Both are mandatory

**No long dashes.** The em dash and the en dash are not used at all. Wherever a dash is needed, write a hyphen with spaces around it

```
Before:  Bullet Hero — less a game than a player for animations
After:   Bullet Hero - less a game than a player for animations
```

**No full stop at the end of a paragraph.** Full stops between sentences inside a paragraph stay. The last sentence of a paragraph, a list item, a table cell and a heading gets no full stop. Question and exclamation marks stay

**Watch the line breaks.** Markdown joins lines that have no blank line between them into one paragraph. A line with no full stop followed by another line turns into two sentences glued together

So inside a paragraph, every line followed by another line ends with a full stop. Put a blank line before every separate thought

Other marks:

- **The colon** is the working mark for explaining and listing, use it freely
- **The semicolon** is never used. Write a full stop or a separate list item instead
- **Exclamation marks** are rare, at most one per long text
- **Quotes** are straight `"quotes"` only, never `«»`
- **Parentheses** are welcome for a short aside, a caveat or a dry joke

## Layout

- **Short paragraphs,** one to three lines
- **A bulleted list** for any enumeration longer than two items. Numbered lists only for steps and choices
- **A table** wherever three or more things are compared on several properties
- **Italics** (`*text*`) for terms, product names and genres: *musical bullet hell*, *Project Arrhythmia*
- **Bold** to stress one word or to open a paragraph with its subject
- **Backticks** for everything technical: files, fields, formats, values, keys, commands
- **No emoji**

## Callouts

A paragraph with one concrete purpose becomes a callout. There are exactly five, and the title is written in the page's language:

| Callout | English title | Russian title | What it opens |
|---|---|---|---|
| `> [!tip] Recommendation` | Recommendation | Рекомендация | do it this way |
| `> [!tip]` | Tip | Подсказка | a shortcut, a trick, a faster route |
| `> [!info]` | Worth knowing | Интересно | context that explains a decision |
| `> [!warning]` | Warning | Предупреждение | this will cost time or quality |
| `> [!caution]` | Caution | Внимание | this destroys work or ships a broken level |

**At most two callouts per page,** because a third stops reading as emphasis. Reference pages may have two per section. A page about something that does not exist yet opens with a `> [!warning]` about its status, and that one does not count

## Voice

- **Address the reader as "you"** (in Russian, the formal "вы"). Never say "I" on a docs page. When the project has to be named, it is "the developers". Notes in `notes/` may speak in the first person, since a note is its author's report
- **No history in docs.** A docs page describes how things work now. "It used to be X" belongs in a note
- **No claims of being better.** A comparison is allowed only when it helps the reader understand faster
- **State the limits of knowledge.** "Most likely", "not known yet". False confidence is worse than not knowing
- **Every judgement comes with its reason.** An adjective without a reason is a defect
- **Numbers instead of adjectives.** Seconds, frames, megabytes, versions, object counts
- **Irony is dry and rare,** a short aside in parentheses. Reference pages carry almost none
- **No profanity** in any language, including crude stand-in words
- **Never invent** an address, a number or a fact. With no source, say it is unknown

## Structure of a page

1. `# H1` and a one-line summary of up to 200 characters
2. The first paragraph answers the question instead of preparing for it: it says what the thing is
3. `##` sections, one topic each: the claim, then the mechanism or the steps, then the conclusion
4. Where it fits, concrete advice or "read next" links at the end
5. The ending never retells the page

A guide page takes 2 to 4 minutes to read, about 2000 to 3500 characters. A reference page can be longer, but every section stands on its own

## What gives away someone else's text

- a long dash, a full stop at the end of a paragraph, a semicolon
- "It's not just X, it's a whole Y"
- rule-of-three flourishes: "faster, cheaper, more reliable"
- empty openers: "in today's world", "let's dive in", "it's no secret that"
- a closing paragraph that repeats what was already said
- enthusiastic adjectives with no reason: "incredible", "amazing", "a powerful tool"
- polite filler and apologies to the reader
- symmetrical phrasing written for rhythm instead of meaning
- generic advice nobody checked against this game

## Before and after

**An opening paragraph**

```
Before:
In today's world of level design, the Bullet Hero editor holds a special place — it's not just a
tool, it's a whole ecosystem. Let's dive in and see why.

After:
The editor builds a level from objects that live on a stretch of time and move along keyframes. Below is how it is arranged and in what order to work with it
```

**A judgement**

```
Before:
The Blob format is an amazing solution that dramatically speeds up loading and makes your workflow more productive.

After:
`Blob` loads faster than `Json`, but it cannot be read by eye or diffed in git. Keep a level in `Json` while you work on it and convert it to `Blob` before publishing
```

**Something that does not exist yet**

```
Before:
The official server will offer a convenient way to share your levels with the whole world.

After:
There is no official server yet. The protocol the game will use to talk to it has not been designed, so this page describes only what has already been decided
```

## Checklist before a pull request

1. The page can be skimmed: one thought per sentence, details lower on the page or on their own page
2. No em dashes and no en dashes
3. No paragraph, list item or heading ends with a full stop
4. No glued lines: every separate thought is its own paragraph or separated by a full stop within the line
5. No semicolons, no emoji, at most one exclamation mark
6. No profanity
7. Commas, colons and agreement follow the norm, no typos
8. Every judgement has its reason next to it
9. Numbers, field names and links come from a source
10. No "I" in `docs/`, the project is "the developers"
11. At most two callouts
12. The first paragraph after the H1 is a one-line summary of up to 200 characters
13. The ending does not retell the page
