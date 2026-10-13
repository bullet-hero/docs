---
title: Comment fonctionne l'éditeur
date: 2026-10-12
tags: [level_author]
---

# Comment fonctionne l'éditeur

Objet, image, intervalle, calque, parent, image clé - les six idées sur lesquelles repose tout l'éditeur

Une fois ces six idées claires, le reste de l'éditeur se comprend tout seul :

| Idée | En bref |
|---|---|
| Objet | une forme (ce que tu vois) et un collider (ce qui touche), deux champs séparés |
| Image | une cellule de temps, pas un instant |
| Intervalle | la durée de vie d'un objet : un début et une durée, la fin exclue |
| Calque | l'ordre de dessin, additionné aux calques de tous les parents |
| Parent | transmet sa transformation, son état actif et sa durée de vie à ses enfants |
| Image clé | la valeur d'un champ sur une image, le jeu fait passer la valeur d'une image clé à l'autre tout seul |

Un mot inconnu - [[1_glossary]]

## Objet

Un objet, c'est ce qui est dessiné et ce qui touche. Ce sont deux champs différents : une forme (ce que tu vois) et un collider (ce qui touche).
Un rayon qui brille mais ne te touche jamais est un objet avec une forme et sans collider. Un mur invisible, c'est l'inverse

## Image et intervalle

Une image est une cellule de temps, pas un instant. L'image 30 occupe une durée, pas un point.
La timeline compte à partir de un. Un niveau de 900 images contient les images 1 à 900. Le nombre 901 est la limite de fin, pas une image

Un intervalle est la durée de vie d'un objet : un début et une durée. La fin ne fait pas partie de l'intervalle.
Deux objets placés bout à bout ne se chevauchent donc pas sur une image commune

Plus - [[4_frames-and-time]]

## Calque et parent

Un calque est un ordre de dessin. Il est relatif : le calque d'un objet s'additionne aux calques de tous ses parents

Un calque plus élevé se dessine devant. De deux formes sur le même calque résultant, la plus récente (l'id le plus élevé) se dessine derrière. La forme qui doit être au-dessus reçoit donc un calque plus élevé

> [!caution] Attention
> Glisser un objet sous un autre parent change son ordre de dessin, même si tu n'as jamais touché au nombre

Un parent transmet sa transformation, son état actif et sa durée de vie à ses enfants.
L'intervalle d'un enfant doit se trouver à l'intérieur de l'intervalle de son parent

L'éditeur ne coupe jamais ce que tu as écrit. Il garde ta valeur et calcule la valeur effective à part.
C'est pourquoi rétrécir un parent est réversible : élargis-le de nouveau et l'enfant revient

## Image clé

Une image clé est la valeur d'un champ sur une image. Le jeu fait passer la valeur d'une image clé à l'autre tout seul.
Chaque champ a son propre jeu d'images clés : position, rotation, échelle, taille, ancres et pivot

> [!info] Bon à savoir
> Un champ sans image clé n'est pas cassé, il prend la valeur par défaut. Inutile de tout animer par souci d'ordre

Ce que stocke une image clé et comment la valeur passe d'une image clé à l'autre - [[5_keyframes-and-easing]]

## Coordonnées

Les positions, tailles et distances sont en unités du monde. Le point (0, 0) est le centre de l'écran tant que la caméra n'a pas d'images clés à elle. X augmente vers la droite, y vers le haut

Le zoom de la caméra est la hauteur de la zone visible en unités, {{v:camera.default-height}} par défaut. Un écran 16:9 montre donc x d'environ -{{v:camera.default-half-width}} à {{v:camera.default-half-width}} et y de -{{v:camera.default-half-height}} à {{v:camera.default-half-height}}. Un écran plus large ou plus étroit ne change que la largeur

Une image clé de position est relative au parent. C'est le décalage du pivot de l'objet par rapport au point d'ancrage du parent, et elle tourne et change d'échelle avec le parent. Un objet sans parent est placé en coordonnées du monde. Un enfant de la caméra bouge avec la caméra

- **pivot** - le point du rectangle propre de l'objet que la position place et autour duquel agissent la rotation et l'échelle. `(0.5, 0.5)`, le centre, par défaut
- **ancres** - le point du rectangle du parent à partir duquel la position est comptée, de `(0, 0)` (en bas à gauche) à `(1, 1)` (en haut à droite). Le centre par défaut. Deux ancres différentes étirent l'enfant avec le parent

La rotation se fait dans le sens inverse des aiguilles d'une montre. Le fichier la stocke en radians, et l'assistant IA écrit aussi des radians. L'inspecteur affiche des degrés par défaut, le paramètre d'éditeur `{{ui:settings_game-editor_interface-rotation-unit}}` passe aux radians

Ensuite : [[4_frames-and-time]], [[5_keyframes-and-easing]], [[1_readability-and-fairness]]
