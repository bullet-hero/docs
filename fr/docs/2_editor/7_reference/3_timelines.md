---
title: Timelines
date: 2026-10-02
tags: [level_author]
---

# Timelines

Les timelines montrent le niveau dans le temps : les objets, les images clés de l'objet sélectionné, le modèle d'un prefab, l'audio et les événements. La grille de pulsations aide à placer tout cela sur la musique

## Timeline du niveau

Montre chaque objet du niveau dans le temps. Chaque objet est un clip. La rangée où se trouve un clip est le **calque** de l'objet

Un clip est un **intervalle** semi-ouvert. Un objet sur les images 10-19 se termine exactement là où commence un objet qui démarre à l'image 20. Les deux ne dessinent jamais ensemble sur une image commune

> [!info] Bon à savoir
> L'intervalle d'un enfant doit se trouver dans celui de son parent. C'est **résolu à la lecture et jamais stocké**. Rétrécis le parent et les enfants sont coupés, mais leurs valeurs ne changent pas. Étire-le de nouveau et tout revient. Un objet racine au-delà de la fin du niveau est une donnée valide, il ne joue simplement pas

> [!tip] Conseil
> Quatre outils se trouvent dans la barre de boutons : `{{ui:editor_timeline-tool-selection_tooltip}}` sélectionne et déplace, `Edges` fait glisser un bord, `Scissors` coupe le clip sous le curseur, `Marquee` ajoute à la sélection chaque clip que touche le rectangle tracé. Le menu s'ouvre avec un clic droit sur un *espace vide*. Un appui sur un clip commence un glissement

Un placement de prefab et les objets qu'il apporte sont dessinés dans la couleur du prefab

Comment les outils traitent un placement :
- Sa durée vient du modèle par défaut. Une autre durée sur un placement est enregistrée comme un remplacement de ce seul placement
- Si tu fais glisser son bord de début avec `Edges`, l'endroit où il lit le modèle se déplace avec lui. Ainsi, l'image à l'intérieur reste où elle était
- `Scissors` le coupe en deux placements du même modèle, et chacun joue sa propre partie. Le modèle lui-même ne change pas
- Les objets qu'un placement a apportés ne peuvent pas être coupés. Coupe le placement lui-même, ou coupe ces objets en mode prefab

