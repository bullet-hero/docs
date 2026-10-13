---
title: Thèmes
date: 2026-10-02
tags: [level_author]
---

# Thèmes

Un thème est une palette de 64 couleurs à laquelle les objets renvoient par numéro d'emplacement. Change le thème, et tout ce qui y renvoie change avec lui

Une couleur de type `Theme` ne stocke aucune couleur à elle, seulement un numéro d'emplacement.
Elle prend ce que contient cet emplacement dans le thème actif sur l'image actuelle

Pourquoi c'est mieux que des couleurs saisies à la main et comment garder un niveau lisible avec n'importe quel thème - [[5_color-and-postprocessing]]

## Ce que contient un thème

- **Un nom** - affiché dans les listes et les sélecteurs
- **Un ID**, `ThemeId`. Les clés de thème renvoient à un thème par lui, pas par son nom
- **64 couleurs** sur une grille de 8 par 8, chacune avec sa transparence
- **Un nom d'emplacement** pour chaque emplacement, facultatif. Tant que tu n'as nommé aucun emplacement, le fichier stocke `null` au lieu de la liste des noms

Un thème est une donnée dans `level.json`, pas un fichier séparé dans le dossier du niveau (voir [[1_level-needs]]).
Un niveau peut contenir autant de thèmes que voulu

Le jeu n'attribue aucun rôle à un emplacement : le thème `Balanced` du jeu regroupe simplement ses 64 couleurs par teinte

## Comment une couleur trouve sa valeur

En deux étapes :
1. La piste `Theme` de la timeline des événements dit quel thème est actif sur cette image
2. Une couleur de type `Theme` désigne un emplacement de 0 à 63 dans le thème actif

Parmi ce qui peut renvoyer à un thème, il y a par exemple la couleur d'une forme (chacun de ses coins séparément), la couleur d'un texte et le fond du niveau

**La position d'un emplacement est son identité.** Déplace une couleur vers un autre emplacement, et tout ce qui renvoyait à l'ancien change de couleur

## Changer de thème au fil du temps

Entre deux clés de thème, le jeu fond en douceur toute la palette d'un thème vers l'autre.
Le lissage vient de la clé la plus tardive (voir [[5_keyframes-and-easing]])

S'il n'y a aucune clé de thème, chaque emplacement est blanc

> [!warning] Avertissement
> Une nouvelle clé reçoit `Linear`, donc la palette glisse sur toute la portion depuis la clé de thème précédente jusqu'à celle-ci. Pour que le thème change pile sur le drop, mets `Constant` sur la clé du drop

> [!caution] Attention
> Une clé de thème peut survivre au thème lui-même. Supprime un thème auquel des clés renvoient encore, et toutes ces images deviennent blanches. Les clés elles-mêmes restent. L'éditeur redemande confirmation avant de supprimer un tel thème

## Comment créer et modifier un thème

L'onglet `Themes` parmi les ressources du niveau montre les thèmes du niveau. Il a `{{ui:settings_level-settings_resources-themes-add}}` et `{{ui:settings_level-settings_resources-themes-import}}`.
Cliquer sur une ligne ouvre le `{{ui:settings_level-settings_theme-editor}}` :
- `{{ui:field_common_name}}` du thème
- `Theme Id` et `{{ui:settings_level-settings_theme-editor-regenerate-id}}`
- la grille de 8 par 8. Cliquer sur une case la sélectionne, affiche `Color:` avec son numéro et charge la couleur dans la roue sous la grille
- `{{ui:editor_theme-editor_color-name}}` pour la case sélectionnée

L'éditeur travaille sur une copie. Rien n'atteint le niveau tant que tu n'as pas enregistré. L'enregistrement lui-même est une seule étape d'annulation

## Comment choisir un emplacement

Passe une couleur en `Theme` et ouvre `{{ui:editor_select-theme_color}}`

La grille montre la palette telle qu'elle est fondue sur l'image de la clé en cours de modification, pas à la tête de lecture.
À côté se trouvent les deux clés de thème qui entourent cette image et ce que contient l'emplacement sélectionné dans chacune. Un emplacement sans nom est étiqueté `{{ui:editor_search_unnamed}}`

## Comment partager et importer

- **La bibliothèque de l'appareil.** `{{ui:editor_level-theme-item_export}}` dans la ligne d'un thème l'enregistre dans `resources/themes` - la bibliothèque partagée de l'appareil, où `resources` se trouve à côté de `levels` (voir [[4_level-folder-and-backups]]). `{{ui:settings_level-settings_theme-library}}` l'affiche et marque ce qui est déjà `{{ui:editor_theme-library-item_in-level}}`. `{{ui:editor_library_delete}}` retire un thème de la bibliothèque. L'importation copie le thème dans le niveau, donc le niveau ne dépend jamais de ta bibliothèque. `{{ui:settings_level-settings_theme-library}}` affiche aussi les thèmes des collections, avec des étiquettes de source - [[16_library-and-collections]]
- **Les thèmes du jeu.** `{{ui:editor_search-title_theme}}` propose les thèmes livrés avec le jeu à côté des thèmes du niveau

À lire ensuite : [[5_color-and-postprocessing|Couleur, thèmes et post-traitement]], [[1_readability-and-fairness|Lisibilité et équité]]
