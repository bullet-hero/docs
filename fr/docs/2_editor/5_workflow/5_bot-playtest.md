---
title: Comment un bot joue ton niveau
date: 2026-10-02
tags: [level_author]
---

# Comment un bot joue ton niveau

Un bot joue le niveau avec les mêmes contrôles que toi et vérifie la lisibilité, pas la difficulté. Il ne garantit pas que le niveau puisse être terminé

Il observe ce qui vole, cherche de l'espace libre et déplace le même personnage que toi.
Il marche, fait des dashs, subit des dégâts et meurt

Le bot se choisit avant le début d'un niveau, à côté des vies et de la vitesse

## Un bot dans l'éditeur

Dans l'éditeur, un bot dirige le joueur d'aperçu :
1. Ouvre `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_player_title}}`
2. Coche `{{ui:settings_game-editor-player_bot}}`
3. Active le joueur d'aperçu dans la barre d'outils

Le joueur d'aperçu n'a pas de choix de bot, c'est toujours `{{ui:enum_bot-kind_reflex}}`. Seul ce bot n'a besoin de rien de préparé à l'avance.
Il continue de fonctionner pendant que tu modifies le niveau, à n'importe quelle vitesse de lecture, marche arrière comprise

Juste après un balayage, le bot joue moins bien pendant un instant : il réapprend ce qui l'attend

Pendant que tu fais glisser une poignée de gizmo ou que tu tapes dans un champ de texte, le joueur d'aperçu n'écoute pas tes contrôles

**`{{ui:settings_game-editor-player_bot-debug}}`**, dans les mêmes paramètres, dessine par-dessus le niveau. C'est désactivé par défaut, et ses trois parties sont activées, donc dès que tu l'actives tu vois tout le tableau d'un coup :
- `{{ui:settings_game-editor-player_bot-debug-grid}}` - combien d'espace libre le bot pense avoir dans chaque partie de l'écran. Le rouge marque l'endroit où il s'attend à être touché, et la couleur s'estompe à mesure que l'espace grandit. Rien n'est dessiné là où il se considère en sécurité
- `{{ui:settings_game-editor-player_bot-debug-target}}` - le point vers lequel il se dirige. Une cible qui ne bouge pas signifie que le bot est satisfait, pas bloqué
- `{{ui:settings_game-editor-player_bot-debug-reach}}` - jusqu'où il compte aller : l'anneau intérieur en marchant, l'extérieur avec un dash. Il ne choisit jamais de cible en dehors d'eux

Seul `{{ui:enum_bot-kind_reflex}}` est dessiné. Active-le en pause, là où l'image reste immobile

**Une partie complète avec n'importe quel bot.** Dans les paramètres du niveau, sur l'onglet `{{ui:settings_level-settings_play}}`, il y a la même liste `{{ui:settings_level-settings_bot}}` que sur l'écran du niveau dans le menu : `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`. Cela lance une vraie partie du niveau, pas le joueur d'aperçu

## Lire le résultat

Un bot vérifie la lisibilité, pas la difficulté :
- le bot passe tranquillement une section qui est difficile pour toi. Alors la section se lit bien, et c'est l'entraînement qui te manque
- le bot est touché au même endroit encore et encore. Regarde cet endroit : en général, c'est un danger qui ne laisse aucune place pour s'échapper. Un humain ne le lira pas mieux

## Ce qu'un bot promet et ce qu'il ne promet pas

**Un bot ne garantit pas que le niveau puisse être terminé.** C'est un joueur qui ne se fatigue pas, pas un joueur qui ne perd pas.
Si une section exige d'entrer correctement dans un motif une seconde avant son arrivée, le bot sera touché. Ce n'est pas un bug

> [!info] Bon à savoir
> Un bot ne peut pas tricher, c'est ainsi qu'il est construit. Il a les mêmes contrôles qu'un joueur et rien de plus : la même vitesse, le même dash, la même hitbox, les mêmes dégâts. Là où un joueur ne peut pas passer, le bot ne le peut pas non plus

**Un bot charge l'appareil.** Il cherche de l'espace libre à chaque image.
Sur un appareil faible, attends-toi à des chutes d'images par seconde. Sur un niveau lourd, les premières secondes seront les pires

## Un niveau qui a battu le bot

Les bots ne progressent que sur des niveaux qu'ils n'ont pas encore vus. Les niveaux qu'un bot termine déjà ne lui apprennent rien

Ton niveau a battu le bot ? Envoie-le :
1. Ouvre une issue dans [bullet-hero/releases](https://github.com/bullet-hero/releases/issues)
2. Écris quel bot a perdu et où
3. Joins le dossier du niveau

Suite : [[1_readability-and-fairness|Lisibilité et équité]], [[3_difficulty-curve|Difficulté]]
