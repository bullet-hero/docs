---
title: Lisibilité et équité
date: 2026-10-01
tags: [level_author]
---

# Lisibilité et équité

Le joueur doit comprendre ce qui l'a tué. Montre un danger avant qu'il ne devienne dangereux, laisse au moins 12 images pour réagir et fais ressortir le danger davantage que le décor

Il n'existe qu'un seul test d'équité : **en mourant, le joueur s'en prend-il à lui-même ou au niveau ?**
Tout ce qui est sur cette page pousse la réponse vers "à lui-même"

## Annoncer le danger

Un danger doit être visible avant de devenir dangereux

Une forme et un collider sont deux champs distincts d'un même objet.
Un avertissement est donc simple : un rayon avec une forme et sans collider brille et ne touche pas. Une demi-seconde plus tard, un deuxième apparaît à côté, cette fois avec un collider

L'inverse est permis aussi : un mur invisible est un objet sans forme mais avec un vrai collider

> [!caution] Attention
> Un danger invisible n'est équitable que dans un seul cas : le joueur sait déjà qu'il est là, parce que le niveau l'a montré plus tôt

## Temps de réaction

Une personne remarque un danger et réagit en 0,2-0,25 seconde environ, au mieux.
À 60 images de niveau par seconde, cela fait 12-15 images

Un danger qui apparaît moins de 12 images avant le contact (10, par exemple) ne peut pas être passé du premier coup. On ne peut que l'apprendre.
Quand c'est acceptable - [[3_difficulty-curve#Mémorisation]]

## Contraste

Ce qui est dangereux doit se détacher du fond davantage que le décor.
L'échec le plus fréquent est un projectile sombre sur un fond sombre, précisément au moment où le fond change lui aussi

> [!tip] Recommandation
> Prends les couleurs du fond et du projectile dans le thème. Une seule modification du thème garde alors le contraste partout. Les couleurs saisies à la main ne le gardent que jusqu'à la première modification

## Un danger, un aspect

Chaque type de danger a besoin de son propre aspect reconnaissable, et de son propre son si tu utilises le son. Une fois que le joueur a appris que telle chose touche, tout ce qui lui ressemble doit toucher aussi

Ne contredis pas tes propres signaux. Si quelque chose qui ressemble à du décor tue à un endroit, le joueur cesse de faire confiance à tout ce qui ressemble à du décor

## La structure l'emporte sur la densité

Un écran plein de mouvement se lit comme du bruit, pas comme de la difficulté.
Un joueur ne distingue pas 40 projectiles. Il distingue un mur avec un trou, une vague, une spirale, un couloir

Huit objets structurés sont plus difficiles et plus équitables que quarante sans structure

## Un niveau se joue toujours de la même façon

Un niveau n'a ni conditions, ni compteurs, ni déclencheurs qui réagissent au joueur. Tout est écrit sur la timeline.
L'aléatoire ne change pas non plus : le même endroit donne les mêmes nombres sur n'importe quel appareil

Un niveau ne peut donc pas être rendu réactif. Mais il ne peut pas non plus devenir injuste par accident, seulement exprès

Entre deux parties, seul change ce que le joueur choisit : les vies, la vitesse de lecture et les checkpoints.
Plus - [[3_difficulty-curve#Ce que le joueur choisit]]

À lire ensuite : [[3_difficulty-curve|Difficulté et courbe]], [[5_color-and-postprocessing|Couleur, thèmes et post-traitement]]
