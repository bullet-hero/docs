---
title: Prêt pour la publication
date: 2026-10-02
tags: [level_author]
---

# Prêt pour la publication

Chaque service vérifie un niveau selon ses propres règles, donc l'un peut l'accepter et un autre le refuser. Seule une erreur bloque la publication, un avertissement envoie le niveau en modération

La vérification se lance d'elle-même dans l'onglet `{{ui:settings_level-settings_publication}}` des paramètres du niveau, dans n'importe quelle version. La destination choisit le profil : `{{ui:editor_share_archive}}` est vérifié par `{{ui:editor_publish_profile-local}}`, le plus souple, `{{ui:editor_share_steam}}` par le profil du Workshop. Le profil standard est celui d'un serveur public, et le profil de la version pour les stores n'est pas proposé dans le jeu, ses limites sont ci-dessous. Plus - [[17_publishing]]

## Trois verdicts

| Verdict | Ce qui se passe |
|---|---|
| **`Error`** | le service refuse, l'envoi est bloqué avant de commencer |
| **`Warning`** | publiable, mais une personne regardera le niveau. Le serveur le place dans la file de modération |
| **`Advice`** | une remarque, ne bloque rien |

Un niveau qui reste sur ton appareil n'est évalué par rien du tout

## Le profil du Workshop

Plus souple que le profil standard pour l'instant, parce que la politique de licences va encore être réécrite :
- toute licence CC BY passe, 3.0 et 4.0 : BY, BY-SA, BY-NC, BY-NC-SA, BY-ND, BY-NC-ND. Ainsi que CC0, SIL OFL, MIT, Apache et l'Unlicense
- toujours refusés : tous droits réservés, les licences de la famille GPL et un texte de licence personnalisé
- seulement un avertissement : aucune licence indiquée, une ressource sans fiche, pas de lien vers la page source
- une classification par âge et des auteurs du niveau ne sont pas exigés
- les limites de taille sont les mêmes que dans le profil standard

> [!caution] Attention
> La musique sous CC BY-ND est acceptée, mais selon CC 4.0, une musique synchronisée avec une image animée compte toujours comme une adaptation, et ND interdit de distribuer des adaptations. Un niveau construit sur un morceau ND peut être retiré à la demande du titulaire des droits. Mieux vaut prendre un autre morceau

## Ce qui donne une erreur

Dans le profil standard :
- la licence du niveau lui-même n'est pas acceptée
- aucune classification par âge
- personne n'est crédité pour le niveau
- une ressource n'a pas de fiche
- la licence d'une ressource est refusée ou non indiquée
- une ressource est récupérée d'une manière que le service n'accepte pas
- une ressource vient d'un site interdit
- quelque chose dépasse les limites de taille

## Ce qui donne un avertissement

- une ressource n'a pas de lien vers sa page source. Une œuvre que tu as faite toi-même n'a pas de telle page, donc cela ne bloque jamais
- une autorisation sans portée ou sans preuve
- une autorisation expirée
- un site avec plus d'un type de conditions

## Ce qui donne un conseil

- la fiche d'une ressource que le niveau n'a plus

## Pourquoi, et que faire

Chaque ligne du rapport nomme sa ressource : par nom de fichier ou par le nom que tu lui as donné. Le `?` en fin de ligne déplie les détails : quelle licence a la ressource, lesquelles le service accepte à la place, combien elle pèse par rapport à la limite et où corriger

## Limites de taille

| Limite | Profil standard | Version pour les stores |
|---|---|---|
| Par ressource | `{{v:publish.standard.max-resource-mb}} Mo` | `{{v:publish.strict.max-resource-mb}} Mo` |
| Par fichier de données | `{{v:publish.standard.max-data-file-mb}} Mo` | `{{v:publish.strict.max-data-file-mb}} Mo` |
| Par niveau | `{{v:publish.standard.max-level-mb}} Mo` | `{{v:publish.strict.max-level-mb}} Mo` |

Une version pour les stores exige aussi l'attribution et les hachages, et refuse les liens arbitraires.
Les tailles réduites ne sont pas un avis plus sévère. C'est ce qu'un téléphone peut réellement télécharger sur un réseau mobile

## Un rapport propre

> [!caution] Attention
> Un rapport propre sur les seules métadonnées ne veut pas dire "prêt". Deux vérifications ont besoin du fichier du niveau lui-même : une ressource sans fiche, et l'endroit d'où une ressource est récupérée. Un passage sur les seules métadonnées veut dire "rien d'anormal dans ce qui a été lu"

## Pourquoi les services évaluent différemment

Les règles d'un service sont un fichier de données, pas du code.
Chaque service pose la même douzaine de questions environ et y répond à sa manière :
- quelles licences sont acceptables
- comment les ressources peuvent être récupérées
- si une licence inconnue est tolérée
- ce qui doit être rempli
- quelle taille un niveau peut avoir

Un service apporte ses propres réponses, un autre les remplace. C'est pourquoi le même niveau peut être prêt pour un service et refusé par un autre

> [!info] Bon à savoir
> La même vérification tourne à la fois automatiquement sur ta machine et lors de la modération manuelle sur le serveur. Un client sans réseau évalue quand même un niveau correctement, parce que les règles avec lesquelles il a été construit voyagent avec lui

À lire ensuite : [[4_resource-record]], [[2_metadata-and-sharing]]
