---
title: Générateurs
date: 2026-10-12
tags: [level_author]
---

# Générateurs

Un générateur crée du contenu et l'applique au niveau en une seule opération, qui s'annule en une seule étape. Chaque générateur se lance depuis la fenêtre "Générateurs" de la barre d'outils

## Générateurs

Le formulaire d'un générateur est construit à partir de ses propres champs. Il n'y a pas d'interface séparée pour chaque générateur

> [!caution] Attention
> Tout ce qui réécrit ou supprime du contenu existant demande d'abord une confirmation

> [!info] Bon à savoir
> Il y a deux familles. Les **générateurs** (*gen_*) créent du contenu : vagues de balles, motifs radiaux et cache de police. Les **modificateurs** (*mod_*) changent ce qui existe déjà : ajuster des intervalles, quantifier des images clés. Les modificateurs sont décrits à part - [[9_modifiers]]

Plus - [[2_reuse]]

## La fenêtre des générateurs

Les générateurs de contenu et les modificateurs se lancent depuis la fenêtre `{{ui:editor_generators_text}}` de la barre d'outils. Son bloc `{{ui:editor_generators_base-parameters}}` est commun à tous les générateurs : `{{ui:editor_generators-start_frame}}`, `{{ui:editor_generators-end_frame}}`, `{{ui:editor_inspector_layer}}` et `{{ui:editor_generators_seed}}`. Ils appartiennent à la fenêtre, pas à un générateur en particulier

Comment se comporte le bloc :
- La fenêtre s'ouvre sur une seconde à partir de la tête de lecture, avec la graine à 0. `{{ui:editor_generators-seed_random}}` tire une nouvelle graine
- Les images restent dans la timeline sur laquelle tu travailles, de l'image 1 à sa dernière image. En mode prefab, c'est la durée du modèle
- Modifier `{{ui:editor_generators-start_frame}}` pousse `{{ui:editor_generators-end_frame}}` avec lui. Modifier `{{ui:editor_generators-end_frame}}` s'arrête à `{{ui:editor_generators-start_frame}}`. Ils ne se croisent jamais
- `{{ui:editor_inspector_layer}}` reste dans la plage de calques autorisée
- Chaque champ d'image a une épingle qui le maintient au bord de la timeline. `{{ui:editor_generators-whole_level}}` règle les deux, et la fenêtre va de l'image 1 à la dernière image. Les champs restent modifiables, et saisir une valeur dans un champ retire l'épingle de ce bord

`{{ui:editor_generators_group}}` et `{{ui:editor_generators-split_layers}}` sont activés par défaut. Le groupe porte le nom du générateur. Les deux ne concernent que les générateurs de contenu : un modificateur ne crée rien, il n'y a donc rien à grouper

Le contenu généré ne va jamais sous l'objet sélectionné. Il arrive au premier niveau de la portée ou dans son propre groupe

Avant que tu appuies sur `{{ui:editor_generators_run}}`, la fenêtre montre ce qu'un lancement va ajouter. Le bouton est indisponible, et la raison est écrite à la place de l'estimation, si :
- le générateur a besoin du niveau entier et tu es en mode prefab. Ce sont Flash de pulsation, Cache de police, Prévision de capacité et Changer la fréquence d'images
- le générateur a besoin d'une sélection et rien n'est sélectionné
- après le lancement, le niveau aurait plus de 262 144 objets
- un générateur de contenu n'ajouterait rien. Un modificateur n'est pas refusé pour cela

Un générateur qui a besoin de données externes (une piste audio, des pulsations, une image) ne crée rien sans elles, et l'estimation le dit

`{{ui:editor_generators_run}}` ferme la fenêtre. Le contenu généré reste sélectionné, dans la même étape d'annulation

La fenêtre retient sur quel générateur tu étais et quels paramètres tu as saisis quand elle est fermée puis rouverte. `{{ui:editor_generators_reset}}` rétablit les valeurs par défaut

## Niveaux

L'assistant IA ne peut pas lancer ces trois-là. Il commence un nouveau niveau avec son propre `level_create`

### Niveau vide

Vide complètement le niveau. Tout ce qui a été créé est supprimé.
Convient pour repartir de zéro plutôt que pour modifier

`Pin Screen Aspect` (activé par défaut) place une image clé avec un 16:9 fixe sur la piste `{{ui:editor_events-timeline_track_screen-limit}}` à la première image

Plus - [[2_first-level]]

### Niveau depuis un fichier audio

Commence un niveau à partir d'un morceau.
Branche l'audio, ajuste la durée du niveau au morceau et te place au début d'une timeline vide

`Pin Screen Aspect` (activé par défaut) place une image clé avec un 16:9 fixe sur la piste `{{ui:editor_events-timeline_track_screen-limit}}` à la première image

