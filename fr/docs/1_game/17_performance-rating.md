---
title: Évaluation des performances
date: 2026-10-15
tags: [player, level_author]
---

# Évaluation des performances

Avant de jouer, le jeu montre à quel point un niveau est lourd pour ton appareil. Vert veut dire qu'il tourne bien, jaune que c'est juste, rouge qu'il est trop lourd et que la fréquence d'images va chuter

Le score est un nombre où `{{v:performance.score-limit}}` correspond exactement au temps qu'une image peut prendre à ta fréquence d'images cible. La tranche découle du score :

| Tranche | Score |
|---|---|
| `{{ui:level_performance_holds}}` | sous `{{v:performance.score-warning}}` |
| `{{ui:level_performance_tight}}` | de `{{v:performance.score-warning}}` à `{{v:performance.score-limit}}` |
| `{{ui:level_performance_does-not-hold}}` | au-dessus de `{{v:performance.score-limit}}` |
| `{{ui:level_performance_unknown}}` | le niveau ou l'appareil n'a pas été mesuré |

Le score est une prévision pour le moment le plus lourd du niveau, pas pour sa moyenne. Un niveau léger pendant trois minutes qui se fige une seconde reçoit le score de cette seconde

## Où le voir

- le navigateur de niveaux : un point de couleur sur chaque carte de niveau et le groupe `{{ui:root_level-filters_performance}}` dans les filtres
- la page du niveau dans le menu : la tranche et le score
- l'éditeur de niveaux, dans les métadonnées du niveau : le score sur ton appareil et sur les appareils de référence, plus les moments les plus lourds du niveau sous forme d'horodatages

## Les deux moitiés du score

**La moitié du niveau** est mesurée quand le niveau est enregistré dans l'éditeur et stockée dans ses métadonnées. Elle décrit ce que le niveau demande : combien d'objets sont vivants, quelle part de l'écran ils couvrent, combien d'effets et de passes de post-traitement tournent. Un niveau enregistré avant cette fonction n'a pas cet enregistrement et s'affiche comme `{{ui:level_performance_unknown}}` jusqu'à ce qu'il soit enregistré à nouveau. L'éditeur le mesure à l'ouverture du niveau et garde le résultat jusqu'à la fermeture du jeu, sans l'écrire dans le fichier

**La moitié de l'appareil** dit à quelle vitesse ton appareil fait chacune de ces choses. Tant que tu n'as pas mesuré ton appareil, le jeu utilise un appareil de référence de ta plateforme. Tes réglages comptent aussi : l'échelle de rendu, l'anticrénelage, les effets et le post-traitement changent le score sans nouvelle mesure

## Mesurer ton appareil

1. Depuis le menu principal, ouvre `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. Appuie sur `{{ui:settings_graphics-performance_measure}}`
3. Attends quelques minutes. L'écran des réglages se masque et le jeu lance des niveaux de test. Ne passe pas à une autre application

À la fin, la section indique ce qui limite ton appareil (le processeur ou la puce graphique) et quel préréglage `{{ui:settings_quick-setup_performance}}` elle conseille

Si la mesure était instable (l'appareil a trop chauffé, une autre application était occupée), le jeu l'ignore et garde l'appareil de référence. Ferme les autres applications et mesure à nouveau

## Passer à un autre appareil

La mesure appartient à l'appareil sur lequel elle a été faite. Le transfert de profil ([[14_profile-transfer]]) et les sauvegardes dans le cloud ne la transportent pas, donc un nouvel appareil part de son appareil de référence jusqu'à ce que tu le mesures à nouveau
