---
title: "Réutiliser : prefabs, copie, générateurs"
date: 2026-10-02
tags: [level_author]
---

# Réutiliser : prefabs, copie, générateurs

Des objets qu'il faudra plus tard changer tous ensemble forment un prefab, quel que soit leur nombre. Un contenu qui se décrit par une règle forme un générateur. Dans tous les autres cas, copie simplement

Un générateur vaut le coup même pour huit objets : une exécution de générateur est une seule opération à annuler.
Huit objets placés à la main, ce sont huit occasions de rater l'un d'eux

## La copie

Pour une forme qu'il faut répéter quelques fois et qui n'a plus besoin d'être liée à l'original

Il y a cinq tampons de presse-papiers, un par timeline. Des clips copiés sur une timeline ne se collent pas par-dessus des images clés sur une autre

La copie et le collage ne suivent pas le même chemin :
- **Un collage** va toujours dans la timeline que tu regardes
- **Une copie** prend ce qui est sélectionné. La timeline ouverte l'emporte si elle a sa propre sélection. Sinon, la sélection est copiée là où elle se trouve, donc un objet sélectionné pendant que la timeline locale est ouverte est quand même copié

Dupliquer (`Ctrl+D`) n'écrit dans aucun tampon. Ce que tu as copié avant n'est pas perdu

Dupliquer et coller traitent le parent différemment :
- **Une duplication** garde le parent. La copie se place à côté de l'original dans la hiérarchie
- **Un collage** abandonne le parent, et les objets collés se retrouvent au niveau supérieur. L'exception est un parent `{{ui:editor_search-option_camera}}` ou `{{ui:editor_search-option_local-player}}` : dans la portée du niveau, il survit au collage

Les deux cherchent un calque libre uniquement sur les images où tombe chaque objet copié. Un collage sur une portion vide de la timeline garde les calques qu'avaient les objets

Le nom d'une copie est renuméroté. Une fin faite de `_` et de chiffres est l'id de l'objet, donc `Shape_12` devient `Shape_` avec un nouvel id. Un nom sans une telle fin n'en reçoit pas, et une fin qui n'est pas faite que de chiffres (`Wave_2b`) reste telle quelle. Les pistes audio sont renommées de la même façon

Les objets copiés en mode prefab se collent dans le modèle, pas dans le niveau

> [!caution] Attention
> Les tampons sont vidés au chargement d'un niveau. Tous les ids et toutes les images qu'ils contiennent appartiennent au niveau qui était ouvert

## Les prefabs

Pour ce dont tu as besoin de nombreuses fois et que tu veux changer partout d'un coup

Un prefab, c'est un modèle et ses placements. Quand tu donnes un modèle à un placement, le placement reçoit de vraies copies de ses objets avec des ids permanents. Le fichier du niveau ne stocke que le placement lui-même : le modèle, les ids des copies et tes remplacements. Les copies sont reconstruites à partir du modèle à chaque chargement du niveau

Une modification du modèle se propage à chaque placement qui y renvoie.
Une modification d'une copie dans un placement (hors édition du modèle) est enregistrée comme un remplacement de cette seule instance.
Les remplacements survivent aux modifications ultérieures du modèle. C'est pourquoi un prefab sert aussi aux variantes, pas seulement aux clones

Les prefabs peuvent s'imbriquer les uns dans les autres. Un modèle imbriqué peut se modifier depuis l'intérieur d'un autre : les modèles s'ouvrent les uns par-dessus les autres et se ferment dans l'ordre inverse

### Un prefab à partir d'une sélection

Sélectionne des objets et appuie sur `Ctrl+G` (`{{ui:cmd_editor_pack-prefab}}`). La même action se trouve aussi :
- dans la palette de commandes
- dans le menu contextuel de la vue, tant que quelque chose est sélectionné
- dans le menu d'une ligne de la hiérarchie, sous le nom `{{ui:editor_context-menu_pack-prefab}}`
- dans les paramètres du niveau, onglet `{{ui:editor_library_kind-prefabs}}`, `{{ui:settings_level-settings_resources-prefabs-pack}}`

Les objets sélectionnés passent dans un nouveau modèle, un placement de ce modèle prend leur place, et ce placement est sélectionné. C'est une seule opération à annuler.
Un seul objet donne son nom au modèle. Plusieurs objets donnent un modèle nommé `Prefab`

Un placement et un objet qui lui appartient ne peuvent pas être empaquetés à nouveau. Leurs menus proposent `{{ui:editor_context-menu_open-prefab}}` à la place, et leur modèle s'ouvre.
En mode prefab, l'empaquetage n'est pas disponible

## Générateurs et modificateurs

**Les générateurs** créent du contenu selon une règle : une spirale, une grille, une fractale, une vague, une pluie de balles, un éventail de rayons. Tu fixes une fenêtre d'images, un calque et une graine, et tu obtiens des objets. L'estimation du résultat est visible avant que tu appuies sur quoi que ce soit

**Les modificateurs** fonctionnent de la même façon, mais sur ce qui existe déjà : ils ajustent des intervalles, les écartent, quantifient des images clés, recalculent la fréquence d'images, suppriment le contenu d'une fenêtre

## Entre les niveaux : les bibliothèques de l'appareil

Tout ce qui précède fonctionne à l'intérieur d'un seul niveau. Seules les bibliothèques de l'appareil et les collections passent d'un niveau à l'autre

Les thèmes, les effets, les formes et les prefabs s'exportent depuis un niveau et s'importent dans un autre.
Les bibliothèques se trouvent à côté du dossier des niveaux, donc un niveau que tu envoies emporte sa propre copie

Une collection contient des ressources de l'un des sept types, textures, polices et audio compris, et voyage sous forme d'archive ou via le Steam Workshop. Plus - [[16_library-and-collections]]

Suite : [[3_speed-and-shortcuts|Vitesse et raccourcis]], [[4_level-folder-and-backups|Le dossier du niveau et les sauvegardes]]
