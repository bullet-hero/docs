---
title: Difficulté et courbe
date: 2026-10-02
tags: [level_author]
---

# Difficulté et courbe

Conçois en fonction des propres chiffres du joueur - ils sont tous sur [[6_avatar]] et [[7_damage]] - et d'une réaction humaine de 12-15 images. Montre d'abord un nouveau motif sous une forme sans risque

Tu ne peux pas juger ta propre difficulté : teste le niveau sur quelqu'un qui le découvre

## Le joueur en chiffres

Les valeurs exactes de l'avatar sont sur [[6_avatar]] et [[7_damage]]. Ce qu'elles signifient pour un niveau :

| Quoi | Ce que cela signifie pour la conception |
|---|---|
| Hitbox du joueur | bien plus petite que le corps dessiné, donc une balle qui frôle le corps rate souvent |
| Dash | traverse les trois quarts de la hauteur de l'écran presque instantanément |
| Invulnérabilité pendant un dash | dure plus longtemps que le dash lui-même, donc un dash à travers un obstacle fin est sans danger |
| Après un impact | un court recul sans contrôle, puis une fenêtre de grâce qui ignore les impacts suivants |
| Réaction humaine | 0,2-0,25 seconde, soit 12-15 images à 60 images par seconde |
| Valeurs au lancement | 3 vies, vitesse 1.0, checkpoints activés |

Règles empiriques qui en découlent :
- un passage d'une unité de large est large, un passage de 0,6 est serré
- un dash couvre autant de terrain qu'une demi-seconde de course

## Un impact ne tue pas tout de suite

Après un impact, le joueur est repoussé et perd brièvement le contrôle.
Les impacts suivants sont ignorés pendant un moment ([[7_damage]]). Un mur de dix projectiles d'affilée coûte une vie, pas dix

> [!info] Bon à savoir
> L'intuition dit le contraire. Une salve dense a l'air d'une mort instantanée. En réalité, elle coûte moins cher qu'un seul projectile qui arrive exactement quand l'invulnérabilité vient de se terminer

## Ce que le joueur choisit

Les vies, la vitesse de lecture et les checkpoints sont choisis par le joueur sur l'écran de lancement.
Par défaut : 3 vies, vitesse 1.0, checkpoints activés

Tu peux placer des checkpoints, mais tu ne peux obliger personne à les utiliser. Et tu ne peux pas interdire de jouer à demi-vitesse

Conçois en fonction des valeurs par défaut, mais ne construis rien sur le calcul "c'est ici qu'il meurt".
Tu conçois une sensation, pas une punition

## La boucle

Le joueur répète une seule boucle : jouer, mourir, réessayer. Un bon niveau construit ses couches par-dessus, et la boucle doit être :
- simple au début, sans mécaniques difficiles d'emblée
- extensible, pour que les nouveaux éléments arrivent progressivement et qu'elle ne s'essouffle pas
- gratifiante, parce qu'une récompense immédiate pour la bonne action entretient la motivation

## La courbe : enseigner, tester, varier

1. Montre le motif sous une forme sans risque, où une erreur est presque impossible
2. Exige-le pour de vrai
3. Change une variable - vitesse, direction, nombre - et exige-le de nouveau

Si un motif apparaît d'emblée sous sa forme difficile, c'est le niveau qui est mis en cause.
Le joueur meurt et ne comprend pas ce qu'on attendait de lui

L'équité a aussi une limite. Trop "tenir la main" retire le plaisir tout autant que l'injustice

## Mémorisation

Un niveau qui ne se passe que de mémoire est un genre légitime. Mais ce doit être une décision, pas un accident

La limite est simple : après la mort, le joueur doit comprendre ce qu'il doit retenir exactement.
Si c'est encore flou après la dixième mort, ce n'est pas de la mémorisation, c'est du bruit

## Tester avec les yeux d'un autre

Tu ne peux pas juger ton propre niveau toi-même.
Au moment de publier, tu as passé ton propre passage difficile deux cents fois, et pour toi il est facile

> [!tip] Recommandation
> Donne le niveau à quelqu'un qui le découvre et regarde en silence. Ne donne pas d'indices. Un endroit où une personne meurt trois fois et demande ce qu'on attendait d'elle n'est pas difficile, il est confus

## Commencer court

Fais un premier niveau de 1-2 minutes.
L'intérêt s'épuise avant le morceau. Un niveau de quatre minutes, c'est quatre fois plus de travail et dix fois plus de raisons d'arrêter

À lire ensuite : [[1_readability-and-fairness|Lisibilité et équité]], [[4_composition-and-camera|Composition et caméra]]
