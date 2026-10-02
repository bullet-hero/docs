---
title: Damage and lives
date: 2026-10-02
tags: [advanced_player]
---

# Damage and lives

Every hit costs one life, knocks the avatar back for {{v:avatar.knockback-time}} s and gives {{v:avatar.damage-timeout}} s of invulnerability. By default a death rewinds the level to the last checkpoint and restores your lives

## A hit in three stages

1. **The push, `{{v:avatar.knockback-time}}` s.** You are knocked away from whatever hit you at `{{v:avatar.knockback-speed}}` units per second. That is about {{v:avatar.knockback-distance}} units, a whole dash, three quarters of the default screen height. Input is not accepted during it. You cannot dash out of the push: knockback overrides everything
2. **Control returns** after those {{v:avatar.knockback-time}} s
3. **You cannot be hit** for a whole `{{v:avatar.damage-timeout}}` s from the moment of the hit. Every hit inside that second is ignored

If you stand exactly on what hit you, there is nowhere to push. Then you are not knocked back at all

You also cannot be hit while appearing (`{{v:avatar.spawn-time}}` s) and during the `{{v:avatar.dash-invulnerability}}` s of dash protection, [[6_avatar]]

> [!info] Worth knowing
> Sitting inside a danger zone costs one life, not ten. A push into a second danger zone is survivable too. A dense volley looks like instant death, but often costs less than a single bullet that arrives right at the end of the protection second

## Lives

The number of lives is chosen on the level screen: `{{ui:menu_levelview_options-lifes_option-zen}}`, `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}` or `{{ui:menu_levelview_options-lifes_option-custom}}` up to 16, [[2_playing-levels]]

Every hit costs one life. A hit that takes the last one is a death.
`{{ui:menu_levelview_options-lifes_option-zen}}` reacts to hits like any other run - the push, the shield ring, the particle burst and the second of protection work as usual, and the hit counts in the statistics - but a life is never spent, so the run never ends

Your lives are shown by the ring of dots around the avatar: a lit dot is a life in reserve, an unlit one is spent.
The result window shows `{{ui:game_game-result_hits}}` and `{{ui:game_game-result_lives-left}}`

## What a death does

By default a death does not end the run:

1. The level clock smoothly stops over `{{v:checkpoint.rewind-time}}` s of real time. The music sags along with it
2. The level jumps back to the last checkpoint reached. Lives are restored
3. The clock smoothly speeds back up to run speed over another `{{v:checkpoint.rewind-time}}` s. You cannot be hit during the speed-up, otherwise a checkpoint next to a dangerous spot would take all your lives in the first second

Pause stops this speed-up too

If `Checkpoints` is turned off on the level screen, the rewind goes to the start of the level

To have a death open the result window, turn on `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`. Playback then stops.
From that window `{{ui:game_game-result_restart-checkpoint}}` starts a new attempt from the checkpoint reached

## Checkpoints

Checkpoints are placed by the level author. Whether they count is up to you, with the `Checkpoints` toggle

The checkpoint reached is the last one at or before the current position in the level. So going back to it undoes nothing, it just rewinds

The author can make a checkpoint restore health. Then crossing it restores your lives once, right in the middle of the run

The progress bar at the bottom of the screen has a tick at every checkpoint. The bar is turned on in `{{ui:settings_interface_label}}` → `{{ui:settings_interface_show-game-progress}}`

Records with and without checkpoints are kept separately, [[10_statistics]]

## No collision

`{{ui:menu_levelview_options-no-collision_title}}` is a toggle separate from `{{ui:menu_levelview_options-lifes_option-zen}}`, next to `Checkpoints` on the level screen and in the editor's launch panel. Turn it on and the avatar passes through everything: nothing can touch it anymore

A `{{ui:menu_levelview_options-no-collision_title}}` run keeps its own records, separate from `{{ui:menu_levelview_options-lifes_option-zen}}` and from normal runs, and the result window marks it by adding `· No collision` to the `{{ui:menu_levelview_options-lifes_title}}` value, [[10_statistics]]
