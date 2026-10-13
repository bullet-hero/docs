---
title: Publication
date: 2026-10-11
tags: [level_author]
---

# Publication

Un niveau ne s'envoie que depuis l'onglet "Publication" des paramètres du niveau : sous forme d'archive ou vers le Steam Workshop. Le rapport vérifie le niveau de lui-même, et ses erreurs bloquent l'envoi

## L'onglet "Publication"

`Publication` est un onglet des paramètres du niveau. C'est le seul endroit d'où un niveau est envoyé quelque part

En haut, `{{ui:editor_share_destination}}` montre la façon d'envoyer choisie. Appuyer dessus ouvre `{{ui:editor_share_pick-title}}` : les façons que cette version propose sur cet appareil, chacune avec une description d'une ligne.
`{{ui:editor_share_archive}}` est choisi par défaut. Le dernier choix est retenu jusqu'à la fermeture du jeu

En dessous :
- les paramètres propres à cette façon
- son rapport
- le bouton qui la lance : `{{ui:editor_share_export}}` ou `Publier`

Si cette version n'offre aucune façon sur cet appareil, l'onglet affiche `{{ui:editor_share_none}}`

## Le rapport

Le rapport vérifie de lui-même : quand une façon s'ouvre et quand l'un de ses paramètres change. Il n'y a pas de bouton pour cela.
Il commence par la ligne `Errors: N, warnings: N, advice: N`, suivie d'une ligne par problème

Les erreurs bloquent l'envoi. Les avertissements et les conseils sont à ta discrétion

La façon décide des règles selon lesquelles le niveau est jugé. `{{ui:editor_share_archive}}` vérifie selon l'ensemble `{{ui:editor_publish_profile-local}}`, `{{ui:editor_share_steam}}` selon les règles du Workshop. Ce que chaque ensemble exige et ce que veut dire chaque verdict - [[5_publish-readiness]]

## Façons d'envoyer

| Façon | Où elle existe | Ce qu'elle envoie |
|---|---|---|
| `{{ui:editor_share_archive}}` | sur tout appareil doté d'une boîte de dialogue d'enregistrement. Pas sur iOS | un niveau, une collection ou une seule ressource, sous forme de fichier |
| `{{ui:editor_share_steam}}` | la version Steam seulement | un niveau ou une de tes collections |

Une façon que cette version ou cet appareil n'a pas n'apparaît tout simplement pas dans la liste

## Archive

Pour un niveau :

| Élément | Ce qu'il fait |
|---|---|
| `{{ui:editor_share_format}}` | l'un des sept modes d'export, d'un simple dossier à une archive protégée par mot de passe |
| `{{ui:editor_share_passphrase}}` | visible seulement dans les modes protégés. Un mode protégé avec un mot de passe vide ne se lance pas |
| `{{ui:editor_share_export}}` | écrit le niveau là où tu l'indiques |

Ce que chaque mode écrit et ce qui l'ouvre - [[13_export-and-protection#Exporter le niveau]]

Pour une collection ou une seule ressource, `{{ui:editor_share_format}}` propose cinq de ces modes, et tous sont des archives. Il n'y a pas de mode dossier :

| `{{ui:editor_share_format}}` | Ce que tu obtiens | Ce qui l'ouvre |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_zip}}` | un seul fichier | un double clic dans l'Explorateur Windows, rien à installer |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | un zip avec chiffrement AES-256 intégré | 7-Zip ou un autre archiveur, qui demande le mot de passe |
| `{{ui:settings_level-settings_export-mode_zip-protected}}` | tout le zip enveloppé dans OpenPGP | gpg |
| `{{ui:settings_level-settings_export-mode_targz}}` | un seul fichier | n'importe quel archiveur |
| `{{ui:settings_level-settings_export-mode_targz-protected}}` | un tar.gz enveloppé dans OpenPGP | gpg |

`{{ui:editor_share_passphrase}}` apparaît dans les trois modes avec mot de passe. Avec un mot de passe vide, rien n'est exporté.
La vérification de collection ci-dessous s'applique, selon les mêmes règles `{{ui:editor_publish_profile-local}}`

## Steam Workshop

Versions Steam seulement. Les éléments :

