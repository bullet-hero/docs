---
title: Panneaux
date: 2026-10-02
tags: [level_author]
---

# Panneaux

La hiérarchie, les inspecteurs et les timelines sont ancrés autour de la vue. Un clic sur la poignée au bord d'un panneau l'ouvre ou le ferme, un glissement change sa largeur

## Trois panneaux

La vue est au milieu, et trois panneaux sont ancrés autour d'elle :
- le panneau de gauche contient la hiérarchie
- le panneau de droite contient les inspecteurs
- le panneau du bas contient les timelines

Un onglet du panneau de droite qui n'a rien à montrer est masqué. Plus - [[5_object-properties]]

## Poignée du panneau

Chaque panneau a une poignée sur son bord :
- un clic ouvre ou ferme le panneau
- un glissement change sa taille. Un seul mouvement peut sortir un panneau fermé à n'importe quelle largeur

La flèche sur la poignée montre l'état du panneau. Sur un panneau fermé, elle pointe dans un sens, sur un panneau ouvert, elle est tournée d'un demi-tour, quelle que soit la largeur. Une flèche tournée seulement en partie veut dire qu'un glissement est en cours

Un clic ouvre le panneau avec une animation, tout comme les raccourcis : `Ctrl+Left`, `Ctrl+Right` et `Ctrl+Down`. Plus - [[3_speed-and-shortcuts]]

## Largeur

Un panneau est soit fermé, soit quelque part entre sa largeur la plus étroite et sa largeur la plus grande. La largeur la plus étroite est aussi la largeur habituelle : c'est la place dont le contenu du panneau a besoin

| Panneau | Plus étroite | Plus grande |
|---|---|---|
| gauche | 25 % de l'écran | 25 % de l'écran |
| droite | 40 % de l'écran | 50 % de l'écran |
| bas | 35 % de la hauteur de l'écran | 70 % de la hauteur de l'écran |

Le panneau de gauche ne fait que s'ouvrir et se fermer. Le reste de l'éditeur est disposé en fonction de sa largeur

Si tu relâches un glissement plus étroit que la largeur la plus étroite, le panneau va vers ce qui est le plus proche : la position fermée ou la largeur la plus étroite. Exactement à mi-chemin, il s'ouvre. Un seul mouvement ferme donc toujours un panneau

Un clic ouvre le panneau à la largeur où tu l'as laissé ouvert la dernière fois

> [!info] Bon à savoir
> Une largeur obtenue par glissement n'est pas enregistrée. Elle ne vit que dans la session actuelle, donc un panneau élargi ne le restera pas la prochaine fois

## Réduire et ouvrir tout seul

`{{ui:cmd_editor_toggle-minimize-panels}}` ferme tous les panneaux ouverts et ne laisse que la vue. Un nouvel appui rouvre les panneaux qui étaient ouverts. Si aucun ne l'était, les trois s'ouvrent

`{{ui:settings_game-editor_interface-auto-open-panel}}` (paramètres, onglet `{{ui:settings_game-editor_title}}`, `{{ui:settings_interface_label}}`) ouvre le panneau de droite de lui-même quand tu sélectionnes quelque chose. Désactivé par défaut
