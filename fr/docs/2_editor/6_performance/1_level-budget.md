---
title: Budget du niveau
date: 2026-10-01
tags: [level_author]
---

# Budget du niveau

Un téléphone tient confortablement environ 1000 formes dans une image, un PC modeste 5000-10000. L'overdraw coûte plus cher que le nombre : des choses semi-transparentes sur tout l'écran, couche sur couche

## Combien de formes un appareil supporte

Ce qui compte, ce sont les **formes** vivantes en même temps dans une image. Les chiffres sont approximatifs, mais l'ordre de grandeur est juste

| Appareil | Confortable | Limite du jouable |
|---|---|---|
| Téléphone | 1000 | 2000 |
| PC modeste | 5000-10000 | 20000-40000 |
| PC moyen (selon l'enquête Steam) | 50000 | 100000 |

Teste sur l'appareil le plus faible auquel tu as accès.
Sur ton propre PC, tout ira bien, et ça ne veut rien dire

## Texte et effets

Le texte et les effets se comptent aussi en formes

**Texte :** de 2 à 100 formes par objet texte. Le coût dépend de la complexité de la police, du nombre de caractères, du nombre de styles et du fait que le texte soit animé ou non

**Effet :** 10 formes pour l'objet lui-même plus 0,1 forme par particule. Un effet de mille particules fait environ 110 formes

## Overdraw

**Ce qui coûte cher, ce n'est pas le nombre mais l'overdraw.** C'est quand le même pixel est repeint encore et encore

Ce qui en découle :
- un seul remplissage semi-transparent sur tout l'écran coûte plus cher qu'une centaine de projectiles
- des couches de décor semi-transparent empilées sont la chose la plus coûteuse qu'on puisse construire
- si le niveau rame, cherche ce qui couvre tout l'écran au lieu de compter les objets

> [!info] Bon à savoir
> Sur une puce mobile moyenne, une scène de 1000 objets avec un recouvrement de 60-70x passe 95-97 % du temps GPU à colorier des pixels. Mille petites formes partout sur l'écran coûtent moins cher que dix formes semi-transparentes plein écran empilées

## Opaque et semi-transparent

Une forme a le choix entre trois chemins de rendu : `Auto`, `Opaque`, `Transparent`.
Le chemin opaque est moins cher : le GPU écarte à l'avance les pixels recouverts

`Auto` décide tout seul, une fois au chargement. Sa condition stricte : ne jamais changer l'apparence du niveau.
Tout ce dont l'opacité ne peut pas être prouvée devient semi-transparent

> [!warning] Avertissement
> Ne règle le chemin à la main que si tu sais exactement ce que tu fais. Un objet déclaré opaque qui ne l'est pas ne sera pas plus rapide, il s'affichera mal

## Indication de capacité

À l'enregistrement, le niveau note combien d'objets son image la plus lourde a demandés.
C'est une indication pour le chargeur, pas une limite. Un générateur la recalcule

Ensuite : [[2_mobile-devices|Appareils mobiles]], [[3_images-and-fonts|Textures et polices]]
