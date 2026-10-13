---
title: Paramètres de l'éditeur
date: 2026-10-11
tags: [level_author]
---

# Paramètres de l'éditeur

L'enregistrement automatique, la grille, la sélection, les gizmos et les préréglages des nouveaux niveaux se règlent ici. L'enregistrement automatique est activé par défaut et se déclenche {{v:editor.autosave-delay}} secondes après une modification

## Éditeur de jeu

L'enregistrement automatique, la caméra, la sélection et les formats de fichier se règlent ici

| Paramètre | Ce qu'il fait | Par défaut |
|---|---|---|
| `{{ui:settings_game-editor_autosave}}` | active l'enregistrement automatique | activé |
| `{{ui:settings_game-editor_autosave-rate}}` | combien de secondes passent entre une modification non enregistrée et l'enregistrement automatique | {{v:editor.autosave-delay}} |
| `{{ui:settings_game-editor_max-autosave-files}}` | combien de copies sont gardées. Une fois la limite atteinte, la plus ancienne est supprimée | {{v:editor.autosave-copies}} |

Le minuteur ne tourne que tant qu'il y a des modifications non enregistrées

Un enregistrement automatique fait deux choses :
1. Écrit une copie du niveau dans `<game folder>/backups/<level id>/`
2. Enregistre le niveau lui-même, comme le fait `Ctrl+S`

Une copie contient seulement le fichier du niveau. Il y a deux façons de la restaurer :
- dans les paramètres du niveau : `{{ui:settings_level-settings_dangerous-zone}}` → `{{ui:level_backups_open}}`
- à la main : copie-la dans le dossier du niveau sous le nom `level.json` (ou `level.blob`)

