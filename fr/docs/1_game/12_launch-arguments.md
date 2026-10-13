---
title: Arguments de lancement
date: 2026-10-12
tags: [advanced_player, developer]
---

# Arguments de lancement

Les arguments de lancement ouvrent directement un écran, un niveau ou une partie, et les interrupteurs modifient un seul lancement du jeu. Ils se placent après l'exécutable : dans un raccourci, un terminal ou les options de lancement de Steam

Sans arguments, le jeu ouvre le menu principal

Un assistant IA connecté par MCP peut envoyer les mêmes arguments à un jeu déjà lancé - [[7_ai-assistant]]

## Syntaxe

- chaque argument commence par deux tirets : `--editor`
- une valeur suit après un espace ou après `=` : `--speed 1.5` et `--speed=1.5` sont équivalents
- la casse de la clé n'a pas d'importance : `--Editor` fonctionne aussi
- les nombres utilisent un point quelle que soit la langue du système : `1.5`, jamais `1,5`
- une valeur avec des espaces se met entre guillemets doubles : `--level "D:\My Levels\Volcano"`

**Un argument que le jeu ne peut pas utiliser n'arrête jamais le lancement.** Il est abandonné, une ligne à son sujet part dans le log, et le jeu ouvre son écran habituel. Où est le log - [[11_help#Logs]]

**Les arguments inconnus sont ignorés.** Le jeu ne lit que ses propres arguments, ceux à deux tirets. Les arguments d'Unity à un seul tiret, par exemple `-screen-width`, passent sans être touchés. C'est avec eux que se règlent la résolution et le plein écran

## Écrans

| Argument | Ce qui s'ouvre |
|---|---|
| `--menu` | le menu principal, comme sans arguments |
| `--editor` | l'éditeur de niveaux |
| `--game` | le niveau indiqué dans `--level`, et la partie démarre tout de suite |
| `--settings` | le menu principal avec l'écran des paramètres par-dessus |

On passe au plus un argument d'écran. Deux arguments différents s'annulent, et le menu s'ouvre avec un avertissement dans le log

`--settings` peut nommer un onglet : `general`, `audio`, `controls`, `keybindings`, `graphics`, `interface`, `game-editor`, `profile`, `other`. Sans nom, les paramètres s'ouvrent sur l'onglet où tu étais la dernière fois. Un nom inconnu est abandonné, et les paramètres s'ouvrent quand même

Les paramètres s'ouvrent une fois par lancement. Si tu reviens au menu plus tard, ils ne se rouvrent pas. Ce que contient chaque onglet - [[4_settings]]

## Choisir un niveau

`--level` désigne un niveau par son identifiant (`LevelId`) ou par le chemin de son dossier. Un titre ne fonctionne jamais : les titres se répètent, se traduisent et se modifient. Une valeur qui se lit comme un identifiant est toujours prise comme un identifiant

Le niveau est cherché parmi ceux que le jeu affiche déjà dans sa liste. Le jeu ne trouvera pas un dossier qui n'est pas dans la liste

| Avec | Ce qui se passe |
|---|---|
| rien | le menu s'ouvre sur l'écran du niveau et attend `{{ui:menu_levelview_play-btn}}` |
| `--editor` | l'éditeur s'ouvre avec ce niveau |
| `--game` | la partie démarre tout de suite |

Un mot de passe n'est jamais passé en argument. Un niveau protégé le demande à l'écran et s'ouvre après la réponse

## Conditions de partie

Ces conditions remplissent les contrôles de l'écran du niveau, et la partie démarre comme si tu avais appuyé sur `{{ui:menu_levelview_play-btn}}`. Elles ne fonctionnent qu'avec `--game`. Sans lui, elles sont ignorées, avec un avertissement dans le log

