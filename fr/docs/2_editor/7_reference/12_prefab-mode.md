---
title: Mode prefab
date: 2026-10-02
tags: [level_author]
---

# Mode prefab

En mode prefab, tu modifies le modèle, et l'enregistrement répercute la modification sur chacun de ses placements. On y entre avec le bouton "Modifier le prefab" dans l'inspecteur d'un placement, on revient au niveau avec Ctrl+Shift+E

## Mode prefab

> [!caution] Attention
> Tu modifies le modèle, pas l'un de ses placements. L'enregistrement répercute le changement sur chaque placement qui renvoie à ce modèle

Comment fonctionne un placement :
- Dès que tu fais pointer un placement vers un modèle, il reçoit de vraies copies de ses objets avec des ID permanents. Dans l'éditeur, un enfant de prefab est un objet tout à fait ordinaire
- Le fichier du niveau ne garde que le placement : le modèle, les ID des copies et les remplacements. Les copies sont reconstruites à partir du modèle à chaque chargement du niveau
- Un placement peut différer du modèle grâce aux **remplacements propres à chaque instance**. Ils sont enregistrés quand tu modifies un tel objet *hors* du mode prefab
- Les modifications faites en mode prefab n'enregistrent aucun remplacement. Elles changent le modèle lui-même

> [!tip] Conseil
> Les modèles s'ouvrent les uns par-dessus les autres. Un placement à l'intérieur d'un modèle ouvre son propre modèle, et `{{ui:editor_prefab-timeline_close}}` te ramène en arrière. Le même modèle ne peut pas être ouvert deux fois en même temps. La limite d'imbrication est de 8 niveaux

Plus - [[2_reuse]]

## Entrer et sortir

Il y a deux façons d'entrer :
- `{{ui:editor_inspector-prefab_edit}}` dans l'inspecteur d'un placement
- `{{ui:editor_level-prefab-item_edit}}` sur la ligne d'un modèle dans les paramètres du niveau, onglet `Prefabs`. Il n'a besoin d'aucun placement, il ouvre donc aussi un modèle qui n'est placé nulle part, ou placé seulement à l'intérieur d'un autre modèle

`{{ui:editor_context-menu_open-prefab}}` dans un menu contextuel et dans la palette de commandes fait la même chose pour un placement sélectionné, ou pour un objet qu'un placement a apporté. L'objet correspondant à l'intérieur du modèle est sélectionné aussitôt

Il y a deux façons de sortir :
- `{{ui:editor_prefab-timeline_close}}` sur la timeline Prefab remonte d'un niveau, vers le modèle qui a ouvert celui-ci
- l'état dans la barre d'outils principale (`Editing '...'`) et `Ctrl+Shift+E` quittent d'un coup tous les modèles ouverts, pour revenir au niveau

La sélection est vidée à chaque entrée et à chaque sortie. Remonter d'un niveau restaure ce qui était sélectionné dans ce modèle

À l'intérieur d'un modèle, la sélection fonctionne comme dans le niveau : clic, `Ctrl`-clic, rectangle, suppression, copie et repli. Un clic dans la vue n'y choisit rien : la vue continue de montrer le niveau, et un modèle n'y a pas d'aperçu en direct

## À l'intérieur d'un modèle

Chaque objet d'un modèle est rattaché à sa **racine**. La racine :
- couvre tout le modèle. Sa durée est `{{ui:editor_prefab-mode-frame_length}}`, le même nombre dans l'inspecteur de la racine et dans l'onglet `Prefab`
- ne peut pas être supprimée ni recevoir de parent
- a `{{ui:field_common_active}}` et `{{ui:editor_inspector_layer}}` en lecture seule. Ils appartiennent à chaque placement

Un nouvel objet va sous l'objet sélectionné quand il y en a exactement un, racine comprise. Sinon, il va au niveau supérieur du modèle, sous la racine.
Il couvre son parent, ancré aux deux bouts. Au niveau supérieur, c'est tout le modèle

Les générateurs qui ont besoin du niveau entier ne sont pas disponibles ici. Créer un prefab à partir d'une sélection et aplatir un placement sont aussi refusés à l'intérieur d'un modèle

## Créer un prefab à partir d'une sélection

Transforme les objets sélectionnés en un nouveau modèle et met un placement de celui-ci à leur place. Le niveau a le même aspect et se joue de la même façon ensuite

Où le trouver :
- `{{ui:editor_context-menu_pack-prefab}}` dans le menu d'une ligne de la hiérarchie
- le menu contextuel de la vue
- `{{ui:cmd_editor_pack-prefab}}` dans la palette de commandes, `Ctrl+G`
- `{{ui:settings_level-settings_resources-prefabs-pack}}` dans les paramètres du niveau, onglet `Prefabs`

Aucune confirmation n'est demandée, et c'est une seule étape d'annulation. Le nouveau placement se retrouve sélectionné.
Un seul objet donne au modèle son propre nom. Plusieurs objets donnent un modèle appelé `Prefab`. Renomme-le dans les paramètres du niveau, onglet `Prefabs`

Ce qui est refusé :
- un placement, ou un objet qu'un placement a apporté. Les menus proposent `{{ui:editor_context-menu_open-prefab}}` pour ceux-là à la place
- une sélection qui s'imbriquerait sur plus de 15 niveaux. Rien n'est écrit, et le message le dit

## Aplatir un placement

Détache un placement de son modèle : ses objets deviennent des objets ordinaires du niveau et restent exactement où ils sont

Où le trouver : `{{ui:editor_inspector-prefab_flatten}}` dans l'inspecteur du placement, dans le menu d'une ligne de la hiérarchie et dans la palette de commandes

Une confirmation est toujours demandée d'abord. Le niveau a le même aspect ensuite, donc un aplatissement fait par erreur ne serait sinon découvert que bien plus tard, quand une modification du modèle cesse de l'atteindre. Plusieurs placements sélectionnés donnent une seule confirmation et une seule étape d'annulation

Un objet qu'un placement a apporté ne peut pas être aplati seul. Aplatis le placement auquel il appartient

## Aplatir aussi les prefabs imbriqués

Décide de ce qui arrive aux prefabs à l'intérieur de celui que tu aplatis

**Désactivé** - seul le placement visé cesse de suivre son modèle.
Un prefab placé à l'intérieur reste un placement et garde son lien. Modifier ce modèle intérieur atteint toujours le niveau.
C'est la valeur par défaut : c'est ce que demande d'habitude "dépaqueter ce prefab". L'interrupteur est désactivé à chaque ouverture de la confirmation

**Activé** - tout ce qui est imbriqué est aplati aussi.
Après un seul appui, plus rien dans le niveau n'est lié à ces modèles intérieurs, à aucune profondeur

Dans les deux cas, les modèles eux-mêmes restent dans le niveau. Tout l'aplatissement est une seule étape d'annulation
