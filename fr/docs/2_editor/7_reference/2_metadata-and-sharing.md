---
title: Métadonnées et partage d'un niveau
date: 2026-10-11
tags: [level_author]
---

# Métadonnées et partage d'un niveau

Les métadonnées sont la couverture du niveau : nom, description, image, auteurs, classification par âge et avertissements sur le contenu. Aujourd'hui, un niveau arrive à quelqu'un d'autre sous forme de dossier ou par le Steam Workshop

> [!warning] Avertissement
> Le serveur officiel et le site des niveaux n'existent pas encore. Ils arrivent dans une mise à jour après `gv 1.0.0`. D'ici là, un niveau se partage sous forme de dossier ou, dans une version Steam, par le Steam Workshop. Les deux façons sont décrites à la fin de la page

## Le fichier de métadonnées

La couverture du niveau vit dans son propre fichier. Elle se lit sans le niveau lui-même.
Ainsi, un catalogue peut afficher mille niveaux sans en ouvrir un seul

## Identité

Le niveau a un ID stable. Il survit aux changements de nom et aux déplacements de dossier.
Les scores et les commentaires y sont liés, pas au nom

Il y a aussi ton propre numéro de version du niveau. Augmente-le quand tu le modifies. Il n'a aucun rapport avec la version du format

## Nom, description et logo

**Le nom et la description** peuvent être traduits en plusieurs langues. Ils n'ont pas de clés : tu écris le texte de chaque langue directement sur place.
Le texte est stocké dans le niveau. C'est ce qui le distingue des textes de l'interface du jeu

**Le logo** est un fichier à côté du niveau, `logo.png` ou `logo.jpg`

Le logo a sa propre fiche, comme une ressource : licence, auteurs, lien, génération par IA. Ouvre-la avec le bouton `{{ui:settings_level-settings_metadata-level-logo-metadata}}` sous le logo.
Une nouvelle image remet la fiche à zéro, et retirer le logo retire aussi sa fiche. Plus - [[4_resource-record]]

## Auteurs

**Les auteurs** sont les personnes qui ont fait le niveau : le mapping, le design.
Les auteurs des ressources sont crédités à part, dans la fiche propre à chaque ressource.
Les textures, les polices et l'audio ont des fiches, tout comme les thèmes, les effets, les formes et les prefabs

> [!caution] Attention
> Confonds ces deux listes, et le musicien se retrouve sans crédit

## Classification par âge

**La classification par âge** est un seul nombre, l'âge minimum. Elle s'affiche sous la forme "12+". Deux classifications se comparent comme de simples nombres

`{{ui:enum_age-rating_unrated}}` vaut zéro. Cela veut dire que rien n'a été déclaré, pas que le contenu est sans risque

> [!info] Bon à savoir
> Il y a une seule échelle, sans champs séparés pour ESRB, PEGI et RARS. Les niveaux des joueurs ne passent devant aucun organisme de classification, donc une valeur pour chacun serait une supposition

> [!caution] Attention
> La classification est le seul avertissement sur la carte. Si le niveau clignote ou devient bruyant, dis-le dans la description. Dans un jeu de drops et d'effets de glitch, les flashs sont courants, et cette ligne est tout l'avertissement que reçoit un joueur

## Génération par IA

**`Génération par IA`** indique si le contenu propre du niveau a été généré par IA : le design, les objets, les textes.
Chaque ressource et le logo l'indiquent pour eux-mêmes, dans leurs propres fiches

| Valeur | Sens |
|---|---|
| `{{ui:enum_ai-generation_not-specified}}` | rien n'a été déclaré. C'est la valeur par défaut |
| `{{ui:enum_ai-generation_no}}` | tu déclares qu'aucune génération par IA n'a été utilisée |
| `Généré par IA` | tu déclares que le contenu a été généré par IA |

`{{ui:enum_ai-generation_not-specified}}` veut dire "inconnu". Ce n'est pas la même chose que "non"

L'écran du niveau dans le menu affiche "Contient du contenu généré par IA" si le niveau, son logo ou une ressource indique `Généré par IA`

Un assistant IA règle lui-même `{{ui:enum_ai-generation_yes}}`, dans la même étape d'annulation que son premier lot de modifications du niveau. Plus - [[7_ai-assistant]]

> [!info] Bon à savoir
> Comme la classification par âge, c'est la propre déclaration de l'auteur. Le jeu ne la vérifie pas

## Partager un niveau aujourd'hui

1. Compresse le dossier du niveau en zip et envoie-le
2. L'autre personne le décompresse dans son propre dossier `levels`
3. Le niveau s'ouvre. Rien ne s'installe ni ne s'importe

> [!warning] Avertissement
> Chaque fichier du dossier du niveau part avec lui, même un fichier inutilisé. Fais le ménage avant l'envoi

## Steam Workshop

L'onglet `{{ui:settings_level-settings_publication}}` des paramètres du niveau envoie le niveau : sous forme d'archive, et vers le Steam Workshop dans une version Steam. Plus - [[17_publishing]]

Les versions Steam lisent aussi le Workshop : elles affichent et lancent les niveaux de tes abonnements. Plus - [[2_playing-levels]]

Avant de publier, lis [[1_licensing-basics|la section sur les droits]]. Le rapport de l'onglet `{{ui:settings_level-settings_publication}}` évalue le niveau et chaque fiche de ressource selon ces règles

## Partager un niveau plus tard

Un serveur et un site officiels sont prévus

Ensuite : [[4_resource-record|La fiche d'une ressource]], [[4_level-folder-and-backups|Le dossier du niveau et les sauvegardes]]
