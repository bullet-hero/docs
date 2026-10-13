---
title: Serveur entre amis
date: 2026-10-01
tags: [server_host]
---

# Serveur entre amis

Il te faudra les outils serveur ouverts, le build complet du jeu pour chaque joueur et un fichier PublishProfile. La modération et le respect des licences des niveaux reviennent au propriétaire du serveur

> [!warning] Avertissement
> Les outils serveur ne sont pas sortis, le protocole n'est pas conçu. Cette page ne contient que ce qui est déjà décidé

## Ce qu'il te faudra

- **Les outils serveur.** Ils seront ouverts, sous licence MIT. C'est le même code que celui du serveur officiel. Tu peux construire ton propre serveur sur ces outils ou sur tout ce qui en dérive
- **Le build complet du jeu pour tous ceux qui se connectent.** Les builds de Google Play et de l'App Store ne se connectent pas aux serveurs communautaires. Le build complet est sur [GitHub](https://github.com/bullet-hero/releases) et sur le site du projet
- **Un profil de publication.** Le fichier `PublishProfile` décide quels niveaux ton serveur accepte. Plus - [[7_publish-profiles]]
- **Une machine pour le serveur.** La configuration requise, l'environnement d'exécution, les ports et la façon de le lancer ne sont pas encore connus

## Profil de publication

Le profil fixe quelles licences sont acceptées, d'où un niveau peut récupérer des fichiers et quelle est sa limite de taille.
Aucune modification du code n'est nécessaire pour cela

Le serveur officiel tourne avec le préréglage `standard`, défini dans la configuration du serveur. Pars de celui-ci et assouplis-le ou durcis-le selon tes besoins

## Ce que tu prends en charge

- **La modération.** Bullet Hero ne modère pas les serveurs communautaires. Le CLUF du build complet le dit à chaque joueur
- **Pas de commerce.** Par défaut, un niveau est distribué sous *CC BY-NC*, et l'auteur peut choisir une autre licence. Respecte la licence de chaque niveau. Un niveau sous *CC BY-NC* peut être hébergé et partagé gratuitement, mais tu ne peux pas le faire payer ni en tirer de l'argent d'une autre manière
- **Les droits sur les ressources.** Un niveau peut contenir la musique et les graphismes de quelqu'un d'autre. C'est ton profil qui décide avec quelle rigueur le vérifier. Mais une plainte au sujet de l'œuvre de quelqu'un d'autre arrivera chez toi. Les règles du serveur officiel - [[ugc-licensing-policy]]

L'autorisation de distribution non commerciale est donnée par l'auteur de chaque niveau, pas par le jeu. Seul l'auteur peut donc faire une exception

## Ce qui est inconnu

- comment le jeu trouve un serveur et s'y connecte
- si un serveur communautaire aura des comptes
- comment les niveaux sont envoyés et arrivent dans la liste
- si un serveur pour quelques personnes se configurera autrement qu'un serveur public

Ce qui existe déjà pour un grand serveur - [[3_advanced-hosting]]
