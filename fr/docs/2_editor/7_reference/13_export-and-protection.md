---
title: Export et protection
date: 2026-10-11
tags: [level_author]
---

# Export et protection

L'export enregistre le niveau hors du jeu, sous forme de dossier ou d'archive, avec chaque fichier qu'il utilise. Un mot de passe chiffre le contenu du niveau sur le disque, et un mot de passe oublié ne se récupère pas

## Exporter le niveau

L'export se trouve dans l'onglet `{{ui:settings_level-settings_publication}}` des paramètres du niveau : la destination `{{ui:editor_share_archive}}`, le mode dans `{{ui:editor_share_format}}`, et `{{ui:editor_share_passphrase}}` pour un mode protégé. Plus - [[17_publishing]]

Une archive contient le niveau, ses métadonnées et chaque fichier qu'il utilise.
Un morceau qui se trouve hors du dossier du niveau est copié lui aussi. Sa référence est redirigée vers la copie dans l'archive

Le dossier `ai` du niveau, où un assistant IA garde ses notes sur le niveau, est emballé aussi, sauf si `{{ui:settings_level-settings_metadata-level-ai-share}}` est décoché dans les métadonnées du niveau. Un mode avec mot de passe ne l'emballe jamais : des notes de conception lisibles à côté d'un niveau chiffré rendraient le mot de passe inutile. Le rapport indique quand le dossier a été laissé de côté. Plus - [[7_ai-assistant#Le dossier ai]]

| `{{ui:editor_share_format}}` | Ce que tu obtiens | S'ouvre avec |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_folder}}` | le même dossier que celui du niveau sur le disque. Compresse-le et envoie-le | rien de particulier |
| `{{ui:settings_level-settings_export-mode_folder-protected}}` | le même dossier, avec le document du niveau chiffré. Les métadonnées, la couverture et les médias restent lisibles, donc un navigateur de niveaux affiche toujours sa fiche | gpg pour le document du niveau |
| `{{ui:settings_level-settings_export-mode_zip}}` | un seul fichier | un double clic dans l'Explorateur Windows, rien à installer |
| `{{ui:settings_level-settings_export-mode_targz}}` | un seul fichier | n'importe quel archiveur |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | un zip avec son propre chiffrement AES-256. Le sens habituel d'un mot de passe sur une archive | 7-Zip ou tout autre archiveur, qui demande le mot de passe |
| `{{ui:settings_level-settings_export-mode_zip-protected}}`, `{{ui:settings_level-settings_export-mode_targz-protected}}` | la même archive enveloppée dans `.gpg` | gpg |

L'Explorateur Windows n'ouvre aucune des options avec mot de passe. C'est le prix d'un mot de passe

Une collection ou une seule ressource de la bibliothèque accepte les mêmes cinq modes d'archive, y compris ceux avec mot de passe. Les deux modes dossier sont réservés à un niveau. Plus - [[17_publishing#Archive]]

> [!tip] Conseil
> Tout ce qui n'a pas pu suivre (une ressource derrière une URL, un fichier que rien ne référence) est listé dans le rapport après l'export

> [!warning] Avertissement
> Un mot de passe protège le contenu pendant le transfert et contre la copie occasionnelle. Ce n'est pas un DRM : quiconque a le fichier et le mot de passe peut toujours l'ouvrir

## Protéger le niveau

Chiffre le document du niveau sur le disque. Ouvrir le niveau demande le mot de passe

Ce qui est protégé, c'est le **contenu** : objets, images clés, thèmes.
Les métadonnées, la couverture et les médias restent lisibles. Le navigateur de niveaux affiche donc toujours la fiche du niveau sans le mot de passe

Le mot de passe est demandé une fois par session et gardé en mémoire seulement.
Il n'est jamais écrit nulle part, donc l'enregistrement automatique continue de fonctionner

Pour retirer la protection, laisse le champ vide et appuie sur `{{ui:settings_level-settings_protect-apply}}`

> [!caution] Attention
> Un mot de passe oublié ne se récupère pas. Aucune clé n'est gardée nulle part, et il n'existe aucun moyen d'entrer dans le fichier sans lui
