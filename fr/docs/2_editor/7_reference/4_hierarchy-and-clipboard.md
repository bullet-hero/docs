---
title: Hiérarchie et presse-papiers
date: 2026-10-02
tags: [level_author]
---

# Hiérarchie et presse-papiers

La hiérarchie est un arbre des objets de l'image actuelle, rangés par parent. Chaque timeline a son propre tampon de presse-papiers, et la palette de commandes trouve n'importe quelle action de l'éditeur par son nom

## Hiérarchie

Montre chaque objet vivant sur l'**image actuelle**, imbriqué sous son parent

Un objet n'est visible ici que tant que la tête de lecture est dans son intervalle. La liste change donc pendant le balayage.
Une hiérarchie vide veut généralement dire que la tête de lecture est au-delà de la fin du contenu

> [!info] Bon à savoir
> **Un parent** transmet sa transformation à ses enfants. Les calques s'additionnent le long de la chaîne : l'ordre de dessin d'un enfant est son propre calque plus les calques de tous ses ancêtres. Changer de parent déplace donc l'objet dans l'ordre de dessin. Cela change aussi ses valeurs aléatoires : l'aléatoire est lié au calque résultant

> [!tip] Conseil
> Fais un clic droit sur une rangée pour ouvrir ses actions. Sur un écran tactile, un appui long ouvre le même menu

Maintenir une rangée ouvre le menu à la souris aussi. Les clips des timelines n'ont pas de menu par appui long

Fais glisser une rangée sur une autre pour faire de l'objet son enfant. Déposé sur l'espace vide sous les rangées, il perd son parent. Un dépôt est refusé :
- sur l'objet lui-même ou sur le parent qu'il a déjà
- sur un de ses propres enfants
- si la chaîne devenait plus profonde que 15 niveaux

La rangée `{{ui:editor_search-option_camera}}` est épinglée en bas de la liste. Une rangée déposée dessus fait de l'objet un enfant de la caméra du niveau. Dans un modèle de prefab, la caméra ne prend pas d'enfants, mais la racine du modèle, si

Plus : [[3_how-the-editor-thinks|Comment fonctionne l'éditeur]]

## Sélectionner plusieurs objets

Un clic avec `Ctrl` ajoute un objet à la sélection ou l'en retire. Cela marche de la même façon dans la hiérarchie, sur les timelines et dans la vue. `Ctrl` est la seule touche de ce genre : un clic avec `Shift` dans la hiérarchie ne fait rien, il n'y a pas de sélection par plage. La touche peut être réattribuée

Un clic avec `Ctrl`, ou un rectangle qui attrape plus d'un élément, active le **mode de sélection multiple**. Tant qu'il est actif, ce que fait un simple clic dépend de `{{ui:settings_game-editor-multi-select-requires_hold}}` - voir [[14_editor-settings]]

L'élément de sélection de la barre d'outils affiche `{{ui:editor_multi-select_status}}` ou `Selected (N)`. Il fonctionne tant que quelque chose est sélectionné :
- un appui vide toute la sélection
- un double clic ou un clic avec `Shift` active plutôt le mode de sélection multiple. Activé de cette façon, le mode ignore `{{ui:settings_game-editor-multi-select-requires_hold}}`, et chaque simple clic ajoute. C'est ainsi qu'un doigt, qui n'a pas de `Ctrl`, construit une sélection

Le même élément apparaît dans les menus contextuels tant que quelque chose est sélectionné. Là, un appui vide la sélection

Le mode se désactive tout seul quand rien n'est sélectionné, et avec `Escape` si aucun champ de texte n'est en cours de saisie

## Presse-papiers

Transfère une sélection entre niveaux et entre appareils. Chaque timeline a son propre tampon et sa propre ligne d'état

`{{ui:editor_clipboard-serialize_copy}}` écrit tous les tampons dans le presse-papiers du système sous forme de texte.
`{{ui:editor_clipboard-deserialize_paste}}` relit le texte dans les tampons - et **s'arrête là**

> [!info] Bon à savoir
> L'arrêt est voulu. Lire le texte et coller sont deux décisions différentes. L'endroit où le contenu est collé dépend de la tête de lecture et de la portée active. Le contenu n'apparaît que lorsque tu **le colles dans la timeline de ton choix**

Si le presse-papiers du système contient le texte de quelqu'un d'autre, l'éditeur signale une erreur et ne plante pas. Il contient ce que tu as copié en dernier, n'importe où

Il n'existe pas d'action "coller tous les tampons d'un coup". Après `{{ui:editor_clipboard-deserialize_paste}}`, colle toi-même dans chaque timeline

Les images clés collées arrivent à la tête de lecture. Pour chaque propriétaire, sa première image clé collée est placée sur la tête de lecture, comptée dans l'intervalle de ce propriétaire. Les images clés d'événements se décalent d'autant, donc un mouvement de caméra et l'effet qui l'accompagnait restent à la même distance l'un de l'autre

Une image clé est ignorée si elle tombait hors de la timeline de son propriétaire ou sur une image déjà prise sur sa piste. Les images clés ignorées sont comptées et signalées dans un seul message

Une copie ou un collage réussi n'écrit rien dans la console. Seuls les problèmes sont signalés

Plus : [[2_reuse|Réutiliser : prefabs, copie, générateurs]]

## Palette de commandes

Trouve n'importe quelle action de l'éditeur par son nom

Elle liste des commandes, pas du contenu. Ce sont les mêmes actions que lancent la barre d'outils et les menus contextuels

> [!tip] Conseil
> La recherche de contenu (`Ctrl+F`) est sa jumelle. Elle cherche dans chaque objet de la portée actuelle et chaque piste audio. Les ressources n'y figurent pas : chacune se choisit dans le champ qui en a besoin

Plus : [[3_speed-and-shortcuts|Vitesse et raccourcis]]
