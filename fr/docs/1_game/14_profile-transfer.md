---
title: Transfert de profil
date: 2026-10-14
tags: [player]
---

# Transfert de profil

Tout ton profil tient dans un seul fichier zip : niveaux, statistiques, paramètres et bibliothèque. Exporte-le avant de réinstaller ou de passer à un autre appareil, puis importe-le là-bas

Les boutons sont dans `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`. Cela fonctionne sur Windows, Mac, Linux et Android. Ce n'est pas disponible sur iOS

## Ce qui va dans le fichier

| Partie | Dans le dossier de données | Cochée par défaut |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | oui |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | oui |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | oui |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | oui |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | non |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | non |
| `{{ui:settings_profile-transfer_category-recordings}}` | `recordings` | non |

Le fichier est un zip ordinaire et s'ouvre dans n'importe quel archiveur. Il contient les mêmes dossiers que le dossier de données ([[1_installation]]), plus `profile.json`, qui décrit le fichier

## Export

1. Appuie sur `{{ui:settings_profile-transfer_export}}`
2. Coche les parties qu'il te faut
3. Choisis où enregistrer le fichier

L'export fonctionne partout où les paramètres s'ouvrent : dans le menu principal, dans une partie en pause et dans l'éditeur. Les statistiques sont d'abord écrites sur le disque, donc le fichier est à jour

## Import

1. Ouvre les paramètres depuis le menu principal et appuie sur `{{ui:settings_profile-transfer_import}}`
2. Choisis le fichier zip
3. Coche les parties et choisis le mode
4. Confirme

L'import ne fonctionne que depuis le menu principal. Un niveau en cours ou un éditeur ouvert tient ses fichiers, et ils ne peuvent pas être remplacés sous lui

| Mode | Ce qui se passe |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | chaque partie cochée est vidée et remplie depuis le fichier |
| `{{ui:settings_profile-transfer_mode-merge}}` | les niveaux sont ajoutés. Un niveau présent des deux côtés est remplacé en entier par la copie la plus récente. Les statistiques gardent la plus grande valeur de chaque compteur et le meilleur record. Les fichiers de la bibliothèque, les enregistrements automatiques et les rapports sont seulement ajoutés, les tiens restent |

Chaque import demande une confirmation de plus avant d'écrire quoi que ce soit. Un remplacement nomme les parties qu'il vide, une fusion dit combien de niveaux elle ajoute, remplace et garde

**Des paramètres d'un autre type d'appareil.** Un profil de téléphone importé sur un ordinateur (ou l'inverse) garde tes propres contrôles et graphismes. Tout le reste vient du fichier

Le jeu refuse un fichier d'une version plus récente du jeu - mets d'abord le jeu à jour. Il refuse aussi un fichier qui n'est pas un zip, un zip qui n'est pas un profil, un zip protégé par mot de passe et un fichier endommagé. Rien n'est modifié dans aucun de ces cas

## Sauvegarde

Avant tout import, le jeu enregistre les parties qu'il s'apprête à remplacer dans une seule sauvegarde. Elle se trouve dans le dossier `profile-backups` à l'intérieur du dossier de données. Il n'y en a qu'une : l'import suivant l'écrase

- `{{ui:settings_profile-transfer_backup-restore}}` remet la sauvegarde en place. Ce qu'elle remplace devient la nouvelle sauvegarde, donc une restauration peut aussi être annulée
- `{{ui:settings_profile-transfer_backup-save-as}}` enregistre une copie où tu veux
- `{{ui:settings_profile-transfer_backup-delete}}` la supprime
- `{{ui:settings_profile-transfer_clear-cache}}` supprime tout le dossier `profile-backups` : la sauvegarde et tout ce qu'un transfert interrompu a laissé

`{{ui:settings_profile-transfer_backup-to-folder}}` est coché par défaut pendant un import : le jeu demande tout de suite où garder une copie hors du jeu

> [!caution] Attention
> Sur Android, la sauvegarde se trouve dans le dossier de données du jeu et est supprimée avec le jeu. Avant de désinstaller, exporte le profil ou enregistre la sauvegarde ailleurs

Si le jeu se ferme au milieu d'un import, le lancement suivant remet le profil tel qu'il était

## Steam Cloud

Dans la version Steam, ton profil suit ton compte Steam tout seul. Il n'y a pas de bouton : le jeu se synchronise une fois au lancement, envoie ce qui change pendant que tu joues et se synchronise une dernière fois à la fermeture

L'interrupteur appartient à Steam : la case Steam Cloud dans les propriétés du jeu sur Steam. Son état et l'heure de la dernière synchronisation s'affichent dans `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_cloud_title}}`

| Partie | Quand les deux appareils l'ont modifiée |
|---|---|
| `{{ui:settings_profile-transfer_category-statistics}}` | chaque compteur garde la valeur la plus grande et le meilleur record, rien ne se perd |
| `{{ui:settings_profile-transfer_category-settings}}` | la copie la plus récente l'emporte. `{{ui:settings_graphics_title}}` et `{{ui:settings_controls_title}}` restent toujours ceux de chaque appareil |
| `{{ui:settings_profile-transfer_category-levels}}` | la copie la plus récente d'un niveau l'emporte en entier. L'autre va dans les sauvegardes de l'éditeur sur l'appareil qui a perdu |
| `{{ui:settings_profile-transfer_category-library}}` | la copie la plus récente de chaque fichier l'emporte |

- Un niveau supprimé sur un appareil est supprimé sur les autres aussi. Chacun garde son dernier état dans les sauvegardes de l'éditeur
- Les statistiques supprimées sur un appareil sont supprimées sur les autres aussi. Si un autre appareil a joué depuis la dernière synchronisation, sa progression est gardée
- Un niveau plus grand que l'espace que Steam laisse au jeu reste seulement sur son appareil
- `{{ui:settings_profile-transfer_category-backups}}`, `{{ui:settings_profile-transfer_category-reports}}` et `{{ui:settings_profile-transfer_category-recordings}}` ne sont pas synchronisés
- Une copie dans le cloud écrite par une version plus récente du jeu n'est pas touchée tant que le jeu n'est pas mis à jour sur cet appareil
- Le niveau ouvert dans l'éditeur n'est pas remplacé : il se synchronise au lancement suivant
- Avec `{{ui:settings_other_suppress-game-saves}}` activé, rien n'est synchronisé

## Passer d'une version à l'autre sur Android

Une copie du jeu installée depuis un fichier (itch.io et autres) ne peut pas être mise à jour depuis Google Play, et inversement. Les versions sont signées différemment, donc Android refuse la mise à jour. Pour changer :

1. Exporte le profil et enregistre le fichier hors du jeu
2. Désinstalle le jeu
3. Installe l'autre version
4. Importe le profil
