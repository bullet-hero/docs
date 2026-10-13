---
title: Aide et rapports de bug
date: 2026-10-02
tags: [player, level_author]
---

# Aide et rapports de bug

Les bugs du jeu vont dans les issues de releases, les questions sur Discord. Joins la ligne de version des paramètres et les étapes après lesquelles le bug apparaît

Regarde d'abord [[5_troubleshooting]]. Un niveau manquant, "le jeu demande une mise à jour" et une archive refusée y sont traités

## Où écrire

| Quoi | Où |
|---|---|
| un bug dans le jeu ou l'éditeur, une demande pour le jeu | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| un bug dans le SDK ou son code | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| une erreur ou un fait dépassé dans la documentation | [bullet-hero/docs](https://github.com/bullet-hero/docs), [[community]] |
| une question, de l'aide sur un niveau, une discussion | [Discord](https://discord.gg/gkHQrp9NgS) |

Les messages sur GitHub sont publics. Tout le monde peut les lire et y ajouter quelque chose.
Tu peux envoyer une issue ou une pull request à la documentation

Tu doutes que ce soit un bug ? Demande d'abord sur Discord

Tous les liens du projet - [[links]]

## Que mettre dans un rapport de bug

Un bug qui peut être reproduit est corrigé. "Ça a planté" ne peut en général pas être corrigé : personne ne sait quoi répéter

1. **La ligne de version.** Clique sur la ligne de version de l'écran des paramètres et elle se copie toute seule. Elle ressemble à ceci : `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`, [[4_settings]]
2. **Plateforme et appareil :** le système, et pour un téléphone, le modèle
3. **Étapes :** ce que tu as fait, ce que tu attendais et ce qui s'est passé
4. **Le niveau,** si le bug y est lié : son dossier dans une archive, ou l'archive que tu as ouverte. Si le niveau est protégé, dis-le
5. **Le rapport d'erreur,** s'il y a eu une fenêtre d'erreur. `{{ui:root_error_save}}` l'écrit dans le dossier `reports`, `{{ui:root_error_open-reports-folder}}` l'ouvre, [[1_installation]]

> [!tip] Conseil
> Joins les fichiers au message au lieu de les coller dans le texte. Un log est long, et il est difficile à lire au milieu du texte

## Logs

Le jeu écrit un log pendant qu'il tourne. Il aide quand il n'y a pas eu de fenêtre d'erreur du tout

- **Windows :** `Player.log` dans le dossier de données du jeu, `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` (l'emplacement standard d'Unity)
- **Android :** le log va dans logcat. Avec l'appareil branché à un ordinateur, `adb logcat -s Unity` l'affiche
- **Autres systèmes :** pas encore décrit
