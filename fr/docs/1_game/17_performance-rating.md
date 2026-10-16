---
title: Évaluation des performances
date: 2026-10-17
tags: [player, level_author]
---

# Évaluation des performances

Avant de jouer, le jeu montre à quel point un niveau est lourd pour ton appareil, avec une jauge de cinq barres : plus il y a de barres allumées, plus le niveau est léger. Des barres vertes veulent dire qu'il tourne bien, jaunes que c'est juste, rouges que la fréquence d'images va chuter

Le score est un nombre où `{{v:performance.score-limit}}` correspond exactement au temps qu'une image peut prendre à ta fréquence d'images cible. La tranche découle du score :

| Barres | Tranche | Score |
|---|---|---|
| 5 | `{{ui:level_performance_holds}}` | sous `{{v:performance.score-warning}}` |
| 4 | `{{ui:level_performance_tight}}` | de `{{v:performance.score-warning}}` à `{{v:performance.score-limit}}` |
| 3 | `{{ui:level_performance_drops}}` | au-dessus de `{{v:performance.score-limit}}`, jusqu'à `{{v:performance.score-heavy}}` |
| 2 | `{{ui:level_performance_severe-drops}}` | au-dessus de `{{v:performance.score-heavy}}`, jusqu'à `{{v:performance.score-severe}}` |
| 1 | `{{ui:level_performance_does-not-hold}}` | au-dessus de `{{v:performance.score-severe}}` |
| aucune | `{{ui:level_performance_unknown}}` | le niveau ou l'appareil n'a pas été mesuré |

Le score est une prévision pour le moment le plus lourd du niveau, pas pour sa moyenne. Un niveau léger pendant trois minutes qui se fige une seconde reçoit le score de cette seconde

## Où le voir

- le navigateur de niveaux : la jauge sur chaque carte de niveau et le groupe `{{ui:root_level-filters_performance}}` dans les filtres
- la page du niveau dans le menu : la jauge, la tranche et le score
- l'éditeur de niveaux, dans les métadonnées du niveau : le score sur ton appareil et sur les appareils de référence, plus les moments les plus lourds du niveau sous forme d'horodatages

## Les deux moitiés du score

**La moitié du niveau** est mesurée dans l'éditeur dans les secondes qui suivent chaque enregistrement, pendant que vous continuez à travailler, et stockée dans ses métadonnées. Si vous quittez l'éditeur avant la fin, le fichier garde la mesure précédente. Elle décrit ce que le niveau demande : combien d'objets sont vivants, quelle part de l'écran ils couvrent, combien d'effets et de passes de post-traitement tournent. Un niveau enregistré avant cette fonction n'a pas cet enregistrement et s'affiche comme `{{ui:level_performance_unknown}}` jusqu'à ce qu'il soit enregistré à nouveau. L'éditeur le mesure à l'ouverture du niveau et garde le résultat jusqu'à ce que vous quittiez l'éditeur, sans l'écrire dans le fichier

**La moitié de l'appareil** dit à quelle vitesse ton appareil fait chacune de ces choses. Tant que tu n'as pas mesuré ton appareil, le jeu utilise un appareil de référence de ta plateforme. Tes réglages comptent aussi : l'échelle de rendu, l'anticrénelage, les effets et le post-traitement changent le score sans nouvelle mesure

## Mesurer ton appareil

1. Depuis le menu principal, ouvre `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. Appuie sur `{{ui:settings_graphics-performance_measure}}`. Une fenêtre indique ce qui aide la mesure : fermer les autres applications et jeux, brancher un téléphone ou un portable sur le chargeur, ne pas toucher l'appareil
3. Appuie sur `{{ui:settings_graphics-performance_start}}` et attends jusqu'à {{v:performance.benchmark-max-seconds}} secondes. L'écran des réglages se masque, le jeu lance des niveaux de test et affiche dans les coins supérieurs ce qu'il mesure. Ne passe pas à une autre application

`{{ui:settings_graphics-performance_stop}}` arrête la mesure plus tôt. Une mesure arrêtée ou à court de temps n'enregistre rien, et le résultat précédent reste

À la fin, la fenêtre affiche le résultat : la jauge du niveau de démo sur ton appareil, ce qui limite ton appareil (le processeur ou la puce graphique), quel préréglage `{{ui:settings_quick-setup_performance}}` elle conseille et combien de tes niveaux tombent dans chaque tranche. `{{ui:settings_graphics-performance_again}}` mesure une fois de plus

Si la mesure était instable (l'appareil a trop chauffé, une autre application était occupée), le jeu l'utilise quand même, car elle est plus proche de ton appareil que n'importe quelle référence, et la fenêtre le signale. Ferme les autres applications et mesure à nouveau pour un score plus précis

## Passer à un autre appareil

La mesure appartient à l'appareil sur lequel elle a été faite. Le transfert de profil ([[14_profile-transfer]]) et les sauvegardes dans le cloud ne la transportent pas, donc un nouvel appareil part de son appareil de référence jusqu'à ce que tu le mesures à nouveau
