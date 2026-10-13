---
title: Paramètres du niveau
date: 2026-10-02
tags: [level_author]
---

# Paramètres du niveau

Tout ce qui appartient au niveau lui-même se règle ici : durée, images par seconde, graine, orientation, métadonnées, publication. C'est aussi d'ici que le niveau se lance, se vérifie selon les règles et se restaure à partir d'une copie

## Lecture

Les options de lancement valent **pour cette partie seulement**. Rien ici n'est enregistré dans le niveau

`{{ui:settings_level-settings_life-text}}`, `{{ui:field_common_speed}}`, `{{ui:settings_level-settings_checkpoints-toggle}}` et le niveau automatique permettent de répéter un passage sans le modifier

> [!tip] Conseil
> La `{{ui:settings_level-settings_seed}}` d'ici l'emporte sur la graine propre au niveau. C'est le plus haut des trois niveaux de priorité. Sers-t'en pour rejouer exactement la partie que tu viens de voir. `0` veut dire : prendre la graine du niveau, ou une nouvelle à chaque partie

Plus - [[3_difficulty-curve]]

## Base

Durée en images, fréquence d'images et les deux graines du niveau

`{{ui:settings_level-settings_core-seed-value}}` est la graine propre au niveau. Elle fait partie du contenu, et sa modification peut être annulée.
`0` veut dire "une nouvelle graine à chaque partie". C'est la valeur par défaut, donc un niveau ordinaire se joue différemment à chaque fois

> [!tip] Conseil
> `{{ui:settings_level-settings_core-runtime-seed-value}}` montre seulement quelle graine cette session de l'éditeur a obtenue. `{{ui:settings_level-settings_core-runtime-seed-regenerate}}` en tire une nouvelle pour la session seulement : rien n'est écrit et rien ne va dans l'historique d'annulation. Recharger le niveau détermine la graine à nouveau

> [!info] Bon à savoir
> **Une image est une cellule, et le temps est une limite.** Les images se comptent à partir de 1. L'image *f* couvre le temps de (*f*-1)/fps jusqu'à *f*/fps, ce dernier exclu. Un niveau de N images contient les images 1 à N. N+1 est la limite de fin, pas une image

Plus - [[4_frames-and-time]]

## Orientation du niveau

Dans quel sens l'appareil se tient pendant ce niveau

`{{ui:enum_level-orientation_horizontal}}` et `{{ui:enum_level-orientation_vertical}}` tournent l'appareil du joueur pendant toute la durée du niveau. Ce choix l'emporte sur le paramètre du joueur.
Un moniteur ne se tourne pas. Sur ordinateur, un niveau vertical se joue donc entre deux bandes latérales, et c'est ainsi qu'il doit apparaître

`{{ui:enum_level-orientation_not-specified}}` laisse le choix au joueur. Ce n'est pas une valeur par défaut, mais une affirmation sur ton niveau : il se lit correctement dans les **deux** orientations.
Le jeu n'ajuste rien pour lui : rien n'est décalé, rogné ni mis à l'échelle. Le contenu au-delà des bords horizontaux est hors de l'écran dans une orientation et visible dans l'autre.
Ne le choisis qu'après avoir vérifié le niveau dans les deux sens

## Zone dangereuse

Des actions qui suppriment ou réécrivent des fichiers plutôt que du contenu

> [!caution] Attention
> Les listes déroulantes `{{ui:settings_level-settings_quot-level-quot-file-format}}` et `{{ui:settings_level-settings_quot-metadata-quot-file-format}}` réécrivent le niveau et ses métadonnées sur le disque. Changer de format **supprime le fichier dans l'ancien format**. Rien d'autre ne se passe : pas de rechargement, pas de nouvelle simulation, ta sélection et ton historique d'annulation restent. Ce qui est écrit est exactement ce qui est déjà en mémoire

> [!caution] Attention
> `{{ui:settings_level-settings_delete-level-open}}` supprime le dossier du niveau du disque. C'est irréversible

Plus - [[4_not-losing-work]]

## Règles

Les problèmes que la validation a trouvés dans ce niveau :
- références cassées
- ID en double
- cycles de parents
- prefabs imbriqués trop profondément
- segments de pulsation qui se chevauchent

> [!info] Bon à savoir
> **Certains problèmes peuvent être corrigés, un par un ou avec `{{ui:settings_level-settings_rules-fix-all}}`.** Les corrections vont dans un brouillon : `{{ui:editor_save_text}}` les applique en une seule opération annulable, `{{ui:settings_level-settings_raw-discard}}` les abandonne. Les problèmes de graphe (ID, parents, imbrication des prefabs) n'ont pas de correction, et c'est voulu : chacun est une décision de contenu qui n'appartient qu'à toi, et une correction automatique choisirait en silence une réponse parmi plusieurs valides

