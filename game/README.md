# UI strings

Every piece of text the game's interface shows - menus, settings, the level editor, the hints - one
file per language:

```
game/
  en.yaml    English
  ru.yaml    Russian
```

These files are the source the game's string table is built from. They are not pages: the website
does not publish this folder.

## Editing

Each line is a key and its text:

```yaml
editor_common_apply: "Apply"
hint_editor_timeline-level_body: |-
  <b>The whole level at once.</b>

  Every object is a bar...
```

- **Change values only.** Keys are added, renamed and removed by the game's developers. A key that
  exists in one language must exist, with the same name, in every other
- **A one-line value is in double quotes.** Inside them write `\"` for a quote, `\\` for a
  backslash and `\n` for a line break. Everything else - Cyrillic, `<`, `{`, `#`, `:` - is written
  as is
- **A multi-line value is a `|-` block**: every line indented by exactly two spaces, an empty line
  left empty. Never use tabs
- **Keep every tag and every placeholder exactly as it is.** Translate the words between tags, not
  the tags. `{0}`, `{count}` and the like are filled in by the game; `[TRACK]` in square brackets is
  a placeholder the reader replaces
- **Links stay links.** In `<link="https://bullethero.space/en/docs/...">` change the language in
  the address to the file's own language; a `<link="hint_...">` names another hint and never
  changes
- The file is read strictly: a line in any other shape stops the import and names the file and
  line. Use an editor that saves UTF-8, and keep the line endings as they are

### Allowed tags

The game draws text with Unity's UI Toolkit rich text, which supports:

`<b>` `<i>` `<u>` `<s>` `<color=#rrggbb>` `<#rrggbb>` `<mark=#rrggbbaa>` `<link="id">`
`<size=120%>` `<sup>` `<sub>` `<nobr>` `<noparse>` `<indent=10%>` `<align=center>` `<lowercase>`
`<uppercase>` `<alpha=#80>` `<width=60%>` `<voffset=5>` `<cspace=1>`

`<font="...">` does **not** work - it is shown as literal text. Angle brackets in ordinary text are
read as a tag and disappear, which is why placeholders use square brackets. XML entities such as
`&amp;` are not decoded and show up literally - write the character itself.

The colours in use are a fixed set, the same in every language:

| Role | Colour |
|---|---|
| Recommendation | `#7FC97F` |
| Tip | `#5EC8C8` |
| Worth knowing | `#B48CE0` |
| Warning | `#E8B04B` |
| Caution | `#E86A5A` |
| Technical name - a file, a field, a format, a value | `#D4B483` |
| Link | `#59A6FF` |
| Emphasis | `#DCE4E5` |

## Terms

A thing is named the way the [glossary](../en/docs/2_editor/7_reference/1_glossary.md) names it, in
every language.

## A new language

A new language is a new `<code>.yaml` next to these, with every key of `en.yaml`. The game also has
to ship the language, so open an issue first, as for a new language of the docs.
