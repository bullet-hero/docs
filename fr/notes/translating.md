---
title: Traduire
date: 2026-10-13
tags: [contributor]
---

# Traduire

Une traduction est une copie du fichier anglais au même chemin dans le dossier de ta langue, où seul le texte est traduit. Un fait qui apparaît dans une langue est reporté dans toutes les autres

## Des chemins en miroir

Chaque page se trouve au même chemin, avec le même nom de fichier, dans chaque dossier de langue :

```
en/docs/2_editor/4_craft/3_difficulty-curve.md
ru/docs/2_editor/4_craft/3_difficulty-curve.md
zh/docs/2_editor/4_craft/3_difficulty-curve.md
ja/docs/2_editor/4_craft/3_difficulty-curve.md
ko/docs/2_editor/4_craft/3_difficulty-curve.md
es/docs/2_editor/4_craft/3_difficulty-curve.md
fr/docs/2_editor/4_craft/3_difficulty-curve.md
```

Ce qui reste inchangé :

- le nom du fichier et le nom de chaque dossier, préfixes compris
- `date` et `tags` dans le frontmatter (`title` est traduit)
- les `[[wiki-links]]` : leurs cibles sont des noms de fichiers, identiques dans toutes les langues
- les liens externes, les noms d'images, les blocs de code et le code en ligne : fichiers, champs, clés, valeurs, commandes
- la structure : les mêmes titres dans le même ordre, les mêmes listes, tableaux et encadrés

Les titres des encadrés sont traduits dans la langue de la page. Plus - [[style-guide]]

## L'anglais sert de repli

Quand une page manque dans une langue, le site affiche la page anglaise avec un avertissement.
L'inverse ne fonctionne pas : une page qui n'existe que dans `ru/` donne une 404 à un lecteur anglophone

> [!caution] Attention
> N'ajoute jamais une page dans une autre langue avant qu'elle n'apparaisse dans `en/`. Les lecteurs de toutes les autres langues tomberont sur un lien cassé

## Chaque langue porte chaque fait

L'anglais ne fait référence que pour les adresses, pas pour le contenu.
Un fait peut apparaître d'abord dans n'importe quelle langue, puis il est reporté dans toutes les autres. Après une modification, chaque version contient tout ce que savent toutes les versions

- **Ajouter, jamais retirer.** Une information manquante est écrite dans chaque langue où elle manque
- **Les contradictions ne se résolvent pas au hasard.** Deux versions donnent des nombres différents ou des affirmations opposées ? Vérifie la source (le jeu, le SDK) et soulève la question dans la pull request
- **Rien n'est supprimé sans demander,** même un texte qui a l'air dépassé

Une différence de formulation n'est pas un problème. Une différence dans ce que le lecteur apprend en est un

## Comparer les versions

Le dépôt contient un skill pour Claude Code, `compare-translations` (dans `.claude/skills/`). Il fait cette comparaison. Sans lui, fais les deux mêmes passes à la main

**La passe structurelle** compare les versions élément par élément : le frontmatter, le H1, le premier paragraphe, les titres, le nombre de paragraphes, d'éléments de liste, de lignes de tableau et d'encadrés, les cibles des liens, les images, le code

**La passe de sens** lit chaque section côte à côte et cherche les faits qu'une version contient et qu'une autre n'a pas : nombres et unités, noms de champs, de boutons et de touches, conditions et exceptions, avertissements, étapes d'une procédure et leur ordre, exemples

## Le chinois traditionnel est généré

`zh-Hant/` n'est pas traduit à la main. Un script le convertit depuis `zh/` : OpenCC, caractères traditionnels avec le vocabulaire de Taïwan. Une correction d'une page en chinois traditionnel va dans la page `zh/`, et la conversion suivante la reporte. Une modification faite directement dans `zh-Hant/` est écrasée

## Nouvelle langue

Une nouvelle langue s'ajoute entièrement dans ce dépôt, le code du site ne change pas :

1. Copie `frontend/en.yaml` vers `frontend/<code>.yaml`, par exemple `frontend/de.yaml`, et traduis les valeurs. Ce sont les textes propres au site : le menu, les boutons, la recherche, le bandeau des cookies. Garde les clés et chaque `{name}` tels quels
2. Crée le dossier `<code>/` à côté de `en/`, `ru/`, `zh/`, `zh-Hant/`, `ja/`, `ko/` et `es/` et traduis les pages dedans. Une page sans traduction s'affiche en anglais avec un avertissement

Une clé avec des formes `one` / `few` / `many` / `other` dépend d'un nombre. Donne-lui toutes les formes dont ta langue a besoin, le build nomme celles qui manquent.
Une clé non traduite s'affiche en anglais. Le build liste ces clés sous forme d'avertissements

Avant une grosse traduction, ouvre une issue dans [bullet-hero/docs](https://github.com/bullet-hero/docs), pour que deux personnes ne traduisent pas la même chose
