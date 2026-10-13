---
title: Composition et caméra
date: 2026-10-02
tags: [level_author]
---

# Composition et caméra

Garde le contenu important loin du bord : d'autres écrans placent le bord ailleurs, et l'encoche d'un téléphone peut cacher un projectile. Le tremblement de caméra marche sur une mesure, une rotation rapide et un zoom brusque donnent la nausée

## Chaque écran est différent

Le niveau est construit sur un moniteur 16:9. Sur un téléphone 20:9, il montre plus en largeur et moins en hauteur, sur une tablette 4:3, c'est l'inverse.
Un objet qui était posé pile sur le bord se retrouve soit bien à l'intérieur du cadre, soit en dehors

**La piste `{{ui:editor_events-timeline_track_screen-limit}}`** définit comment la zone visible est limitée :
- pas du tout
- un rapport d'aspect fixe
- une plage de rapports d'aspect

Le rapport fixe est le plus prévisible. Tout le monde voit exactement ce que tu as vu, mais les autres écrans ont des bandes sur les bords.
Choisis en connaissance de cause. "Pas du tout" est aussi un choix, et cela veut dire que tu ne sais pas ce que le joueur verra.
Un nouveau niveau vide ou un niveau créé à partir d'un fichier audio commence déjà avec une clé 16:9 fixe sur la première image, sauf si tu décoches `Pin Screen Aspect` à la création

> [!caution] Attention
> L'interface du jeu sort de la zone non sûre de l'écran, le contenu du niveau non. La caméra cadre le niveau par rapport à l'écran entier, donc l'encoche d'un téléphone peut cacher un projectile. Garde le contenu important loin du bord

## La caméra est un outil

La caméra n'est pas un décor de fond. Elle a des pistes d'images clés : `{{ui:editor_dummy_text-15}}`, `{{ui:editor_dummy_text-16}}`, `{{ui:editor_dummy_text-17}}`, `{{ui:editor_dummy_text-18}}`, `{{ui:editor_dummy_text-19}}`

Une rotation de 15 degrés rend un motif simple difficile sans un seul nouvel objet.
Elle casse toutes les directions auxquelles le joueur s'était habitué

Ce pouvoir joue aussi contre toi. La caméra peut rendre un niveau infranchissable, et tu ne le remarqueras pas, parce que tu sais où regarder

> [!warning] Avertissement
> Une rotation rapide, un tremblement constant et un zoom brusque rendent un niveau physiquement impossible à terminer. Pas par la difficulté, mais par ce que ressent le joueur. Le tremblement marche sur une mesure au moment d'un drop et devient insupportable sur une minute

## Calques

L'ordre de dessin est relatif : le calque d'un objet s'additionne aux calques de tous ses parents.
Si tu fais glisser un objet sous un autre parent, ce qui se dessine par-dessus quoi change. Même si le numéro de calque n'a jamais été touché

Garde le décor et le danger dans des plages de calques différentes. Le décor ne cachera alors pas un projectile par accident

## La lisibilité l'emporte sur la beauté

Un joueur qui n'a pas vu un projectile à cause du décor, c'est ton erreur, pas la sienne.
Quand il faut choisir, coupe le décor

À lire ensuite : [[2_mobile-devices|Appareils mobiles]], [[1_readability-and-fairness|Lisibilité et équité]]
