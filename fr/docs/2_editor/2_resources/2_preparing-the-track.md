---
title: Préparer la piste audio
date: 2026-10-01
tags: [level_author]
---

# Préparer la piste audio

Convertis le morceau en ogg : il pèse 8 à 10 fois moins que le wav et, contrairement au mp3, n'ajoute pas de silence au début du fichier. En dehors de l'ogg, seuls le mp3 et le wav se chargent

## Formats

`oga`, `mp2`, `aiff`, `flac` et les modules tracker `mod`, `xm`, `it`, `s3m` ne sont pas acceptés

> [!caution] Attention
> `flac` ne se charge pas du tout : le moteur ne le décode pas. Convertis-le d'abord

> [!warning] Avertissement
> Un encodeur `mp3` ajoute quelques millisecondes de silence au début, et chaque encodeur en ajoute une quantité différente. Si le morceau est réencodé par un autre encodeur, tout le calage sur les pulsations se décale

## Décalage

Même en `ogg`, un morceau ne commence presque jamais pile sur la première pulsation. C'est à cela que sert le décalage du segment de pulsation.
Il se règle en fractions d'image, il est donc plus fin qu'une image

L'ordre est : d'abord le tempo, puis le décalage, et seulement ensuite le contenu

## Volume sonore

Normalise le morceau avant de le mettre dans le niveau. Une normalisation de crête à -1 dB est un bon réglage par défaut

Un niveau nettement moins fort que le suivant donne l'impression que c'est le jeu qui est cassé, pas le morceau

## Durée

La durée du niveau et celle du morceau sont des nombres différents, elles n'ont pas à correspondre.
Un niveau peut se terminer avant le morceau. C'est ainsi qu'on peut faire une fin en fondu

## Plusieurs pistes audio

Il peut y avoir plusieurs pistes audio. Chacune a sa propre position sur la timeline, sa propre vitesse, son volume et sa chaîne d'effets

Effets : chorus, compresseur, distorsion, écho, flanger, filtres, normalisation, égaliseur, changement de hauteur, réverbération

Un effet sur une piste s'entend partout où cette piste joue, pas seulement là où tu le voulais

Ensuite : [[3_where-to-get-resources]], [[2_rhythm-and-structure]]
