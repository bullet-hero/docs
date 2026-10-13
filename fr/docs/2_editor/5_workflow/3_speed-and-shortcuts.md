---
title: Vitesse et raccourcis
date: 2026-10-02
tags: [level_author]
---

# Vitesse et raccourcis

La palette de commandes (Ctrl+Shift+P), la recherche de contenu (Ctrl+F), le bouton Localiser et les flèches sur une timeline font gagner le plus de temps. Chaque touche peut être réattribuée dans les paramètres

## Les quatre plus grands gains de temps

- **`{{ui:editor_search-title_command}}`** (`Ctrl+Shift+P`) - tout ce que l'éditeur sait faire, cherchable par nom. Plus rapide que de se rappeler dans quel panneau se trouve un bouton
- **`Search Content`** (`Ctrl+F`) - aller à un objet ou à une piste audio par son nom. La tête de lecture t'accompagne
- **`{{ui:cmd_editor_ping}}`** - la vue cadre la sélection, la timeline et la hiérarchie défilent jusqu'à elle, tout à la fois. Appuyer de nouveau passe à l'objet suivant d'une sélection multiple
- **Les flèches sur une timeline** - elles se déplacent selon la direction, pas selon la position dans une liste. Tu peux passer d'une image clé à sa voisine sans la souris

## Les touches par défaut

Les groupes et les noms ci-dessous sont ceux qu'affiche `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

### Lecture

| Touche | Nom dans les paramètres | Action |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | lire et mettre en pause |

### Édition

| Touche | Nom dans les paramètres | Action |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | annuler |
| `Ctrl+Y` ou `Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | rétablir |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | enregistrer |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | copier |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | coller |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | dupliquer |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | créer un prefab à partir de la sélection |

### Sélection

| Touche | Nom dans les paramètres | Action |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | supprimer la sélection |
| `Ctrl` maintenu | `{{ui:settings_keybindings_editor_multi_select}}` | sélection multiple |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | vider toutes les sélections d'un coup : objets, images clés, audio et pulsations |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | quitter le mode prefab et revenir au niveau |

### Affichage

| Touche | Nom dans les paramètres | Action |
|---|---|---|
| `Ctrl+F` | `Search Content` | rechercher du contenu |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | exécuter une commande |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | afficher ou masquer le panneau de gauche |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | afficher ou masquer le panneau de droite |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | afficher ou masquer le panneau du bas |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | afficher ou masquer les groupes d'outils au-dessus de la vue |
| `` ` `` maintenu | `{{ui:settings_keybindings_editor_preview}}` | aperçu : l'interface de l'éditeur est masquée tant que la touche est enfoncée |

### Timeline

| Touche | Nom dans les paramètres | Action |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | faire défiler le repliement : chaque sous-arbre, seulement les types choisis, rien |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | activer ou désactiver l'aimantation |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | l'outil de sélection |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | l'outil de sélection rectangulaire |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | l'outil ciseaux |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | l'outil bords |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | replier les objets sélectionnés sur la timeline |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | ouvrir la timeline du niveau |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | ouvrir la timeline locale |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | ouvrir la timeline audio |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | ouvrir la timeline des événements |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | ouvrir la timeline du prefab |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | la fenêtre de la grille de pulsations, où l'on marque le tempo par appuis. `{{ui:settings_keybindings_editor_beat_tap}}` lui-même n'a pas de touche par défaut, attribues-en une si tu en as besoin |
| `Ctrl` maintenu avec la molette | `{{ui:settings_keybindings_timeline_pan_modifier}}` | panoramique |
| `Shift` maintenu avec la molette | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | zoom |

`Z X C V B N` suivent la barre d'outils de la timeline de gauche à droite, et `Q W E R T` suivent la rangée d'onglets. Une timeline qui a moins d'outils les perd par la droite : la timeline locale n'a que `Z X C V`. Une lettre pour laquelle la timeline ouverte n'a pas d'outil ne fait rien

### Gizmos

| Touche | Nom dans les paramètres | Action |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | sélection |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | position |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | rotation |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | échelle |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | taille |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | ancres |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | pivot |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | masqué : la sélection reste, mais ni les poignées ni le contour ne sont dessinés |

### Fenêtre

