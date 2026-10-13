---
title: Bac à sable et tutoriel
date: 2026-10-02
tags: [player]
---

# Bac à sable et tutoriel

Le bac à sable est une arène du menu principal où tu peux déplacer l'avatar, lancer sur toi n'importe laquelle des six attaques et suivre le tutoriel en six étapes. Il n'a besoin d'aucun niveau

Au premier lancement, le jeu propose le tutoriel une fois : `{{ui:menu_tutorial-offer_confirm}}` ouvre le bac à sable sur le tutoriel, `{{ui:menu_tutorial-offer_cancel}}` ferme la proposition pour de bon. Le bac à sable lui-même reste dans le menu dans tous les cas

## Le panneau

Le bac à sable a un seul panneau à gauche. Clique sur sa poignée pour replier le panneau, ou fais glisser la poignée pour élargir ou rétrécir le panneau. Le panneau a cinq onglets :

| Onglet | Ce qu'il fait |
|---|---|
| `{{ui:sandbox_tab_home}}` | ce qu'est le bac à sable et ce que fait chaque onglet |
| `{{ui:sandbox_tab_tutorial}}` | les étapes du tutoriel et ce qu'il faut faire en ce moment |
| `{{ui:sandbox_tab_controls}}` | le mode de l'appareil avec lequel tu diriges en ce moment, l'interrupteur du capteur de mouvement et un accès à tous les paramètres des contrôles |
| `{{ui:sandbox_tab_attacks}}` | lance à la main n'importe laquelle des six attaques ou laisse les vagues venir d'elles-mêmes |
| `{{ui:sandbox_tab_game}}` | les vies, la vitesse des attaques, le bot et la caméra libre |

`{{ui:settings_common_title}}` ouvre les paramètres du jeu par-dessus le bac à sable. `{{ui:sandbox_panel_exit}}` revient au menu principal

## Pause

Le bouton de pause est dans le coin supérieur droit de l'écran. `Esc` ouvre aussi la pause au lieu de quitter le bac à sable. La pause arrête tout, comme dans un niveau : l'avatar, les attaques et le tutoriel. La fenêtre de pause propose `{{ui:root_error_continue}}`, `{{ui:settings_common_title}}` et `{{ui:game_game-result_back-to-menu}}`

## Tutoriel

Six étapes, dans l'ordre :

1. `{{ui:sandbox_tutorial_move_title}}` - parcourir à peu près la largeur de l'écran
2. `{{ui:sandbox_tutorial_dash_title}}` - faire trois dashs
3. `{{ui:sandbox_tutorial_dodge_title}}` - tenir 10 secondes sous des salves ralenties sans prendre de coup. Un coup relance le compte
4. `{{ui:sandbox_tutorial_dash-through_title}}` - l'anneau grandit au-delà des bords de l'écran, donc la seule sortie est un dash à travers son bord. Il faut passer deux anneaux - un anneau raté n'annule pas un anneau déjà passé. Rien ne te touche pendant un dash
5. `{{ui:sandbox_tutorial_choose-mode_title}}` - essayer les modes de l'onglet `{{ui:sandbox_tab_controls}}` et appuyer sur `{{ui:sandbox_tutorial_confirm-mode}}`
6. `{{ui:sandbox_tutorial_done_title}}` - `{{ui:sandbox_tutorial_play-level}}` lance le niveau du tutoriel

Pendant qu'une étape se joue dans l'arène, le panneau se replie et l'étape s'affiche sous forme de petite carte en haut de l'écran. Les touchers passent à travers la carte. La poignée ouvre toujours le panneau. Aux étapes `{{ui:sandbox_tutorial_choose-mode_title}}` et `{{ui:sandbox_tutorial_done_title}}`, le panneau s'ouvre de lui-même, sur l'onglet `{{ui:sandbox_tab_tutorial}}`

Un coup ou une mort ne relance que l'étape où ils sont arrivés, pas tout le tutoriel, et l'étape devient rouge jusqu'à ce qu'elle soit réussie. Les étapes réussies sont vertes

Cliquer sur une étape de la liste lance cette étape, y compris une étape déjà réussie. Après une étape réussie, le tutoriel passe à la suivante non réussie. Le tutoriel ne compte comme terminé que quand chaque étape est réussie - c'est aussi à ce moment qu'il est écrit dans les statistiques. `{{ui:sandbox_tutorial_restart}}` sur le même onglet le relance à tout moment

> [!warning] Avertissement
> Avec `{{ui:sandbox_game_immortal}}` dans l'onglet `{{ui:sandbox_tab_game}}`, les coups ne sont pas comptés du tout, donc les étapes `{{ui:sandbox_tutorial_dodge_title}}` et `{{ui:sandbox_tutorial_dash-through_title}}` ne les voient pas non plus. Garde quelques vies pendant le tutoriel

## Contrôles

Les modes changent pour l'appareil qui dirige en ce moment, et sont enregistrés tout de suite. Le capteur de mouvement n'a pas de mode `{{ui:enum_control-mode_relative}}`. Ce que veut dire chaque mode - [[3_controls#Modes de contrôle]]

## Attaques et jeu

- `{{ui:sandbox_attacks_auto}}` lance des vagues aléatoires avec un écart de `{{ui:sandbox_attacks_gap}}`, comme l'arrière-plan du menu principal
- `{{ui:sandbox_attacks_clear}}` retire toutes les attaques de l'écran
- `{{ui:sandbox_game_speed}}` ralentit ou accélère seulement les attaques. L'avatar se déplace toujours à sa propre vitesse
- Vies : `{{ui:sandbox_game_immortal}}`, 1, 3 ou 5. Quand elles sont épuisées, elles reviennent, le bac à sable ne s'arrête pas
- `{{ui:sandbox_game_bot}}` confie l'avatar au même bot qui joue dans l'arrière-plan du menu principal
- `{{ui:sandbox_game_free-camera}}` permet de regarder au-delà des bords de l'écran : déplace la vue avec le bouton du milieu de la souris ou deux doigts, zoome avec la molette ou en pinçant. Le cadre bleu montre ce que voit la caméra du niveau, et `{{ui:sandbox_camera_back}}` y ramène la vue. Les contrôles, le dash et les attaques fonctionnent comme sans elle
- Une mort se déroule comme dans un niveau : les attaques ralentissent et disparaissent, l'avatar apparaît au centre avec toutes ses vies
