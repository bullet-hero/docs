---
title: Se connecter à un serveur
date: 2026-10-01
tags: [player]
---

# Se connecter à un serveur

Le jeu aura le serveur officiel OWS pour tous les builds et des serveurs communautaires NOWS pour le build complet uniquement. Bullet Hero ne modère pas les serveurs communautaires, alors connecte-toi à ceux dont tu connais le propriétaire

> [!warning] Avertissement
> Il n'y a pas encore de serveurs, et le jeu ne peut pas s'y connecter. Il n'y a ni format d'adresse, ni écran de connexion, ni comptes

## Quels serveurs il y aura

| | OWS | NOWS |
|---|---|---|
| Nom complet | Official Web Services | Non-official web services |
| Qui le fait tourner | Bullet Hero | n'importe qui |
| Qui le modère | Bullet Hero | le propriétaire du serveur |
| Quels builds s'y connectent | tous | le build complet uniquement |

**OWS est le serveur par défaut.** Chaque build du jeu sur chaque plateforme le connaît, rien n'est à configurer

**Les NOWS sont des serveurs communautaires.** Bullet Hero ne les contrôle pas et ne les modère pas

**Le Steam Workshop est un troisième canal pour les niveaux sur PC.** Les builds Steam listent et lancent les éléments auxquels tu es abonné, et y publient des niveaux et des collections depuis l'éditeur - [[17_publishing]]

## Quels builds se connectent

| Build | D'où | OWS | NOWS |
|---|---|---|---|
| Build des boutiques | Google Play, App Store | oui | non |
| Build complet | [GitHub](https://github.com/bullet-hero/releases) et le site du projet | oui | oui |

Un build des boutiques ne peut se connecter d'aucune façon à un serveur communautaire.
La prise en charge des NOWS en est retirée à la compilation, elle n'est pas cachée derrière un paramètre

La raison, ce sont les règles des boutiques. Une boutique juge ce qu'un programme peut faire, pas les boutons qu'il affiche. Et le contenu que voient d'autres personnes doit être modéré selon ses règles

Il est prévu que le build complet ait son propre identifiant d'application, pour qu'on puisse l'installer sur Android à côté de la version des boutiques. Pour l'instant, tous les builds Android partagent un seul identifiant, `com.vertoker.BulletHero`

## Ce qu'aura OWS

- des comptes et des conditions d'utilisation
- une vérification de chaque niveau avant publication : un niveau avec une erreur est refusé, un niveau avec un avertissement part chez un modérateur
- des signalements de niveaux et d'utilisateurs, et leur blocage

Ce qu'un compte stockera n'est pas encore décidé. Le serveur aura sa propre politique de confidentialité, qui apparaîtra en même temps que lui. Elle décrira le compte et expliquera comment le supprimer. Les politiques du jeu et du site ne couvrent pas le serveur - [[game-privacy-policy]], [[privacy-policy]]

## Quand

La publication dans le Steam Workshop fonctionne déjà dans les builds Steam. Pour le reste, il n'y a pas de dates. L'ordre est le suivant : OWS, puis le build Google Play, puis le build App Store

Il n'y a pas encore de jeu à plusieurs sur un serveur, il n'a pas été conçu

## Risques des serveurs des autres

Un serveur communautaire est géré par une personne que tu ne connais très probablement pas.
Bullet Hero ne contrôle pas et ne modère pas ces serveurs. Le CLUF du build complet le dit directement

| Risque | Pourquoi |
|---|---|
| Niveaux aux droits non vérifiés | le propriétaire décide quoi vérifier et peut ne rien vérifier. Un niveau peut contenir une musique que son auteur n'avait pas le droit de partager |
| Personne ne modère le contenu | rien ne garantit que quelqu'un regarde ce qui est envoyé |
| Fichiers venant d'autres sites | la politique standard permet à un niveau de récupérer un fichier par un lien direct. Quand tu ouvres un tel niveau, le jeu télécharge le fichier depuis un site choisi par l'auteur du niveau. C'est pourquoi les builds des boutiques l'interdisent |
| Le propriétaire voit ton trafic | il n'y a pas encore de protocole, donc on ne sait pas ce que le serveur recevra exactement. Pars du principe que le propriétaire voit tout ce que tu envoies |
| Le serveur peut disparaître | un niveau qui n'existe que sur ce serveur disparaît avec lui |

Par défaut, un niveau est distribué sous *CC BY-NC*, et l'auteur peut choisir une autre licence dans les métadonnées du niveau. Un serveur doit respecter la licence de chaque niveau. Sous *CC BY-NC*, personne ne peut héberger un niveau à des fins commerciales, serveur communautaire compris, et un serveur qui fait payer de tels niveaux enfreint la licence de chacun de leurs auteurs

> [!tip] Recommandation
> Ne te connecte qu'aux serveurs dont tu connais le propriétaire. Garde ta propre copie de chaque niveau auquel tu tiens : un niveau est un dossier de fichiers, et la copie sur ton disque ne dépend d'aucun serveur

## CLUF

Le build complet est livré avec un CLUF (EULA). Il dit : les serveurs communautaires sont des services tiers, Bullet Hero ne les contrôle pas et ne les modère pas

Les builds des boutiques te demanderont d'accepter un CLUF avant de publier un niveau

Aucun de ces textes n'a encore été écrit

## À lire ensuite

- [[ugc-licensing-policy]] - les règles qu'un niveau doit respecter pour être publié
- [[2_hosting]] - si tu veux faire tourner un serveur toi-même
