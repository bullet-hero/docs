---
title: Statistiques
date: 2026-10-02
tags: [advanced_player]
---

# Statistiques

Le jeu compte les tentatives, les morts, les impacts et le temps pour chaque niveau et pour tout l'appareil. Tout est stocké localement dans le dossier stats. Un record est gardé séparément pour chaque ensemble de conditions de partie

## Deux fichiers

| Fichier | Ce qu'il contient |
|---|---|
| `stats/statistics.json` | tout ce qui te concerne : sur tous les niveaux et tous les écrans |
| `stats/<LevelId>.json` | tout ce que tu as fait avec un niveau |

Les fichiers sont en JSON, les heures sont en UTC. Rien n'est envoyé nulle part

Le dossier `stats` se trouve à côté de `levels` dans le dossier du jeu, [[1_installation]]. Il n'est jamais dans un niveau.
Ainsi, un niveau envoyé à un ami n'arrive pas déjà réussi. Et ta progression survit à la suppression du niveau et à son nouvel import

## L'onglet "Profil"

`{{ui:settings_common_title}}` → `{{ui:settings_profile_tab}}` montre le fichier commun de l'appareil :

| Section | Lignes |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`, `{{ui:settings_profile_last-played}}`, `{{ui:settings_profile_launches}}`, `{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`, `{{ui:settings_profile_game-time}}`, `{{ui:settings_profile_editor-time}}`, `{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`, `{{ui:settings_profile_clears}}`, `{{ui:settings_profile_deaths}}`, `{{ui:settings_profile_hits}}`, `{{ui:settings_profile_levels-played}}`, `{{ui:settings_profile_levels-cleared}}`, `{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`, `{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`, `{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`, `{{ui:settings_profile_tutorial-first}}`, `{{ui:settings_profile_tutorial-last}}` - un tutoriel ne compte comme terminé que quand chaque étape du [[13_sandbox|tutoriel du bac à sable]] est faite |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`, `{{ui:settings_profile_levels-deleted}}`, `{{ui:settings_profile_objects}}`, `{{ui:settings_profile_operations}}`, `{{ui:settings_profile_generators}}`, `{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`, `{{ui:settings_profile_device-touch}}`, `{{ui:settings_profile_device-gamepad}}`, `{{ui:settings_profile_device-gyro}}` |

Le temps est compté en secondes réelles, pas en temps du niveau. Le ralenti à un checkpoint et une partie à demi-vitesse comptent pour la durée qu'ils ont réellement prise

Les lignes des appareils montrent quel appareil a dirigé l'avatar en jeu. Un appareil simplement connecté ne compte pas

## Par niveau

Le fichier d'un niveau contient :

- quand tu y as joué pour la première et la dernière fois
- le temps réel passé dans le niveau et le nombre de sessions
- les tentatives (chaque redémarrage en est une nouvelle), les réussites, les morts, les impacts, les dashs
- les retours à un checkpoint et les parties abandonnées
- le point le plus loin atteint et la première réussite
- où tu meurs dans le niveau : par part de la longueur et par checkpoint

## Records

Un record est gardé par conditions de partie : vies, vitesse, checkpoints activés ou non, collisions activées ou non, et le bot.
La vitesse compte jusqu'au centième, exactement comme à l'écran

Le mode zen (0 vie) compte quand même les impacts : chaque collision entre dans ses chiffres, seules les vies et la fin de la partie sont épargnées

Une partie bat le record aux mêmes conditions si, dans cet ordre :

1. elle est allée plus loin
2. elle a pris moins d'impacts
3. elle s'est terminée avec plus de vies
4. elle a utilisé moins de dashs

Un record enregistre aussi la graine de la partie et la version du niveau à ce moment.
La version ne fait pas partie des conditions. Ainsi, un record établi avant que le niveau soit retravaillé reste visible, avec la version affichée à côté

**Une partie lancée depuis l'éditeur compte, mais n'établit aucun record.** Elle s'ajoute aux tentatives, aux morts et aux impacts. Elle ne donne ni record, ni meilleure progression, ni première réussite, parce que le niveau n'existait qu'en mémoire

## Écrire, supprimer, geler

Le jeu écrit les statistiques toutes les 30 secondes. Et immédiatement à la fin d'une partie, à un changement d'écran et en quittant.
Un plantage coûte au plus 30 secondes de données

- **Supprimer :** `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_other_cache-title}}`. Tu y trouves `{{ui:settings_other_cache-orphan-statistics}}` et `{{ui:settings_other_cache-all-statistics}}`
- **Supprimer avec le niveau :** supprimer un niveau propose `{{ui:root_level-delete_statistics}}`
- **Geler :** le mode anonyme arrête toute écriture jusqu'à la fermeture du jeu, [[4_settings]]
- **Emporter sur un autre appareil :** exporte le profil et importe-le là-bas. Une fusion garde la plus grande valeur de chaque compteur, [[14_profile-transfer]]

> [!warning] Avertissement
> Un dossier de niveau copié à la main garde l'identifiant du niveau. L'original et la copie partagent un même fichier de statistiques