| Élément | Ce qu'il fait |
|---|---|
| `{{ui:editor_publish_visibility}}` | qui voit l'élément : `{{ui:editor_publish_visibility-public}}`, `{{ui:editor_publish_visibility-friends-only}}` ou `{{ui:editor_publish_visibility-private}}`. Par défaut `{{ui:editor_publish_visibility-private}}` |
| `{{ui:editor_publish_changelog}}` | la note de modification de cet envoi. Un champ multiligne, avec son étiquette sur sa propre ligne |
| `Title and description go up in` | la langue dans laquelle le texte de l'élément est pris (voir ci-dessous) |
| `{{ui:editor_share_steam-descriptors}}` | cinq cases à cocher, les descripteurs de contenu propres à Steam (voir ci-dessous) |
| `Publier` | envoie le niveau |

Le niveau est toujours vérifié selon les règles du Workshop. Il n'y a pas de choix de règles ici

L'élément du Workshop est rempli à partir du niveau :
- le titre et la description sont le nom et la description du niveau, dans une seule langue
- l'aperçu est la couverture du niveau, en png ou jpg, de 1 Mo au plus. Toute autre couverture est ignorée, et l'élément est envoyé sans image
- le jeu fixe les tags lui-même, voir "Tags du Workshop" plus bas

Le premier appui sur `Publier` crée l'élément. Les suivants mettent à jour le même élément.
Le jeu le retrouve par l'ID propre du niveau parmi les éléments que tu as publiés, donc rien n'est stocké dans le niveau

Un niveau protégé ne peut pas être publié. Plus - [[13_export-and-protection]]

