---
title: Images clés et lissage
date: 2026-10-12
tags: [level_author]
---

# Images clés et lissage

Une image clé est une valeur sur une image d'une piste, plus le lissage avec lequel elle est atteinte. Tout ce qui, dans un niveau, bouge, change de couleur ou s'allume et s'éteint est une liste d'images clés

Les idées de base - [[3_how-the-editor-thinks]]. Chaque champ de l'inspecteur d'images clés - [[5_object-properties]]

## Ce qui peut être animé

Chaque piste a ses propres images clés, indépendantes des autres :

| Propriétaire | Pistes |
|---|---|
| n'importe quel objet | position, rotation, échelle, taille, ancres, pivot |
| forme | couleur, UV |
| texte | couleur, taille de police, `{{ui:editor_dummy_text-11}}` (quelle part du texte est écrite), `{{ui:editor_dummy_text-12}}` (quelle part est cachée derrière le masque) |
| caméra | position, rotation, zoom, pivot, tremblement |
| niveau | arrière-plan, thème, limite de l'écran, chacun des 12 effets de post-traitement |
| joueur | taille, vitesse, visibilité, contrôle, collision |

L'image clé de couleur d'une forme peut aussi être un dégradé sur le rectangle de l'objet. Son champ `{{ui:editor_keyframe-color_layout}}` choisit la disposition : `{{ui:enum_color4-x4-key-type_value}}` (une couleur), `{{ui:enum_color4-x4-key-type_vertical}}` (de bas en haut), `{{ui:enum_color4-x4-key-type_horizontal}}` (de gauche à droite) ou `{{ui:enum_color4-x4-key-type_bari-centrical}}` (une couleur à chaque coin)

Une image clé de taille de police est soit un seul nombre, une taille fixe en unités du monde, soit une plage avec `{{ui:field_common_auto-size}}` activé. Le texte est dessiné au `{{ui:field_common_max}}` de la plage et rétrécit vers son `{{ui:field_common_min}}` jusqu'à tenir dans son rectangle

Les images clés d'un objet sont comptées depuis le début de son intervalle. Déplacer l'objet dans le temps emporte donc toute son animation

La position est définie par rapport au parent. Une image clé stocke la valeur elle-même, pas un écart par rapport à l'image clé précédente

La visibilité, le contrôle et la collision du joueur sont soit activés, soit désactivés. Ces images clés n'ont pas de lissage : il n'y a rien à mélanger

La première image clé sur une piste de joueur vide ne change rien à l'écran : visibilité, contrôle et collision démarrent activés, taille et vitesse démarrent aux valeurs habituelles du joueur. Avec le contrôle désactivé, ou le joueur masqué, le joueur ne peut pas être dirigé : le curseur disparaît et un appui n'est pas pris en compte. Un joueur masqué est quand même touché : seule la collision en décide

## Texte : remplissage et apparition

Deux pistes de texte cachent les caractères de façons différentes. Les deux prennent une part de 0 à 1 et comptent les caractères du texte

**`{{ui:editor_dummy_text-11}}`** est la part du texte qui est écrite : 0 - rien, 1 - tout. Un caractère non écrit n'est pas dessiné du tout, la ligne raccourcit donc. Une piste vide écrit tout le texte. Chaque image clé fixe la direction :
- `{{ui:enum_text-fill-direction_forward}}` (par défaut) - depuis le premier caractère, comme une machine à écrire
- `{{ui:enum_text-fill-direction_backward}}` - depuis le dernier caractère
- `{{ui:enum_text-fill-direction_from-center}}` - grandit à partir du milieu
- `{{ui:enum_text-fill-direction_to-center}}` - grandit depuis les deux bouts et se rejoint au milieu

**`{{ui:editor_dummy_text-12}}`** est la part des caractères cachés derrière le masque : 0 - tous visibles, 1 - tous masqués. Un caractère caché garde sa place et est dessiné comme un caractère de masque, `{{v:text.appearing-mask-default}}` par défaut. Le masque est le champ `{{ui:editor_inspector-appearing_mask}}` de l'objet texte, et s'il contient plusieurs caractères, chaque caractère caché prend l'un d'eux. Une piste vide ne cache rien. Chaque image clé fixe le mode :
- `{{ui:enum_text-appearing-mode_random}}` (par défaut) - dispersés, mais avec la même dispersion à chaque partie. Un caractère caché à 0,3 l'est encore à 0,6, le texte se révèle donc au lieu de clignoter
- `{{ui:enum_text-appearing-mode_forward}}` - les caractères cachés sont à la fin, le texte apparaît depuis son début
- `{{ui:enum_text-appearing-mode_backward}}` - les caractères cachés sont au début