| Touche | Nom dans les paramètres | Action |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | activer ou désactiver le plein écran. Fonctionne sur n'importe quel écran, sur ordinateur uniquement |
| `Ctrl+S` | `{{ui:settings_keybindings_window_settings_save}}` | écrire les paramètres sur le disque tout de suite, pendant que les paramètres sont ouverts. Dans l'éditeur, `Ctrl+S` enregistre plutôt le niveau |

### Navigation

| Touche | Nom dans les paramètres | Action |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | monter sur la surface où tu as cliqué en dernier |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | descendre sur la surface où tu as cliqué en dernier |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | aller à gauche sur la surface où tu as cliqué en dernier |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | aller à droite sur la surface où tu as cliqué en dernier |

Les touches seules, comme les chiffres des gizmos, les lettres de la timeline et `Space`, ne font rien pendant que tu tapes dans un champ de texte. Un `2` dans un champ d'image ne change pas de gizmo

## Les flèches sur une timeline

Une flèche choisit l'élément le plus proche dans cette direction à l'écran. Le même appui trouve le même élément à n'importe quel zoom

- Depuis une sélection multiple, une flèche part de l'élément le plus avancé dans la direction appuyée. Elle ne revient jamais dans le bloc que tu as sélectionné
- Un déplacement avec une flèche remplace toujours la sélection. Il n'y ajoute jamais rien
- La timeline ne défile que de ce qu'il faut pour montrer le nouvel élément. Cliquer sur l'affichage de la tête de lecture centre toujours la vue
- Tant que le joueur de test est activé, les flèches le contrôlent, lui, et pas la timeline. La hiérarchie et l'onglet `{{ui:settings_level-settings_raw}}` gardent leurs flèches dès que tu cliques dedans

## Voir le niveau

**L'aperçu.** Maintiens `` ` `` pour masquer l'interface de l'éditeur et ne regarder que le niveau. C'est un maintien, pas un interrupteur : relâche la touche et tout revient. Le niveau, les bandes noires, le joueur et les limites de la caméra restent visibles.
Il n'y a ni bouton ni paramètre pour cela. La touche se réattribue sous le nom `{{ui:settings_keybindings_editor_preview}}`

**La grille de la vue** s'active avec son bouton de la barre d'outils ou la commande `{{ui:cmd_editor_viewport-grid}}`. Elle démarre désactivée. Cela se change dans `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}`, et le fait que tu l'aies activée n'est pas retenu d'une session à l'autre

**L'aimant des gizmos** aimante à la grille ce que fait glisser un gizmo. Il est activé par défaut et ne dépend pas du mode de gizmo. Il se bascule avec son bouton de la barre d'outils et la commande `{{ui:cmd_editor_gizmo-magnet}}`

**La pause est l'état normal pour regarder.** La grille, les colliders, la superposition du bot, les poignées des gizmos et le contour de la sélection continuent tous d'être dessinés pendant que la lecture est en pause. Saisir une poignée de gizmo met la lecture en pause

## Réattribuer les touches

Chaque touche peut être réattribuée : `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

Seules les touches que tu as changées sont stockées. Les autres viennent des valeurs par défaut.
Donc une valeur par défaut améliorée t'atteint si tu n'as pas touché à cette touche.
`{{ui:settings_keybindings_reset}}` retire simplement tes changements, et toutes les touches reviennent aux valeurs par défaut

> [!tip] Conseil
> Les noms des touches ne sont pas écrits en dur dans l'interface. Après une réattribution, la palette de commandes et chaque menu contextuel affichent tout de suite la nouvelle touche

## Touches appuyées et touches maintenues

Une touche appuyée ne se déclenche que si ses touches de modification correspondent exactement.
`Ctrl+Shift+P` ne se déclenche pas aussi comme `Ctrl+P`, et un `T` seul ne se déclenche pas pendant que `Ctrl` est maintenu

Une touche maintenue se déclenche si ses touches de modification font partie de ceux qui sont maintenus. Elle précise un geste déjà en cours

> [!info] Bon à savoir
> C'est pourquoi deux touches maintenues peuvent partager exprès un même bouton. La sélection multiple et le panoramique de la timeline sont tous deux sur `Ctrl` et ne se gênent pas

Suite : [[1_order-of-work|L'ordre de travail]], [[2_reuse|Réutiliser : prefabs, copie, générateurs]]
