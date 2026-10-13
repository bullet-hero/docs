---
title: Contrôles
date: 2026-10-02
tags: [player]
---

# Contrôles

Tu peux jouer à la souris, à l'écran tactile, à la manette ou au capteur de mouvement. À la souris, maintenir le bouton gauche dirige l'avatar, et Space, Shift ou le bouton droit déclenchent le dash

Les touches se réattribuent dans les paramètres des contrôles, les boutons de la manette non

Pour apprendre les contrôles pas à pas ou essayer chaque mode sans lancer de niveau - [[13_sandbox]]

## Appareils

Tous les contrôles se règlent dans `{{ui:settings_common_title}}` → `{{ui:settings_controls_title}}`, un groupe par appareil

| Appareil | Mode par défaut | Déplacement | Dash |
|---|---|---|---|
| `{{ui:enum_control-device_keyboard-mouse}}` | `{{ui:enum_control-mode_absolute}}` | maintenir le bouton gauche, l'avatar suit la souris | `Space`, `Shift`, le bouton droit de la souris ou un double clic (0,3 s) |
| `{{ui:enum_control-device_touchscreen}}` | `{{ui:enum_control-mode_relative}}` | glisser un doigt n'importe où sur l'écran | un deuxième doigt |
| `{{ui:enum_control-device_gamepad}}` | `{{ui:field_common_direction}}` | l'un ou l'autre stick | n'importe quel bouton sauf `Start` et `Select` |
| `{{ui:enum_control-device_device-gyro}}` | `{{ui:field_common_direction}}` | incliner l'appareil par rapport à l'horizontale, pleine vitesse à 20° | un appui n'importe où sur l'écran |

La souris seule suffit : le bouton gauche dirige l'avatar, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}` déclenche le dash. Le clavier est facultatif

Sur une manette, `Start` met en pause et reprend. Les boutons de la manette ne se réattribuent pas : en jeu, n'importe quel bouton sauf `Start` et `Select` déclenche le dash, y compris le bouton de face droit. Dans le menu de pause, le bouton de face droit sert de "retour", comme dans tout menu

## Modes de contrôle

| Mode | Ce que signifie ton entrée |
|---|---|
| `{{ui:enum_control-mode_absolute}}` | une position. Le curseur y saute, l'avatar le rattrape |
| `{{ui:enum_control-mode_relative}}` | un mouvement. Le curseur l'accumule, l'avatar rattrape le curseur |
| `{{ui:field_common_direction}}` | une direction. Il n'y a pas de curseur du tout |

Le déplacement est instantané dans tous les modes : ni accélération ni glissade

Dans les modes à curseur, l'avatar rattrape le curseur à sa propre vitesse de marche. Il reste donc en retard sur une souris rapide.
Un dash va vers le curseur. Si le curseur est proche, le dash est plus court et s'arrête pile dessus

Ce qui se passe quand tu relâches le bouton de direction ou lèves le doigt dépend d'une seule case à cocher - `{{ui:settings_controls-keyboard-mouse_km-cursor-return}}` pour la souris, `{{ui:settings_controls-touchscreen_touch-cursor-return}}` pour l'écran tactile :

- cochée - l'avatar s'arrête là où il est, le curseur revient sur lui. C'est le réglage par défaut de la souris
- décochée - le curseur reste là où tu l'as laissé, et l'avatar marche jusqu'à lui. Seuls les dégâts peuvent déplacer le curseur. C'est le réglage par défaut de l'écran tactile

En mode `{{ui:field_common_direction}}`, un stick poussé à mi-course donne la moitié de la vitesse. Un dash va toujours sur toute sa longueur

Sur un écran tactile en mode `{{ui:enum_control-mode_absolute}}`, le curseur se trouve au-dessus de ton doigt (`{{ui:settings_controls-touchscreen_touch-finger-offset-y}}`). Ainsi, le doigt ne cache pas l'avatar

Pendant qu'un doigt dirige l'avatar, un deuxième doigt déclenche le dash là où il se pose - sur un panneau ou sur un bouton aussi. L'interface ne reçoit pas ce toucher, donc un dash n'appuie jamais sur rien par accident

Les chiffres exacts - [[6_avatar]]

## Capteur de mouvement

Le capteur de mouvement n'a pas de calibrage. L'avatar reste immobile quand le téléphone est posé à plat, écran vers le haut

- penche le bord droit vers le bas, et l'avatar va à droite
- penche le bord du haut vers le bas, et il monte
- `{{ui:settings_controls-device_sensitivity}}` 1 donne la pleine vitesse à 20°. À 2, la moitié de l'inclinaison suffit

Le capteur suit l'écran : passe le téléphone en paysage et reviens, la droite reste la droite.
Le capteur a deux modes, `{{ui:enum_control-mode_absolute}}` et `{{ui:field_common_direction}}`

## Réattribution

- **Les commandes de jeu** sont dans `{{ui:settings_controls_title}}` : le mode, `{{ui:settings_controls-keyboard-mouse_dash-keys}}`, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}`, la sensibilité, la zone morte, le lissage du mouvement, l'inversion, le joystick et le bouton de dash à l'écran. `{{ui:settings_controls_reset}}` remet chaque appareil aux valeurs par défaut de cette plateforme
- **Les raccourcis** sont dans `{{ui:settings_keybindings_label}}`. Presque tous sont pour l'éditeur. Hors de l'éditeur, il y a `{{ui:settings_keybindings_window_toggle_fullscreen}}` (`F11` par défaut), `{{ui:settings_keybindings_window_settings_save}}` (`Ctrl+S` quand les paramètres sont ouverts) et les touches de navigation. `{{ui:settings_keybindings_reset}}` annule toutes les réattributions

Quand le jeu attend une touche, il affiche `Appuie sur une touche pour "..."`.
La règle est alors `{{ui:settings_escape-cancels_backspace}}`

Pour les touches, le jeu ne garde que ce que tu as réattribué. Si une attribution par défaut s'améliore plus tard, elle te parvient, sauf si tu as changé cette attribution toi-même. L'onglet `{{ui:settings_controls_title}}` est enregistré en entier, donc ses nouvelles valeurs par défaut ne te parviennent pas

Les raccourcis de l'éditeur - [[3_speed-and-shortcuts]]

## Plusieurs appareils à la fois

Un seul appareil dirige l'avatar - le dernier que tu as utilisé.
Le changement se fait tout seul, dans la même image, sans aucun menu

Le jeu interroge chaque appareil actif à chaque image. Une manette qu'on ne touche pas envoie des zéros, et cela ne compte pas comme une utilisation

À la première image, rien n'a encore été utilisé, donc la plateforme décide : la souris sur un ordinateur, l'écran tactile sur un téléphone

Le dash et la pause fonctionnent depuis n'importe quel appareil actif, quel que soit celui qui dirige. Un bouton de manette déclenche le dash pendant que la souris dirige. Un dash seul ne prend pas la main sur la direction

Un appareil ne peut diriger l'avatar que si :

- il est marqué comme actif
- la plateforme le prend en charge
- il est connecté en ce moment

`{{ui:settings_controls-active_now}}` en haut montre lequel dirige

> [!tip] Conseil
> Un schéma de contrôle semble ne rien faire ? En général, un autre appareil a été touché après lui. Regarde d'abord `{{ui:settings_controls-active_now}}`
