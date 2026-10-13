---
title: FAQ
date: 2026-10-02
tags: [player, level_author]
---

# FAQ

Bullet Hero est un hybride gratuit de jeu de rythme et de bullet hell. Aucun compte n'est nécessaire, et il n'y a pas encore de serveur. Les joueurs créent les niveaux dans l'éditeur intégré et se les passent sous forme de dossier ou d'archive

## Le jeu

### Qu'est-ce que Bullet Hero ?

Un hybride de *jeu de rythme* et de *bullet hell*. Un niveau, c'est de la musique et des formes qui bougent sur elle. Tu diriges un petit carré, et il doit survivre jusqu'à la fin du morceau

Bullet Hero est conçu comme un moteur pour le genre. C'est pourquoi la plupart des niveaux sont créés par les joueurs dans l'éditeur intégré.
Plus - [[1_game/index]]

### Le jeu est-il gratuit ?

Oui. Le jeu n'a ni achats, ni publicité, ni contenu payant.
Plus - [[1_licensing-basics]]

### Où le trouver ?

Tous les builds et toutes les boutiques - [[download]]

Le jeu est sorti, version `gv {{v:version.gv}}`. Les builds ne sont pas signés

### Faut-il un compte ou internet ?

Non. Il n'y a ni comptes ni serveur, et le jeu n'envoie rien nulle part

Internet n'est nécessaire que pour un seul type de niveau : celui qui charge un fichier depuis l'adresse web de son auteur.
Plus - [[1_installation]]

### Où sont stockés les niveaux ?

Dans le dossier `levels`, à l'intérieur du dossier de données du jeu. Pour l'ouvrir : `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`.
Plus - [[1_installation]]

## Jouer des niveaux

### Comment jouer un niveau que quelqu'un t'a envoyé ?

Mets le dossier dans `levels` et clique sur `{{ui:root_level-browser_refresh}}` dans la liste des niveaux.
Une archive (`.zip`, `.tar.gz`) s'ouvre via l'éditeur, avec le générateur `{{ui:gen_level_archive}}`.
Plus - [[2_playing-levels]]

### Le jeu dit que le niveau vient d'une version plus récente. Que faire ?

Mettre le jeu à jour. Une ancienne version n'ouvre pas les fichiers d'une version plus récente, pour ne jamais les lire de travers.
Plus - [[5_troubleshooting]]

### Peut-on récupérer un mot de passe de niveau oublié ?

Non. La clé n'est stockée nulle part : ni dans le jeu, ni dans le fichier, ni chez qui que ce soit.
Plus - [[5_troubleshooting]]

### Le jeu peut-il jouer un niveau tout seul ?

Oui, avec la condition `{{ui:menu_levelview_options-bot}}` sur l'écran du niveau : `{{ui:enum_bot-kind_reflex}}` ou `{{ui:enum_bot-kind_warm}}`. Un bot a les mêmes contrôles que toi, et il peut perdre lui aussi.
Plus - [[9_bots]]

## Créer des niveaux

### Comment créer un premier niveau ?

`{{ui:menu_main_editor-btn}}` dans le menu principal, puis `{{ui:settings_editor-settings_editor-settings}}`, puis `{{ui:settings_editor-settings_create-level}}`.
Copie un morceau dans le dossier du niveau, règle le tempo (bpm), place un objet avec deux images clés et lance un test.
Plus - [[2_first-level]]

### Quels fichiers de musique fonctionnent ?

`ogg`, `mp3` et `wav`, rien d'autre. `flac`, `aiff` et les modules de tracker ne se chargent pas

`ogg` est le meilleur choix. Il est 8 à 10 fois plus léger que `wav` et, contrairement à `mp3`, n'ajoute pas de silence au début.
Plus - [[2_preparing-the-track]]

### Puis-je utiliser n'importe quelle chanson ?

Rien n'est vérifié sur ton propre disque. La licence de la musique compte quand un niveau est proposé à un service, et de tels services n'existent pas encore.
Plus - [[1_licensing-basics]]

### Comment partager un niveau ?

À la main, sous forme de dossier ou d'archive. Un build Steam peut aussi publier un niveau dans le Steam Workshop. Il n'y a pas encore de serveur officiel.
Plus - [[6_sharing-by-hand]], [[17_publishing]]

## Le projet

### Y a-t-il des classements en ligne ou un catalogue de niveaux ?

Pas encore. Le serveur officiel et les serveurs communautaires sont en développement.
Plus - [[4_server/index]]

### Pourquoi le code du jeu est-il fermé ?

J'ai des raisons personnelles pour cela.
Quand le développement s'arrêtera pour de bon, tous les dépôts deviendront ouverts, et l'organisation [bullet-hero](https://github.com/bullet-hero) pourra être confiée à quelqu'un d'autre

Le SDK, la documentation et le futur serveur sont déjà ouverts. Plus - [[index]]

### Tu as trouvé un bug ?

Signale un bug du jeu dans [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Pose tes questions sur [Discord](https://discord.gg/gkHQrp9NgS).
Où écrire et quoi joindre - [[11_help]]

Tous les liens du projet - [[links]]