Pour faire taper une ligne, anime `{{ui:editor_dummy_text-11}}` de 0 à 1. Pour la décoder à partir du bruit, anime `{{ui:editor_dummy_text-12}}` de 1 à 0

## Conseils

- N'anime que ce qui bouge. Une piste sans image clé prend la valeur par défaut
- Pour un changement pile sur une pulsation, utilise `Constant`, par exemple un changement de thème sur le drop
- La rotation ne se ramène pas à un tour : une image clé à 0 degré et une autre à 720 font tourner l'objet deux fois. En radians, comme les écrivent le fichier et l'assistant IA, c'est 0 et 12,566

## Entre deux images clés

Avant la première image clé et après la dernière, la valeur reste fixe.
Entre deux images clés, le jeu prend la part du temps écoulé, la fait passer par le lissage et mélange les deux valeurs

La part est comptée en temps, pas en images dessinées. La courbe est donc la même à 30 et à 144 fps

**Le lissage appartient à la seconde image clé de la paire.** Le lissage d'une image clé définit le tronçon qui arrive sur elle depuis la précédente.
Le lissage de la première image clé d'une piste ne se voit donc jamais. Une nouvelle image clé reçoit `Linear`

Le champ `{{ui:hint_editor_inspector_ease_header}}` ouvre la fenêtre `{{ui:editor_search-title_ease}}`, où chaque lissage est dessiné sous forme de courbe.
Tu peux sélectionner plusieurs images clés, même sur des pistes différentes, et les modifier en une seule étape d'annulation

## 29 lissages

`Linear` est une ligne droite. `Constant` garde la valeur précédente et saute sur l'image clé

Les 27 autres forment neuf familles de trois : `In`, `Out` et `InOut`. Par exemple, `InSine`, `OutSine`, `InOutSine`

| Famille | Forme |
|---|---|
| `Sine` | la courbe la plus douce |
| `Quad`, `Cubic`, `Quart`, `Quint` | puissances 2, 3, 4 et 5 |
| `Expo` | exponentielle |
| `Circ` | un quart de cercle |
| `Back` | dépasse la plage et revient |
| `Elastic` | oscille autour de la valeur |

`In` démarre lentement et finit vite. `Out` démarre vite et se pose. `InOut` est lent aux deux bouts.
De `Sine` à `Expo`, chaque famille est plus marquée que la précédente

> [!caution] Attention
> `Back` et `Elastic` sortent de la plage : `Out` dépasse la cible, `In` recule au-delà du départ. Le collider bouge avec l'objet. Un projectile censé s'arrêter au bord d'une zone sûre y entre donc pendant quelques images

## Valeurs aléatoires

Une valeur dans une image clé n'est pas forcément un seul nombre :
- un nombre : `{{ui:field_common_value}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_float-type_random-min-max-step}}`
- un vecteur (position, échelle, etc.) : `{{ui:field_common_value}}`, `{{ui:enum_vector-type_random-rect}}`, `{{ui:enum_vector-type_random-rect-step}}`, `{{ui:enum_vector-type_random-circle}}`, `{{ui:enum_color-type_random-lerp}}`, `{{ui:enum_vector-type_random-lerp-step}}`
- une couleur : `{{ui:field_common_value}}`, `{{ui:editor_events-timeline_track_theme}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_color-type_random-lerp}}`

`{{ui:enum_vector-type_random-rect}}` tire chaque axe séparément. `{{ui:enum_color-type_random-lerp}}` tire un seul nombre pour tous les axes, le point tombe donc sur la ligne entre A et B.
Les formes avec un pas arrondissent le résultat vers le bas à un multiple du pas. Un pas de 0 désactive la grille, et la valeur se comporte comme la forme sans pas.
Ensuite, l'image clé est mélangée comme n'importe quelle autre

La même graine donne le même niveau. Le nombre aléatoire est calculé à partir de la graine, de l'image de l'image clé, du calque, de l'image de début de l'objet, de la piste et du canal. Plus - [[8_determinism]]

Ensuite : [[2_rhythm-and-structure|Rythme et structure]], [[6_themes|Thèmes]]
