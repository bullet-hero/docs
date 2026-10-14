---
title: Succès
date: 2026-10-14
tags: [player]
---

# Succès

Les succès se débloquent d'eux-mêmes à partir de vos statistiques. Seuls comptent les niveaux créés par d'autres et les parties jouées de façon loyale. La liste se trouve dans le menu principal, sous `{{ui:menu_main_achievements-btn}}`

## La liste

`{{ui:menu_main_achievements-btn}}` dans le menu principal ouvre tous les succès de votre version, par groupes. Un succès verrouillé montre votre progression, un succès débloqué montre le jour où il l'a été. Un succès secret apparaît comme `{{ui:menu_achievements_hidden_name}}` tant qu'il n'est pas débloqué

## Ce qui compte

**Une partie loyale** est une partie où :

- aucun bot ne joue
- les collisions sont activées
- la vitesse est de `{{v:achievements.fair-min-speed}}` ou plus
- vous avez des vies : une partie en `{{ui:menu_levelview_options-lifes_option-zen}}` ne compte que là où un succès le demande

Les checkpoints sont autorisés. Une partie lancée depuis l'éditeur ne compte jamais, elle n'établit pas de record non plus - [[10_statistics]]

**Pas votre propre niveau.** Un niveau que vous avez ouvert dans l'éditeur sur cet appareil est le vôtre. Le terminer ne compte que pour le succès qui récompense le test de votre propre niveau. Les niveaux intégrés, ceux du Workshop et ceux de vos amis comptent

## Où c'est enregistré

`stats/achievements.json`, à côté des statistiques. Il ne retient que la date de déblocage de chaque succès. Qu'un succès soit débloqué est décidé à chaque fois à partir des statistiques, donc le fichier ne peut pas être perdu : supprimez-le, et au prochain lancement tout ce que vous avez gagné revient, daté de ce jour-là

Effacer les statistiques dans les paramètres conserve vos succès. Le transfert de profil et Steam Cloud emportent le fichier : deux appareils finissent avec tous les succès débloqués sur l'un ou l'autre - [[14_profile-transfer]]

## Steam

Dans une version Steam, chaque succès est aussi débloqué sur Steam, et Steam affiche sa propre notification. L'enregistrement de Steam l'emporte : un succès que Steam possède est débloqué dans le jeu avec la date de Steam. Un succès que le jeu a et que Steam n'a pas est débloqué à nouveau si vos statistiques le justifient encore

Toutes les autres versions affichent la notification du jeu en haut de l'écran