Plus : [[3_how-the-editor-thinks|Comment fonctionne l'éditeur]], [[4_composition-and-camera|Composition et caméra]]

## Timeline locale

Montre les images clés de l'**objet sélectionné**. Chaque propriété animable a sa propre piste : position, rotation, échelle, taille, ancres, pivot, couleur, UV, taille de police

Ici, les images se comptent **depuis le début de l'intervalle de l'objet**. Déplace l'objet et toute son animation se déplace avec lui

> [!info] Bon à savoir
> **Une piste vide est une donnée valide**, pas un trou. Une piste sans images clés prend la valeur par défaut. C'est pourquoi un nouvel objet n'anime rien tant que tu n'as pas placé d'image clé

Une valeur ne se mélange qu'entre des images clés voisines. L'intervalle décide quelles images existent, mais pas comment les valeurs se mélangent

Sur un objet issu d'un prefab, une piste qui correspond encore au modèle est dessinée dans la couleur du prefab. Ajoute, déplace ou modifie une image clé dessus et la couleur disparaît : la piste contient maintenant un remplacement

En mode prefab, avec la racine du modèle sélectionnée, cette timeline est aussi longue que tout le modèle

Plus : [[3_how-the-editor-thinks|Comment fonctionne l'éditeur]]

## Timeline du prefab

La timeline propre au mode prefab. Montre les objets du **modèle**

> [!info] Bon à savoir
> Sa durée est la durée propre du modèle, pas l'intervalle d'un de ses placements. Un modèle se modifie comme un petit niveau autonome. Il peut être placé de nombreuses fois et à des moments différents

Une rangée est la **racine** du modèle, et elle couvre toute la durée du modèle. Tous les autres objets du modèle en dépendent :
- la rangée racine peut être sélectionnée. L'inspecteur et la timeline locale montrent alors la racine
- elle ne peut être ni glissée, ni étirée, ni coupée
- elle se replie comme tout parent. Une racine repliée masque tout le modèle sur cette timeline

> [!warning] Avertissement
> La sélection n'est pas partagée avec le reste de l'éditeur. Il n'y a pas d'aperçu en direct d'un placement précis. Les modifications changent le modèle et se propagent à chaque placement qui y renvoie

Plus : [[2_reuse|Réutiliser : prefabs, copie, générateurs]]

## Timeline audio

Montre les pistes audio du niveau avec leur forme d'onde. Elle permet d'aligner facilement le contenu sur ce qu'on entend

> [!tip] Conseil
> `{{ui:editor_inspector-audio-span_fit}}` dans l'inspecteur ajuste la piste à la vraie durée du clip. Le bouton est indisponible s'il n'y a pas de clip ou si la vitesse est 0 : une piste figée n'a pas de durée
> `{{ui:editor_inspector-audio-span_fit-level}}` allonge aussi le niveau, jusqu'à ce que tout le clip tienne. Les deux boutons demandent d'abord une confirmation

> [!caution] Attention
> Le curseur `{{ui:editor_inspector-audio_volume}}` dans l'inspecteur est le fader de la piste. Le volume en images clés est une piste Volume distincte sur la timeline locale. À la lecture, les deux se multiplient

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Timeline des événements

Montre les images clés du niveau qui n'appartiennent à aucun objet :
- la position, la rotation, le zoom, le pivot et le tremblement de la caméra
- les marqueurs et les checkpoints
- la limite de l'écran
- l'arrière-plan et le thème
- chaque effet de post-traitement
- la visibilité, le contrôle, la collision, la taille et la vitesse du joueur

> [!info] Bon à savoir
> La piste **Pulsation** est ici l'exception. Ses éléments ont un intervalle, et c'est la seule piste sur laquelle agissent `Edges` et `Scissors`

> [!tip] Conseil
> Une couleur peut renvoyer au thème du niveau au lieu d'une valeur fixe. Changer le thème recolore alors d'un coup tout ce qui y renvoie

Plus : [[4_composition-and-camera|Composition et caméra]], [[6_themes]]

## Grille de pulsations

Aide à placer le contenu sur la musique. Les générateurs travaillent sur les mêmes pulsations que celles que tu vois

Ce sont des métadonnées de création, pas une mécanique. **La lecture ne lit pas la grille**

La grille est une liste de **segments**. Chacun a un tempo constant : BPM, décalage de phase, pulsations par mesure.
Les segments ne se chevauchent pas. Les trous entre eux sont nécessaires : une intro sans batterie, un break, la fin après le morceau. Une seule piste de tempo ne pourrait pas l'exprimer

> [!tip] Conseil
> `TAP` enregistre les appuis à la tête de lecture. `{{ui:editor_beat-tap_commit}}` les transforme en un segment, du premier appui au dernier. Les pulsations se comptent toujours depuis le début du segment et ne s'accumulent pas, donc l'erreur reste sous la moitié d'une image

Plus : [[2_rhythm-and-structure|Rythme et structure]]

## Segment de pulsation

Une partie à tempo constant : BPM, décalage de phase en images fractionnaires, pulsations par mesure, un nom et une couleur

Un seul segment est affiché, même si plusieurs sont sélectionnés. Chaque champ sauf le nom est propre à un segment. Les modifier ensemble les ferait se confondre

> [!caution] Attention
> Un segment est identifié par son image de début. Donc **le déplacer change son identité**. Après un déplacement, sélectionne de nouveau le segment à son nouveau début

> [!tip] Conseil
> Ici, les appuis recalent la phase du segment sélectionné au lieu d'en créer un nouveau. Le BPM et le décalage changent en une seule étape d'annulation

Plus : [[2_rhythm-and-structure|Rythme et structure]]