| Argument | Valeur | Contrôle sur l'écran du niveau |
|---|---|---|
| `--speed` | au-dessus de `0` et jusqu'à `2`, arrondi à `0.1` | `{{ui:field_common_speed}}` |
| `--lives` | de `0` à `16`, `0` correspond à `{{ui:menu_levelview_options-lifes_option-zen}}` | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0` ou un entier positif, `0` veut dire une nouvelle graine à chaque partie | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`, `reflex`, `warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`, `--no-checkpoints` | - | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | - | `{{ui:menu_levelview_options-no-collision_title}}` |

Une condition omise prend sa valeur par défaut : 3 vies, vitesse `1.0`, checkpoints activés, pas de bot, graine `0`, collisions activées

Une partie lancée ainsi est une partie ordinaire. Elle entre dans les statistiques comme n'importe quelle autre, [[10_statistics]]

## Interrupteurs pour tout le lancement

Ces trois-là fonctionnent avec n'importe quel écran et ne modifient jamais un paramètre enregistré :

| Argument | Ce qu'il fait |
|---|---|
| `--autosave on`, `--autosave off` | active ou désactive l'enregistrement automatique de l'éditeur pour ce lancement. L'onglet de paramètres `{{ui:settings_game-editor_title}}` montre la valeur forcée et ne permet pas de la changer |
| `--suppress-game-saves` | mode anonyme pour tout le lancement. Il ne peut pas être désactivé dans le jeu, [[4_settings#Mode anonyme]] |
| `--frame-stats` | écrit dans le log un résumé du temps par image, avec le temps GPU et CPU. Sert aux mesures de performances |

`--frame-stats` écrit une ligne par écran toutes les 30 secondes, et aussi à chaque changement de la fenêtre au-dessus de l'écran. Les 3 premières secondes d'un écran ne sont pas comptées

## Combinaisons

| Commande | Résultat |
|---|---|
| rien ou `--menu` | menu |
| `--editor` | l'éditeur sans niveau ouvert |
| `--settings` | menu, paramètres ouverts sur l'onglet où tu étais la dernière fois |
| `--settings graphics` | la même chose, sur l'onglet `{{ui:settings_graphics_title}}` |
| `--level X` | menu sur l'écran du niveau X, attend `{{ui:menu_levelview_play-btn}}` |
| `--level X --game` | niveau X, une partie en cours |
| `--level X --editor` | l'éditeur avec le niveau X ouvert |
| `--game` sans `--level` | menu et un avertissement |
| `--menu --editor` | menu et un avertissement |
| `--speed 2` sans `--game` | la condition est ignorée, avec un avertissement |
| `--editor --autosave off` | l'éditeur, enregistrement automatique désactivé pour ce lancement seulement |
| `--autosave maybe` | ignoré avec un avertissement, ton paramètre décide |
| `--suppress-game-saves` | menu. Aucun des enregistrements propres du jeu pendant ce lancement n'atteint le disque |
| `--level X --game --suppress-game-saves` | niveau X, une partie en cours, et aucune statistique ne reste après |
| `--editor --suppress-game-saves` | l'éditeur. Les enregistrements des niveaux, l'enregistrement automatique et les sauvegardes sont écrits, les paramètres et les statistiques non |

## Exemples

Sur Windows, depuis un terminal ou un raccourci :

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

Dans Steam, les options de lancement du jeu ne prennent que les arguments, sans l'exécutable : `--editor --autosave off`

## Android

Android n'a pas de ligne de commande. Les arguments sont passés dans l'extra de type chaîne `bh` de l'intent qui lance le jeu, et sont découpés exactement comme une ligne tapée. Depuis un ordinateur, cela se fait avec `adb` :

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **Les guillemets comptent.** Tout le `am start` va entre guillemets doubles, la valeur de `bh` entre guillemets simples. Sinon le shell de l'appareil découpe la ligne : seul le premier argument atteint `bh`, et les autres vont à `am` comme ses propres paramètres
- **`-S` arrête d'abord le jeu en cours.** Les arguments sont lus une seule fois, au lancement. Les envoyer à un jeu déjà lancé ne change rien

iOS n'a pas du tout d'arguments de lancement
