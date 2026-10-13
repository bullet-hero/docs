---
title: Modificateurs
date: 2026-10-12
tags: [level_author]
---

# Modificateurs

Un modificateur change ce qui est déjà dans le niveau : il retire du contenu, recalcule les fps, aplatit les prefabs, quantifie les images clés, ajuste et décale les intervalles. Un lancement s'annule en une seule étape

## Retirer du contenu

Retire le contenu du niveau qui correspond aux conditions données

> [!caution] Attention
> Le modificateur change ce qui existe au lieu d'ajouter. Tout ne peut être récupéré qu'avec une seule étape d'annulation. Lis les paramètres avant de le lancer

Il agit sur la fenêtre d'images de la fenêtre des générateurs. En mode inverse, il retire au contraire ce qui ne partage aucune image avec cette fenêtre. En mode inverse ou avec `{{ui:editor_generators-whole_level}}` activé, il peut retirer bien plus que ce qui est visible à l'écran, donc il demande d'abord une confirmation

Plus - [[2_reuse]]

## Changer la fréquence d'images

Recalcule chaque numéro d'image pour une autre fréquence d'images.
Les timings restent sur les mêmes secondes

> [!warning] Avertissement
> Les images sont des nombres entiers. Tout ce qui ne se divise pas exactement est arrondi. Après deux recalculs, le niveau peut donc ne pas revenir à l'original

Le formulaire montre la fréquence d'images actuelle du niveau pour référence, en lecture seule. Tout vrai changement de fréquence d'images demande d'abord une confirmation. Le modificateur a besoin du niveau entier, il est donc indisponible en mode prefab

Plus - [[4_frames-and-time]]

## Aplatir les prefabs

Transforme chaque placement de prefab de cette portée en objets ordinaires.
Le lien avec le modèle disparaît. Les objets restent exactement où ils étaient

> [!info] Bon à savoir
> Le niveau a le même aspect qu'avant le lancement : rien n'est supprimé ni déplacé. Les modifications des placements individuels sont déjà écrites dans les objets eux-mêmes et ne se perdent pas. Les modèles restent dans le niveau, sauf si tu demandes de les supprimer

## Quantifier les images clés

Ramène les images clés sur un pas régulier.
Ainsi, une animation à la main irrégulière tombe sur la pulsation

Agit sur la sélection, et ne se lance pas sans elle

La grille est prise à la première source qui s'applique :
1. `Use Beat Grid` est activé (par défaut) et le niveau a une grille de pulsations. Les lignes sont les pulsations de ses segments, chaque pulsation divisée en `Division` parties. Un modèle de prefab n'a pas de grille de pulsations
2. `Use Bpm` est activé (par défaut). Une ligne sur chaque pulsation de `Bpm` à la fréquence d'images du niveau, divisée en `Division` parties
3. `Use Bpm` est désactivé. Une ligne toutes les `Step Frames` images, à partir de l'image 1

Chaque ligne est placée à partir de son temps exact et seulement ensuite arrondie à une image. Ainsi, la grille reste sur la pulsation même là où une pulsation ne fait pas un nombre entier d'images : 167 BPM à 60 fps, c'est 21,56 images par pulsation

`Offset Frames` décale chaque ligne, `Mode` envoie une image clé située entre deux lignes vers la plus proche, la précédente ou la suivante, `Tracks` choisit quelles pistes sont aimantées. Les étiquettes du formulaire sont les noms des paramètres eux-mêmes et ne sont pas traduites

> [!warning] Avertissement
> Une image clé dont la ligne est déjà prise par une autre image clé de la même piste reste où elle était. Une quantification grossière laisse donc certaines images clés hors de la grille au lieu de les fusionner. Par ailleurs, une image clé n'est jamais déplacée avant le début de son objet

Plus - [[2_rhythm-and-structure]], la grille de pulsations - [[3_timelines#Grille de pulsations]]

## Ajuster les intervalles

Place les intervalles des enfants dans l'intervalle de leur parent.
Deux façons : rétrécir les enfants ou étirer les parents.
Les ancres ne changent dans aucune des deux

> [!info] Bon à savoir
> Un enfant qui dépasse son parent est une donnée valide. Il joue simplement coupé. Ajuster est une décision sur le contenu, pas la correction d'un bug, donc cela ne se lance jamais tout seul

Plus - [[4_frames-and-time]]

## Échelonner

Décale la sélection dans le temps.
Des objets qui commençaient ensemble apparaissent l'un après l'autre

Agit sur la sélection, et ne se lance pas sans elle

Plus - [[2_reuse]]
