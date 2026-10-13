---
title: La fiche de ressource
date: 2026-10-02
tags: [level_author]
---

# La fiche de ressource

La fiche note d'où vient une ressource et à quelles conditions : le lien, la licence, les autorisations, les auteurs. Un champ de licence vide signifie "personne n'a vérifié", et une telle ressource est refusée

> [!tip] Recommandation
> Remplis la fiche dès que tu ajoutes la ressource. C'est le seul moment où tu te souviens encore d'où elle vient

## Ce que contient la fiche

Chacune de tes ressources dans un niveau a sa propre fiche. Elle est stockée dans le niveau et voyage avec lui.
Ainsi, l'attribution ne se perd pas : où que le niveau aboutisse, le fichier garde la trace de son origine et de ses conditions

Les champs de la fiche :
- **Titre** et **description** de l'œuvre originale, tous deux peuvent être traduits dans d'autres langues
- **Url** - la page de l'œuvre : la publication ou la page de l'auteur, une page de store
- **Licence** - les conditions auxquelles l'œuvre est distribuée
- **Autorisations** - [[2_legal-resource-paths|option B]], une entrée par titulaire des droits, avec portée, dates et preuve
- **Auteurs** - tous ceux qui doivent être crédités pour cette ressource, séparément des auteurs du niveau lui-même
- **Sources** - texte libre sur l'origine, pour tout ce qu'un lien ne peut pas exprimer
- **Hachages** - les hachages du contenu des fichiers de la ressource
- **Génération par IA** - si l'œuvre a été générée par une IA : `{{ui:enum_ai-generation_not-specified}}`, `{{ui:enum_ai-generation_no}}` ou `{{ui:enum_ai-generation_yes}}`

**Le lien mène à la page avec les conditions, pas à un téléchargement direct.** Un modérateur a besoin de la page, pas du fichier

## Un champ vide signifie "inconnu"

> [!caution] Attention
> Un champ de licence vide, c'est `NoSpecifiedLicense`, et une telle ressource est refusée. Cela ne veut pas dire "les conditions sont correctes". Cela veut dire "personne n'a vérifié"

Tout le modèle fonctionne ainsi : une valeur vide signifie "rien de déclaré", pas "tout est permis".
Une classification par âge `Unrated`, une portée d'autorisation `Undefined` et une génération par IA `{{ui:enum_ai-generation_not-specified}}` fonctionnent de la même façon

`NoSpecifiedLicense` peut en plus indiquer d'où le fichier a été pris : YouTube, SoundCloud, Spotify.
Le verdict n'en change pas. Le modérateur voit simplement quelle conversation l'attend

## Hachages

Remplis les hachages dès le premier jour, même là où ils ne sont pas exigés.
La plainte d'un titulaire des droits nomme une œuvre. Pour y répondre, il faut retrouver tous les niveaux qui contiennent cette œuvre.
Par le nom, c'est de la devinette, par le hachage, c'est une recherche exacte

## Fiches obsolètes

La fiche d'une ressource que le niveau n'a plus donne un conseil, pas une erreur.
Elle ne bloque rien, mais il vaut quand même mieux la retirer

## Une ressource sur la carte du niveau

La fiche d'une ressource peut être marquée pour s'afficher sur la carte du niveau. C'est prévu pour la musique.
Une ligne avec cette ressource apparaît alors sous les auteurs du niveau. Tout le reste reste dans les crédits complets

## La fiche de la couverture

La couverture du niveau a aussi une fiche. La couverture n'est pas une ressource du niveau, donc sa fiche s'ouvre à côté de la couverture dans l'onglet des métadonnées, avec le bouton `{{ui:settings_level-settings_metadata-level-logo-metadata}}`

- Une nouvelle image recommence la fiche à zéro, et celle-ci ne contient que le hachage du fichier. Une autre image est une autre œuvre, et les auteurs précédents seraient crédités à tort
- Le même fichier choisi à nouveau laisse la fiche telle quelle
- Retirer la couverture retire aussi sa fiche. Annuler ramène les deux

Une ressource ou une couverture marquée `{{ui:enum_ai-generation_yes}}` fait afficher sur l'écran du niveau la ligne "Contient du contenu généré par IA"

À lire ensuite : [[5_publish-readiness]], [[2_metadata-and-sharing]]
