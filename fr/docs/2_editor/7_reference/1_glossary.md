---
title: Glossaire
date: 2026-10-11
tags: [level_author]
---

# Glossaire

La liste principale des termes du projet. L'interface du jeu, cette documentation et tout autre texte sur Bullet Hero utilisent ces mots, et un nouveau terme est d'abord ajouté ici

## Contenu du niveau

| Terme | Sens |
|---|---|
| **Niveau** | Tout ce dont est faite une partie : objets, audio, événements et ressources propres |
| **Objet** | Un élément créé par l'auteur sur la timeline, avec son propre intervalle, sa transformation et son parent |
| **Objet vide** | Un objet qui ne dessine rien : une transformation, un intervalle et des enfants. Chaque autre type ajoute ce qui lui est propre par-dessus |
| **Forme** | De la vraie géométrie que dessine un objet, pas une image. Le jeu en génère lui-même environ 500 |
| **Collider** | Ce contre quoi un objet entre en collision. Il peut différer de ce que l'objet dessine |
| **Prefab** | Un modèle réutilisable d'objets, placé dans un niveau autant de fois que nécessaire |
| **Mode prefab** | Modifier le contenu propre d'un modèle au lieu du niveau qui l'entoure |
| **Effet** | Un émetteur : à chaque image, il crée ses propres objets à partir de quelques paramètres |
| **Objet d'image** | Un objet créé par un effet. Le moteur le gère : on ne peut ni le sélectionner ni le modifier |
| **Thème** | Une palette à laquelle le niveau renvoie par index : recolorer est une modification, pas cent |

## Temps et animation

| Terme | Sens |
|---|---|
| **Image** | L'unité de temps du niveau. Une image est une cellule, et le temps est la limite entre deux cellules |
| **Image clé** | Une valeur fixée par l'auteur à une image. Entre deux images clés, la valeur est interpolée |
| **Piste** | Une rangée d'images clés d'une propriété animable : position, rotation, volume |
| **Timeline** | L'axe des images sur lequel on construit le niveau : un onglet par type de contenu |
| **Intervalle** | Quand un objet existe : une image de début et une durée, mais pas d'image de fin |
| **Tête de lecture** | L'image affichée en ce moment |
| **Lissage** | Comment la valeur passe de l'image clé précédente à celle-ci |
| **Marqueur** | Un point nommé sur la règle du niveau, pour revenir au bon endroit |
| **Checkpoint** | L'endroit où une mort ramène le joueur |

## Placement et dessin

| Terme | Sens |
|---|---|
| **Ancre** | Un bord qui suit le bord du parent : rétrécis le parent et l'enfant bouge avec lui |
| **Calque** | L'ordre de dessin, et il est relatif : le calque de l'enfant s'ajoute à celui du parent |
| **Pivot** | Le point autour duquel l'objet tourne et se met à l'échelle, dans son propre rectangle |
| **Gizmo** | Les poignées de glissement dessinées sur l'objet sélectionné dans la vue |
| **Aimantation** | Attirer un glissement vers quelque chose : vers le contenu avec l'aimant, vers la musique avec l'interrupteur de pulsation |

## Musique

| Terme | Sens |
|---|---|
| **Pulsation** | La grille propre à la musique : l'auteur la fixe, et rien ne la lit pendant le jeu |
| **Segment de pulsation** | Une partie à tempo constant avec son propre tempo, sa phase et sa longueur de mesure |
| **BPM** | Pulsations par minute - la vitesse d'un segment de pulsation |
| **Appui** | Un appui pendant que tu marques le tempo. Assez d'appuis décrivent un segment de pulsation |

## Automatisation et données

| Terme | Sens |
|---|---|
| **Générateur** | Une automatisation de la création : il produit du contenu du niveau à partir de quelques paramètres |
| **Modificateur** | Un générateur qui modifie ou supprime ce qui existe déjà au lieu d'ajouter |
| **Graine** | Le nombre d'où vient chaque valeur aléatoire du niveau : une partie se rejoue exactement à l'identique |
| **Données brutes** | Tout le modèle enregistré sous forme d'un seul arbre modifiable. Rien n'y est vérifié, et c'est voulu |
| **Assistant IA** | Un client d'IA connecté à l'éditeur par MCP. Il modifie le niveau ouvert sous tes yeux, une étape d'annulation par lot |

## Ressources et partage

| Terme | Sens |
|---|---|
| **Bibliothèque** | Les ressources sur l'appareil, à réutiliser d'un niveau à l'autre : ta bibliothèque, tes collections et celles de tes abonnements |
| **Collection** | Un dossier de ressources réutilisables, de sept types au plus. L'import en fait une copie, donc le niveau n'en dépend pas |
