---
title: AI assistant
date: 2026-10-12
tags: [level_author]
---

# AI assistant

An AI client that speaks MCP can edit the level open in the editor while you watch. Each AI batch is one undo step, and the AI cannot publish, delete files or write over another level

The game on Windows, Linux and Mac ships an MCP server for this. The AI edits through the same operations you do, so every change appears in the viewport at once and lands in the history like your own

Any client that speaks MCP works, such as a chat app or a coding assistant. Nothing in the game is tied to one AI

## Connecting a client

1. Open `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`
2. Tick `{{ui:settings_game-editor_mcp-enabled}}`. The status line under the settings shows the port the editor listens on
3. Press `{{ui:settings_game-editor_mcp-copy-config}}`. The clipboard now holds the client config with both paths filled in
4. Paste it into the MCP server settings of your client
5. Open a level in the editor, or ask the AI to open the editor or a level itself

The copied config looks like this:

```json
{ "mcpServers": { "bullet-hero": { "command": "<path to BH.MCP>", "args": ["--endpoint", "<path to endpoint.json>"] } } }
```

The server file `BH.MCP` lives beside the game:

| System | Server file |
|---|---|
| Windows | `<game folder>/BH.MCP.exe` |
| Linux | `<game folder>/BH.MCP` |
| Mac | `<game>.app/Contents/Resources/mcp/osx-arm64/BH.MCP`, on Intel `osx-x64` instead of `osx-arm64` |

Only this computer can connect, and only one client at a time.
Phones and tablets have no MCP section: the assistant is desktop only

Several copies of the game may run at once. The AI works in the last one started until you ask it to switch, and it can list them all. Each copy still takes one client. For several copies, keep `{{ui:settings_game-editor_mcp-port}}` at `0`, since two copies cannot listen on one port

## What the AI can and cannot do

The AI can do almost everything you can:
- read the level: the hierarchy, objects, keyframes, events and resources
- create, change and delete objects, keyframes, markers, checkpoints, audio tracks and the beat grid
- run generators, pack and place prefabs, work inside Prefab Mode
- import a texture, font or audio file into the level
- fill in the attribution record of a texture, font or audio file after importing it: title, description, link, sources and authors - [[4_resource-record]]
- use the game's own preset effects, themes, fonts and sounds. `resources_list` marks them as the game's, and they need no import
- undo and redo, save the open level, open another level, create a new one
- start and pause playback, as your play button does
- move the game to another screen, such as the editor, a level or the settings, with the same arguments a launch takes - [[12_launch-arguments]]
- start the game when it is not running, if the server lies beside the installed game and MCP is already on

A run started this way counts in your statistics like any other, so the AI starts one only when you ask it to

It cannot:
- publish to Steam Workshop
- delete a level or any file
- write over another level or another file. An import whose file name is already taken is refused
- open a level that is read-only, or a protected level whose password you have not entered in this session
- open another level while the open one has unsaved changes

**One AI batch is one step in history.** It shows on the `{{ui:settings_level-settings_history}}` tab as `{{ui:op_group_ai-batch}}` with the AI's own caption. One `Ctrl+Z` removes the whole batch. More on history - [[10_level-settings#History]]

