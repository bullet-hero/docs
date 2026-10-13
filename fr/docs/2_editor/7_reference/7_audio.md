---
title: Audio
date: 2026-10-02
tags: [level_author]
---

# Audio

Le son d'une piste audio passe par une chaîne d'effets : il y en a 11, de la normalisation et du compresseur à l'écho et à la réverbération. La chaîne, la vitesse et le volume se règlent dans l'inspecteur de piste audio

## Inspecteur de piste audio

Montre le clip de la piste audio sélectionnée, sa vitesse, le volume du fader et la chaîne d'effets.
Les effets : passe-bas, passe-haut, écho, réverbération, chorus, changement de hauteur, distorsion, flanger, compresseur, normalisation et un égaliseur paramétrique

`{{ui:field_common_speed}}` et `{{ui:editor_inspector-audio_volume}}` sont des curseurs, pas des champs de saisie. Ainsi, la plage autorisée est visible

> [!caution] Attention
> **Le volume ici est un fader.** Le volume en images clés est une piste distincte sur la timeline locale. Pendant la lecture, les deux se multiplient

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Normaliser

Tire constamment le signal vers un volume cible. Ainsi, des clips de sources différentes sonnent aussi fort sans réglage manuel.
Utilise-le si les pistes du niveau n'ont pas été mixées ensemble

Il agit sur le volume global. La dynamique à l'intérieur d'une piste se change avec le [[7_audio#Compresseur|Compresseur]]

- `Lowest Volume` l'empêche de remonter le silence et le bruit jusqu'au souffle
- `Maximum Amp` limite combien il peut amplifier

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Compresseur

Écrase les parties fortes pour que les faibles puissent sonner plus haut. Une piste compressée s'entend sous tout le reste du niveau et ne sature pas.
On l'utilise d'habitude pour réparer une chanson qui se perd derrière ses propres effets

- `Threshold` - à partir d'où il commence à agir
- `Attack` et `Release` - à quelle vitesse il serre et relâche. Trop vite et tu coupes les attaques ou tu obtiens un pompage audible
- `Make Up Gain` rend le volume qu'il a pris

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Passe-bas

Laisse passer les graves et coupe tout ce qui est au-dessus de `Cutoff Freq`. On dirait que le son vient de sous l'eau ou de derrière un mur

Baisse la fréquence de coupure : la piste perd d'abord son air, puis sa clarté, et à la fin tout sauf les basses.
En haut de la plage, le filtre est presque transparent. La piste sonne comme le fichier

> [!tip] Conseil
> La chaîne d'effets appartient à la **piste** et ne s'anime pas en images clés. Elle ne peut pas changer en douceur dans le temps. Coupe la piste là où le changement est nécessaire et règle les moitiés différemment

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Passe-haut

Le miroir du passe-bas : laisse passer les aigus et coupe tout ce qui est en dessous de `Cutoff Freq`

Monte la fréquence de coupure : la piste s'amincit jusqu'à un petit haut-parleur ou un appel téléphonique.
On l'utilise d'habitude pour faire sonner les choses petites avant que tout s'ouvre

> [!tip] Conseil
> La chaîne d'effets appartient à la **piste** et ne s'anime pas en images clés. Elle ne peut pas changer en douceur dans le temps. Coupe la piste là où le changement est nécessaire et règle les moitiés différemment

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## EQ paramétrique

Une seule bande paramétrique : amplifie ou coupe une partie choisie du spectre.
Contrairement au [[7_audio#Passe-bas|passe-bas]] et au [[7_audio#Passe-haut|passe-haut]], il peut aussi ajouter. C'est pourquoi on l'utilise pour faire de la place dans le mix plutôt que pour créer un effet

- `Center Freq` - où se trouve la bande
- `Octave Range` - la largeur de la bande. Étroite pour une correction précise, large pour une coloration d'ensemble
- `Frequency Gain` sous 1 coupe, au-dessus de 1 amplifie

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Distorsion

Écrête la forme d'onde. Le son se remplit d'harmoniques qu'il n'avait pas : sale, saturé, rageur.
L'effet le plus simple ici : un seul bouton, `Level` - à quel point l'écrêtage mord

Par effet secondaire, elle aplatit la dynamique. Une piste très distordue perd ses parties calmes.
Là où une section doit sonner implacable, c'est utile. Là où elle ne le doit pas, c'est destructeur

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Écho

Répète le signal à intervalles égaux. Chaque répétition est plus faible que la précédente.
Un écho est rythmique, et les répétitions peuvent se compter. C'est ce qui le distingue de la queue floue de la [[7_audio#Réverbération|réverbération]] : tu entends des copies séparées, pas une pièce

- `Delay` - la distance entre les copies en millisecondes
- `Decay` - quelle part de chaque copie passe dans la suivante

Prends le délai à partir du tempo de la chanson, et l'écho tombera sur la pulsation au lieu de la brouiller

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Réverbération

Place la piste dans un espace. D'abord viennent les premières réflexions sur les murs proches, puis une queue qui s'estompe.
C'est le plus gros effet ici : ses champs décrivent une pièce, pas une répétition. Les répétitions, c'est le travail de l'[[7_audio#Écho|écho]]

Le son principal se règle avec trois champs :
- `Decay Time` - la taille de la pièce
- `Room` - combien on l'entend
- `Room HF` - baisse-le et les murs sonnent doux et absorbants

Le reste, c'est du réglage fin. Passe-y une fois ces trois champs justes

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Chorus

Superpose au signal trois copies légèrement retardées, à la hauteur ondulante. Une seule source sonne comme plusieurs.
Le résultat, c'est de la largeur et de l'épaisseur, pas une répétition. Les retards sont trop courts pour s'entendre séparément

Les trois copies le distinguent du [[7_audio#Flanger|flanger]], où une seule copie balaie

- `Rate` - la vitesse de l'ondulation
- `Depth` - l'amplitude de l'ondulation
- `Feedback` - monte-le et le son se rapproche d'un flanger

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Flanger

Mélange au signal lui-même un retard très court et ondulant de ce signal. Les deux s'annulent à des fréquences qui bougent avec le retard.
Ce creux qui se déplace, c'est le souffle d'un moteur à réaction. L'effet vient de l'annulation, pas d'une copie

C'est la même famille que le [[7_audio#Chorus|chorus]]. Mais il y a une seule copie et le retard est plus court, donc tu entends un balayage, pas de la largeur

Le creux est le plus profond quand `Dry Mix` et `Wet Mix` sont réglés proches l'un de l'autre

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]

## Changement de hauteur

Change la hauteur de la piste sans changer sa vitesse.
Tout l'intérêt est là : le timing du niveau est lié à la chanson. La piste ne peut donc pas simplement être rééchantillonnée, comme le fait le champ `{{ui:field_common_speed}}` de la piste elle-même

- `Pitch` - un multiplicateur. 1 ne change rien, 2 monte d'une octave
- `FFT Size` et `Overlap` échangent la qualité contre le coût

Avec un grand décalage, le son s'entendra toujours comme traité

> [!tip] Conseil
> La chaîne d'effets appartient à la **piste** et ne s'anime pas en images clés. Elle ne peut pas changer en douceur dans le temps. Coupe la piste là où le changement est nécessaire et règle les moitiés différemment

> [!info] Bon à savoir
> La **réinitialisation** à côté de ce bouton remet chaque champ à sa valeur par défaut, `{{ui:field_common_mix-level}}` compris. Sa valeur par défaut est le plancher de -80 dB, donc la réinitialisation désactive aussi l'effet

Plus : [[2_preparing-the-track|Préparer la piste audio]]