> [!tip] Conseil
> Un enfant qui dépasse de l'intervalle de son parent n'est **pas** signalé. Ce sont des données légales qui se comportent comme prévu. Si tu veux vraiment ajuster les durées de vie, lance le modificateur `{{ui:mod_span_fit}}` depuis les générateurs. Il ramène les enfants à l'intérieur ou élargit les parents

Plus - [[4_not-losing-work]]

## Métadonnées

Tout ce qui concerne le niveau sans être le niveau lui-même : nom, description, couverture, licence, classification par âge et auteurs

Le nom et la description s'écrivent pour chaque langue, ici même.
Un joueur dont tu n'as pas rempli la langue reçoit la première que tu as remplie

> [!info] Bon à savoir
> Aucune clé de traduction n'est nécessaire ici. Un niveau est du contenu, pas une partie de l'interface du jeu

La licence et les auteurs accompagnent le niveau partout où il est partagé. C'est ainsi que le crédit survit à une republication

Plus - [[2_metadata-and-sharing]]

## Tags du niveau

Les tags sont tes propres mots. Ils s'affichent exactement comme tu les as écrits et ne sont jamais traduits.
Le joueur s'en sert pour filtrer les niveaux dans le navigateur de niveaux

Écris les tags séparés par des virgules. Garde-les courts et généraux : un genre, une ambiance, une mécanique.
Un tag n'aide que si d'autres niveaux l'utilisent aussi. Un tag que personne d'autre ne tapera ne filtre rien

## Collections

Fait entrer dans le niveau des ressources d'une collection, ou construit une collection à partir des ressources propres du niveau. L'onglet se trouve juste après `{{ui:editor_library_kind-prefabs}}`

- `Importer` - ouvre une collection, coche des entrées, appuie sur `Importer`. Les dépendances suivent, et tout l'import est une seule étape d'annulation
- `{{ui:editor_collections_mode-build}}` - coche les ressources du niveau et appuie sur `{{ui:editor_collections_build}}`, vers `{{ui:editor_collections_target-new}}` ou une de tes collections

Une entrée que le niveau possède déjà dans une autre version ouvre `{{ui:editor_resource-conflict_title}}`. Rien n'est écrasé en silence

Plus - [[16_library-and-collections]]

## Publication

Le seul endroit d'où un niveau est envoyé quelque part : sous forme d'archive ou vers le Steam Workshop

`{{ui:editor_share_destination}}` choisit la destination. En dessous se trouvent les contrôles propres à cette destination, son rapport et le bouton qui la lance.
Le rapport vérifie le niveau de lui-même, sans bouton à presser. Les erreurs bloquent l'envoi, les avertissements et les conseils non

Plus - [[17_publishing]]

## Historique

Chaque modification de cette session est une ligne ici. La plus récente en haut, comme un `git log`

La colonne la plus à gauche est la ligne principale.
Une colonne à part est une branche. C'est une ligne que tu as laissée derrière toi quand tu as annulé une modification et pris un autre chemin

L'anneau marque où tu te trouves. Le cercle vert marque le dernier enregistrement

Un clic sur une ligne ramène le niveau exactement à cet état.
Le retour applique une opération par image. Tu vois donc le niveau changer au lieu d'attendre devant un écran figé

> [!warning] Avertissement
> L'éditeur est en lecture seule pendant le retour. Tu peux encore déplacer la caméra et faire un balayage, mais pas modifier. Annuler arrête le retour là où il en est, et c'est toujours un état réel du niveau

> [!tip] Conseil
> L'historique ne vit que dans la session actuelle. Il n'est jamais écrit sur le disque, et rouvrir le niveau le remet à zéro. Sa taille est limitée : les branches abandonnées les plus anciennes partent en premier, puis les modifications les plus anciennes

## Données brutes

Tout le modèle enregistré du niveau sous forme d'un seul arbre de champs. C'est le fichier lui-même, avant que l'éditeur le traite

> [!caution] Attention
> **Rien ici n'est validé.** C'est la porte de secours pour ce qu'aucun autre écran ne couvre encore. Elle écrira une valeur que le reste de l'éditeur considère comme impossible

Un point plein à côté d'un champ veut dire que tu l'as modifié pendant cette session.
Un point creux veut dire que quelque chose à l'intérieur a changé. Sans lui, une modification trois niveaux plus bas dans une branche repliée serait invisible

Le bouton `{{ui:settings_level-settings_raw-apply}}` est masqué, pas désactivé, quand il n'y a rien à appliquer.
Une application vide pousserait un échange de niveau dans la pile d'annulation sans raison

Plus - [[4_not-losing-work]]
