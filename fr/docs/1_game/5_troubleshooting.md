---
title: Résolution des problèmes
date: 2026-10-03
tags: [player]
---

# Résolution des problèmes

Un niveau copié à la main apparaît dans la liste après une nouvelle analyse. Un niveau d'une version plus récente demande une mise à jour du jeu, et une archive .7z doit être recompressée en zip. Un mot de passe oublié ne se récupère pas. Discord montre ton activité seulement dans une version Steam, avec l'application Discord lancée

Tu n'as pas trouvé ton problème ? Où le signaler - [[11_help]]

## Un niveau n'est pas dans la liste

- **Copié à la main.** Le dossier du niveau doit se trouver directement dans `levels`, [[1_installation]]. Après la copie, appuie sur `{{ui:root_level-browser_refresh}}`
- **Un élément du Workshop.** La version Steam ne montre que tes abonnements. `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` ajoute les dossiers trouvés sur le disque. Ils sont marqués `{{ui:root_level-entry_not-listed}}`
- **Rien ne s'affiche du tout.** Le dossier des niveaux est peut-être inaccessible. Dans cet état, le nettoyage du stockage dans `{{ui:settings_other_title}}` ne s'exécute pas et affiche `L'analyse des niveaux n'a rien trouvé, ce nettoyage a donc été refusé`

## Un niveau ne se charge pas

L'écran de chargement montre l'étape : `{{ui:root_loading_reading}}`, `{{ui:root_loading_validating}}`, `{{ui:root_loading_resources}}`, `{{ui:root_loading_building}}`

- **Un fichier à une adresse web.** Un niveau peut prendre un fichier depuis un lien au lieu de le garder dans son dossier. `{{ui:settings_general_title}}` → `{{ui:settings_general_resource-web-timeout}}` est le nombre de secondes pendant lesquelles le jeu attend un tel fichier
- **Un niveau endommagé.** Un niveau en `Json` est du texte, il se lit à l'œil. Un `Blob` endommagé est refusé en entier. Plus - [[4_level-folder-and-backups]]
- **Une fenêtre d'erreur.** Elle propose `{{ui:root_error_copy}}`, `{{ui:root_error_save}}` et `{{ui:root_error_open-reports-folder}}`. Le rapport va dans le dossier `reports`. Joins-le à un rapport de bug dans [bullet-hero/releases](https://github.com/bullet-hero/releases/issues), [[11_help]]
- **`Le niveau demande plus d'objets par image que cet appareil n'en permet`.** Ce n'est pas une erreur de chargement. Le niveau se joue, mais une partie n'est pas dessinée. Plus - [[1_level-budget]]

## "Mise à jour requise"

Une ancienne version du jeu n'ouvre pas les fichiers d'une version plus récente. Mets le jeu à jour

| Message | Que faire |
|---|---|
| `Ce niveau a été créé dans une version plus récente du jeu...` | mettre le jeu à jour |
| `Cette archive contient un niveau d'une version plus récente du jeu...` | mettre le jeu à jour |
| `Le presse-papiers contient du contenu de l'éditeur copié dans une version plus récente du jeu...` | mettre le jeu à jour |
| `Tes paramètres ou tes statistiques ont été enregistrés par une version plus récente du jeu...` | `{{ui:root_update-required_download}}`, `{{ui:root_update-required_keep}}` ou `{{ui:root_update-required_overwrite}}` |

Une carte marquée `{{ui:root_level-entry_newer-version}}` ou `{{ui:root_level-entry_newer-file}}` est le même refus. Il se voit avant même l'ouverture du niveau

### Paramètres ou statistiques d'une version plus récente

Dans ce cas, le jeu tourne avec les valeurs par défaut. Jusqu'à sa fermeture, il n'enregistre rien de ce qui lui est propre, et les fichiers plus récents restent intacts. C'est le mode anonyme, [[4_settings]].
Avec `--suppress-game-saves`, il n'y a pas de bouton `{{ui:root_update-required_overwrite}}`

Les statistiques d'un niveau venant d'une version plus récente ne s'affichent pas. Jouer le niveau les écrase, sauf si les enregistrements sont désactivés

### Pourquoi le jeu refuse

Chaque changement du format de fichier reçoit un nouveau numéro de génération. Une version du jeu ne lit pas un fichier d'une génération plus récente, pour ne pas le lire de travers

## Un niveau protégé

Avant l'ouverture, le jeu demande un `{{ui:level_passphrase_password}}`.
Le mot de passe est demandé une fois par session et gardé uniquement en mémoire

Seul le contenu est chiffré : objets, images clés, thèmes. Le titre, la couverture et les médias restent lisibles, donc la carte s'affiche même sans le mot de passe

Supprimer un niveau protégé ne demande pas le mot de passe

> [!caution] Attention
> Un mot de passe oublié ne se récupère pas. La clé n'est stockée nulle part - ni dans le jeu, ni dans le fichier, ni chez personne

## Une archive est refusée

| Message | Cause |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | c'est un `.7z`. Recompresse-le en `.zip` |
| `{{ui:editor_create-level_archive-wrong-password}}` | le mot de passe ne correspond pas |
| `{{ui:editor_create-level_archive-damaged}}` | l'archive est cassée, redemande-la |
| `{{ui:editor_create-level_archive-not-archive}}` | le fichier n'est pas du tout une archive de niveau |

Une archive renommée n'est pas un problème : le jeu reconnaît le format aux octets du fichier.
Quelles archives sont acceptées - [[2_playing-levels]]

## Discord ne montre pas à quoi je joue

- **Pas une version Steam.** Seules les versions Steam montrent ton activité dans Discord
- **Discord est fermé.** L'application de bureau Discord doit tourner sur le même ordinateur. Tu l'as lancée après le jeu ? Le statut apparaît au prochain changement d'écran
- **L'activité est masquée.** Dans Discord : `User Settings` -> `Activity Privacy` -> partage tes activités détectées
- **Un niveau à toi n'affiche pas de nom.** C'est voulu : seul un niveau du Workshop ou livré avec le jeu est nommé, et l'éditeur ne nomme jamais son niveau. Pourquoi - [[game-privacy-policy#Discord Rich Presence]]
