---
title: Skins
date: 2026-10-15
tags: [player, advanced_player]
---

# Skins

Le corps de l'avatar est une grille de cases, et une skin décide ce que dessine chaque case : une forme et une des couleurs de la skin. Une skin peut aussi éteindre les yeux, les mains, l'ombre et les effets. Compose-en une dans le menu principal, sous `{{ui:menu_main_avatar-btn}}`, à partir de formes prêtes, d'une palette et d'un éditeur de grille, ou écris le fichier à la main

Une skin ne change que l'apparence. La hitbox, la vitesse et l'anneau de hitbox restent les mêmes pour toutes les skins

## Le hub de l'avatar

`{{ui:menu_main_avatar-btn}}` dans le menu principal ouvre un écran à part. Ton avatar marche à gauche et le panneau occupe la moitié droite. `{{ui:menu_avatar_bot}}` en bas à gauche te passe l'avatar, pour essayer la skin en mouvement, et le curseur `{{ui:menu_avatar_damage}}` à côté montre comment la skin perd des cases quand la santé baisse. La barre en haut du panneau saute à chaque section :

| Section | Ce qu'elle fait |
|---|---|
| `{{ui:menu_avatar_tab-shapes}}` | des formes prêtes, dessinées avec les yeux et les mains qui vont avec. Un clic pose la forme sur ta skin et garde tes couleurs. Les formes rondes et polygonales ont des yeux, les formes à motifs n'en ont pas. La première carte est l'avatar classique : il se porte en entier, couleurs comprises |
| `{{ui:menu_avatar_tab-colors}}` | les couleurs du corps et les yeux. Choisis une cible, puis une couleur. Les mains, les traînées et la teinte du dash suivent tes couleurs d'elles-mêmes |
| `{{ui:menu_avatar_elements}}` | chaque bouton active ou désactive une partie de l'avatar |
| `{{ui:menu_avatar_editor}}` | la grille elle-même : sa taille, les pièces de ses cases, la forme, la couleur, la rotation, le miroir et l'échelle de chaque pièce, et tes propres formes |

`{{ui:menu_avatar_randomize}}` en haut à droite donne à ta skin une forme et des couleurs au hasard. Il est désactivé tant que tu portes l'avatar classique. `{{ui:menu_avatar_tab-skins}}`, juste à côté, liste tes fichiers de skin : un clic sur l'un d'eux te le fait porter, et les boutons exportent, suppriment, importent et dupliquent. `{{ui:menu_avatar_create}}` crée une nouvelle skin à partir d'une forme au hasard, dans des couleurs au hasard. Un fichier que le jeu ne sait pas lire peut quand même être supprimé depuis là

Chaque changement est enregistré tout de suite. Le premier changement sur l'avatar classique crée un nouveau fichier de skin, et tu portes ce fichier à partir de là

### L'éditeur

1. `{{ui:menu_avatar_paint}}` pose la pièce sélectionnée dans une case, `{{ui:menu_avatar_erase}}` la vide. Glisse sur la grille pour traiter plusieurs cases d'un coup
2. `{{ui:menu_avatar_pieces}}` liste ce que les cases peuvent dessiner. `+` copie la pièce sélectionnée, `-` la retire et ses cases prennent la première pièce
3. La pièce sélectionnée prend une forme intégrée ou une des formes propres à la skin. `{{ui:menu_avatar_new-mesh}}` en dessine une nouvelle : place des points, puis relie-en trois en un triangle
4. `{{ui:menu_avatar_columns}}` et `{{ui:menu_avatar_rows}}` redimensionnent la grille. Les cases sont carrées, donc une grille plus haute que large donne un corps haut
5. `{{ui:menu_avatar_rotate-left}}` et `{{ui:menu_avatar_rotate-right}}` font tourner toute la skin d'un quart de tour : la grille et chaque pièce avec elle

Le haut d'une skin est son avant : l'avatar se tourne pour pointer là où il se déplace

Un changement qui casse le corps - trop peu de cases, ou des cases en deux morceaux - n'est pas enregistré. La raison s'affiche sous la grille jusqu'à ce que tu la corriges

## Où sont rangées les skins

Dans le dossier `skins` du dossier de données ([[1_installation]]). Une skin est un fichier `.json`. `selection.json` à côté retient quelle skin tu portes

- sur ordinateur, `{{ui:menu_avatar_open-folder}}` ouvre le dossier
- sur téléphone, utilise `{{ui:menu_avatar_import}}` et `{{ui:menu_avatar_export}}` : ils ouvrent le sélecteur de fichiers du système

Les skins voyagent avec le transfert de profil et avec Steam Cloud - [[14_profile-transfer]]

## Le fichier

Voici une skin exportée, abrégée :

