---
title: Ressources du niveau
date: 2026-10-12
tags: [level_author]
---

# Ressources du niveau

Les textures, formes, thèmes, effets et prefabs d'un niveau vivent dans son dossier et voyagent avec lui. Chaque ressource a sa propre fiche avec sa source, sa licence et ses auteurs

## Bibliothèque

Les ressources enregistrées sur **cet appareil**. Elles sont partagées par tous les niveaux que tu ouvres ici

Importer copie la ressource *dans le niveau*.
Un niveau est un dossier de fichiers, et il emporte tout ce dont il a besoin. C'est ce qui le garde portable

La bibliothèque est donc une commodité pour toi. Celui qui joue ton niveau n'en dépend jamais

La bibliothèque liste trois sources, chacune sous forme de pastille : `{{ui:editor_library-source_library}}`, `{{ui:editor_library-source_local}}` et, dans une version Steam, `{{ui:editor_library-source_workshop}}`.
Choisir une entrée l'importe avec ses dépendances. Si le niveau contient déjà une autre version, le jeu demande laquelle garder

Plus - [[16_library-and-collections]], [[2_reuse]]

## Textures

Les images que ce niveau emporte.
**Le jeu lui-même ne fournit aucune texture.** Chaque texture qu'utilise un niveau a été ajoutée ici

Un niveau n'est qu'un dossier de fichiers. Une texture y vit et voyage avec le niveau : compresse le dossier, envoie-le, décompresse, joue

Les formes **ne sont pas** des textures, ce sont de vraies géométries. Elles n'ont besoin de rien dans cet onglet

Plus - [[3_images-and-fonts]]

## Formes

Les formes propres au niveau. Elles s'ajoutent aux ~500 formes que le jeu génère

Une forme est une **vraie géométrie**, pas une image.
Le rectangle de l'objet est la boîte de la forme, et les deux sortes de formes s'y placent différemment :
- **une forme intégrée garde ses proportions.** Son côté le plus long couvre le rectangle, donc un `Triangle` de taille (2, 2) se dessine sur 2 de large et environ 1,73 de haut
- **une forme définie par le niveau est étirée au rectangle**, telle qu'elle a été dessinée dans sa boîte. Un contour fourni par l'assistant IA est ajusté à la boîte, il remplit donc exactement le rectangle

> [!tip] Conseil
> **Une forme et une hitbox sont le même genre de données.** Un objet porte deux références : une pour ce qui est dessiné, une pour ce qui touche. Aucune ne dérive de l'autre. Un rayon d'avertissement inoffensif, une hitbox plus simple que son dessin et un mur invisible sont donc du contenu ordinaire

Plus - [[1_level-needs]]

### Noms des formes intégrées

Le nom d'une forme intégrée est composé de parties, toujours dans cet ordre. `Circle_S2_T8_I` est la moitié droite d'un cercle, sous forme d'anneau épais de 1/8 du rayon, inversée

| Partie | Sens |
|---|---|
| forme | `Square`, `Circle`, `Triangle`, `RightTriangle` ou un polygone régulier : `Pentagon`, `Hexagon` et ainsi de suite |
| `S2`, `S4`, `S8` | un secteur : une moitié, un quart, un huitième. Il commence tout en haut et tourne dans le sens horaire, donc `S2` est la moitié droite. Sans `S` - la forme entière |
| `_2` après `S4` | l'autre quart : celui en bas à droite au lieu de celui en haut à droite. Il n'existe que là où la forme donne une figure différente |
| `T2`, `T4`, `T8`, `T16`, `T32` | un anneau, épais de 1/2, 1/4, 1/8, 1/16 ou 1/32 du rayon. Sans `T` - plein |
| `I` | inversé : la boîte (ou son secteur) moins la forme |

Une forme sans autre partie, comme `Circle`, est la forme entière et pleine. Toutes les combinaisons n'existent pas. La moitié d'un carré n'est qu'un rectangle, une taille plus étroite suffit donc

## Thèmes

Un thème est une **palette**. Les couleurs du niveau peuvent y renvoyer au lieu de contenir des valeurs littérales

Changer le thème actif restyle d'un coup tout ce qui y renvoie.
Le thème actif peut être animé sur la timeline des événements. C'est ainsi qu'un niveau change tout son aspect en plein morceau

Les thèmes peuvent être enregistrés dans la bibliothèque de l'appareil et réutilisés dans d'autres niveaux

