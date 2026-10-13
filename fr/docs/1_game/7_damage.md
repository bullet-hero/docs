---
title: Dégâts et vies
date: 2026-10-02
tags: [advanced_player]
---

# Dégâts et vies

Chaque coup coûte une vie, repousse l'avatar pendant {{v:avatar.knockback-time}} s et donne {{v:avatar.damage-timeout}} s d'invulnérabilité. Par défaut, une mort ramène le niveau au dernier checkpoint et restaure tes vies

## Un coup en trois temps

1. **La poussée, `{{v:avatar.knockback-time}}` s.** Le coup te repousse loin de sa source à `{{v:avatar.knockback-speed}}` unités par seconde. Cela fait environ {{v:avatar.knockback-distance}} unités, un dash entier, trois quarts de la hauteur de l'écran par défaut. Les entrées ne sont pas acceptées pendant ce temps. Tu ne peux pas sortir de la poussée en dash : le recul passe avant tout
2. **Le contrôle revient** après ces {{v:avatar.knockback-time}} s
3. **Aucun coup ne t'atteint** pendant toute la `{{v:avatar.damage-timeout}}` s qui suit le coup. Chaque coup dans cette seconde est ignoré

Si tu te trouves exactement sur la source du coup, il n'y a nulle part où pousser. Alors il n'y a pas de recul du tout

Aucun coup ne t'atteint non plus pendant l'apparition (`{{v:avatar.spawn-time}}` s) et pendant les `{{v:avatar.dash-invulnerability}}` s de protection du dash, [[6_avatar]]

> [!info] Bon à savoir
> Rester dans une zone dangereuse coûte une vie, pas dix. Une poussée dans une deuxième zone dangereuse se survit aussi. Une salve dense ressemble à une mort instantanée, mais coûte souvent moins qu'une seule balle qui arrive juste à la fin de la seconde de protection

## Vies

Le nombre de vies se choisit sur l'écran du niveau : `{{ui:menu_levelview_options-lifes_option-zen}}`, `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}` ou `{{ui:menu_levelview_options-lifes_option-custom}}` jusqu'à 16, [[2_playing-levels]]

Chaque coup coûte une vie. Un coup qui prend la dernière est une mort.
`{{ui:menu_levelview_options-lifes_option-zen}}` réagit aux coups comme n'importe quelle autre partie - la poussée, l'anneau de bouclier, l'éclat de particules et la seconde de protection fonctionnent comme d'habitude, et le coup compte dans les statistiques - mais aucune vie n'est jamais dépensée, donc la partie ne finit jamais

Tes vies sont affichées par l'anneau de points autour de l'avatar : un point allumé est une vie en réserve, un point éteint est dépensé.
La fenêtre de résultat montre `{{ui:game_game-result_hits}}` et `{{ui:game_game-result_lives-left}}`

## Ce que fait une mort

Par défaut, une mort ne termine pas la partie :

1. L'horloge du niveau s'arrête en douceur en `{{v:checkpoint.rewind-time}}` s de temps réel. La musique ralentit avec elle
2. Le niveau revient au dernier checkpoint atteint. Les vies sont restaurées
3. L'horloge réaccélère en douceur jusqu'à la vitesse de la partie en `{{v:checkpoint.rewind-time}}` s de plus. Aucun coup ne t'atteint pendant l'accélération, sinon un checkpoint à côté d'un endroit dangereux prendrait toutes tes vies dans la première seconde

La pause arrête aussi cette accélération

Si `Checkpoints` est désactivé sur l'écran du niveau, le retour se fait au début du niveau

Pour qu'une mort ouvre la fenêtre de résultat, active `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`. La lecture s'arrête alors.
Depuis cette fenêtre, `{{ui:game_game-result_restart-checkpoint}}` lance une nouvelle tentative depuis le checkpoint atteint

## Checkpoints

Les checkpoints sont placés par l'auteur du niveau. C'est toi qui décides s'ils comptent, avec l'interrupteur `Checkpoints`

Le checkpoint atteint est le dernier situé à la position actuelle dans le niveau ou avant. Y revenir n'annule donc rien, cela rembobine simplement

L'auteur peut faire qu'un checkpoint restaure la santé. Le franchir restaure alors tes vies une fois, en pleine partie

La barre de progression en bas de l'écran a un repère à chaque checkpoint. La barre s'active dans `{{ui:settings_interface_label}}` → `{{ui:settings_interface_show-game-progress}}`

Les records avec et sans checkpoints sont gardés séparément, [[10_statistics]]

## Sans collision

`{{ui:menu_levelview_options-no-collision_title}}` est un interrupteur distinct de `{{ui:menu_levelview_options-lifes_option-zen}}`, à côté de `Checkpoints` sur l'écran du niveau et dans le panneau de lancement de l'éditeur. Active-le et l'avatar traverse tout : plus rien ne peut le toucher

Une partie `{{ui:menu_levelview_options-no-collision_title}}` garde ses propres records, séparés de `{{ui:menu_levelview_options-lifes_option-zen}}` et des parties normales, et la fenêtre de résultat la signale en ajoutant `· Sans collision` à la valeur de `{{ui:menu_levelview_options-lifes_title}}`, [[10_statistics]]