```json
{"g":3,"v":{
  "id":"9b2f0d64-1c3a-4e8b-8f21-6a0c5d7e9f13",
  "name":"Hex knight",
  "size":1.0,
  "columns":5,"rows":5,
  "mask":60651675406,
  "cells":[0,0,0,0,1,1,1,0,0,1,2,1,0,0,1,1,1,0,0,0,0],
  "parts":[
    {"shape":"00000000-0000-0000-0000-000000016000","color":0},
    {"shape":"00000000-0000-0000-0000-000000001000","color":1,"scale":0.9},
    {"shape":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","color":2,"rotation":90.0,"mirror":true}
  ],
  "colors":[[0,{"r":0.51,"g":0.76,"b":0.96,"a":1.0}],[0,{"r":0.2,"g":0.4,"b":0.9,"a":1.0}],[0,{"r":1.0,"g":1.0,"b":1.0,"a":1.0}]],
  "meshes":[{"id":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","vts":[[0,{"x":-0.5,"y":-0.5}],[0,{"x":0.5,"y":-0.5}],[0,{"x":0.0,"y":0.5}]],"idxs":[0,1,2]}],
  "elements":125
}}
```

`g` est la génération du format de fichier, `v` contient la skin. Le plus simple est d'exporter une skin et de modifier la copie

| Clé | Ce que c'est |
|---|---|
| `id` | qui est la skin : un GUID qui lui est propre. Le jeu nomme le fichier d'après lui, mais trouve une skin par cette clé, donc le nom du fichier n'a pas d'importance |
| `name` | le nom affiché dans la liste |
| `size` | la taille à laquelle le corps est dessiné, de `{{v:skin.size-min}}` à `{{v:skin.size-max}}` du classique. La hitbox ne change pas |
| `columns`, `rows` | la largeur et la hauteur de la grille, de `{{v:skin.grid-min}}` à `{{v:skin.grid-max}}`. Les cases sont carrées : le côté le plus long couvre tout le corps |
| `mask` | quelles cases sont remplies, sous la forme d'un seul nombre de 64 bits : la case de la colonne `x` et de la rangée `y` est le bit `y * 8 + x`, rangée 0 en bas. Une rangée fait toujours 8 bits de large, quoi que dise `columns` |
| `cells` | la pièce que dessine chaque case remplie, un index dans `parts`, dans l'ordre des bits à partir du plus bas. Laissé vide, chaque case dessine la pièce 0 |
| `parts` | ce que dessine une case : `shape` (l'id d'une forme intégrée, ou l'`id` d'un des `meshes` de la skin), `color` (un index dans `colors`), `rotation` (degrés), `mirror` et `scale` (de `{{v:skin.part-scale-min}}` à `{{v:skin.part-scale-max}}` de la case) |
| `colors` | les couleurs du corps, de 1 à `{{v:skin.colors-max}}`. Une couleur s'écrit `[0,{"r":…,"g":…,"b":…,"a":…}]`, chaque canal de 0 à 1 |
| `meshes` | jusqu'à `{{v:skin.meshes-max}}` formes propres à la skin : un `id` (n'importe quel GUID qui n'est pas celui d'une forme intégrée), des points `vts` dans la boîte de -0.5 à 0.5 et des triangles `idxs` de trois points chacun |
| `elements` | quelles parties de l'avatar sont dessinées, sous la forme d'une somme : yeux 1, mains 2, ombre 4, traînée 8, traînée du dash 16, éclat d'impact 32, teinte du dash 64. 127 dessine tout, une nouvelle skin commence à 125 : tout sauf les mains. La grille est toujours dessinée |
| `eyes`, `hands`, `shadow`, `move_effect`, `dash_effect`, `damage_effect`, `dash_body` | les couleurs du reste de l'avatar, sous la même forme que `colors`. Une partie éteinte dans `elements` garde sa couleur |

Une clé omise garde la valeur de l'avatar classique. Le plus simple est de copier l'id d'une forme intégrée depuis une skin exportée : les préréglages à motifs sous `{{ui:menu_avatar_tab-shapes}}` n'utilisent que des formes intégrées. Un fichier écrit à la main peut omettre `id` - `{{ui:menu_avatar_import}}` lui en donne un

## Ce qu'une skin doit respecter

- `columns` et `rows` vont de `{{v:skin.grid-min}}` à `{{v:skin.grid-max}}`, et `mask` ne remplit aucune case en dehors
- au moins `{{v:skin.filled-min}}` cases sont remplies, et toutes se touchent par un côté : le corps est d'un seul tenant
- `cells` est vide ou contient exactement une pièce pour chaque case remplie
- au plus `{{v:skin.parts-max}}` pièces, et la forme et la couleur de chaque pièce existent
- le corps et l'ombre sont dessinés avec une opacité d'au moins `{{v:skin.body-alpha-min}}`

Une skin qui enfreint une règle apparaît grisée dans `{{ui:menu_avatar_tab-skins}}` avec la raison, et ne peut pas être portée. Un second fichier avec le même `id` aussi. Si la skin portée se casse, l'avatar classique est dessiné et ton choix est conservé. Une skin écrite par une version plus récente du jeu affiche `{{ui:menu_avatar_newer}}`

## Santé

La santé n'est montrée que par les cases remplies. Les cases perdues restent comme des fantômes sombres, du bord vers le centre, et la dernière case tient tant qu'il reste un peu de santé. Moins il y a de cases remplies, plus chacune vaut de santé - [[7_damage]]
