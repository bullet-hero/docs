---
title: Installation
date: 2026-10-14
tags: [player]
---

# Installation

Le jeu garde les niveaux, les paramètres et les statistiques dans un seul dossier de données. Mettre à jour ne présente aucun risque : une nouvelle version lit toutes les anciennes données. Sur Android, désinstaller le jeu efface aussi les niveaux

Le téléchargement est ici - [[download]]

## Où sont tes fichiers

| Système | Dossier |
|---|---|
| Windows | `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

Le plus rapide est de l'ouvrir depuis le jeu : `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`

Ce qu'il contient :

| Dossier | Contenu |
|---|---|
| `levels` | tes niveaux, chacun dans son propre dossier |
| `backups` | les enregistrements automatiques de l'éditeur |
| `stats` | les statistiques |
| `settings.json` | les paramètres |
| `reports` | les rapports d'erreur |

## Désinstallation

Sur Windows, Linux et Mac, la version gratuite est livrée avec un désinstalleur à côté du jeu : `unins000.exe` sur Windows, `unins000` sur Linux, et `unins000` à côté de `Bullet Hero.app` sur Mac. Lance-le et il retire le jeu tout seul, sans poser une seule question. Tes niveaux, tes paramètres et tes statistiques restent dans le dossier de données

Il ne retire que les fichiers du jeu lui-même. Tout ce que tu as mis toi-même dans le dossier du jeu reste, et le dossier ne disparaît qu'une fois vide. Si le jeu tourne, le désinstalleur le ferme d'abord, comme le ferait son bouton de fermeture, et le serveur MCP de l'IA avec lui. Un niveau aux modifications non enregistrées les perd, donc enregistre-le avant de désinstaller

Installé avec l'installateur Windows, le jeu se retire comme n'importe quel autre programme, dans les Paramètres de Windows, sous Applications

Une version de boutique se retire par sa boutique

## Mise à jour

Une nouvelle version du jeu lit toutes les anciennes données sans problème, quelle que soit la mise à jour et quoi qu'elle ait changé

Une ancienne version n'ouvre pas les niveaux d'une version plus récente. Si le jeu te demande de le mettre à jour, mets-le à jour

Dans les versions Google Play et RuStore, le menu principal propose une nouvelle mise à jour, qui se télécharge en arrière-plan. Quand elle est prête, le menu principal affiche `{{ui:menu_update-ready_text}}` - appuie sur `{{ui:menu_update-ready_install-btn}}`. Après un niveau terminé, elles peuvent te demander de noter le jeu

> [!caution] Attention
> Sur Android, désinstaller le jeu supprime aussi tous tes niveaux. Exporte le profil avant de désinstaller - [[14_profile-transfer]]
