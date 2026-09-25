# bullet-hero/docs

Public documentation for **Bullet Hero** — a rhythm / bullet-hell hybrid built as an engine for the
genre. Everything here is published on the game's website (https://bullethero.space/)

## What is documented

| Section | For whom |
|---|---|
| `docs/1_game` | players: installing, playing, settings, and the mechanics for those who want them |
| `docs/2_editor` | level authors: the editor guide and a reference of every panel, generator and effect |
| `docs/3_sdk` | developers: the open SDK, the level format, validation, generators |
| `docs/4_server` | server hosts and developers: official and community servers (planned) |
| `docs/5_contribute` | you: how to write and translate pages in this repository |
| `notes/` | articles, public documents and policies |

## How it works

The repository is an [Obsidian](https://obsidian.md/) vault: open its root folder as a vault and
links, embeds and previews work the same way they do on the site. Any other markdown editor works
too.

```
en/                     English (every page must exist here)
  docs/
    index.md            -> /en/docs
    1_game/index.md     -> /en/docs/game
    1_game/3_controls.md -> /en/docs/game/controls
  notes/cookie-policy.md -> /en/notes/cookie-policy
  download.md           -> /en/download
ru/                     Russian, same paths and file names
assets/                 images, embedded as ![[file.png]]
game/                   the game's UI strings, not pages (see "UI strings")
```

- The `N_` prefix sets the order in the sidebar and never appears in a URL
- Each page starts with `title`, `date` and `tags` frontmatter and a `# Title` heading that repeats
  the title
- Links are `[[file-name]]`, images are `![[image.png]]`
- The full rules are in [`docs/5_contribute`](en/docs/5_contribute/index.md) and in `CLAUDE.md`

## Contributing

1. Fork the repository and create a branch
2. Edit or add pages. **Change every language version**, or say in the pull request which languages
   still need the change
3. Follow the style guide ([`docs/5_contribute/3_style-guide`](en/docs/5_contribute/3_style-guide.md))
4. Open a pull request with a short description of what changed and why

Facts must come from the game, the SDK or its documentation. If you are not sure something is true,
say so in the pull request rather than in the page.

**Translations.** To translate a missing page, copy the English file to the same path under your
language folder and translate the text, keeping file names, links, code and tags unchanged. A new
language also needs a change on the website side, so open an issue first.

The site picks up new content when its submodule pointer is bumped, so a merged change appears on
https://bullethero.space/ with the next site deploy.

## UI strings

`game/` holds every text the game's interface shows, one YAML file per language. They are not pages
and the site does not publish them; the game imports them into its string table. Translators change
values only - see [`game/README.md`](game/README.md).

## License

[MIT](LICENSE)
