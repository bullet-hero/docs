---
name: bullet-hero-text-style
description: The house style for every reader-facing page of bullet-hero/docs (everything under `<lang>/docs`, `<lang>/notes`, `<lang>/download.md`), in any language. Use it when writing, translating or rewriting a page, and when asked to "make it sound like us", "remove the AI tone" or "rewrite in the house style". Do NOT apply it to `CLAUDE.md`, `README.md` or `.claude/` - those are dense English technical text with their own rules.
---

# Bullet Hero text style

How to write a page that could be published on the site without a rewrite. It is derived from the game's own text style (the voice of the in-game hints and guide) and adapted to the website. **Profanity is forbidden in every mode and language**

The style is not decoration. The text reports, it does not sell: every emotion is turned into a list, a table or a number first. A page that sounds like marketing, expert posturing or a friendly AI assistant has failed, even when every fact in it is right

## 0. Simple first. The rule above all others

Derived from the author's own rewrite of `docs/index.md` and `download.md`. A text can have no filler at all and still be hard to read: every sentence is true, but they are chained into one dense argument and the reader has to hold all of it at once. **Beginner pages** (`player`, the first pages of `level_author`, quick start, FAQ, help, every section landing) are written so they can be skimmed. Reference and SDK pages may be denser, but the same rules apply to their sentences

1. **Only what the reader needs now.** Before each sentence ask: does the reader act differently after reading it? If not, cut it or move it to the detailed page. Edge cases, platform caveats, internal reasons ("because the format..."), how the site itself works, what is "not documented here" - out of a beginner page
2. **One sentence, one thought.** No chains of clauses joined by colons, "because", "so", "while", parentheses inside parentheses. Two short sentences beat one long one. A sentence may stand on its own line inside a paragraph (ending with a full stop, the last one without)
3. **The general rule, not the exceptions.** "The numbers usually match" instead of three sentences on when they diverge. The exception lives on the detailed page, behind `More - [[page]]` / `Подробнее - [[page]]`
4. **Navigation before explanation.** A hub page is a short intro plus a table of name -> link and one-line pointers: `Everything you can download is here - [[download]]`. Drop descriptive columns ("what it is", "status") when the link already says it
5. **Say what matters, not how it works.** "This number matters more than all the others" plus a link, instead of the mechanism
6. **Status in a word.** `In development`, `Not available`, `Current version - gv 1.0.0`. No "at the time of writing", no "planned no earlier than"
7. **Expand an abbreviation where it first appears**, e.g. a column `gv` -> `game version`
8. **Talk to the reader.** A question and an answer are fine: `Don't like the documentation? Then you can help write it`. `You may want to...` is fine
9. **Plain words.** A term appears only when the reader will meet it in the game UI, and then it is in backticks exactly as the game shows it

Before (correct, but heavy):
```
The numbers do not follow each other. `gv` and `sv` once started equal and are now free to diverge: an SDK change does not have to move the game version, and a game update does not have to move the SDK version
```

