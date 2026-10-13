---
title: Appareils mobiles
date: 2026-10-02
tags: [level_author]
---

# Appareils mobiles

Sur un téléphone, un doigt couvre l'écran, et le système prend les bords. Garde l'essentiel loin des bords et teste le niveau sur un téléphone modeste : la semi-transparence plein écran l'épuise en premier

Les téléphones sont une cible au même titre que le PC.
Un niveau qui ne se joue que sur PC est à moitié fait

## Un doigt au lieu d'une souris

**Un doigt couvre l'écran.** Une souris est un point, un doigt est une tache sous laquelle on ne voit rien.
Ne construis pas de motif qui oblige à regarder exactement là où se trouve le joueur. Sur PC, ça marche, sur téléphone, c'est un angle mort

**Le contrôle est différent.** Sur PC, le curseur fixe la cible, et le personnage s'y dirige. Sur téléphone, la précision est plus faible, et un doigt a plus d'inertie.
Un passage qu'une souris franchit du premier coup devient une épreuve à part entière sur téléphone

**Rends un passage étroit court dans le temps,** pas étroit en largeur

## Bords et forme de l'écran

> [!caution] Attention
> Les bords appartiennent au système : l'encoche de la caméra, les coins arrondis, les gestes de navigation. L'interface du jeu évite la zone non sûre, le contenu du niveau non. Garde l'essentiel loin des bords, surtout du bord supérieur

**Format d'écran.** Un téléphone fait environ 20:9, nettement plus étroit et plus long que l'écran sur lequel tu travailles.
Au moins une fois, regarde le niveau dans le simulateur d'appareil avec ce format avant de le considérer comme fini

> [!caution] Attention
> Le simulateur d'appareil montre les proportions et les encoches, mais ne dit rien des performances. Un essai sur un vrai appareil modeste vaut plus que tous les raisonnements

## Ce qui épuise un téléphone en premier

Dans l'ordre :
1. La semi-transparence plein écran sur plusieurs couches
2. Le post-traitement, Bloom avant tout. Son coût augmente avec la résolution, pas avec le nombre d'objets
3. Les grandes textures. Une texture de 4096 prend 64 Mo de mémoire avant que quoi que ce soit soit dessiné. Un quart seulement si les paramètres du joueur la compressent
4. Les effets avec beaucoup de particules
5. Et seulement ensuite le nombre de formes

## Antialiasing

L'antialiasing est un paramètre du joueur, pas du niveau.
Mais il explique pourquoi le même niveau se comporte différemment sur deux téléphones semblables :
- `{{ui:enum_anti-aliasing-type_msaa}}` est calculé par échantillon. Son coût augmente avec l'overdraw semi-transparent, exactement là où un téléphone modeste peine déjà
- `{{ui:enum_anti-aliasing-type_fxaa}}` est une seule passe sur l'écran, son coût ne dépend de rien

Ensuite : [[4_composition-and-camera|Composition et caméra]], [[1_level-budget|Budget du niveau]]
