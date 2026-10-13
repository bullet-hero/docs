---
title: Ce dont un niveau a besoin
date: 2026-10-02
tags: [level_author]
---

# Ce dont un niveau a besoin

Le minimum, c'est un morceau. Tout le reste est facultatif, et presque tout, tu l'apportes toi-même

## Ce qu'un niveau peut utiliser

| Quoi | Détails | Où ça vit |
|---|---|---|
| Audio | au moins un morceau, il peut y en avoir plusieurs | le dossier du niveau |
| Textures | quand une forme ne suffit pas | le dossier du niveau |
| Polices | `ttf`, `otf`, `ttc` | le dossier du niveau |
| Formes | 497 intégrées et toutes celles dessinées dans la fenêtre `{{ui:hint_level_shape-editor_header}}` | intégrées au jeu ou au niveau |
| Thèmes, effets, prefabs | des données, pas des fichiers | dans `level.json` |

L'audio, les textures et les polices sont de vrais fichiers.
Eux seuls alourdissent le dossier, demandent une trace de leur origine avant publication et peuvent se perdre lors d'un déplacement

Sans police propre, le texte est dessiné avec ce que le système a sous la main

**Le jeu n'embarque aucune texture.** Les formes intégrées sont de la géométrie, pas des illustrations. Elles n'ont pas de pixels, ne pèsent rien et n'ont nulle part d'où être chargées

> [!tip] Recommandation
> Pense à une forme avant une texture, toujours. Une texture, c'est un fichier qu'on peut perdre lors d'un déplacement, de la mémoire au chargement et une ligne dans le registre des licences. Une forme ne coûte rien de tout cela

## Le poids du dossier

Il n'y a pas de limite stricte. Mais un niveau voyage par copie, et la personne qui le reçoit voit le poids du dossier

Un morceau de 4 minutes en `ogg` pèse 4-6 Mo. Le même morceau en `wav` pèse environ 40 Mo

## Plusieurs sources pour une ressource

Une ressource peut avoir une liste d'endroits d'où la récupérer : un fichier à côté du niveau, un chemin absolu, un lien direct.
Le jeu parcourt la liste jusqu'à ce que quelque chose se charge

> [!tip] Recommandation
> Garde un lien en complément du fichier, pas à sa place. Un site peut tomber, déménager ou se mettre à servir autre chose. Un fichier dans le dossier reste là où est le niveau

## Les droits sur les fichiers

Si le niveau quitte ton disque, chaque fichier qu'il contient a besoin d'une licence qui le permet.
Cela se règle dès le début, par les ressources que tu choisis

Plus - [[2_editor/3_rights/index]]

Ensuite : [[2_preparing-the-track]], [[3_images-and-fonts]]