The first AI batch that changes a level sets its `{{ui:settings_level-settings_metadata-level-ai-generated}}` to `{{ui:enum_ai-generation_yes}}`, inside the same step. Undoing the batch reverts it. More - [[2_metadata-and-sharing#AI generation]]

## You have priority

The AI never fights you for the editor:
- while you drag a gizmo handle or scrub the timeline, the AI's edits are refused, and it waits and tries again
- the AI takes the playhead only while you are idle: not playing, not dragging, not typing, not saving
- the editor starts playing a level as it opens, so the AI may pause it to look at frames. A level the AI opens or creates itself stays paused. If you are watching playback on purpose, the AI asks before pausing
- if you touch the editor while the AI is looking at a frame, the AI stops at once. The playhead stays where you put it
- while a walk through history runs, the AI cannot edit either

While a client is connected, the viewport shows `AI` in its top right corner, under the search buttons. Its colour is the state: green - connected, amber - the AI is working, red - the AI's last call ended in an error.
After the client disconnects, the badge stays for {{v:mcp.badge-hold-seconds}} seconds, so an AI that reconnects for every step does not blink. It hides together with the viewport tools.
Hover over it to read the state in words: `{{ui:editor_agent-badge_connected}}`, and while the AI works, the caption of what it is doing.
The cross beside it disconnects the client and refuses it, and the badge goes away

A stop is not saved. Turning `{{ui:settings_game-editor_mcp-enabled}}` off and on again or restarting the game clears it

## What the AI sees

The AI looks at the level in two ways:
- **a schematic.** A picture of any frame, computed off screen. It does not move the playhead. It shows shapes and hitboxes, but no texts and no effects
- **a capture.** Real pixels, exactly as the level draws, taken through your playhead. For a moment the playhead jumps to that frame and the editor's overlays hide. Then the playhead returns to where you left it, unless `{{ui:settings_game-editor_mcp-follow-ai}}` is on. The picture is framed by the level camera, not by the editor camera

A still of an effect after a jump is close to what continuous play shows, but not always identical

The AI cannot hear the music. It turns the track into numbers: tempo, beats, bars, sections, how loud each band is.
This is an estimate with a confidence, and it can be off, for example by half or double the tempo. The beat grid you set in the level is trusted over the AI's estimate

So when timing matters, the AI may ask you to listen. It plays a range of up to {{v:mcp.max-play-seconds}} seconds in the editor, and this also moves the playhead. Touch the editor, and playback stops where it is

While the editor's sound is muted, the AI does not play anything and asks you to turn the sound on

The AI's own actions make no interface sounds: an undo, a save or a refusal it causes is silent. Only what it plays on purpose is heard

## The ai folder

The AI keeps its memory of the level in the `ai` folder inside the level folder. The next session, with any client, reads it first and continues where the last one stopped

What lies there:
- `CONTEXT.md` - the brief, the music, the section plan, decisions, your remarks and open questions
- other files the AI decides to keep, `.md` or `.json` only
- `manifest.json` - whether the folder travels with the level. The AI cannot change it

The folder appears only when the AI first has something to write. One file holds up to {{v:mcp.ai-file-max-kb}} KB, the whole folder up to {{v:mcp.ai-folder-max-mb}} MB. These are plain text files: you can read, edit or delete them yourself

> [!warning] Warning
> The `ai` folder is not part of the level's history. `Ctrl+Z` does not undo what the AI wrote there

**The folder travels with the level by default**: in an exported archive and in a Steam Workshop upload. To keep it at home, clear `{{ui:settings_level-settings_metadata-level-ai-share}}` on the `{{ui:settings_level-settings_metadata}}` tab of the level settings. The checkbox appears once the folder exists. It is saved to a file at once, so `Ctrl+Z` does not revert it either

An export mode with a password never carries the folder, whatever the checkbox says. More - [[13_export-and-protection#Export level]]

A copy of the level on this device takes the folder along, since a copy is not sharing

## Settings

All of them are in `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}` and are kept on this device only:
- `{{ui:settings_game-editor_mcp-enabled}}` - whether a client can connect at all. Off by default
- `{{ui:settings_game-editor_mcp-port}}` - the port the editor listens on. `0` picks a free one on every start
- `{{ui:settings_game-editor_mcp-follow-ai}}` - on: after a capture the playhead stays on the frame the AI looked at, paused
- `{{ui:settings_game-editor_mcp-reveal-edits}}` - after each AI edit, selects and pings what it created or changed
- `{{ui:settings_game-editor_mcp-operation-delay}}` - how long the editor waits between two AI operations, so you can follow them. `0` applies each at once

Every setting and its default - [[14_editor-settings#AI agent]]

Next: [[4_not-losing-work]], [[13_export-and-protection]]
