---
title: Déterminisme
date: 2026-10-02
tags: [advanced_player]
---

# Déterminisme

Un niveau avec la même graine se joue de la même façon sur n'importe quel appareil et à n'importe quelle fréquence d'images. Son aléatoire est calculé à partir de la graine, et tes actions n'influencent pas le niveau

## Un niveau est une fonction du temps

Un niveau est construit sur une timeline. Chaque objet vit sur un intervalle d'images et se déplace selon des images clés

Le niveau ne lit pas tes actions. Donc l'image 1200 est la même, que l'avatar soit vivant, mort, en plein dash ou qu'un bot joue à ta place

L'influence va dans un seul sens. Un niveau peut changer la taille de l'avatar, le ralentir, lui retirer le contrôle ou désactiver les collisions. Il n'y a aucun canal de retour de l'avatar vers le niveau

Il n'y a pas de déclencheurs. Ils sont en discussion pour de futures versions, mais rien n'est décidé

Un niveau tourne en temps réel. La fréquence d'images ne fixe que la fréquence à laquelle l'écran est redessiné.
La même partie se joue de la même façon à 30 et à 144 images par seconde

## La graine

La graine est prise au premier endroit où elle est définie :

1. `{{ui:level_level-view_seed-value}}` sur l'écran du niveau (`{{ui:level_level-view_seed-randomize}}` en choisit une nouvelle, `{{ui:level_level-view_seed-clear}}` la retire)
2. la graine propre du niveau, fixée par l'auteur
3. une nouvelle graine pour cette partie

`0` veut dire "non définie". Un niveau ordinaire prend donc une nouvelle graine à chaque chargement

La fenêtre de résultat montre la graine de la partie, et le record l'enregistre. Ainsi, une partie chanceuse peut être rejouée

## Comment fonctionne l'aléatoire

Une valeur aléatoire dans un niveau ne vient pas d'un générateur qui garde son état. Elle est calculée à partir de son adresse :

`Hash(seed, keyframe frame, layer, start frame, track, channel)`

La même adresse donne toujours le même nombre. Sur n'importe quel appareil et dans n'importe quel ordre de calcul.
Chaque partie de l'adresse est quelque chose que l'auteur modifie. Donc la même disposition rejoue la même partie

## Ce que ça t'apporte

- **Le bot Warm** planifie un itinéraire à travers tout le niveau avant le début de la partie. C'est possible parce que c'est exactement le niveau pour lequel il a planifié qui se joue
- **Le bot Reflex** construit des images en avance sur l'image actuelle et esquive en fonction d'elles
- **Le retour à un checkpoint** reconstruit l'image voulue au lieu d'annuler quoi que ce soit
- **L'éditeur** construit n'importe quelle image à partir de zéro, donc le balayage est instantané
- **Les records et les statistiques** veulent dire la même chose sur n'importe quel appareil

## Limites connues

Le côté niveau est déterministe. Le côté avatar a des défauts connus qui ne sont pas encore corrigés :

- deux obstacles touchent l'avatar à la même image. Celui qui fixe la direction du recul peut différer d'une partie à l'autre
- l'horloge de l'avatar n'est pas remise à zéro au démarrage du niveau. Un dash peut durer une image de plus ou de moins, selon le temps qu'a pris le chargement du niveau

Rejouer la même partie de bot sur une même version du jeu a donné un résultat identique au dernier chiffre près lors des mesures. Ces défauts ne se déclenchent donc pas sur tous les niveaux.
À cause d'eux, une partie est reproductible en pratique, mais pas garantie
