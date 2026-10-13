---
title: Images, temps et durée d'un niveau
date: 2026-10-12
tags: [level_author]
---

# Images, temps et durée d'un niveau

Un niveau compte le temps dans ses propres images, pas dans les images de l'écran, il se joue donc pareil sur n'importe quel matériel. Tu fixes la durée du niveau, et mieux vaut laisser les fps à la valeur par défaut, 60

## Images du niveau et images de l'écran

Une image du niveau n'a rien à voir avec une image de l'écran.
L'écran dessine autant d'images par seconde que le matériel le permet. Un niveau compte le temps dans ses propres images, et leur nombre par seconde est stocké dans le niveau lui-même. La valeur par défaut est `60`

Le niveau se joue donc pareil à 60 Hz, à 144 Hz et sur un téléphone tombé à 30. La précision des impacts ne dépend pas de la carte graphique

Une image est une cellule, pas un instant. Si un objet se termine à l'image 100 et qu'un autre commence à l'image 100, ils ne se chevauchent pas

Plus précisément : les images comptent à partir de 1, et l'image f couvre le temps de (f-1)/fps à f/fps, bord gauche inclus, bord droit exclu. L'image 1 commence donc tout au début du morceau

## La durée d'un niveau

Tu fixes la durée du niveau. Celle du morceau vient du fichier. Elles n'ont pas à correspondre

Le contenu après la fin du niveau est autorisé. Il n'est simplement jamais joué, et la validation ne s'en plaint pas. Un objet peut dépasser la fin, mais l'assistant IA ne peut pas en créer un qui commence après elle

Un enfant qui dépasse de l'intervalle de son parent fonctionne de la même façon. Le niveau garde ce que tu as écrit, et la durée de vie effective est calculée à part

Pour ajuster les durées de vie des enfants et des parents les unes aux autres, utilise le modificateur `{{ui:mod_span_fit}}` dans `{{ui:editor_generators_text}}`. Il ramène les enfants à l'intérieur ou élargit les parents

## Les fps du niveau

Plus les fps sont élevés, plus tu tombes précisément sur la pulsation. Et plus la même durée prend d'images.
La plage va de 1 à 1000, la valeur par défaut est `60`

> [!tip] Recommandation
> Laisse les fps à la valeur par défaut. À 60, l'oreille ne distingue pas un décalage d'une image, et le nombre d'images clés augmente avec les fps

La timeline est plafonnée à `1000000` images. Cela fait environ 4,6 heures à 60 fps et environ 17 minutes à 1000

> [!warning] Avertissement
> Changer les fps d'un niveau terminé, c'est recalculer chaque image clé. Le modificateur `{{ui:mod_framerate_remap}}` s'en charge, le faire à la main n'est pas réaliste

Ensuite : [[5_keyframes-and-easing]], [[2_rhythm-and-structure]], [[1_order-of-work]]
