---
title: Rythme et structure
date: 2026-10-02
tags: [level_author]
---

# Rythme et structure

Cale d'abord la grille de pulsations : le tempo, puis le décalage, puis les pulsations par mesure. Place le sommet du niveau sur le sommet du morceau, et laisse le joueur respirer dans les breaks

Un jeu de rythme repose sur une seule sensation : le joueur ne bouge pas sur la musique, il la joue

## La grille de pulsations

La grille de pulsations est pour toi, pas pour le jeu. La lecture ne la lit pas.
Tu t'en sers pour placer le contenu sur la musique, et les générateurs travaillent sur les mêmes pulsations

La grille est faite de segments. **Un segment est une portion à tempo constant**, et il peut y en avoir plusieurs.
Entre les segments, il peut y avoir des trous : une intro sans batterie, un break, la queue après la dernière note

Ne cale que les portions qui porteront du contenu. Une intro n'a en général besoin de rien

## Trouver le tempo

1. Trouve le tempo
2. Puis le décalage
3. Puis les pulsations par mesure

Tu ne connais pas le tempo ? Tape-le en rythme avec le morceau dans la fenêtre `{{ui:editor_beat-window_title}}` (`Shift+T`).
Arrondis-le à un nombre entier et ajuste finement avec le décalage

Un morceau est presque toujours écrit dans un tempo entier. Une valeur fractionnaire signifie en général que c'est le décalage qui est faux, pas le tempo

## Le son en mouvement

**Répartis les instruments entre différents types de contenu :**
- la grosse caisse - sous ce qui demande une action au joueur
- les frappes secondaires - sous le mouvement qui ne demande aucune action
- les nappes longues et l'ambiance - sous le fond et la caméra

Le niveau sonne alors en profondeur au lieu de tout frapper sur un seul temps

**L'amplitude d'un mouvement porte la force d'un son.** Un petit mouvement est une frappe faible, un grand une frappe forte.
Un gros effet sur une note faible se lit comme une erreur de synchronisation, même quand les images sont exactes

**La forme d'un mouvement porte l'accent.** Un virage sec souligne une note forte, un arc doux une note faible

**En 4/4, les temps se classent par poids ainsi : 1, 3, 2, 4.** Une action sur le premier temps est la plus intuitive.
La syncope donne du groove. Mais une syncope fréquente ou incohérente laisse le joueur sans savoir où il en est

**Une mesure inhabituelle se découpe en groupes que le joueur peut compter.** En 7/4, des groupes de 4+4+2+2+2 se suivent plus facilement que 4+4+4+2

## Structure

Les sections sont ce dont un joueur se souvient.
Un niveau sans sections, ce sont quatre minutes de la même chose, même si quelque chose de nouveau arrive toutes les cinq secondes

**La répétition enseigne.** Un motif qui revient est reconnu et appris plus vite. Mais trop de répétition ennuie, et briser un motif établi sans raison se lit comme de la négligence, pas comme de la variété

> [!tip] Recommandation
> Pose des marqueurs sur la structure du morceau avant de placer le premier objet : intro, couplet, refrain, break, drop, outro. Ils s'affichent sur chaque timeline et ne coûtent rien

> [!caution] Attention
> Le sommet du niveau doit tomber sur le sommet du morceau, et les pauses sont obligatoires. Un break, c'est là où le joueur respire. Un niveau sans pauses épuise les gens avant de devenir difficile

La fin mérite réflexion elle aussi : soit un dernier sommet, soit un fondu calme. Un niveau ne devrait pas simplement se couper

## Pourquoi des segments, pas des clés

La grille de pulsations est une liste de portions, pas une piste de clés.
Une piste de clés ne peut pas exprimer l'absence : sa dernière clé s'étirerait jusqu'à la fin du niveau. Et les segments ont besoin de trous entre eux

À lire ensuite : [[4_frames-and-time|Images, temps et durée d'un niveau]], [[3_difficulty-curve|Difficulté et courbe]]
