---
title: Markdown kitchen sink
date: 2026-09-17
tags: [meta, reference]
---

# Markdown kitchen sink

Every feature the renderer supports, on one page, so a styling change can be checked
against all of them at once.

## Text

Regular text, **bold**, *italic*, ***both***, ~~struck through~~, `inline code`, and a
[plain link](https://github.com/vertoker/bullet-hero-sdk). Also ==highlighted text==.

A footnote reference[^1] sits inline.

[^1]: And the footnote body lands at the bottom of the page.

## Callouts

> [!NOTE]
> Callouts use the Obsidian syntax. This one is informational.

> [!WARNING]
> This one warns. It maps onto the game's amber warning colour.

> [!DANGER]
> And this one is an error, in the game's muted coral.

## Lists

- First item
- Second item
  - Nested item
  - Another nested item
- Third item

1. Ordered one
2. Ordered two
3. Ordered three

- [x] A finished task
- [ ] An unfinished one

## Table

| Component | Prefix | Example |
| --- | --- | --- |
| Game | `gv` | `gv 0.11.0` |
| SDK | `sv` | `sv 0.4.2` |
| Site | `fv` | `fv 0.11.1` |
| Backend | `bv` | not yet |

## Code

```ts
export function localePath(lang: Lang, path = ''): string {
  const rest = path.replace(/^\/+/, '')
  return rest ? `/${lang}/${rest}` : `/${lang}`
}
```

```csharp
public sealed class LevelLoader
{
    public Level Load(string path) => _serializer.Deserialize(File.ReadAllBytes(path));
}
```

## Quote

> A long quotation, used for citing someone rather than for calling something out.
> It wraps across lines and keeps its indent.

## Image

![[placeholder.svg]]

## Horizontal rule

---

And text after the rule.
