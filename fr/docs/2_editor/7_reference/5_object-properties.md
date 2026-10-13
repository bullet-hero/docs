---
title: Propriétés de l'objet
date: 2026-10-12
tags: [level_author]
---

# Propriétés de l'objet

L'inspecteur d'objet modifie les champs de l'objet sélectionné, l'inspecteur d'images clés modifie les images clés sélectionnées, sur toutes les pistes que touche la sélection à la fois

## Inspecteur d'objet

Montre les champs de l'objet sélectionné. Chaque type a les champs communs d'un objet vide. Forme, Effet, Texte et Prefab ajoutent les leurs en dessous

`{{ui:field_common_active}}` désactive à la fois le rendu *et* la collision. Les enfants en héritent. Un objet masqué ici ne peut pas tuer le joueur

> [!caution] Attention
> `{{ui:editor_inspector_layer}}` se règle par rapport au parent, pas dans l'absolu. À côté se trouve le calque global, en lecture seule. C'est celui qu'utilise le rendu : ton calque plus les calques de tous les ancêtres

> [!tip] Conseil
> Modifier un champ sur un objet issu d'un prefab enregistre un **remplacement d'instance**. La case à côté montre le remplacement et l'annule

Le bouton du parent montre de quoi dépend l'objet, `{{ui:editor_inspector-parent_btn}}` compris. Il ouvre la fenêtre `{{ui:editor_picker_select-parent}}` : chaque objet de la portée, avec des options fixes en haut :
- dans le niveau - `{{ui:editor_inspector-parent_btn}}` et `{{ui:editor_search-option_camera}}`. `{{ui:editor_search-option_camera}}` est la caméra du niveau, et son enfant bouge avec elle
- dans un modèle de prefab - une seule rangée `{{ui:editor_search-option_prefab-root}}`. Elle veut dire à la fois "pas de parent" et la racine du modèle : là, c'est la même chose. La caméra et le joueur ne peuvent pas être parents dans un modèle

Un parent réservé s'affiche avec son ID : `Camera (-1)`, `Local Player (-2)`, `Prefab Root (-3)`. L'assistant IA ne peut utiliser que la caméra (-1) et, dans un modèle, la racine (-3)

Le bouton à côté sélectionne le parent. Sur un objet au premier niveau d'un modèle, il sélectionne la racine du modèle. Il est indisponible quand plusieurs objets sont sélectionnés et quand il n'y a rien à sélectionner : pas de parent, ou le parent est la caméra ou le joueur

Un onglet du panneau de droite qui n'a rien à montrer est masqué. Si l'onglet ouvert se vide, le panneau passe au premier onglet qui a quelque chose. Si tous les onglets sont vides, le panneau affiche `{{ui:editor_right-panel_placeholder}}`

