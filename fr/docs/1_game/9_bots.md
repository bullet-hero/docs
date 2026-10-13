---
title: Bots
date: 2026-10-02
tags: [player, advanced_player]
---

# Bots

Un bot joue un niveau à ta place avec tes propres contrôles. Il regarde ce qui arrive, cherche de l'espace libre et déplace le même personnage que toi : il marche, fait des dashs, subit des dégâts et meurt

**Un bot ne garantit pas la réussite.** Il ne se fatigue pas, mais il peut perdre. Si un motif doit être abordé correctement une seconde avant qu'il arrive, le bot se fait toucher. Rien n'est cassé quand cela arrive

**Un bot charge l'appareil.** Chercher de l'espace libre est un vrai travail à chaque image. Attends-toi à des chutes d'images par seconde sur un appareil faible. Sur un niveau lourd, les premières secondes sont les pires

Pour choisir un bot, utilise la condition `{{ui:menu_levelview_options-bot}}` sur l'écran du niveau : `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}` ou `{{ui:enum_bot-kind_warm}}`. Il se choisit pour chaque partie, comme les vies et la vitesse

> [!info] Bon à savoir
> Un bot ne peut pas tricher, et c'est ainsi qu'il est construit, pas une promesse. Il a les mêmes contrôles que toi et rien de plus : la même vitesse, le même dash, la même hitbox, les mêmes dégâts. Il ne peut rien traverser que tu ne pourrais pas traverser

## Un niveau a battu le bot ?

Les bots s'améliorent sur les niveaux qu'ils n'ont pas encore vus. Un tel niveau vaut la peine d'être envoyé

Ouvre une issue dans [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Écris quel bot a perdu et où, et joins le dossier du niveau

## Deux bots

À chaque image, un bot donne une entrée, comme le fait un clavier, et rien d'autre. Il n'a accès ni à la position de l'avatar, ni à sa santé, ni à l'état du niveau.
Si le bot ne répond pas à une image, c'est ton appareil qui dirige à cette image

| | `{{ui:enum_bot-kind_reflex}}` | `{{ui:enum_bot-kind_warm}}` |
|---|---|---|
| Ce qu'il connaît | les 1,5 secondes suivantes, recalculées à chaque image | tout le niveau, calculé une fois |
| Quand il charge l'appareil | à chaque image pendant qu'il joue | une fois, avant la partie |
| Ce qu'il sait faire | éviter ce qu'il voit devant lui | suivre un plan qu'aucune anticipation ne trouverait jamais |
| Ce qui le met en échec | un motif qu'il fallait aborder une seconde plus tôt | un niveau qui a changé sous lui |
| Comment il dirige | par direction | par cible |

Le bot Warm vise zéro dégât. Il le paie par une étape de chargement supplémentaire, `{{ui:root_loading_baking}}`. Elle peut durer des dizaines de secondes

Le `?` à côté de `{{ui:menu_levelview_options-bot}}` prévient de cela à l'avance, avec un paragraphe par bot. `{{ui:root_loading_cancel}}` arrête le calcul et te rend la partie.
L'itinéraire du bot Warm dépend de la graine, [[8_determinism]]

## Où d'autre jouent les bots

- **Le joueur de test de l'éditeur** : `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor-player_bot}}`. Seul le bot Reflex y joue : il n'a besoin de rien de préparé à l'avance et il survit aux retours en arrière. Plus - [[5_bot-playtest]]
- **L'arrière-plan du menu principal** : l'arène derrière les boutons est un bot Reflex qui joue en direct sans aucune anticipation

Le bot fait partie des conditions d'un record. Une partie de bot ne remplace donc jamais ton meilleur résultat, [[10_statistics]]
