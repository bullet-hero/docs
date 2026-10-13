---
title: Jouer des niveaux
date: 2026-10-11
tags: [player]
---

# Jouer des niveaux

Choisis un niveau dans la liste des niveaux, règle les conditions de la partie et lance-la. Le niveau de quelqu'un d'autre est un simple dossier : copie-le dans le dossier des niveaux et actualise la liste

## Menu principal

| Bouton | Ce qu'il fait |
|---|---|
| `{{ui:menu_main_levels-btn}}` | la liste des niveaux, décrite plus bas |
| `{{ui:menu_main_editor-btn}}` | l'éditeur de niveaux, [[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | une arène sans niveau et le tutoriel, [[13_sandbox]] |
| `{{ui:settings_common_title}}` | tous les paramètres, [[4_settings]] |
| `{{ui:menu_main_story-btn}}` | ne fonctionne pas encore |
| `{{ui:menu_main_multiplayer-btn}}` | ne fonctionne pas encore |

## La liste des niveaux

`{{ui:menu_main_levels-btn}}` dans le menu principal ouvre la liste des niveaux. Les niveaux viennent de trois endroits :

- `{{ui:root_level-source_local}}` - le dossier `levels`, [[1_installation]]
- `{{ui:root_level-source_builtin}}` - les niveaux livrés avec le jeu
- `Workshop` - versions Steam uniquement. Il montre les niveaux de tes abonnements. Les collections de ressources de tes abonnements ne sont pas des niveaux : elles apparaissent dans la bibliothèque de l'éditeur, [[16_library-and-collections]]

En haut se trouvent le champ de recherche, `{{ui:root_level-browser_sort}}`, `{{ui:root_level-browser_layout}}` (grille ou liste) et `{{ui:root_level-browser_filters}}`. La liste s'ouvre en grille.
Tu peux trier par `{{ui:root_level-browser_sort-relevance}}`, `{{ui:root_level-browser_sort-title}}`, `{{ui:root_level-browser_sort-duration}}`, `{{ui:root_level-browser_sort-progress}}` et `{{ui:root_level-browser_sort-recent}}`. La flèche à côté du bouton de tri (`{{ui:root_level-browser_reverse}}`) inverse l'ordre. `{{ui:root_level-browser_sort-relevance}}` n'a pas de sens

La recherche regarde d'abord les noms des niveaux, puis les auteurs, puis les tags

`{{ui:root_level-browser_filters}}` ouvre une fenêtre avec plus de filtres. La liste derrière elle change à chaque appui :

- `{{ui:root_level-filters_ai}}` - `{{ui:root_level-filters_ai-yes}}`, `{{ui:root_level-filters_ai-no}}` et `{{ui:root_level-filters_ai-unspecified}}`
- `{{ui:root_level-filters_length}}` - le niveau le plus court et le plus long, et s'il faut montrer les niveaux dont la durée est inconnue
- `{{ui:root_level-filters_progress}}` - `{{ui:root_level-filters_progress-unplayed}}`, `{{ui:root_level-filters_progress-started}}`, `{{ui:root_level-filters_progress-cleared}}`, `{{ui:root_level-filters_progress-bot}}`
- `{{ui:root_level-filters_recent}}` - les dernières 24 heures, 7 jours ou 30 jours
- `{{ui:root_level-filters_age}}` - la classification d'âge la plus haute à montrer
- `{{ui:root_level-filters_other}}` - masquer les niveaux protégés par un mot de passe, masquer les niveaux d'une version plus récente du jeu
- `{{ui:root_level-filters_tags}}` - un appui sur un tag l'exige, deux appuis l'excluent

`{{ui:root_level-filters_progress}}` et `{{ui:root_level-filters_recent}}` n'existent que dans la liste du menu principal. La liste de l'éditeur a ses propres filtres.
Le bouton montre combien de filtres sont actifs, et `{{ui:root_level-browser_reset}}` les désactive tous. Les filtres restent en place jusqu'à la fermeture du jeu

Tu as copié un niveau dans le dossier ? Appuie sur `{{ui:root_level-browser_refresh}}` et la liste se met à jour

Un cadenas sur une carte signifie que le niveau est protégé par un mot de passe

Un appui long ou un clic droit sur une carte ouvre un menu : `{{ui:level_passphrase_open}}` et `{{ui:root_level-browser_delete}}`.
`{{ui:root_level-browser_delete}}` sur un niveau du `Workshop` te désabonne de l'élément et supprime ses fichiers. Steam doit être lancé pour cela : sinon Steam télécharge à nouveau le niveau. Les niveaux intégrés ne peuvent pas être supprimés

## Ajouter le niveau de quelqu'un d'autre

Un niveau est un simple dossier de fichiers. Tu peux le mettre dans une archive et l'envoyer à un ami

**Un dossier.** Copie le dossier du niveau dans `levels` et appuie sur `{{ui:root_level-browser_refresh}}`.
Copie le dossier du niveau lui-même : celui qui contient `level.json` (ou `level.blob`) et `metadata.json`

**Une archive.** Ouvre l'éditeur et crée un nouveau niveau avec le générateur `{{ui:gen_level_archive}}`.
Choisis ensuite le fichier avec le bouton `{{ui:editor_create-level_archive-choose}}`

| Fichier | Résultat |
|---|---|
| `.zip`, `.tar.gz` | s'ouvre |
| `.zip` avec son propre mot de passe, `.zip.gpg`, `.tar.gz.gpg` | s'ouvre après `{{ui:editor_create-level_archive-protected}}` |
| `.7z` | refusé pour l'instant. Recompresse-le en zip |
| tout le reste | refusé, [[5_troubleshooting]] |