Plus - [[6_themes]], [[5_color-and-postprocessing]]

## Effets

Des effets de particules `VFX Graph` que le niveau peut placer

Les effets sont un **enrichissement facultatif**. Un niveau qui n'en utilise aucun se joue exactement comme prévu

Un effet utilise le même hasard à graine que tout le reste du niveau. Il se rejoue donc à l'identique sur n'importe quel appareil.
Les effets peuvent être enregistrés dans la bibliothèque de l'appareil et réutilisés dans d'autres niveaux

**Le jeu ne fournit aucun effet préréglé.** Chaque effet qu'utilise un niveau y a été créé ou pris dans la bibliothèque

Plus - [[1_level-budget]]

## Prefabs

Des groupes d'objets réutilisables.
Un prefab contient ses propres objets modèles. Placer un prefab écrit de vraies copies de ces objets dans le niveau

Modifier le modèle plus tard se répercute sur chaque placement.
Un placement peut quand même différer du modèle grâce aux remplacements propres à chaque instance

> [!warning] Avertissement
> Les prefabs n'ont **aucun préréglage fourni par le jeu**, pas plus que les effets. Le jeu ne fournit des préréglages que pour les thèmes, les polices, les sons de l'interface et les formes intégrées. La bibliothèque est le seul moyen de partager un prefab entre niveaux : la bibliothèque de ton appareil ou une collection. Plus - [[16_library-and-collections]]

Plus - [[2_reuse]]

## Métadonnées de la ressource

Titre, description, sources, licence et auteurs d'une ressource

C'est ainsi que l'attribution survit.
Une texture, une police ou un fichier audio pris quelque part emporte, à l'intérieur du niveau, d'où il vient et à quelles conditions. Cette fiche va partout où va le niveau

> [!tip] Recommandation
> Remplis-la quand tu ajoutes la ressource. C'est le seul moment où tu te souviens encore d'où elle vient

Plus - [[4_resource-record]]

## Éditeur de thème

Les emplacements d'un thème et les couleurs qu'ils contiennent

> [!caution] Attention
> Le contenu du niveau renvoie à un emplacement par sa position. Donc **renuméroter les emplacements restyle tout ce qui y renvoie**

> [!tip] Conseil
> Enregistre un thème terminé dans la bibliothèque de l'appareil. Tu pourras alors l'utiliser dans d'autres niveaux

Plus - [[6_themes]], [[5_color-and-postprocessing]]

## Référence de couleur du thème

Fait pointer cette couleur vers un **emplacement du thème du niveau** au lieu d'une valeur littérale

Quand le thème change, tout ce qui renvoie à un emplacement se restyle d'un coup.
Les thèmes peuvent être animés sur la timeline des événements. C'est ainsi qu'un niveau change toute sa palette en plein morceau sans toucher un seul objet

> [!tip] Conseil
> Les échantillons montrent la palette à l'image de la clé que tu modifies, jamais à la tête de lecture. La fenêtre nomme les thèmes de part et d'autre de cette image. Pour choisir d'après un aspect plus tardif, modifie une clé placée plus tard

Plus - [[6_themes]], [[5_color-and-postprocessing]]

## Éditeur de forme

Construit une forme à partir de points et des arêtes qui les relient

Tu modifies des points et des arêtes. **Les triangles sont déduits automatiquement et jamais modifiés.**
Un coin partagé par trois triangles est donc un seul point à faire glisser, pas trois qui se séparent

> [!warning] Avertissement
> Les arêtes n'existent que dans l'éditeur, le format stocke des triangles. Une arête qui ne ferme aucune boucle est donc abandonnée à l'enregistrement. L'éditeur le signale au lieu de l'abandonner en silence

Plus - [[3_images-and-fonts]]

## Licences

Les conditions sous lesquelles ce niveau et ses ressources sont placés

Un niveau emporte chaque fichier dont il a besoin : images, polices, audio. Chaque fichier peut venir avec ses propres conditions.
**Ces conditions sont consignées pour chaque ressource**, pas seulement pour le niveau dans son ensemble. Un niveau fait de pièces empruntées peut donc dire exactement ce qui a été emprunté et à quelles conditions

> [!tip] Recommandation
> Lis-les avant de réutiliser quoi que ce soit du niveau de quelqu'un d'autre

Plus - [[1_licensing-basics]]
