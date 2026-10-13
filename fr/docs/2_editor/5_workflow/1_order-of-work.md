---
title: L'ordre de travail
date: 2026-10-12
tags: [level_author]
---

# L'ordre de travail

D'abord le morceau, les fps, la grille de pulsations et les marqueurs, puis un squelette en formes nues et son playtest. La décoration, le thème et les effets viennent en dernier

Les étapes vont de la plus coûteuse à la moins coûteuse.
Plus une étape arrive tôt, plus elle coûte cher à refaire une fois que tout repose dessus

## Les fondations

1. **Le morceau final.** Converti, normalisé, coupé. Tout le reste se mesure à partir de lui. Remplacer le morceau plus tard décale chaque image du niveau
2. **Les FPS et la durée du niveau.** Les deux peuvent changer, mais ce sont les fps qui coûtent cher : après un changement, toutes les images clés sont recalculées. La valeur par défaut est `60`, et il n'y a en général aucune raison de la changer
3. **La grille de pulsations.** Segments, tempo, décalage, signature rythmique. Tant que la grille est fausse, rien ne s'aimante correctement aux pulsations. Tout ce qui est placé avant elle devra être déplacé plus tard
4. **Des marqueurs sur la structure.** Intro, couplet, refrain, break, drop, outro. C'est dix minutes de travail, et les marqueurs sont visibles sur toutes les timelines

## Le squelette et son playtest

5. **Le squelette.** Les motifs principaux en formes nues. Pas de décoration, pas de thème, pas d'effets
6. **Le playtest du squelette.** Avant la décoration : une fois une section décorée, tu n'auras plus envie de la supprimer

> [!caution] Attention
> Le squelette est l'étape où le niveau est vraiment conçu. Et c'est l'étape qu'on saute le plus souvent. Un squelette qui n'est pas amusant à jouer ne le deviendra pas grâce à la décoration. Il deviendra un niveau décoré qui n'est pas amusant à jouer

## Le remplissage

7. **Le contenu.** Étoffe les motifs et ajoute les objets qui n'étaient jusque-là que suggérés
8. **Les thèmes et la couleur.** Dès le début, définis les couleurs comme des renvois au thème, pas comme des valeurs fixes
9. **Les effets et le post-traitement.** En dernier. Ce sont les plus faciles à pousser trop loin, et ils sont difficiles à juger tant que le niveau change encore
10. **Les métadonnées.** Nom, description, auteurs, classification par âge. Remplis la fiche d'une ressource dès que tu l'ajoutes, pas à cette étape

## Trois habitudes qui économisent du travail

C'est vrai que tu construises le niveau toi-même ou que l'assistant IA le fasse :
- **Tout ce qui se répète est un prefab.** Modifie le modèle une fois et chaque copie suit - [[2_reuse]]
- **Un contour qu'aucune forme intégrée ne donne est une forme du niveau**, dessinée dans l'éditeur de formes ou donnée par l'IA sous forme de polygone. Elle se dessine et touche comme un seul objet, contrairement à une pile de rectangles
- **Utilise tout le cadre 16:9.** Une grande marge vide, c'est de l'écran que le joueur voit et que le niveau gaspille. Garde le danger loin du bord même, la décoration peut l'atteindre - [[4_composition-and-camera]]

## Ce qui coûte peu et ce qui coûte cher à changer

**Peu coûteux à changer à la fin :** les couleurs via le thème, la décoration, le post-traitement, la description du niveau

**Coûteux :** les fps, le morceau, la grille de pulsations et la hiérarchie

> [!warning] Avertissement
> Changer le parent d'un objet change à la fois sa transformation, sa durée de vie et son ordre de dessin. C'est pourquoi restructurer un niveau terminé demande rarement une seule modification

Enregistre à chaque étape. Ce que couvrent l'enregistrement automatique et l'annulation - [[4_not-losing-work]]

Suite : [[2_reuse|Réutiliser : prefabs, copie, générateurs]], [[4_not-losing-work|Ne pas perdre son travail]]
