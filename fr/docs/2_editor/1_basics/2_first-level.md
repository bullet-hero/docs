---
title: "Ton premier niveau : le parcours"
date: 2026-10-02
tags: [level_author]
---

# Ton premier niveau : le parcours

Six étapes jusqu'au premier test : créer un niveau, ajouter un morceau, poser le rythme, placer des objets, lancer un test, enregistrer

## Six étapes

Ce n'est que l'ordre de travail. Ce que fait chaque champ, l'aide à côté de son panneau l'explique

**1. Crée le niveau.** `{{ui:settings_editor-settings_editor-settings}}` → `{{ui:settings_editor-settings_create-level}}`. Choisis un préréglage, donne un nom et une durée. La durée peut changer plus tard

**2. Ajoute le morceau.** Copie le fichier audio dans le dossier du niveau et branche-le. `ogg` marche le mieux, et `flac` ne se charge pas. Plus - [[2_preparing-the-track]]

**3. Pose le rythme.** L'onglet `{{ui:editor_inspector-beat_tab}}` : BPM, décalage, pulsations par mesure. La grille n'est pas pour le jeu, elle est pour toi : le contenu s'y aimante

Tu ne connais pas le tempo ? Marque-le par appuis en rythme avec le morceau dans la fenêtre `{{ui:editor_beat-window_title}}` (`Shift+T`). Les appuis eux-mêmes n'ont pas de touche par défaut

**4. Place les premiers objets.** Crée un objet, donne-lui une forme et pose deux images clés sur sa position. Le jeu fait passer la valeur d'une image clé à l'autre tout seul

**5. Vérifie.** Lance un test directement depuis l'éditeur. Le plus probable, c'est que tout bouge soit beaucoup trop vite, soit beaucoup trop lentement. C'est normal : la vitesse ne se règle qu'à l'oreille

**6. Enregistre.** `Ctrl+S`

La sauvegarde automatique est activée par défaut. {{v:editor.autosave-delay}} secondes après une modification non enregistrée, elle enregistre le niveau et en met une copie dans `backups/<level id>/`. Plus - [[4_not-losing-work#L'enregistrement automatique]]

## Garde le premier niveau petit

> [!tip] Recommandation
> Prends un morceau court, 1-2 minutes. Un niveau de 4 minutes, c'est quatre fois plus de travail et dix fois plus de raisons de l'abandonner en cours de route

Commence par le motif le plus simple qui fonctionne, pas par le plus difficile que tu as imaginé.
Joue toi-même le niveau du début à la fin avant de le montrer à qui que ce soit

Laisse les générateurs, les prefabs et les modificateurs pour plus tard. Ils font gagner du temps sur un grand niveau et gênent sur un premier

## Le morceau et les droits

Un morceau pour toi-même ne demande la permission de personne. Les droits ne sont vérifiés qu'à la publication.
Plus - [[1_licensing-basics]]

Les règles complètes de publication sur le serveur officiel - [[ugc-licensing-policy]]

## Et ensuite

Comment fonctionne l'éditeur - [[3_how-the-editor-thinks]]

Après le premier test - la conception de niveaux : [[2_editor/4_craft/index]]

Quand le niveau dépasse le stade de l'ébauche - [[1_order-of-work]]