Plus : [[3_how-the-editor-thinks|Comment fonctionne l'éditeur]]

## Inspecteur d'images clés

Montre les images clés sélectionnées. **Toutes les pistes que touche la sélection sont visibles à la fois**, pas seulement la dernière sur laquelle tu as cliqué.
Une sélection peut contenir des images clés de position et de rotation, des images clés de différents objets, et des images clés d'objets, d'audio et d'événements ensemble

> [!tip] Conseil
> Le choix `{{ui:enum_search-domain_ease}}` agit sur toutes les pistes à la fois et prend **une seule étape d'annulation**. Une sélection de position et de rotation change en une opération, pas en deux

> [!info] Bon à savoir
> Le champ `{{ui:editor_frame-key-view_key-frame}}` est verrouillé quand plusieurs images clés sont sélectionnées. Sur une piste, une image est unique. Un seul nombre pour toutes les images clés les fondrait en une seule et supprimerait les autres sans prévenir. Pour déplacer plusieurs images clés à la fois, fais-les glisser sur la timeline

Une valeur vide veut dire que les images clés sélectionnées y **diffèrent**

Plus : [[3_how-the-editor-thinks|Comment fonctionne l'éditeur]]

## Intervalle

Règle quand l'objet existe. La plage est semi-ouverte : l'image de début en fait partie, l'image de fin non.
Un objet qui se termine à 20 et un objet qui commence à 20 ne dessinent jamais ensemble sur cette image

> [!info] Bon à savoir
> **L'intervalle d'un enfant doit se trouver dans celui de son parent. C'est résolu à la lecture et jamais stocké.** Rétrécis le parent et les enfants sont coupés, mais ce qui est écrit ici ne change pas. Étire-le de nouveau et tout revient. Un objet racine au-delà de la fin du niveau est une donnée valide, il ne joue simplement pas

> [!info] Bon à savoir
> **Les ancres** veulent dire "ce bord suit le bord du parent", et elles décident de ce qui joue. Un bord ancré se place sur le bord du parent, donc un enfant ancré s'étire avec un parent qui grandit. Son animation garde le timing créé par l'auteur

La durée d'un placement de prefab vient du modèle par défaut, mais elle peut être saisie comme n'importe quelle autre. Une autre valeur enregistre un remplacement de ce placement. La case à côté de l'intervalle le montre et rétablit la durée du modèle

La racine d'un modèle de prefab n'a pas de bloc d'intervalle. À sa place se trouve une rangée `{{ui:editor_prefab-mode-frame_length}}` : la durée de tout le modèle, la même valeur que `{{ui:editor_prefab-mode-frame_length}}` dans l'onglet `{{ui:field_common_prefab}}`. Les champs `{{ui:field_common_active}}` et `{{ui:editor_inspector_layer}}` de la racine sont en lecture seule, et la racine ne peut être ni supprimée ni recevoir de parent

Plus : [[4_frames-and-time|Images, temps et durée d'un niveau]]

## Lissage

Règle comment la valeur arrive à cette image clé depuis la précédente

> [!info] Bon à savoir
> Le lissage appartient au côté **entrant** d'une image clé. Il règle le passage de l'image clé précédente à celle-ci, et c'est exactement ainsi que la lecture le lit. Donc, sur la première image clé d'une piste, le lissage n'a aucun effet

> [!tip] Conseil
> Si plusieurs images clés sont sélectionnées, le choix s'applique à toutes à la fois en **une seule étape d'annulation**. Même si les images clés sont sur des pistes différentes et appartiennent à des objets différents. Un choix vide veut dire que les images clés sélectionnées diffèrent

Plus : [[5_keyframes-and-easing]]

## Calque

Règle l'ordre de dessin **par rapport au parent**, pas dans l'absolu. Un calque résultant plus élevé dessine devant. De deux formes sur le même calque résultant, la plus récente (l'ID le plus élevé) dessine derrière

> [!caution] Attention
> Le rendu utilise ce nombre plus les calques de tous les ancêtres. La somme s'affiche en lecture seule dans le champ `{{ui:editor_inspector-global_layer}}` en dessous. Le même calque veut donc dire des choses différentes sous des parents différents. Changer de parent change l'endroit où l'objet se dessine

> [!info] Bon à savoir
> Le calque participe aussi à l'aléatoire. Une valeur aléatoire est liée au calque résultant, donc déplacer un objet dans la hiérarchie change les nombres qu'il a tirés. Deux objets avec le même calque résultant ET la même image de début obtiennent les mêmes nombres

Plus : [[3_how-the-editor-thinks|Comment fonctionne l'éditeur]]

## Forme

Règle ce que l'objet **dessine**

> [!info] Bon à savoir
> Une forme est de la vraie géométrie, pas une image. Elle est ajustée à son rectangle, et son grand côté vaut exactement 1. Le rectangle de l'objet est donc exactement ce qu'on voit à l'écran

> [!info] Bon à savoir
> Le jeu génère environ 500 formes selon quatre axes : silhouette, secteur, épaisseur et inversion. Un niveau peut ajouter les siennes. Une valeur vide est valide : un objet sans image mais avec une hitbox est un mur invisible

Plus : [[1_readability-and-fairness|Lisibilité et équité]]

## Collider

Règle ce contre quoi l'objet **entre en collision**. C'est un choix à part, qui ne dépend pas de ce que l'objet dessine

> [!info] Bon à savoir
> L'un n'est pas dérivé de l'autre, exprès. Un rayon d'avertissement inoffensif, une hitbox plus simple que l'image et un mur invisible sont du contenu ordinaire, pas des astuces

> [!tip] Conseil
> Les deux champs choisissent dans les deux mêmes collections. Une forme créée par le niveau convient à l'un comme à l'autre

Dans les modes d'affichage des hitbox, un objet sans collider ne dessine rien, et un objet inactif non plus. C'est ainsi que le décor se distingue du danger. Leur dessin se règle dans [[14_editor-settings]]

Plus : [[1_readability-and-fairness|Lisibilité et équité]]

## Type de shader

Règle par quel chemin l'objet est rendu

> [!caution] Attention
> `{{ui:enum_shader-type_auto}}` décide une seule fois, au chargement du niveau. La règle est stricte : l'aspect du niveau ne doit pas changer. Tout ce qui ne peut pas être prouvé opaque devient transparent. La géométrie n'est pas prise en compte, seulement l'alpha

> [!tip] Conseil
> L'étiquette à côté montre ce que `{{ui:enum_shader-type_auto}}` a réellement choisi. Elle est lue directement dans les données de rendu, pas recalculée. Ainsi, l'étiquette ne peut pas contredire ce qui est à l'écran

Plus : [[1_level-budget|Le budget du niveau]]

## Valeurs actuelles

Montre ce que **sont** les objets sélectionnés sur l'image actuelle, pas ce que tu y as écrit. Chaque nombre est lu dans la simulation en cours. Il correspond donc à ce qu'on voit dans la vue

Le carré au bout d'une rangée est l'état des images clés de ce champ :
- bleu - une image clé se trouve sur cette image. Un clic sur le carré la sélectionne
- ambre - l'image est entre deux images clés, la valeur est interpolée
- gris - la piste a des images clés, mais l'image est en dehors. La valeur est maintenue
- creux - la piste est vide, le champ prend la valeur par défaut du moteur

Les flèches déplacent la tête de lecture vers l'image clé précédente ou suivante de cette piste

Une rangée UV se lit comme deux paires : d'abord la mosaïque, puis le décalage

Sous la ligne viennent les valeurs composées : le calque additionné, l'activité héritée et la transformation qui tient compte des parents. Aucune image clé ne les règle, donc elles n'ont pas d'indicateur

> [!info] Bon à savoir
> Une piste d'images clés vide est une donnée valide, pas une donnée manquante. Elle veut dire que l'objet utilise la valeur par défaut de ce champ

> [!info] Bon à savoir
> En mode prefab, cette section est masquée. Un modèle ne joue pas ses propres images, il n'y a donc rien à montrer sur une image
