# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working in this repository.

## Project overview

Public documentation for **Bullet Hero** — a rhythm / bullet-hell hybrid built as a **universal
engine for the genre**, not as a single game. This repository is plain markdown and nothing else: it
is the `content/` git submodule of the website (`bullet-hero/frontend`, closed), which compiles it
at build time and prerenders every page. It is open so the community can fix text and add
translations.

Bullet Hero is a **software complex**, and the docs are split by product first, audience second:

| Product | Repo | Status | Docs folder |
|---|---|---|---|
| Game (Unity client) | [bullet-hero/game](https://github.com/bullet-hero/game), closed | released, `gv` | `docs/1_game/` |
| Level editor (inside the game) | bullet-hero/game, closed | released, `gv` | `docs/2_editor/` |
| SDK (level/save data model, MIT) | [bullet-hero/sdk](https://github.com/bullet-hero/sdk), open | released, `sv` | `docs/3_sdk/` |
| Server (official OWS + community NOWS) | [bullet-hero/backend](https://github.com/bullet-hero/backend), open, empty | not built, `bv` | `docs/4_server/` |
| These docs | [bullet-hero/docs](https://github.com/bullet-hero/docs), open | open | `docs/5_contribute/` |
| Website | bullet-hero/frontend, closed | `fv` | not documented here |
| Public builds + players' issues | [bullet-hero/releases](https://github.com/bullet-hero/releases), open | every public `gv` | linked from `download.md` |

All repos live in the [bullet-hero](https://github.com/bullet-hero) organization. Where to report:
game bugs and requests -> `releases` issues, the SDK and its code -> `sdk` issues, doc text -> `docs`.

Versions use a letter prefix across the complex: game `gv`, SDK `sv`, site `fv`, backend `bv`, each
major.minor.revision.

## Rules

### 1. No commit

**Never commit. Only the author commits.** If the author ever asks for a commit explicitly, its
message carries **no trailers at all** — no `Co-Authored-By:`, no "Generated with Claude Code".
Community changes arrive as pull requests (see `README.md`).

### 2. English in the repo, Russian in conversation

Repository text outside the language folders (`CLAUDE.md`, `README.md`, `.claude/`) is English only.
Page content is written in the language of its folder (`en/`, `ru/`). When talking to the author —
chat replies, explanations, questions — **always respond in Russian**, in dense telegraphic style
(no filler, abbreviations like "т.е.", "т.к." welcome).

### 3. Every reader-facing page follows `bullet-hero-text-style`

Load the `bullet-hero-text-style` skill before writing or rewriting any page under `<lang>/`. It
covers punctuation (spaced hyphen instead of dashes, no full stop closing a paragraph), voice
("you" and "the developers" in docs, never "I"), callouts, structure, and a checklist. Profanity is
forbidden everywhere.

### 4. Every language, every time

A page is written in **all** languages at once (currently `en` and `ru`), at the same path with the
same file name. After changing a page in one language, run the `compare-translations` skill on it —
information is added to every language, never removed without asking.

### 5. Never invent facts

Numbers, field names, file names, shortcuts and URLs come from the game repo, the SDK repo or the
site. When no source exists, the page says the thing is unknown or planned. Sources on the author's
machine: game `C:\Projects\Unity\Bullet Hero` (its `CLAUDE.md`, `Docs/`, and the string table
`Assets/Addressables/Strings/Strings.csv`), SDK inside it at `Assets/Plugins/BulletHeroSDK`.

One exception runs the other way: **the avatar's numbers are defined here** (`docs/1_game/6_avatar`,
`7_damage`) — the game is built to match them, and the SDK's `AvatarRules` + `AvatarRulesTests` pin
the same values. A number changes on these pages first.

### 6. One glossary

Use the terms of `docs/2_editor/7_reference/1_glossary`, in every language; a new term is added there
first. The Russian term is the one the game's UI uses.

## Layout

```
<lang>/                      en (source of truth for routing), ru
  docs/                      documentation, nested by product
    index.md                 -> /<lang>/docs          (the hub: who are you, where to go)
    1_game/index.md          -> /<lang>/docs/game     (folder landing page, labels the sidebar group)
    1_game/3_controls.md     -> /<lang>/docs/game/controls
    2_editor/4_craft/…       -> /<lang>/docs/editor/craft/…
  notes/                     flat: articles, public documents, policies (sorted by date)
  download.md                -> /<lang>/download
  tags/<tag>.md              -> /<lang>/tags/<tag>  (one page per tag, see "Audience tags")
assets/                      images, embedded as ![[file.png]]
.claude/skills/              bullet-hero-text-style, compare-translations
```

- **Order is set by an `N_` prefix** on every file and folder inside `docs/` (`1_`, `2_`, … `10_`).
  `index.md` has no prefix and takes its folder's position. The prefix never reaches a URL. To
  reorder, rename — Obsidian updates the links (enable "Automatically update internal links").
- Names without the prefix are unique within a language, and a prefixed name is identical across
  languages.
- `notes/` has no subfolders and no prefixes. `notes/cookie-policy` is linked from the site's cookie
  banner — never rename it.
- A file outside `docs/`, `notes/`, `tags/` and `download.md` is not routed by the site.

## Page format

```markdown
---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

One line that says what the page is, up to 200 characters, no markup.

The body...
```

- **Frontmatter is `title`, `date` (`YYYY-MM-DD`, set at creation) and `tags`.** Nothing else is read.
- **`# H1` is required** and equals `title` — the site renders the body only, so the H1 is the visible
  page title.
- **The first paragraph after the H1 is the page's description** in listings, search and link previews
  (cut at 200 characters).
- Sections `##`, subsections `###` — they produce anchors and the table of contents.
- **Links:** `[[3_difficulty-curve]]` by full file name, `[[3_difficulty-curve#Anchor]]` for a section,
  `[text](https://…)` outside. Links resolve to a language-less route, so the same source works in
  every language. Link to a folder landing with its path: `[[2_editor/4_craft/index]]`.
  An alias-less link is shown with the target page's title in the reader's language, so write the
  sentence to read well with the title in place. `[[target|text]]` keeps its own text.
- **No table-of-contents lists.** Navigation is the sidebar. A folder's `index.md` is a real introduction
  to its section, not a list of its children.
- **Images:** `![[file.png]]`, the file lives in `assets/`.
- **Callouts:** `> [!note]`, `[!info]`, `[!tip]` (blue), `[!warning]`, `[!caution]` (amber),
  `[!danger]`, `[!bug]` (red). Which to use is defined in the style skill.
- **Code highlighting** exists only for `ts tsx js json csharp bash yaml css md`. Other languages
  render as plain text.
- GFM tables, task lists, footnotes and `==highlights==` work. No MDX, no JSX: `{` and `<` are literal.

## Audience tags

Every docs page has 1-3 of these tags (`snake_case`, no `#`), shown on the page:

| Tag | Who |
|---|---|
| `player` | a regular player |
| `advanced_player` | a player who wants the mechanics |
| `level_author` | makes levels in the editor |
| `developer` | builds on the SDK or extends the game |
| `server_host` | runs a server for themselves and friends |
| `server_advanced` | a large host, invested enough to extend or write a server |
| `contributor` | edits the texts and translations in this repo |

Notes use topic tags instead (currently `legal`).

**Every tag in use has a page** `<lang>/tags/<tag>.md` in **every** language: file name = tag code,
frontmatter `title` (the localized label shown instead of the code) and `date`, no `tags`. Body: `# H1`
= title, first paragraph = who this audience is (<= 200 chars), then 1-3 short paragraphs on what
the reader needs and where to start (a couple of wiki-links). The site appends the list of tagged
pages itself — never list pages by hand. A new tag = a new page in every language, same commit.

## Translations

- English is the source of truth for **routing**: a page missing in a language falls back to English on
  the site with a notice. A page that exists only in `ru/` gives English readers a 404, so never do
  that.
- It is **not** the source of truth for **information**: anything added in any language is carried to
  all of them (`compare-translations`).
- Adding a new language means adding its folder here **and** adding it to `LANGS` in the frontend
  (`plugins/content-scan.ts`, `src/i18n/`) — ask the author.

## Verification

This repo has no build of its own. Verify through the frontend:

```bash
cd D:/Projects/Web/bullet-hero-frontend
git -C content fetch D:/Projects/Web/bullet-hero-docs <branch> && git -C content checkout FETCH_HEAD
# or, for uncommitted work, copy the working tree into content/
pnpm lint && pnpm build
```

- The build prints `[content] N unresolved wiki link(s)` — keep it at zero.
- `[content] … both answer at …` means two files collapse to one URL after the prefix is stripped.
- Restore the submodule to its pinned commit afterwards (`git submodule update content`).
- End each task with concrete manual check steps: which URLs to open, what to look at.

## Future

- **In-game docs.** The game does not embed these pages. Its hints link to `docs/2_editor` pages by
  URL, and `HintSiteLinksTests` in the game repo fails on a renamed or removed target. Renaming such
  a page is fine, but tell the game side.
- **Server docs.** `docs/4_server/` describes plans. It is rewritten once the backend exists.
