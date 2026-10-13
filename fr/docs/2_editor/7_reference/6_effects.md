---
title: Effets
date: 2026-10-01
tags: [level_author]
---

# Effets

Un effet, ce sont des particules VFX Graph dont les paramètres sont répartis en modules : combien de particules, d'où elles partent, comment elles bougent, de quelle couleur et de quelle taille elles sont. Tu les modifies dans l'inspecteur ou dans l'éditeur d'effets

## Inspecteur d'effet

Montre les paramètres d'un effet `VFX Graph` par groupes : configuration, principal, forces, forme, angle, échelle et couleur. Tous les groupes sont visibles à la fois

> [!info] Bon à savoir
> Les effets **tirent leur aléatoire comme tout le reste** : à partir des nombres que tu modifies, pas de l'état d'un générateur. Le niveau se rejoue donc à l'identique sur n'importe quel appareil

> [!tip] Conseil
> Les couleurs peuvent renvoyer au thème du niveau au lieu d'une valeur fixe. Les types dégradés ouvrent l'éditeur de dégradés commun

Plus : [[1_level-budget|Le budget du niveau]]

## Principal - combien de particules et pendant combien de temps

Règle combien de particules existent, combien de temps elles vivent et avec quoi elles sont dessinées. C'est tout ce qui est vrai avant la première force. L'autre moitié, ce sont les [[6_effects#Forces - ce qui fait bouger une particule|Forces]]

`Nombre de particules` est le principal levier de coût. C'est exactement le nombre que compte la prévision de capacité du niveau

Un émetteur coûte à peu près son nombre multiplié par sa durée de vie. Doubler `Limites de durée de vie` coûte autant que doubler le nombre

`Forme` est la silhouette de chaque particule, tirée du même ensemble que celui des objets ordinaires. `Texture` est l'image par-dessus. Les deux champs peuvent être vides. Une particule sans texture est le cas ordinaire et bon marché

> [!warning] Avertissement
> Le nombre est plafonné à 1024. C'est la capacité du graphe lui-même. Un graphe VFX traite toute sa CAPACITÉ à chaque image, pas seulement les particules vivantes. Un système coûte donc autant qu'il a demandé, même s'il lui en faut moins

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut en une seule étape d'annulation

Plus : [[1_level-budget|Ce qu'un niveau peut se permettre]]

## Configuration - quand l'émetteur se tait

Règle quand l'émetteur arrête d'émettre. Désactivé, il émet tant que l'objet vit. C'est le cas ordinaire : la salve se termine avec l'objet

`Image d'arrêt` se compte depuis le début de l'intervalle propre de l'OBJET, pas depuis la timeline du niveau. Un effet à la fin d'un niveau peut donc se taire trois cents de ses propres images plus tard

Les particules déjà vivantes vont au bout de leur vie. L'émission est coupée, et l'image s'estompe en douceur

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet les deux champs à leurs valeurs par défaut en une seule étape d'annulation

Plus : [[1_level-budget|Ce qu'un niveau peut se permettre]]

## Angle - rotation de la particule

Règle comment une particule est tournée au cours de sa vie. Il y a cinq variantes :
- `Valeur` - un angle fixe
- les deux variantes `Curves` lisent une courbe
- les deux variantes `Aléatoire` tirent une valeur entre A et B pour chaque particule

Les rangées présentes dépendent du choix. Les deux variantes à courbe diffèrent par CE QUI lit la courbe :
- `Over Life` - la durée de vie de la particule
- `By Speed` - la vitesse de la particule, à travers la fenêtre de vitesse en dessous

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet tout le groupe à ses valeurs par défaut, `Type` compris. La courbe ou la paire aléatoire que tu as réglée est perdue

Plus : [[1_readability-and-fairness|La lisibilité]]

## Couleur - couleur de la particule

Règle comment une particule est colorée au cours de sa vie. Six variantes : les cinq mêmes que pour [[6_effects#Angle - rotation de la particule|Angle]] et [[6_effects#Échelle - taille de la particule|Échelle]], seulement avec des dégradés au lieu de courbes, plus un `Random` de dégradé supplémentaire :
- `Over Life` lit le dégradé selon la durée de vie de la particule
- `By Speed` le lit selon la vitesse de la particule
- `Random` prend une couleur du dégradé par particule au lieu de le parcourir
- les deux variantes `Aléatoire` du bas tirent une couleur entre deux couleurs

> [!tip] Conseil
> Une couleur peut ici renvoyer au thème, comme partout ailleurs dans le niveau. Ainsi, l'effet suit un niveau qui change de palette en cours de route

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet tout le groupe à ses valeurs par défaut, `Type` compris. Le dégradé ou la paire de couleurs que tu as réglé est perdu

Plus : [[5_color-and-postprocessing|La couleur et les thèmes]]

## Échelle - taille de la particule

Règle la taille d'une particule au cours de sa vie. Les cinq mêmes variantes que pour [[6_effects#Angle - rotation de la particule|Angle]] : une taille fixe, une courbe ou une plage par particule

Il y a ici deux courbes, car la taille a deux axes. `Curve X` et `Curve Y` se lisent indépendamment. Une particule peut s'étirer et rétrécir en même temps

> [!warning] Avertissement
> La rangée sous les courbes est RÉUTILISÉE. Avec `Valeur` et les deux variantes `Aléatoire`, c'est la taille elle-même. Avec `By Speed`, c'est la fenêtre de vitesse. La légende à côté et son aide disent ce qu'est la rangée en ce moment

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet tout le groupe à ses valeurs par défaut, `Type` compris. Les deux courbes et la paire aléatoire sont perdues

Plus : [[1_readability-and-fairness|La lisibilité]]

## Forme - d'où partent les particules

Règle le volume d'apparition : un point, un anneau, un rectangle, un segment, un cône ou un tore. Elle décide seulement où une particule COMMENCE. Ce qui lui arrive ensuite, ce sont les [[6_effects#Forces - ce qui fait bouger une particule|Forces]]

Changer `Type` change l'ensemble des champs en dessous. Les rangées sont réutilisées : la première est le rayon d'un cercle, le rayon supérieur d'un cône ou le petit rayon d'un tore, selon ce qui est choisi

`Arc` est la part du bord utilisée, en radians, dans le sens antihoraire depuis l'axe +X. Moins d'un tour complet donne un éventail

> [!tip] Conseil
> `Ouverture` transforme un anneau statique en anneau qui bouge. Il décide où, sur le bord, tombe la particule suivante : au hasard, en tournant dans un sens, en aller-retour ou le long d'une sinusoïde. `Boucle` est l'émetteur rotatif classique

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet tout le groupe à ses valeurs par défaut, `Type` compris. La forme que tu as réglée, avec ses rayons et son ouverture, est perdue

Plus : [[4_composition-and-camera|La composition]]

## Forces - ce qui fait bouger une particule

Règle tout ce qui fait bouger une particule après son apparition. La [[6_effects#Forme - d'où partent les particules|Forme]] décide où elle commence, et ce groupe décide où elle vole

Les champs sont de deux sortes. Les confondre est l'erreur habituelle :
- les paires `Start` sont tirées UNE FOIS à la naissance d'une particule, entre leur minimum et leur maximum. Écarte une paire et une salve régulière devient un éventail
- tout le reste agit EN CONTINU pendant toute la vie de la particule

Champs de la deuxième sorte :
- `Vitesse linéaire` est un vent, pas une poussée
- `Force linéaire` est une accélération, donc elle s'accumule
- `Vitesse orbitale` fait tourner les particules autour du centre, pas sur elles-mêmes

> [!tip] Conseil
> `Vitesse de déplacement` multiplie tout le résultat. Ainsi, un effet terminé peut être ralenti ou accéléré sans toucher aux autres champs

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet les onze champs à leurs valeurs par défaut en une seule étape d'annulation

Plus : [[4_composition-and-camera|La composition]]

## Éditeur d'effets

Construit un effet de particules et le montre sur le canevas

> [!info] Bon à savoir
> Les groupes de paramètres sont les mêmes que dans l'inspecteur d'effet. Ici, ils se modifient comme un **brouillon** : rien n'arrive dans le niveau tant que tu n'as pas enregistré

> [!tip] Conseil
> Enregistre l'effet dans la bibliothèque partagée de l'appareil pour l'utiliser dans d'autres niveaux

Plus : [[1_level-budget|Le budget du niveau]]
