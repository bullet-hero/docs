---
title: Pourquoi Bullet Hero
date: 2026-10-03
tags: [player, level_author]
---

# Pourquoi Bullet Hero

Bullet Hero est gratuit, tourne sur Windows et Android, et son SDK, sa documentation et ses builds sont ouverts. Le cœur gère des milliers d'objets à l'écran sur téléphone et est couvert par plus de 8000 tests

## Gratuit

Le jeu est gratuit et le restera. Il n'y aura ni achats, ni publicités, ni contenu payant

Je n'exclus pas une monétisation par des dons volontaires, mais rien au-delà

## Disponible partout, tout est universel

Le jeu est partout où j'ai pu le porter
- Plateformes : Windows, Android (plus tard iOS, Linux, Mac)
- Boutiques : Steam, Google Play (plus tard App Store)

Tout dans le jeu fonctionne avec n'importe quels contrôles, les niveaux sont les mêmes partout, et chaque partie du jeu (l'éditeur, le multijoueur, les serveurs) fonctionne de la même façon partout

## Un code largement ouvert

Le SDK, la documentation, les builds et le serveur sont dans des dépôts ouverts. Seuls le jeu lui-même et le site sont fermés.
Tous les dépôts - [[links]]

## Le cœur technique le plus rapide

Des milliers d'objets à l'écran, des centaines d'effets et de textes en même temps. Et tout cela tourne sur téléphone avec un objectif de 60 FPS (souvent plus)

## Un cœur technique très stable

Le jeu dispose de nombreux mécanismes qui assurent la stabilité du jeu et de ses modèles de données
- Le versionnage de tout (plus de détails ici - [[5_versioning]])
- Un versionnage multimodal et la migration des données, les données des niveaux ne casseront pas
- Plus de 8000 tests sur l'ensemble du jeu, littéralement chaque aspect du jeu est couvert par des tests

Et beaucoup d'autres vérifications. Avec le cœur rapide, cela donne un très bon rapport entre stabilité et performances

## Multijoueur (en développement)

Le multijoueur sous toutes ses formes : sur un seul appareil, en local, via un serveur, et beaucoup d'interactions intéressantes

## Serveurs ouverts (en développement)

Un serveur officiel et des serveurs communautaires que n'importe qui peut faire tourner. Le code du serveur sera ouvert. Les catalogues de niveaux et la communication de base arriveront avec le serveur.
Plus - [[4_server/index]]

## De nombreuses langues

Le jeu vise à prendre en charge la plupart des langues du monde dès l'installation. Je pense qu'un jeu ne devrait avoir aucune barrière de langue

Bien sûr, personne ne peut connaître toutes les langues du monde, mais grâce aux progrès de l'IA et à la communauté, cet objectif est tout à fait atteignable

## Une politique de licence ouverte

Toutes les données du jeu s'accompagnent d'un choix souple de licences (surtout [Creative Commons](https://creativecommons.org/))
pour tes niveaux et les ressources que tu utilises. Cela rend la réutilisation des ressources des autres plus ouverte

Plus - [[ugc-licensing-policy]]

## Intégration avec chaque service quand c'est possible

Le jeu a plus de 10 variantes de build, et chacune a ses propres intégrations selon la boutique par laquelle elle est distribuée

Plus - [[download]]

## Déterminisme et stabilité

Le jeu a un aléatoire déterministe, et chacun de ses facteurs est lié à la graine et aux paramètres du niveau.
Cela veut dire que l'aléatoire peut toujours être reproduit si tu connais le niveau et que tu as la graine

Plus - [[8_determinism]]

## Éditeur

Le jeu a un éditeur de niveaux vaste et souple, dans lequel tu peux créer presque tout

L'éditeur a de nombreuses fonctions uniques : [[8_generators]], le débogage et bien plus

## Un format de niveau ouvert

Le SDK C# lit et écrit les niveaux de la même manière que le jeu. Le jeu et le serveur passent par lui, et toi aussi tu peux.
Avec lui, tu peux créer tes propres niveaux ou ressources uniques, ou tes propres services construits par-dessus

Plus - [[3_sdk/index]]
