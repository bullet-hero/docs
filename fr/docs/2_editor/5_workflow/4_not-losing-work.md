---
title: Ne pas perdre son travail
date: 2026-10-02
tags: [level_author]
---

# Ne pas perdre son travail

Ton travail est protégé par l'enregistrement automatique, l'annulation et une copie du dossier du niveau. Seule une copie du dossier est un instantané complet du niveau. Changer le format du fichier et supprimer un niveau ne s'annulent pas

Chaque protection couvre ce que les autres ne couvrent pas. L'enregistrement automatique et l'annulation ne remplacent pas une copie du dossier, parce que le niveau entier tient dans un seul dossier

## L'habitude

> [!tip] Recommandation
> `Ctrl+S` après chaque section terminée. Une copie du dossier du niveau avant chaque restructuration. La vérification `{{ui:settings_level-settings_rules}}` avant de considérer le niveau comme fini

## L'enregistrement automatique

L'enregistrement automatique est activé par défaut. Il fonctionne ainsi :
1. Une modification non enregistrée apparaît - un compte à rebours de `60` secondes démarre
2. Le jeu écrit une copie du niveau dans `backups/<level id>/` dans le dossier du jeu, hors de `levels`
3. Puis il enregistre le niveau lui-même, comme le ferait `Ctrl+S`

Un éditeur ouvert sans aucun changement n'écrit rien.
Tout ce qui a changé depuis le dernier enregistrement, manuel ou automatique, n'existe qu'en mémoire

`25` copies sont conservées, la plus ancienne est supprimée en premier.
Une copie ne contient que le fichier du niveau, sans métadonnées, morceau ni images. Elle survit à la suppression du niveau, sauf si tu coches `{{ui:root_level-delete_backups}}`.
La copie d'un niveau protégé est verrouillée avec le mot de passe de ce niveau

L'interrupteur, l'intervalle et le nombre de copies se règlent dans `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}`

**Restaurer :** paramètres du niveau, onglet `{{ui:settings_level-settings_dangerous-zone}}`, `{{ui:level_backups_open}}`. Les copies vont de la plus récente à la plus ancienne, chacune nommée d'après le moment où elle a été prise.
Le fichier actuel est d'abord copié lui-même dans `backups`, donc une restauration peut elle aussi être annulée

Tu peux aussi restaurer à la main : copie la sauvegarde dans le dossier du niveau sous le nom `level.json` (ou `level.blob`)

## Les modifications non enregistrées

Une action qui remplacerait le niveau ouvert ou le quitterait demande d'abord quoi faire des modifications non enregistrées :
- ouvrir un autre niveau depuis la liste des niveaux, y compris copier un niveau et ouvrir la copie
- créer un niveau
- `{{ui:settings_level-settings_quit}}` depuis les paramètres de l'éditeur et depuis les paramètres du niveau
- `{{ui:level_backups_open}}`
- dans `{{ui:settings_level-settings_dangerous-zone}}` : copier le niveau et ouvrir la copie, changer le format du fichier, définir un mot de passe

La boîte de dialogue propose trois réponses :
- `{{ui:editor_save_text}}` - enregistre le niveau et poursuit l'action
- `{{ui:editor_unsaved-changes_discard}}` - le bouton rouge, la seule réponse qui perd des modifications
- `{{ui:editor_cancel_text}}` - ne fait rien

Jouer depuis les paramètres du niveau pose aussi la question, mais avec deux réponses : `{{ui:editor_unsaved-changes_save-play}}` et `{{ui:editor_cancel_text}}`. Ici, les modifications ne peuvent pas être abandonnées, parce qu'au retour du jeu le niveau est relu depuis le disque.
S'il n'y a rien de non enregistré, la boîte de dialogue n'apparaît pas

## Ce que couvre l'annulation

L'annulation couvre les modifications du niveau, et seulement elles. Chaque changement d'objets, d'images clés, de ressources, de thèmes, de prefabs et de paramètres passe par un seul tampon d'opérations

Ce qui ne change pas le niveau ne s'annule pas :
- le gizmo choisi, l'outil de la timeline, l'activation de l'aimantation et de la grille
- la disposition des panneaux, l'onglet ouvert, la position de la tête de lecture
- les presse-papiers
- une graine de session régénérée. Recharger le niveau la tire de nouveau
- **l'enregistrement**. L'annulation revient en arrière sur le niveau en mémoire, pas sur le fichier sur le disque

## Ce qui ne s'annule pas du tout

Deux actions écrivent directement sur le disque :
- **Changer le format du fichier du niveau.** Écrire le niveau en `Blob` supprime le `Json` précédent. Et un `Blob` ne se lit ni ne se répare à l'œil
- **Supprimer un niveau.** C'est pourquoi c'est caché dans `{{ui:settings_level-settings_dangerous-zone}}`

## L'onglet des données brutes

L'onglet `{{ui:settings_level-settings_raw}}` affiche tout le fichier enregistré sous forme d'arbre de champs. Il ne vérifie rien : ni règles, ni limites

C'est le dernier recours. Toutes les modifications d'une session s'appliquent comme une seule opération, et elle peut être annulée

> [!caution] Attention
> Rien n'a vérifié ce que tu as écrit dans l'onglet `{{ui:settings_level-settings_raw}}`. Garde une copie du dossier du niveau sous la main. Plus - [[4_level-folder-and-backups#Sauvegardes et récupération]]

## Les règles

La vérification qui vaut la peine d'être lancée est l'onglet `{{ui:settings_level-settings_rules}}`. Il montre ce que la validation a trouvé : références cassées, ids en double, cycles de parents, prefabs imbriqués trop profondément, segments de pulsation qui se chevauchent

Le jeu peut corriger certains problèmes : un par un ou tous d'un coup avec le bouton `{{ui:settings_level-settings_rules-fix-all}}`.
Les corrections s'appliquent avec le bouton `{{ui:editor_save_text}}`, comme une seule opération qui peut être annulée. `{{ui:settings_level-settings_raw-discard}}` les abandonne.
Les problèmes du graphe n'ont pas de correction

L'intervalle d'un enfant qui dépasse celui de son parent n'est pas une erreur. Ce sont des données normales, et elles se comportent comme prévu.
Pour ajuster les durées de vie, lance le modificateur `{{ui:mod_span_fit}}`

Suite : [[4_level-folder-and-backups|Le dossier du niveau et les sauvegardes]], [[1_order-of-work|L'ordre de travail]]