L'envoi emporte le dossier `ai` du niveau, où un assistant IA garde ses notes sur le niveau, sauf si `{{ui:settings_level-settings_metadata-level-ai-share}}` est décoché dans les métadonnées du niveau. Tous ceux qui s'abonnent le reçoivent avec le niveau. Plus - [[7_ai-assistant#Le dossier ai]]

> [!warning] Avertissement
> Si tu n'as pas accepté l'accord juridique du Steam Workshop, l'élément est envoyé mais reste masqué. Accepte l'accord sur la page de l'élément. Le jeu ouvre cette page dans l'overlay Steam

### Langue du titre

Steam affiche un titre et une description par élément. Le jeu prend la première langue qu'il trouve, dans cet ordre :
1. `{{ui:settings_game-editor_publish-language}}` dans les paramètres `{{ui:settings_game-editor_title}}` : `{{ui:enum_publish-language_english}}` (par défaut) ou `{{ui:enum_publish-language_system}}`, la langue de l'appareil. Plus - [[14_editor-settings]]
2. ta propre langue, c'est-à-dire celle de l'interface du jeu
3. l'anglais
4. la première langue dans laquelle le texte a été écrit

La description est cherchée d'abord dans la langue du titre, pour qu'ils correspondent.
Un nom non localisé (texte simple) est envoyé exactement tel qu'il est écrit, et la ligne affiche `{{ui:editor_share_steam-language-as-written}}`

### Descripteurs de contenu

`{{ui:editor_share_steam-descriptors}}` a cinq cases à cocher, les descripteurs de contenu propres à Steam :
- `{{ui:editor_share_steam-descriptor-mature}}`
- `{{ui:editor_share_steam-descriptor-violence}}`
- `{{ui:editor_share_steam-descriptor-some-nudity}}`
- `{{ui:editor_share_steam-descriptor-frequent-nudity}}`
- `{{ui:editor_share_steam-descriptor-adult-only}}`

Ils sont envoyés à chaque publication et ne sont jamais stockés dans le niveau. Chaque publication envoie l'ensemble complet, donc une case décochée retire aussi le descripteur d'un élément déjà publié.
Ils partent dans une seconde mise à jour juste après l'envoi. Si cette partie échoue, l'élément est quand même publié, et le résultat indique que les descripteurs n'ont pas été fixés

### Après la publication

En cas de succès, le formulaire montre quel élément a été créé ou mis à jour, et un bouton `{{ui:editor_publish_open-item}}`. Il ouvre la page de l'élément dans Steam

En cas d'échec, le formulaire montre :
- la raison en mots simples, `Publishing failed: ...`
- `What was sent and what Steam answered: ...` - une ligne technique en anglais. Elle vaut la peine d'être citée au développeur quand tu signales un problème
- un `?` qui déplie pourquoi Steam refuse de cette façon, et trois liens : `{{ui:editor_publish_help-docs}}` (cette page), `{{ui:editor_publish_help-steam-support}}` et `{{ui:editor_publish_help-agreement}}`

Les lignes de journal propres au jeu sur la publication sont toujours en anglais, quelle que soit la langue de l'interface

| Raison | Que faire |
|---|---|
| `{{ui:enum_workshop-failure_steam-not-running}}` | lance Steam et relance le jeu depuis Steam |
| `{{ui:enum_workshop-failure_not-owner}}` | publie depuis ce compte, ou fais une copie du niveau, qui part alors comme un nouvel élément |
| `{{ui:enum_workshop-failure_access-denied}}` | le compte ne possède pas le jeu, le compte est limité (aucun achat sur Steam pour l'instant) ou le Workshop lui est fermé |
| `{{ui:enum_workshop-failure_invalid-param}}` | le Workshop du jeu n'est pas configuré pour les envois, ou Steam tourne sous l'ID d'un autre jeu. Relance Steam et le jeu |
| `{{ui:enum_workshop-failure_limit-exceeded}}` | supprime d'anciens éléments dans tes fichiers du Workshop |
| `{{ui:enum_workshop-failure_connection}}` | vérifie la connexion et l'état de Steam |
| `{{ui:enum_workshop-failure_invalid-request}}` | un titre de 128 caractères au plus, une description de 8000 au plus, un aperçu png ou jpg de 1 Mo au plus |
| `{{ui:enum_workshop-failure_staging}}` | vérifie l'espace libre sur le disque et que les fichiers du niveau ne sont pas ouverts dans un autre programme |

Si un nouvel élément est créé mais que son envoi est refusé, le jeu supprime cet élément vide, pour qu'aucun élément abandonné ne reste dans le Workshop

## Versions sans Steam

Une version sans Steam n'affiche pas `{{ui:editor_share_steam}}` dans la liste. `{{ui:editor_share_archive}}` reste

## Comment partager une collection

Une collection se partage depuis sa page dans l'onglet "Bibliothèque". `{{ui:editor_share_share}}` ouvre le même panneau dans une fenêtre : `{{ui:editor_share_archive}}`, et dans la version Steam aussi `{{ui:editor_share_steam}}` pour une de tes collections

La vérification de collection :
- elle a un nom
- elle a une licence indiquée
- elle n'est pas vide
- chaque fichier qu'elle nomme s'y trouve
- chaque ressource à laquelle renvoient ses entrées y est incluse

Une licence manquante dépend de la façon. Pour `{{ui:editor_share_archive}}`, c'est un avertissement, et l'export se fait. Pour `{{ui:editor_share_steam}}`, c'est une erreur.
Les erreurs bloquent l'envoi. Plus sur les collections - [[16_library-and-collections]]

## Comment partager une seule ressource

Chaque ligne de thème, de forme, d'effet et de prefab dans la bibliothèque a aussi un bouton `{{ui:editor_share_share}}`.
Il emballe la ressource avec tout ce dont elle a besoin (par exemple les formes, les textures et les prefabs imbriqués d'un prefab) sous forme de collection d'une seule entrée

Seule la destination `{{ui:editor_share_archive}}` est disponible, avec les mêmes cinq formats que pour une collection, y compris ceux avec mot de passe. Le destinataire importe le fichier par `{{ui:editor_library_import-archive}}`, comme n'importe quelle collection

## Tags du Workshop

Le jeu fixe les tags lui-même :

| Élément | Tags |
|---|---|
| niveau | `level` |
| collection | `collection` et un par type présent à l'intérieur : `prefabs`, `themes`, `shapes`, `effects` |

Les textures, les polices et l'audio ne reçoivent pas de tags et ne vont pas seuls dans le Workshop. Ils vont à l'intérieur d'une collection, comme ce qu'utilisent ses prefabs, thèmes, formes et effets. Une collection faite uniquement de médias est refusée avec une ligne qui en donne la raison, et une telle collection se partage mieux sous forme d'archive

> [!info] Bon à savoir
> Les "Collections" propres à Steam sont des listes d'éléments du Workshop choisis à la main, une fonction de Valve. Elles n'ont rien à voir avec les collections de Bullet Hero

## Abonnements

La version Steam lit tes abonnements :
- les niveaux apparaissent dans la liste des niveaux sous `{{ui:editor_library-source_workshop}}`, [[2_playing-levels]]
- les collections apparaissent dans la bibliothèque de l'éditeur sous la pastille `{{ui:editor_library-source_workshop}}`, en lecture seule

À lire ensuite : [[5_publish-readiness]], [[1_licensing-basics]], [[16_library-and-collections]]