Plus - [[2_preparing-the-track]]

### Importer une archive de niveau

Construit un niveau à partir d'une archive faite par ce jeu.
Formats : `.tar.gz` et `.zip`. Les deux peuvent être protégés par mot de passe

Le type de fichier est détecté d'après le contenu, pas d'après le nom. Une archive renommée s'ouvre quand même.
Le jeu reconnaît `7z` mais ne le lit pas encore et le refuse

> [!tip] Conseil
> Une archive d'une ancienne version s'ouvre sans préparation. Le jeu la convertit lui-même au format actuel à l'import

> [!warning] Avertissement
> Par défaut, un niveau importé reçoit un nouvel ID. Il n'écrase donc pas un niveau déjà présent sur cet appareil. Ne décoche cette case que pour restaurer un niveau qui se trouvait autrefois sur cet appareil

## Balles

Plus sur tous les générateurs de balles - [[1_readability-and-fairness]]

> [!caution] Attention
> Le `Collider` d'un générateur de balles est vide par défaut. Ses balles dessinent un carré et ne peuvent pas blesser le joueur tant que tu n'as pas choisi de collider, par exemple la même forme que `Shape`. Les autres générateurs qui placent des formes, ceux de géométrie et Forme d'onde audio, ont le même champ avec la même valeur par défaut

### Vague de balles

Une rangée de balles qui bougent ensemble.
Le motif de base, et celui par lequel commencer. Ses paramètres reviennent dans les autres générateurs de balles

### Spirale de balles

Les balles partent le long d'un rayon qui tourne. Le résultat est le mur en spirale classique

### Pluie de balles

Les balles tombent sur une zone pendant une durée donnée.
La densité et la dispersion se règlent.
L'endroit où tombe chaque balle vient de la `{{ui:editor_generators_seed}}` de la fenêtre, pas de la graine du niveau. La même graine répète exactement un lancement, et une autre graine donne une autre disposition. L'assistant IA passe sa propre graine, `0` s'il n'en donne pas d'autre, donc deux lancements censés différer ont besoin de deux graines

### Balles à tête chercheuse

Les balles s'incurvent vers l'endroit où le joueur est censé se trouver.
La trajectoire est calculée à l'avance, pas pendant le jeu. Le résultat est donc le même sur n'importe quel appareil

### Faisceau laser

Un rayon traverse le terrain.
L'avertissement et la phase qui fait mal sont des objets différents. Ainsi, l'avertissement peut être montré, et il ne tue pas.
Le rayon d'avertissement n'entre jamais en collision. Le rayon qui tire ne blesse qu'avec un `Collider` choisi

## Géométrie

Plus sur tous les générateurs de géométrie - [[2_reuse]]

### Polygone

Place des formes sur les sommets ou les arêtes d'un polygone régulier

### Radial

Place des copies autour d'un cercle. La base de la plupart des motifs symétriques

### Spirale

Place des copies le long d'une spirale. Le rayon et l'angle grandissent ensemble

### Grille

Remplit un rectangle de copies d'une forme à distances égales

### Fractale

Répète une forme à l'intérieur d'elle-même, plus petite à chaque fois.
Le nombre d'objets croît de façon exponentielle avec la profondeur. Augmente la profondeur un cran à la fois

## Audio et effets

### Forme d'onde audio

Construit des objets à partir de la forme d'une piste audio. Le niveau suit visiblement ce qu'on entend

Plus - [[2_reuse]]

### Flash de pulsation

Place un flash sur chaque pulsation.
Les pulsations viennent de la carte des pulsations du niveau. S'il n'y a pas de carte, des marqueurs.
Ce qui clignote est donc exactement ce que tu vois sur la grille

Plus - [[2_rhythm-and-structure]]

## Ressources et utilitaires

### Objets depuis une texture

Transforme une image en objets, un par cellule.
L'image devient du contenu du niveau et s'anime comme tout le reste

Plus - [[3_images-and-fonts]]

### Cache de police

Rassemble chaque caractère qu'utilise le texte du niveau et les précalcule.
Aucun caractère n'est alors préparé au moment où il s'affiche pour la première fois

> [!tip] Recommandation
> Lance-le une fois le texte terminé. Un caractère ajouté plus tard sans nouveau précalcul cause une saccade la première fois qu'il s'affiche

Plus - [[3_images-and-fonts]]

### Prévision de capacité

Enregistre les limites recommandées du niveau : combien d'objets et d'effets il lui faut en même temps

> [!info] Bon à savoir
> Elle n'affecte pas ce qui s'affiche. Le jeu alloue à l'avance des tampons pour ces limites. Sinon, les tampons grandiraient au milieu du niveau, et cela causerait une saccade

Plus - [[1_level-budget]]
