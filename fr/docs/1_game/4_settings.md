---
title: Paramètres
date: 2026-10-14
tags: [player]
---

# Paramètres

Les paramètres les plus importants se règlent au premier lancement : le jeu ouvre de lui-même une configuration rapide avec la langue, le volume, les performances et les effets. Une réinitialisation ne touche que les paramètres, les niveaux restent

## Les onglets

| Onglet | Ce qu'il contient |
|---|---|
| `{{ui:settings_general_title}}` | la langue - chacune nommée dans sa propre langue, `Русский (ru)`. `Système (fr)` suit l'appareil et montre quelle langue il a retenue. Aussi le nombre de fichiers de niveau chargés à la fois, le délai d'attente pour un fichier à une adresse web, `{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | le volume : `{{ui:settings_audio_volume}}`, `{{ui:settings_audio_game}}`, `{{ui:settings_audio_ui}}`, `{{ui:settings_audio_editor-ui}}`, `{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | les appareils et la façon de diriger, [[3_controls]] |
| `{{ui:settings_keybindings_label}}` | les raccourcis, surtout ceux de l'éditeur, [[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | l'affichage, les images par seconde, l'antialiasing, `{{ui:settings_graphics-colliders-mode_title}}`, les textures, les effets, le post-traitement |
| `{{ui:settings_interface_label}}` | l'interface en jeu, `{{ui:settings_interface_open-menu-on-lose}}`, `{{ui:settings_interface_menu-background}}`, `{{ui:settings_interface_levels-layout}}`, l'orientation de l'écran, la superposition des statistiques |
| `{{ui:settings_game-editor_title}}` | les paramètres propres à l'éditeur, y compris son propre `{{ui:settings_interface_levels-layout}}` |
| `{{ui:settings_profile_tab}}` | tes statistiques, [[10_statistics]] |
| `{{ui:settings_other_title}}` | le nettoyage du stockage, le transfert de profil et l'état de Steam Cloud ([[14_profile-transfer]]), l'accès aux dossiers sur Android, le mode anonyme, `{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}` choisit ce qu'on voit derrière les boutons du menu principal : une arène vivante où un bot esquive des attaques, un champ de formes qui tournent, ou rien

`{{ui:settings_interface_levels-layout}}` choisit comment s'ouvre la sélection des niveaux - une `{{ui:enum_level-browser-layout_grid}}` de couvertures ou une `{{ui:enum_level-browser-layout_list}}` de lignes avec descriptions. Il y en a deux : celui de l'onglet `{{ui:settings_interface_label}}` est pour le menu (`{{ui:enum_level-browser-layout_grid}}` par défaut), celui de l'onglet `{{ui:settings_game-editor_title}}` est pour l'éditeur (`{{ui:enum_level-browser-layout_list}}` par défaut). Le bouton à côté du champ de recherche change quand même la vue jusqu'à ce que tu quittes cet écran

## Configuration rapide

`{{ui:settings_quick-setup_title}}`, un bouton de l'onglet `{{ui:settings_general_title}}` au-dessus de `{{ui:settings_general-open_folder}}`, pose quelques-unes des questions les plus importantes, une catégorie par page. Au tout premier lancement, elle s'ouvre d'elle-même, avant la proposition du tutoriel.
Chaque réponse a une ligne qui dit ce qu'elle fait. Les pages s'ouvrent dans n'importe quel ordre, `{{ui:settings_quick-setup_next}}` ne fait que suggérer la suivante

| Page | Question | Réponses | Ce que ça change |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}` et chaque langue du jeu, nommée dans sa propre langue | la même chose que sur l'onglet `{{ui:settings_general_title}}` |
| | `{{ui:settings_audio_volume}}` | un curseur | la même chose que sur l'onglet `{{ui:field_common_audio}}` |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`, `{{ui:settings_quick-setup_performance-economy}}`, `{{ui:settings_quick-setup_performance-recommended}}`, `{{ui:settings_quick-setup_performance-max}}` | l'échelle de rendu (PC), l'antialiasing, la taille des textures, les images par seconde des effets - mais pas la limite d'images par seconde : chaque réponse tourne à la fréquence de l'écran. `{{ui:settings_quick-setup_performance-minimum}}` désactive aussi les effets de particules et le post-traitement et limite les images à 512 |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`, `{{ui:settings_quick-setup_comfort-soft}}`, `{{ui:settings_quick-setup_comfort-minimal}}` | chaque effet de post-traitement et l'éclatement de l'avatar. `{{ui:settings_quick-setup_comfort-soft}}` désactive les glitchs, le grain, le flou, la distorsion de l'objectif et les franges de couleur |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | rien ici : le tutoriel permet d'essayer chaque schéma de contrôle et de choisir le tien. Il s'ouvre depuis le menu principal ou le bac à sable |

La réponse marquée `{{ui:settings_quick-setup_default-badge}}` est celle avec laquelle le jeu démarre sur ton appareil. Un choix s'applique tout de suite et se voit dans les paramètres complets.
Si tes paramètres ne correspondent à aucune réponse, aucune n'est mise en avant et une ligne le dit - ce sont tes propres paramètres, et un appui les remplace

## Sections repliées

Les onglets longs sont découpés en sections. Ce qu'on change souvent est ouvert, les réglages fins sont repliés : une section s'ouvre par son titre.
Le bouton à côté de la réinitialisation de l'onglet replie ou déplie toutes les sections à la fois

Sur l'onglet `{{ui:settings_controls_title}}`, seul l'appareil que tu as en main est ouvert

## Réinitialisation

Chaque onglet a sa propre réinitialisation.
`{{ui:settings_other_reset}}` dans `{{ui:settings_other_title}}` réinitialise tous les onglets à la fois

Une réinitialisation ne touche que les paramètres. Tes niveaux restent

## La ligne de version

L'écran des paramètres a une ligne de version. Un clic dessus la copie

Elle ressemble à ceci : `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`.
C'est la ligne à citer dans un rapport de bug, [[11_help]]

## Graphismes

**Antialiasing.** Sur PC, la valeur par défaut est `{{ui:enum_anti-aliasing-type_msaa}}`. Un téléphone démarre sans antialiasing. Chaque forme du jeu est une vraie géométrie, et `{{ui:enum_anti-aliasing-type_msaa}}` lui donne des bords nets sans flou sur toutes les plateformes

`{{ui:enum_anti-aliasing-type_fxaa}}` est pour les téléphones faibles. C'est une seule passe sur tout l'écran, et son coût est constant. Le coût de `{{ui:enum_anti-aliasing-type_msaa}}` augmente quand beaucoup de formes transparentes sont dessinées les unes sur les autres

Le TAA n'est volontairement pas proposé. Il laisse une traînée derrière les balles rapides, et son tremblement gêne les effets de glitch

**Images par seconde.** La fréquence d'images cible se règle à la main, pas par la synchronisation verticale. Ainsi, le timing d'un niveau est le même sur un écran à 60 Hz et à 144 Hz.
Tant que `{{ui:settings_graphics_vsync}}` est activé (PC uniquement), la limite d'images par seconde ne fait rien

> [!tip] Recommandation
> Sur un appareil faible, baisse d'abord **l'échelle de rendu** sous 1. Elle ne coûte que de la netteté, et l'interface reste en taille réelle. PC uniquement

Plus - [[2_mobile-devices]]

## Mode colliders uniquement

Un mode pour s'entraîner, une section repliée de l'onglet `{{ui:settings_graphics_title}}`. Avec `{{ui:settings_graphics-colliders-mode_active}}` activé, un niveau en jeu dessine chaque hitbox comme un aplat d'une seule couleur sur un fond uni, et rien d'autre.
Disparaissent : l'apparence des formes elles-mêmes, les formes sans collider, les effets, les textes, le post-traitement et l'arrière-plan du thème.
Ne changent pas : la musique, les collisions, la caméra et ses tremblements, les checkpoints, l'interface et les statistiques - une partie dans ce mode compte comme n'importe quelle autre.
Ton avatar est dessiné comme d'habitude

Le mode ne fonctionne que pendant qu'on joue des niveaux. L'éditeur, le bac à sable et l'arrière-plan du menu sont dessinés comme d'habitude

| Option | Ce qu'elle fait |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | activée (par défaut) - les aplats sont semi-transparents selon l'alpha de la couleur, et les obstacles qui se chevauchent apparaissent plus sombres. L'alpha ne descend jamais sous 0,15. Désactivée - chaque aplat est opaque, et l'alpha de la couleur est verrouillé |
| `{{ui:settings_graphics-colliders-mode_color}}` | la couleur des aplats, rouge avec un alpha de 0,6 par défaut. La vue des colliders de l'éditeur utilise la même teinte avec sa propre opacité |
| `{{ui:settings_graphics-colliders-mode_background}}` | ce qui est dessiné derrière les aplats, gris foncé par défaut - pas noir, pour que le bord du cadre de la caméra se voie sur les bandes noires qui l'entourent |

Les deux couleurs sont repliées sous leur propre libellé : déplie celle qu'il te faut pour obtenir sa roue chromatique

## Mode anonyme

S'active dans `{{ui:settings_other_title}}` → `{{ui:settings_other_suppress-game-saves}}`

Tant que le mode est activé, le jeu n'enregistre rien de ce qui lui est propre. `settings.json`, les statistiques globales et les statistiques des niveaux restent intacts sur le disque.
Un paramètre modifié fonctionne quand même jusqu'à la fermeture du jeu

Le travail sur les niveaux est enregistré comme d'habitude : enregistrer, exporter, importer, copier et supprimer.
L'enregistrement automatique et les sauvegardes de l'éditeur fonctionnent aussi, ils ont leur propre interrupteur

Le mode dure jusqu'à la fermeture du jeu et n'est mémorisé nulle part

Si tu le désactives, les paramètres actuels sont enregistrés. Tout ce qui a été joué pendant ce temps est abandonné

> [!info] Bon à savoir
> Le mode s'active aussi tout seul. L'[[12_launch-arguments|argument de lancement]] `--suppress-game-saves` l'active pour tout le lancement, et il ne peut pas être désactivé dans le jeu. Des paramètres ou des statistiques d'une version plus récente du jeu l'activent aussi. Le jeu demande alors à chaque lancement s'il faut les garder ou les écraser avec les valeurs par défaut