Plus - [[4_not-losing-work#L'enregistrement automatique]]

`{{ui:settings_game-editor_camera-min-size}}` et `{{ui:settings_game-editor_camera-max-size}}` limitent jusqu'où la vue de l'éditeur peut zoomer et dézoomer

`{{ui:settings_game-editor-multi-select-requires_hold}}` et `{{ui:settings_game-editor-pick-invisible_aabb}}` changent ce que veut dire un clic dans la vue.
Vérifie-les si la sélection se comporte soudain autrement que d'habitude

`{{ui:settings_game-editor-level-serialize_mode}}` et `{{ui:settings_game-editor-resources-serialize_mode}}` fixent le format par défaut pour l'écriture sur le disque

`{{ui:settings_game-editor_publish-language}}` choisit la langue dans laquelle le titre et la description d'un élément du Workshop sont publiés en premier : `{{ui:enum_publish-language_english}}` (par défaut) ou `{{ui:enum_publish-language_system}}`, la langue de l'appareil

Plus - [[3_speed-and-shortcuts]]

## Grille

La grille de la vue est dessinée derrière le niveau et aide à placer les objets

| Paramètre | Ce qu'il fait | Par défaut |
|---|---|---|
| `{{ui:settings_game-editor_grid-active-default}}` | si la grille est activée à l'ouverture de l'éditeur. Ce n'est que l'état de départ | désactivé |
| `{{ui:settings_game-editor-grid_size}}` | le côté d'une cellule, en unités du monde | 1 |
| `{{ui:settings_game-editor-grid_opacity}}` | à quel point les lignes sont visibles, de 0 à 1 | 0,25 |

Le bouton de la grille dans la barre d'outils l'active et la désactive. Cet état n'est pas enregistré d'une session à l'autre

L'aspect de la grille :
- Elle n'a pas de bord. La cellule change par paliers de 10 quand tu zoomes, et la grille plus fine apparaît progressivement
- Si un niveau de la grille demandait trop de lignes, ce niveau est désactivé plutôt qu'allégé
- La couleur des lignes est toujours l'inverse de l'arrière-plan de la caméra sur l'image actuelle, pour que la grille reste visible quand l'arrière-plan change. Tu ne règles que l'opacité

Avec l'aimantation activée, glisser une position s'accroche à la demi-cellule : aux intersections et aux centres des cellules. Elle utilise la grille que tu vois. Avec la grille désactivée, la position s'accroche à un pas fixe

## Sélection

| Paramètre | Ce qu'il fait | Par défaut |
|---|---|---|
| `{{ui:settings_game-editor-multi-select-requires_hold}}` | activé : en mode de sélection multiple, un clic n'ajoute que si `Ctrl` est maintenu, et un clic simple remplace la sélection. Désactivé : tant que le mode est actif, chaque clic ajoute | activé |
| `{{ui:settings_game-editor-preview-collider-on_select}}` | dessine la hitbox de chaque objet sélectionné sous forme de remplissage translucide | désactivé |
| `{{ui:settings_game-editor-pick-invisible_aabb}}` | un clic choisit un objet par tout son rectangle, pas par ce qu'il dessine | désactivé |
| `{{ui:settings_game-editor_selection-long-press-delay}}` | combien de temps dure un appui maintenu avant qu'un menu s'ouvre, en secondes | 0,5 |
| `{{ui:settings_game-editor_selection-long-press-threshold}}` | de combien le curseur peut bouger pendant l'appui avant que cela devienne un glissement | 8 |
| `{{ui:settings_game-editor_selection-collider-opacity}}` | à quel point la hitbox d'un objet sélectionné est dessinée opaque | 0,5 |
| `{{ui:settings_game-editor_selection-collider-opacity-view}}` | la même chose pour l'affichage de toutes les hitbox, plus pâle parce que des centaines s'y superposent | 0,25 |

Relâcher `Ctrl` en mode de sélection multiple n'efface rien et ne quitte pas le mode. Seul le clic simple suivant remplace la sélection. Plus sur ce mode - [[4_hierarchy-and-clipboard]]

Le bouton des colliders dans la barre d'outils affiche les hitbox de tout ce qui est dans l'image, cercle du joueur compris. Cet état n'est pas enregistré d'une session à l'autre. S'il y a trop de hitbox à l'écran, l'affichage se désactive de lui-même avec un message plutôt que d'en dessiner seulement une partie

Un objet sans collider ne dessine de hitbox dans aucun des deux affichages, pas plus qu'un objet inactif

La couleur de remplissage des deux affichages est `Settings > Graphics > Colliders Only Mode > Fill Color`, partagée avec le mode "Colliders seulement" du jeu ([[4_settings]]). Les deux opacités ci-dessus restent des paramètres propres à l'éditeur

## Gizmos

| Paramètre | Ce qu'il fait | Par défaut |
|---|---|---|
| `{{ui:settings_game-editor_gizmos-scale}}` | la taille des poignées de glissement dans la vue, de 0,1 à 10. Une poignée taillée pour la souris est difficile à toucher du doigt | 1 |

Les poignées gardent la même taille à l'écran quel que soit le zoom

## Agent IA

`{{ui:settings_game-editor_mcp_title}}` permet à un client IA qui parle MCP de modifier le niveau ouvert. Seulement sur Windows, Linux et Mac : les téléphones et les tablettes n'affichent pas cette section

| Paramètre | Ce qu'il fait | Par défaut |
|---|---|---|
| `{{ui:settings_game-editor_mcp-enabled}}` | permet à un client de se connecter. Seul cet ordinateur peut se connecter, un client à la fois | désactivé |
| `{{ui:settings_game-editor_mcp-port}}` | le port sur lequel l'éditeur écoute. `0` en choisit un libre à chaque démarrage, sinon de {{v:mcp.port-min}} à {{v:mcp.port-max}}. Tout autre nombre est rejeté | 0 |
| `{{ui:settings_game-editor_mcp-follow-ai}}` | où va la tête de lecture après que l'IA a regardé une image. Désactivé : là où tu l'avais laissée. Activé : elle reste sur cette image, en pause | activé |
| `{{ui:settings_game-editor_mcp-reveal-edits}}` | après chaque modification de l'IA, sélectionne et localise ce qu'elle a créé ou changé. Jamais pendant que tu glisses, tapes ou lis | activé |
| `{{ui:settings_game-editor_mcp-operation-delay}}` | les secondes que l'éditeur attend entre deux opérations de l'IA, de 0 à {{v:mcp.operation-delay-max}}. `0` applique chacune tout de suite. Lire, mettre en pause et déplacer la tête de lecture ne sont jamais retardés, pas plus que ce que l'IA ne fait que lire | {{v:mcp.operation-delay}} |

`{{ui:settings_game-editor_mcp-copy-config}}` copie la configuration qu'attend un client MCP, avec le chemin du serveur et celui du fichier de connexion du jeu déjà remplis

La ligne sous les paramètres dit ce que fait l'éditeur : désactivé, à l'écoute sur un port, connecté, ou arrêté depuis le badge IA dans l'éditeur

Ces paramètres sont gardés sur cet appareil seulement

Plus - [[7_ai-assistant]]

## Créer un niveau

Les `{{ui:settings_editor-settings_level-presets}}` fixent ce avec quoi un nouveau niveau commence : vide ou avec un petit échafaudage.
Sans préréglage, il faudrait construire cet échafaudage à la main à chaque fois

> [!caution] Attention
> Les `{{ui:settings_editor-settings_parameters}}` fixent ce qu'il est malcommode de changer plus tard : la durée en images et la fréquence d'images

> [!tip] Conseil
> Les listes `{{ui:settings_editor-settings_quot-level-quot-file-format}}` et `{{ui:settings_editor-settings_quot-metadata-quot-file-format}}` choisissent le format dans lequel le niveau et ses métadonnées sont écrits sur le disque. Les deux peuvent être changés plus tard dans la `{{ui:settings_level-settings_dangerous-zone}}` du niveau

Plus - [[2_first-level]]

## Bibliothèque

`{{ui:settings_editor-settings_library}}` est le dernier onglet, après `{{ui:settings_editor-settings_community}}`. Il contient les ressources que tu réutilises d'un niveau à l'autre : la bibliothèque de l'appareil, tes propres collections et, dans la version Steam, les collections que tu suis par un abonnement dans le Steam Workshop

La colonne de gauche choisit le type : `{{ui:settings_level-settings_collections}}`, puis prefabs, thèmes, formes et effets, puis textures, polices et audio.
C'est ici que tu crées et modifies des collections, copies des entrées de l'une à l'autre, les importes et les exportes, et, dans la version Steam, publies les tiennes

Plus - [[16_library-and-collections]]

## Utiliser le travail des autres

Chaque ressource externe d'un niveau (musique, images, polices, textes) doit correspondre à l'une de ces deux options :
- une licence au moins aussi libre que `CC BY-NC`
- l'autorisation propre du titulaire des droits pour une diffusion publique non commerciale

> [!caution] Attention
> Un "bien sûr, pas de problème" en privé ne suffit pas. Un niveau sous `CC BY-NC` est diffusé publiquement. L'autorisation doit couvrir exactement cela, pas seulement ton usage personnel

Un niveau qui reste sur ton appareil n'est pas vérifié.
Les règles s'appliquent à un moment précis : quand le niveau est remis à un service

Les règles complètes, la liste des licences acceptées, le modèle de demande et où chercher des ressources :
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