After (the author's version):
```
The version numbers do not have to follow each other, but in most cases they match.
Versions are also bumped together, and a shared update carries the same version
```

## 1. Punctuation. Hard rules

Punctuation is correct everywhere except for two deliberate departures. Both are mandatory

**Departure 1. No long dashes.** The em dash `—` is banned completely, and so is the en dash `–`. Wherever a dash is required, write a spaced hyphen ` - `

```
Right:  Bullet Hero - less a game than a player for animations
Wrong:  Bullet Hero — less a game than a player for animations
```

**Departure 2. No full stop at the end of a paragraph.** Full stops between sentences inside a paragraph stay. The last sentence of a paragraph, a list item, a table cell and a heading get no full stop. Question and exclamation marks stay

**Important for the site.** Markdown merges consecutive lines with no blank line between them into one paragraph. A line with no full stop followed by another line becomes two sentences glued together. So:
- inside a paragraph, sentences are separated by full stops and written on one line
- a thought that has to stand on its own line gets a blank line before it (it is a separate paragraph)
- a line break for width (hard wrap) is allowed only inside one sentence

Everything else follows the norms of the language: commas around clauses and parentheticals, colons for explanations and lists, correct agreement. Typos and agreement errors are defects, not style

Other marks:
- The colon is used often, it is the working mark for explaining and unpacking
- The semicolon is never used. Use a full stop or a separate list item instead
- Exclamation marks are rare, at most one per long text
- Rhetorical questions are allowed, including as section headings: `## What next?`
- Quotes are straight `"quotes"` only. Russian guillemets `«»` are not used. Quotes mark ironic distance and coined terms (Chinese uses full-width `“”`, see section 9)
- An ellipsis is rare and only marks a broken-off thought
- Parentheses are used often, for a short aside, a caveat or a joke on the side

## 2. Layout

- Frontmatter `date` is the date of the page's last update, not of its creation. Any edit to a file sets its `date` to the day of the edit
- Every page starts with frontmatter and a `# H1` equal to `title`. Sections use `##`, subsections `###`. Deeper is not needed (on the site `##` and `###` produce anchors and the table of contents)
- **The opening after `# H1` answers, it does not announce.** It never describes the page ("what X is, how Y works and where Z lies"). It gives the short answer to the question the page exists for, so it is worth reading on its own, even if the reader stops there. The first paragraph is the site's description in listings and link previews (cut at 200 characters, no markup), so the core of the answer goes there. The answer may run on into a second or third paragraph. If the page is short, the opening is merged with the body instead of repeating it: no separate summary line on top of a page that is itself a few lines long

  Before: `Where to report a bug or ask a question, and what to write so the bug can be reproduced`

  After: `Game bugs go to the releases issues, questions to Discord. Attach the version string from the settings screen and the steps that lead to the bug`
- Bulleted lists with `-`, nested by indentation. Use a list wherever an enumeration is longer than two items
- Numbered lists only for sequential steps and for choices
- `*Italics*` for terms, product names and genres: `*musical bullet hell*`, `*Project Arrhythmia*`
- `**Bold**` to stress a single word (usually a quantifier) or to open a paragraph with its subject: `**The level folder** holds...`
- Backticks for everything technical: files, fields, formats, values, classes, commands, keys
- **A version is always its prefix plus the number, in backticks:** `gv 1.0.0`, `sv 1.1.0`, `fv 1.0.0`, `bv 1.0.0`, `mg 2`. Never a bare `1.0.0`, never "version 1.0.0" or "SDK 1.0.0" without the prefix. In `title` and `# H1` (where backticks do not render) it is plain text: `gv 1.0.0`. Third-party versions (Unity, NuGet packages) are not ours and keep their own form
- A table wherever three or more things are compared on several properties. Reach for a table before a paragraph
- Paragraphs are short, one to three lines. No walls of text
- External links are markdown links with the full address and scheme. Links inside the repository are `[[wiki-links]]`
- Never use emoji

## 3. Labelled paragraphs (callouts)

A paragraph with one concrete purpose is written as a callout. There are exactly five labels, anything else is an ordinary paragraph

| Callout | ru label | en label | What it opens |
|---|---|---|---|
| `> [!tip] Recommendation` | Рекомендация | Recommendation | do it this way |
| `> [!tip]` | Подсказка | Tip | a shortcut, a trick, a faster route |
| `> [!info]` | Интересно | Worth knowing | context that explains a decision |
| `> [!warning]` | Предупреждение | Warning | this will cost time or quality |
| `> [!caution]` | Внимание | Caution | this destroys work or ships a broken level |

The callout title is the label in the page's language: `> [!info] Worth knowing`, `> [!info] Интересно`. A recommendation must have its title, otherwise it cannot be told apart from a tip

**At most two callouts per page.** A third stops reading as emphasis and starts reading as decoration. The exception is reference pages, where every in-game hint window became a section: there the limit is two per section

A page about something that does not exist yet (the server, plans) opens with a `> [!warning]` about its status. It does not count toward the limit

## 4. Voice

**Who is speaking.**
- In `docs/` the text addresses the reader as "you" (in Russian, the formal "вы")
- The project speaks impersonally, never as "the developers" or "we": advice is `it is recommended` / `рекомендуется` / `建议`, a fact has the thing itself as its subject: `The game ships no textures at all`
- Where a page needs the author's own opinion or decision, it says "I" (`I recommend`, `я рекомендую`, `我建议`). The game is made by one person, so "I" is honest there. Keep it for a real judgement or a decision the author owns, not for plain facts
- In `notes/` first person and personal experience are allowed: a note is its author's report
- Never address the reader as "friends", "colleagues" or "dear readers"

**No history and no changelog in docs.** Documentation describes how things work now. "It used to be X and now it is Y" belongs in a note in `notes/`, not on a docs page

**No claims of being better than anything.** A comparison is allowed only when it makes the reader understand faster: "in *Project Arrhythmia* an object also lives on a stretch of time, but the hierarchy is arranged differently" explains, "we are more flexible than the competition" does not

**The limits of knowledge are stated plainly.** `most likely`, `not known yet`, `at the time of writing`, `this is only what has been checked`. False confidence is worse than not knowing. If a feature does not exist yet, the page says so

**Every judgement comes with its reason.** Not "a bad format" but "the format is awkward because it cannot be opened without the editor". An adjective without a reason is a defect

**Numbers instead of adjectives.** Seconds, frames, units, megabytes, versions, object counts. Whatever can be counted is counted

**Mechanics over emotion.** Explain how a thing works inside. The reader leaves with an understanding of the mechanism, not with an impression

**Irony is dry and rare.** A short aside in parentheses, with no build-up. Reference and technical pages carry almost none

**No profanity. Never, in any mode, in any language.** Crude stand-in words are not used either

**Never invent an address, a number or a fact.** Every link, number and field name comes from the code or documents of the game, the SDK or the site. When there is no source, say it is unknown, or do not write the text

## 5. Structure

**A docs page.**
1. `# H1` and the opening that answers the page's question (see section 2)
2. The body never repeats the opening. It gives the details, cases and steps behind it
3. `##` sections, one topic each: claim -> mechanism or steps -> conclusion
4. At the end, where it fits, a list of concrete advice or "read next" links as `[[wiki-links]]`
5. The ending never retells the page

A guide article is 2-4 minutes of reading (2000-3500 characters). A reference page can be longer, but every section stands on its own

**A note (`notes/`).** The article template:
1. A caveat instead of an introduction, lowering inflated expectations or explaining the title
2. One line on what the text covers
3. Disclaimers, if the topic needs them
4. `##` sections: claim -> personal experience or how it works -> conclusion
5. Advice as a list, including the option "don't do it"
6. A direct address to the reader at the end: a question, a call to action or a self-ironic full stop

**Legal text (`notes/` tagged `legal`).** No irony, no personal experience, precise wording. Punctuation follows section 1

## 6. What must not be in the text

These are the marks of someone else's text or of AI text. They destroy recognisability more than any mistake

- A long dash `—` or `–` in any form
- A full stop at the end of a paragraph, list item or heading
- A semicolon
- Profanity and crude stand-ins
- "It's not just X, it's a whole Y"
- Rule-of-three flourishes: "faster, cheaper, more reliable"
- Empty openers: "in today's world", "let's dive in", "it's no secret that"
- A summarising ending that repeats what was already said
- Enthusiastic adjectives with no reason: "incredible", "amazing", "a powerful tool"
- Polite filler and apologies to the reader
- Symmetrical pretty phrasing for the sake of rhythm. Write by meaning
- Generic advice that was never checked against this game
- "I" in `docs/` for a plain fact, or "the developers" / "we" for the project

## 7. Rewrite examples

**Example 1. Opening paragraph**

Before (AI):
```
In today's world of level design, the Bullet Hero editor holds a special place — it's not just a
tool, it's a whole ecosystem. Let's dive in and see why.
```

After:
```
The editor builds a level from objects that live on a stretch of time and move along keyframes. Below is how it is arranged and in what order to work with it
```

**Example 2. A judgement**

Before (AI):
```
The Blob format is an amazing solution that dramatically speeds up loading and makes your workflow more productive.
```

After:
```
`Blob` loads faster than `Json`, but it cannot be read by eye or diffed in git. Keep a level in `Json` while you work on it and convert it to `Blob` before publishing
```

**Example 3. Something unknown**

Before (AI):
```
The official server will offer a convenient way to share your levels with the whole world.
```

After:
```
There is no official server yet. The protocol the game will use to talk to it has not been designed, so this page describes only what has already been decided
```

## 8. Checklist before handing over

1. Zero `—` and `–` characters
2. No paragraph, list item or heading ends with a full stop
3. No glued lines: every separate thought is either its own paragraph or separated by a full stop within the line
4. No `;`, no emoji, at most one `!`
5. No profanity
6. Commas, colons and agreement follow the norm, no typos
7. Every judgement has its reason next to it
8. Numbers, field names and links come from a source, nothing is invented
9. No "the developers" or "we" in `docs/`: advice is impersonal, "I" only for the author's own opinion
10. At most two callouts (or two per section on a reference page)
11. The opening after `# H1` answers the page's question (core within the first 200 characters), never describes the page, and is not repeated below
12. The ending does not retell the text, and nothing from section 6 is present

## 9. Language notes

The rules above apply to every language with no exceptions. Language-specific points:

- **Russian:** the reader is "вы" (formal, lowercase). Quotes are straight `"лапки"`, never `«ёлочки»`. Advice is "рекомендуется", the author's opinion is "я". Callout titles are Рекомендация, Подсказка, Интересно, Предупреждение, Внимание. Russian dash rules (dash between subject and predicate, etc.) are satisfied with a spaced hyphen ` - `
- **English:** callout titles are Recommendation, Tip, Worth knowing, Warning, Caution. Standard English punctuation otherwise
- **Chinese (`zh`, Simplified):** follows the game's `TEXT-STYLE.md` section 8, adapted to markdown. Terms come from `game/zh-glossary.md` (one spelling per term, `strict` rows always), a UI label is quoted from `game/zh.yaml`'s own value
  - The reader is `你`, never `您`. Advice is `建议`, the author's opinion is `我`, never `开发者` or `我们`
  - Full-width punctuation `，。：？！（）`, quotes `“”`. Code, file names and anything in backticks keep ASCII punctuation
  - Departure 2 holds: no `。` closes a paragraph, list item, table cell or heading. `。` between sentences stays
  - Departure 1 becomes: no dash of any kind - no `——`, no `—`, and no spaced hyphen ` - ` either. Use `，`, `：` or a new sentence. `More - [[page]]` is written `更多：[[page]]`
  - No `；` - two sentences or `，`
  - No space between hanzi and Latin letters or digits (`在Bullet Hero中`, `60帧`), the way the game writes it
  - Callout titles are 建议, 提示, 须知, 警告, 注意 (`> [!tip] 建议`)
  - Kept in Latin: product and format names (`Bullet Hero`, `JSON`, `BPM`), file extensions, keyboard keys, field names
  - **A paragraph is one line in the source.** Markdown turns a line break inside a paragraph into a space, which shows up between Chinese sentences and breaks search. A sentence that must stand on its own line is a separate paragraph (blank line before it)
  - **Punctuation goes outside the bold markers**: `**粗体**。正文`, never `**粗体。**正文`. Markdown does not close `**` that follows a full-width mark and is followed by a hanzi, so the second form prints the asterisks. The same holds for `` **`code`**正文 `` - drop the bold around code
  - `*Italics*` has no effect on hanzi worth relying on (Chinese fonts have no italic): use it only on Latin product names; stress with `**bold**`
- Technical terms, code, API names, file names and CLI commands stay in English in every language and are never translated