Une archive renommée s'ouvre quand même : le jeu reconnaît le format aux octets du fichier.
Une archive d'une ancienne version du jeu est mise à jour à l'import

Par défaut, un niveau importé reçoit son propre identifiant. Il n'écrase donc pas un niveau déjà présent sur l'appareil

Plus - [[6_sharing-by-hand]]

## L'écran du niveau

L'écran du niveau montre la couverture, les auteurs, la description et l'auteur de la musique. Il a aussi les boutons `{{ui:level_level-view_authors}}` et `{{ui:level_level-view_licenses}}`

Le nom de l'auteur et la ligne de la musique ouvrent leur propre lien si les métadonnées du niveau en contiennent un

La classification d'âge est fixée par l'auteur du niveau. Le jeu ne la vérifie pas

"Contient du contenu généré par IA" apparaît quand l'auteur a déclaré que le niveau, sa couverture ou une de ses ressources a été généré par IA. C'est aussi une déclaration de l'auteur lui-même. L'absence de cette ligne ne veut pas dire "pas d'IA" : l'auteur peut simplement n'avoir rien dit

Avant une partie, tu peux choisir les conditions :

| Condition | Choix |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}` (la partie ne finit jamais), `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}`, `{{ui:menu_levelview_options-lifes_option-custom}}` (un curseur jusqu'à 16) |
| `{{ui:field_common_speed}}` | `0.5`, `1.0`, `2.0`, `{{ui:menu_levelview_options-lifes_option-custom}}` (un curseur jusqu'à 2). Le niveau et la musique changent ensemble |
| `Checkpoints` | activé ou désactivé, [[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | activé ou désactivé. L'avatar traverse tout, [[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`, [[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | un nombre, `{{ui:level_level-view_seed-randomize}}`, `{{ui:level_level-view_seed-clear}}`. `0` - une nouvelle graine à chaque partie, [[8_determinism]] |

`Jouer` lance la partie

La pause propose `{{ui:game_pause-window_continue-btn}}`, `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}` (une fois un checkpoint atteint), `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}` et `{{ui:game_game-result_back-to-menu}}`. `{{ui:game_game-result_back-to-options}}` revient à l'écran du niveau avec les conditions de départ de la partie, ou à l'onglet `Jouer` de l'éditeur si la partie a été lancée depuis là

## La fenêtre de résultat

La fenêtre affiche `Réussi` ou `{{ui:game_game-result_lose}}` et trois sections : `Progression`, `{{ui:game_game-result_section-damage}}` et `{{ui:game_game-result_section-conditions}}`

- lignes : `Terminé`, `{{ui:game_game-result_checkpoint}}`, `{{ui:field_common_time}}`, `{{ui:game_game-result_length}}`, `{{ui:game_game-result_hits}}`, `{{ui:game_game-result_lives-left}}`, `{{ui:game_game-result_streak}}`
- conditions de la partie : `{{ui:field_common_speed}}`, `{{ui:menu_levelview_options-lifes_title}}`, `{{ui:menu_levelview_options-bot}}`, `{{ui:game_game-result_seed}}`, `Checkpoints`. Pour une partie `{{ui:menu_levelview_options-no-collision_title}}`, `· Sans collision` s'ajoute à `{{ui:menu_levelview_options-lifes_title}}`
- boutons : `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}`, `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}`, `{{ui:game_game-result_back-to-menu}}`

Par défaut, la fenêtre ne s'ouvre pas en cas d'échec. À la place, la partie revient au dernier checkpoint.
Pour changer cela - `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`

## Records

L'écran du niveau a un bloc de record : `{{ui:menu_levelview_record-best}}`, `{{ui:menu_levelview_record-attempts}}` et `{{ui:menu_levelview_record-clears}}` (ou `{{ui:menu_levelview_record-none}}`)

Chaque ensemble de conditions a son propre record : vies, vitesse, checkpoints, collisions et bot. Le bloc montre le record des conditions sélectionnées en ce moment.
Les tentatives et les réussites sont comptées pour toute partie

Comment un record est choisi - [[10_statistics]]

## Marques sur les cartes

| Marque | Ce qu'elle signifie |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | le dossier du Workshop est sur le disque, mais il ne fait pas partie de tes abonnements. Visible seulement quand `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` est activé |
| `{{ui:root_level-entry_unverified}}` | la source du niveau n'a pas répondu |
| `{{ui:root_level-entry_newer-version}}`, `{{ui:root_level-entry_newer-file}}` | cette version du jeu n'ouvre pas le niveau, [[5_troubleshooting]] |
| `{{ui:root_level-entry_level-missing-badge}}` | le dossier n'a pas de `level.json`, le niveau ne peut donc pas être lancé, [[4_level-folder-and-backups]] |
| `{{ui:root_level-entry_meta-missing-badge}}` | le dossier n'a pas de `metadata.json` lisible. La carte montre le nom du dossier, et le niveau se joue, [[4_level-folder-and-backups]] |

## Supprimer un niveau

Appui long ou clic droit sur une carte → `{{ui:root_level-browser_delete}}`. Le jeu demande d'abord une confirmation

Avec le niveau, tu peux supprimer ses statistiques (`{{ui:root_level-delete_statistics}}`) et ses sauvegardes (`{{ui:root_level-delete_backups}}`)

Supprimer un niveau protégé ne demande pas de mot de passe
