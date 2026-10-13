---
title: Le dossier du niveau et les sauvegardes
date: 2026-10-11
tags: [level_author]
---

# Le dossier du niveau et les sauvegardes

Un niveau vit dans son propre dossier, dans levels à l'intérieur du dossier du jeu. Ne renomme pas les fichiers qu'il utilise, et une sauvegarde complète est une copie du dossier du niveau

## Ce que contient le dossier

Le dossier du niveau se trouve dans `levels`, à l'intérieur du dossier du jeu. Où se trouve le dossier du jeu - [[1_installation]]

| Fichier | Ce que c'est |
|---|---|
| `level.json` | le contenu du niveau. Au format binaire - `level.blob` |
| `metadata.json` | nom, description, auteurs, tags. Au format binaire - `metadata.blob` |
| `logo.png` ou `logo.jpg` | la couverture |
| le morceau, les textures, les polices | tout le reste de ce qu'utilise le niveau, juste à côté de `level.json` |

À côté de `levels` se trouve `resources` avec les bibliothèques de l'appareil : `themes`, `effects`, `shapes`, `prefabs`.
Elles ne font pas partie du niveau. Tu y exportes ce que tu veux réutiliser, et tu importes depuis là

Le même dossier `resources` contient `collections`, un dossier par collection. Plus - [[16_library-and-collections]]

Un niveau envoyé à quelqu'un d'autre emporte en lui tout ce dont il a besoin. Les bibliothèques ne voyagent pas avec lui

## Ce qu'il ne faut pas toucher à la main

> [!caution] Attention
> Ne renomme pas les fichiers qu'utilise le niveau. Les références vers eux sont stockées par nom, un fichier renommé est donc un fichier manquant

Ne modifie pas `level.json` dans un éditeur de texte pendant que le niveau est ouvert dans le jeu. L'enregistrement depuis l'éditeur écrase tes modifications sans prévenir

Ne garde dans le dossier du niveau rien que le niveau n'utilise pas. Tout voyage avec le dossier

Le format du fichier est déterminé par l'extension, pas par un champ à l'intérieur. Changer le format dans l'éditeur écrit donc un nouveau fichier et supprime l'ancien.
Sinon deux fichiers resteraient sur le disque, sans moyen de savoir lequel est le vrai

## Quand l'un des deux fichiers manque

Un dossier qui n'a que l'un des deux fichiers `level.json` et `metadata.json` apparaît quand même dans la liste des niveaux. Les fichiers binaires `level.blob` et `metadata.blob` comptent de la même façon

| Manquant | Dans le jeu | Dans l'éditeur |
|---|---|---|
| `level.json` | la carte est complète, mais le niveau ne peut pas être lancé | restauré depuis la copie automatique la plus récente. Sans copie, un niveau vide est écrit |
| `metadata.json` | la carte affiche le nom du dossier, et le niveau se joue | un nouveau `metadata.json` est écrit avec le nom du dossier et les paramètres par défaut |

Un `metadata.json` que le jeu ne peut pas lire compte comme manquant. L'éditeur le déplace vers `metadata.json.bak` avant d'écrire le nouveau, rien n'est donc perdu

L'éditeur demande avant d'écrire quoi que ce soit. Un niveau intégré ou du `Workshop` n'est jamais modifié sur place : sans `metadata.json`, il est proposé en copie, et sans `level.json`, il ne peut pas être ouvert

## Sauvegardes et récupération

**Une sauvegarde complète est une copie du dossier du niveau.** Elle contient tout, ressources comprises.
Fais une copie avant chaque grosse refonte et date-la

**La sauvegarde automatique ne garde que le fichier du niveau.** Ni métadonnées, ni morceau, ni textures.
Chaque sauvegarde automatique met une copie dans `backups/<level id>/` du dossier du jeu, en dehors de `levels`. `25` copies sont conservées. Comment restaurer une copie - [[4_not-losing-work#L'enregistrement automatique]]

**Un niveau `Json` qui ne s'ouvre plus n'est pas perdu.** Le fichier est du texte, tu peux donc l'ouvrir dans n'importe quel éditeur de texte et le corriger à l'œil. Le jeu lui-même n'ouvre pas un niveau qui échoue au chargement, l'onglet `{{ui:settings_level-settings_raw}}` n'aide donc pas ici. Il montre le modèle d'un niveau déjà ouvert

Un `Blob` ne se sauve pas de cette façon. Il est binaire, et un fichier endommagé est refusé en entier plutôt que lu en partie

Ce qu'il faut savoir avant de modifier dans l'onglet `{{ui:settings_level-settings_raw}}` - [[4_not-losing-work#L'onglet des données brutes]]

Ensuite : [[4_not-losing-work]], [[2_metadata-and-sharing]]
