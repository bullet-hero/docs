---
name: compare-translations
description: Compare one page (or a whole folder) of bullet-hero-docs across all its language versions and reconcile them so that no information is lost in any language. Use after editing a page in one language, before a release, when reviewing a translation PR, or when asked to "check translations", "sync ru/en", "what's missing in the Russian version".
---

# Compare translations

Every page lives at the same path in each language folder: `en/docs/2_editor/4_craft/3_difficulty-curve.md` and `ru/docs/2_editor/4_craft/3_difficulty-curve.md`. English is the site's source of truth for routing and fallback, but **information may have been added in any language first**. The goal is the union: after this skill runs, every language version carries every fact, and nothing was deleted silently

## 1. Input

- A language-less path: `docs/2_editor/4_craft/3_difficulty-curve` (with or without `.md`), or a folder: `docs/3_sdk`, or `all`
- Find every `<lang>/<path>` that exists. Languages are the top-level folders listed in `CLAUDE.md` (currently `en`, `ru`)
- For a folder, also list pages that exist in one language and are missing in another. Those are reported, not auto-translated, unless the user asks

## 2. Structural pass

Compare the versions element by element, in order. Report every mismatch:

| Element | What must match |
|---|---|
| frontmatter | `date` and `tags` identical. `title` is translated, but present |
| `# H1` | present, equal to that version's `title` |
| first paragraph | present, one line, at most 200 characters |
| `##` / `###` headings | same count, same order, same level |
| paragraphs per section | same count (a split or merged paragraph is reported, not always wrong) |
| lists | same number of items, same nesting |
| tables | same number of rows and columns, same header meaning |
| callouts | same type, same position, title in the page's own language |
| `[[wiki-links]]` | the same targets (targets are file names, identical in every language) |
| external links | the same URLs |
| images `![[...]]` | the same files |
| code blocks | identical content (code is never translated), comments may differ |
| inline code | the same identifiers, file names, keys and values |

## 3. Meaning pass

Read each section side by side and look for facts that one version has and another lacks:
- numbers and units (seconds, frames, pixels, megabytes, counts, versions)
- names of fields, buttons, menus, keys and shortcuts
- conditions and exceptions ("only on Android", "unless the level is protected")
- warnings and consequences
- steps in a procedure, and their order
- examples

A difference in wording is **not** a finding. A difference in what the reader learns **is**

## 4. Report

Before editing anything, print one table per page:

| Section | Difference | Present in | Missing in | Action |
|---|---|---|---|---|
| `## Keyframes` | the 0.2 s dash duration | ru | en | add to en |
| `## Export` | `.7z` is refused by name | en | ru | add to ru |
| `## Budget` | object limit 5000 vs 3000 | en, ru (differ) | - | **ask** |

Then a short list of pages that exist in only one language

## 5. Apply

- **Add, never remove.** Missing information is written into every language that lacks it, so the result is the union of all versions
- **Contradictions are not resolved by guessing.** Different numbers, opposite claims or different procedures are listed and put to the user as a question. Check the source (game code, SDK, game docs) when it is available and cite it in the question
- **Nothing is deleted without asking,** including content that looks outdated
- Added text follows the `bullet-hero-text-style` skill and the page's language rules (callout titles in that language, straight quotes, spaced hyphens)
- Structure is aligned too: a missing heading, table row or callout is added in the same position
- `date` and `tags` are synchronised to the same values. When they differ, keep the later `date` and the union of `tags`, and mention it in the report
- After applying, run the structural pass again and confirm it is clean

## 6. Checks this skill does not replace

The site build (`pnpm build` in bullet-hero-frontend) still reports unresolved wiki-links, and the style checklist in `bullet-hero-text-style` still applies to the added text
