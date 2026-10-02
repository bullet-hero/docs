---
title: Sandbox and tutorial
date: 2026-10-02
tags: [player]
---

# Sandbox and tutorial

The sandbox is an arena in the main menu where you can move the avatar, fire any of the six attacks at yourself and take the six-step tutorial. No level is needed for it

On the first launch the game offers the tutorial once: `{{ui:menu_tutorial-offer_confirm}}` opens the sandbox on the tutorial, `{{ui:menu_tutorial-offer_cancel}}` closes the offer for good. The sandbox itself stays in the menu either way

## The panel

The sandbox has one panel on the left. Click its handle to collapse the panel, or drag the handle to make the panel wider or narrower. The panel has five tabs:

| Tab | What it does |
|---|---|
| `{{ui:sandbox_tab_home}}` | what the sandbox is and what each tab does |
| `{{ui:sandbox_tab_tutorial}}` | the tutorial steps and what to do right now |
| `{{ui:sandbox_tab_controls}}` | the mode of the device you are steering with right now, the motion sensor switch and a way to all the control settings |
| `{{ui:sandbox_tab_attacks}}` | fires any of the six attacks by hand or lets waves come on their own |
| `{{ui:sandbox_tab_game}}` | lives, attack speed, the bot and the free camera |

`{{ui:settings_common_title}}` opens the game settings on top of the sandbox. `{{ui:sandbox_panel_exit}}` returns to the main menu

## Pause

The pause button is in the top right corner of the screen. `Esc` also opens the pause instead of leaving the sandbox. The pause stops everything, as in a level: the avatar, the attacks and the tutorial. The pause window has `{{ui:root_error_continue}}`, `{{ui:settings_common_title}}` and `{{ui:game_game-result_back-to-menu}}`

## Tutorial

Six steps, in order:

1. `{{ui:sandbox_tutorial_move_title}}` - travel about the width of the screen
2. `{{ui:sandbox_tutorial_dash_title}}` - dash three times
3. `{{ui:sandbox_tutorial_dodge_title}}` - last 10 seconds under slowed volleys without a hit. A hit starts the count again
4. `{{ui:sandbox_tutorial_dash-through_title}}` - the ring grows past the edges of the screen, so the only way out is a dash through its edge. You need to pass two rings - a failed ring does not cancel one already passed. Nothing hits you during a dash
5. `{{ui:sandbox_tutorial_choose-mode_title}}` - try the modes on the `{{ui:sandbox_tab_controls}}` tab and press `{{ui:sandbox_tutorial_confirm-mode}}`
6. `{{ui:sandbox_tutorial_done_title}}` - `{{ui:sandbox_tutorial_play-level}}` starts the tutorial level

While a step is played on the arena, the panel collapses and the step is shown as a small card at the top of the screen. Touches pass through the card. The handle still opens the panel. On the `{{ui:sandbox_tutorial_choose-mode_title}}` and `{{ui:sandbox_tutorial_done_title}}` steps the panel opens by itself, on the `{{ui:sandbox_tab_tutorial}}` tab

A hit or a death restarts only the step it happened on, not the whole tutorial, and the step turns red until it is passed. Passed steps are green

Clicking a step in the list starts that step, including one already passed. After a step is passed, the tutorial moves on to the next unpassed one. The tutorial counts as completed only when every step is passed - that is also when it is written to statistics. `{{ui:sandbox_tutorial_restart}}` on the same tab restarts it at any moment

> [!warning] Warning
> With `{{ui:sandbox_game_immortal}}` on the `{{ui:sandbox_tab_game}}` tab, hits are not counted at all, so the `{{ui:sandbox_tutorial_dodge_title}}` and `{{ui:sandbox_tutorial_dash-through_title}}` steps do not see them either. Keep a few lives while you take the tutorial

## Controls

Modes change for the device that is steering right now, and are saved at once. The motion sensor has no `{{ui:enum_control-mode_relative}}` mode. What each mode means - [[3_controls#Control modes]]

## Attacks and game

- `{{ui:sandbox_attacks_auto}}` fires random waves with a `{{ui:sandbox_attacks_gap}}` gap, like the main menu background
- `{{ui:sandbox_attacks_clear}}` removes all attacks from the screen
- `{{ui:sandbox_game_speed}}` slows down or speeds up only the attacks. The avatar always moves at its own speed
- Lives: `{{ui:sandbox_game_immortal}}`, 1, 3 or 5. When they run out, they come back, the sandbox does not end
- `{{ui:sandbox_game_bot}}` hands the avatar to the same bot that plays in the main menu background
- `{{ui:sandbox_game_free-camera}}` lets you look past the edges of the screen: move the view with the middle mouse button or two fingers, zoom with the wheel or a pinch. The blue frame shows what the level camera sees, and `{{ui:sandbox_camera_back}}` returns the view to it. Controls, dash and attacks work the same as without it
- A death plays out as in a level: the attacks slow down and vanish, the avatar appears in the center with full lives
