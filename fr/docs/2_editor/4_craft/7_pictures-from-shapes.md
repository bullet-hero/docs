---
title: Des images à partir de formes
date: 2026-10-13
tags: [level_author]
---

# Des images à partir de formes

Construis d'abord une illustration à partir des formes intégrées et ne dessine les tiennes que là où aucune ne convient. Pose la lumière et l'ombre sur une seule forme de base, fais de chaque élément répété un prefab, et compare le résultat avec l'illustration d'origine posée sur le niveau

## Les formes intégrées d'abord

Une forme intégrée est une vraie géométrie aux bords nets, et la réutiliser ne coûte rien.
Un cercle et un carré s'étirent à n'importe quelle taille : un carré étiré et tourné est n'importe quelle barre, ligne ou baguette, un cercle étiré est une ellipse

Ne dessine ta propre forme dans l'éditeur de formes que là où aucune forme intégrée ne convient : un manteau, une main, une voile.
Ne lui donne que ses vrais coins, avec des bords droits entre eux. Une douzaine de coins se lit mieux qu'une centaine tracés le long de chaque pixel

> [!tip] Recommandation
> Le détail est le prix des bords nets. Un contour déchiqueté ou une jointure visible gâche une illustration plus qu'une encoche perdue

## Une base, les détails par-dessus

La lumière et l'ombre sont des formes séparées posées sur une seule forme de base, découpées le long de son bord.
Deux formes qui se touchent seulement bord à bord laissent entre elles une fine jointure de fond, et elle se voit

Une partie recouverte par une autre se prolonge en dessous. Un cou passe un peu sous le manteau et la tête, une jambe sous l'ourlet.
Les parties se rejoignent alors encore quand l'une d'elles bouge

## Les répétitions sont des prefabs

Tout ce qui apparaît plus d'une fois est un prefab : un œil, une fenêtre, un pétale.
Construis-en un, fais-en un prefab, place les autres, et ne change sur chaque copie que ce qui diffère : sa position, sa taille, ses couleurs. Chacun de ces changements est un remplacement de cette copie

Une seule modification du modèle atteint alors chaque copie, et le niveau reste léger

## Calques

Donne à chaque objet son propre calque. Deux objets sur un même calque au même moment se dessinent dans un ordre que tu n'as pas choisi.
Garde la base sous ses détails et les détails sous ce qui se trouve par-dessus

## Comparer avec l'original

Importe l'illustration d'origine comme texture et pose-la sur un rectangle exactement de sa taille, par-dessus tout le reste.
Pour comparer, active le rectangle. Désactive-le pour le reste du travail au lieu de le rendre transparent : un objet désactivé ne dessine rien du tout

Vérifie l'illustration dans son ensemble, puis en zoomant, partie par partie : les bords, les jonctions entre les parties, les nuances

À lire ensuite : [[2_reuse]], [[4_composition-and-camera]]
