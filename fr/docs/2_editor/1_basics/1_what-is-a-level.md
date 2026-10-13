---
title: Ce qu'est un niveau
date: 2026-10-02
tags: [level_author]
---

# Ce qu'est un niveau

Un niveau est un dossier ordinaire sur le disque : le fichier du niveau, les métadonnées et tout ce qu'il utilise. Construis-le en Json et transmets-le comme une copie du dossier, rien n'est à installer

## Ce que contient le dossier

Le dossier n'est ni une ligne dans une base de données ni une archive chiffrée

Il y a deux fichiers principaux :
- `level.json` - le niveau lui-même : objets, images clés, thèmes, ressources
- `metadata.json` - la couverture : nom, description, auteurs, tags, durée

À côté se trouve tout ce que le niveau utilise : le morceau, les textures, les polices.
Le jeu n'embarque aucune texture. Tout ce que tu vois dans un niveau est soit une forme intégrée, soit un fichier de ce dossier

La couverture est un fichier à part, pour que lister mille niveaux ne signifie pas ouvrir mille niveaux

La liste complète des fichiers - [[4_level-folder-and-backups]]

## Json ou Blob

Tu choisis le format du fichier à la création du niveau :

| Format | Ce que c'est |
|---|---|
| `Json` | du texte brut, s'ouvre dans n'importe quel éditeur et se corrige à la main |
| `Blob` | un fichier binaire, se charge des dizaines de fois plus vite et pèse trois fois moins, illisible à l'œil |

> [!tip] Recommandation
> Construis le niveau en `Json` et convertis-le en `Blob` une fois terminé. Si le niveau ne s'ouvre plus, `Json` se lit et se corrige à la main. `Blob` est presque irréparable : un seul octet endommagé fait échouer le contrôle d'intégrité

## Comment transmettre un niveau

Un niveau voyage par copie. Compresse le dossier, envoie-le, décompresse-le, ouvre-le.
Rien n'est installé, inscrit ni importé

Sur PC, ça marche toujours. Sur un téléphone - partout où le système te laisse entrer

Ce qui en découle :
- une sauvegarde d'un niveau est une copie du dossier
- ne renomme pas les fichiers dans le dossier : les ressources sont retrouvées par leur nom
- un niveau `Json` que l'éditeur refuse d'ouvrir peut encore se lire à l'œil. L'onglet `{{ui:settings_level-settings_raw}}` ne montre qu'un niveau déjà ouvert

> [!caution] Attention
> Ne modifie pas `level.json` dans un éditeur de texte pendant que le niveau est ouvert dans le jeu. L'enregistrement depuis l'éditeur écrase tes modifications sans prévenir

## Le format est ouvert

Le modèle de données des niveaux vit dans un dépôt séparé sous licence MIT - [bullet-hero/sdk](https://github.com/bullet-hero/sdk).
Un niveau peut donc se lire sans le jeu, et tu peux écrire ton propre outil pour le format. Un défaut du format se voit aussi de l'extérieur

Plus sur le format - [[3_sdk/index]]

Ensuite : [[2_first-level]], [[4_level-folder-and-backups]]
