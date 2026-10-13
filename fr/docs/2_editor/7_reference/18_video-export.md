---
title: Export vidéo
date: 2026-10-03
tags: [level_author]
---

# Export vidéo

L'éditeur rend le niveau ouvert dans un fichier vidéo grâce à ffmpeg installé sur ton ordinateur. Le rendu se fait hors temps réel, une image à la fois, donc la vidéo est exacte quelle que soit la lenteur de la machine

L'export fonctionne sur Windows, macOS et Linux. Il n'est pas disponible sur téléphone

## Où le trouver

- `{{ui:editor_video-export_open}}` dans la colonne latérale des paramètres du niveau
- la commande `{{ui:cmd_editor_export-video}}` dans la palette de commandes

La fenêtre s'ouvre par-dessus l'éditeur. Ouverte depuis les paramètres du niveau, elle y revient à la fermeture. Pendant le rendu d'une vidéo, la fenêtre ne peut pas être fermée : `{{ui:editor_video-export_stop}}` met fin au rendu

## Installer ffmpeg

ffmpeg ne fait pas partie du jeu. Installe-le une fois, et la fenêtre le trouve d'elle-même. Il faut la version `{{v:ffmpeg.min-version}}` ou plus récente. Une version plus ancienne est refusée, et la fenêtre nomme la version trouvée

| Système | Commande d'installation |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | le paquet de ta distribution, par exemple `sudo apt install ffmpeg` |

> [!warning] Avertissement
> Certaines distributions Linux fournissent un ffmpeg plus ancien que `{{v:ffmpeg.min-version}}` (Ubuntu 24.04 fournit la 6.1). Installe alors une version plus récente depuis le site de ffmpeg et indique-la à la fenêtre

La fenêtre cherche ffmpeg dans cet ordre :
1. le fichier que tu as choisi avec `{{ui:editor_video-export_ffmpeg_choose}}`. Rien d'autre n'est alors cherché
2. le chemin dans la variable d'environnement `BH_FFMPEG`
3. `tools/ffmpeg` dans le dossier de données du jeu
4. chaque dossier de `PATH`
5. les dossiers où écrivent les installateurs habituels

`{{ui:editor_video-export_ffmpeg_auto}}` oublie le fichier choisi et cherche à nouveau. `{{ui:editor_video-export_ffmpeg_check}}` refait la vérification, par exemple juste après une installation

Ton ffmpeg peut contenir des encodeurs matériels (NVIDIA, AMD, Intel, Apple). La fenêtre essaie chacun sur un dixième de seconde de noir et n'utilise que ceux qui fonctionnent vraiment sur cet ordinateur

## Options de la fenêtre

| Option | Ce qu'elle fait |
|---|---|
| `{{ui:editor_video-export_container}}`, `{{ui:editor_video-export_codec}}` | le type de fichier et la façon dont il est compressé, voir les formats plus bas |
| `{{ui:editor_video-export_resolution}}` | la taille de la vidéo. La largeur et la hauteur sont des nombres pairs de `{{v:video-export.min-size}}` à `{{v:video-export.max-size}}` |
| `{{ui:editor_video-export_fps}}` | les images par seconde de la vidéo, jusqu'à `{{v:video-export.max-fps}}`. Elles ne dépendent pas de la fréquence d'images propre au niveau. En dessous de `{{v:video-export.min-simulation-rate}}`, chaque image est simulée en plusieurs pas, pour que le bot joue comme dans le jeu |
| `{{ui:editor_video-export_range}}` | tout le niveau, la plage de boucle de la timeline, ou tes propres images de début et de fin |
| `{{ui:editor_video-export_quality}}` | la place que prend la vidéo. Masqué pour les formats sans perte de toute façon |
| `{{ui:editor_video-export_full-chroma}}` | la couleur pour chaque pixel au lieu d'un sur deux. Des lignes colorées fines plus nettes, un fichier plus gros |
| `{{ui:editor_video-export_seed}}` | la graine du hasard du niveau. `0` garde la graine qu'utilise l'éditeur |
| `{{ui:editor_video-export_preroll}}` | combien de secondes avant le début sont jouées mais pas enregistrées, pour que les effets aient déjà leur historique. `{{v:video-export.default-preroll}}` par défaut, jusqu'à `{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | `{{ui:enum_bot-kind_reflex}}` par défaut, `{{ui:enum_bot-kind_warm}}`, ou `{{ui:enum_bot-kind_none}}` pour une vidéo sans avatar. Les impacts ne font rien pendant un export |
| `{{ui:editor_video-export_post-processing}}`, `{{ui:editor_video-export_effects}}` | les mêmes interrupteurs que dans l'éditeur, pour la vidéo seulement |
| `{{ui:editor_video-export_audio}}` | les pistes du niveau dans la vidéo |

Chaque option a son propre `?` dans la fenêtre.

L'interface de l'éditeur, la grille, les gizmos, la sélection et les limites de la caméra n'entrent jamais dans la vidéo. La caméra du niveau cadre l'image, et des bandes noires remplissent ce que son format ne couvre pas

## Vitesse de rendu

La vidéo ne dépend pas de la vitesse de ton ordinateur. Le temps du niveau et le bot avancent tous deux d'exactement une image de la vidéo par image rendue, donc une machine lente rend la même vidéo, simplement plus tard

`{{ui:enum_bot-kind_warm}}` calcule tout son parcours avant la première image, et la fenêtre montre où il en est. S'il ne trouve aucun parcours, l'export s'arrête et demande un autre bot

## Formats

Un format, c'est deux choix : `{{ui:editor_video-export_container}}` et `{{ui:editor_video-export_codec}}`. Seules les paires que ton ffmpeg sait produire sont listées. La ligne en dessous dit quel son va avec la paire et quel fichier tu obtiens

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | Son | Bon pour |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264, HEVC, AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | envoyer et mettre en ligne n'importe où |
| `{{ui:editor_video-export_container_mkv}}` | H.264, HEVC, AV1, VP9, FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | l'archivage, FFV1 sans aucune perte |
| `{{ui:editor_video-export_container_mov}}` | H.264, HEVC, ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | le montage dans Premiere, DaVinci Resolve, Final Cut |
| `{{ui:editor_video-export_container_webm}}` | VP9, AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | le web |
| `{{ui:editor_video-export_container_gif}}`, `{{ui:editor_video-export_container_webp}}`, `{{ui:editor_video-export_container_apng}}` | - | pas de son | de courts clips en boucle pour les discussions et les pages |
| `{{ui:editor_video-export_container_sequence}}` | PNG, JPEG, WebP, TIFF | `audio.wav` à côté des images | n'importe quel logiciel de montage l'importe |
| `{{ui:editor_video-export_container_audio}}` | WAV, FLAC, MP3, Opus | le format lui-même | le son du niveau seul, rien n'est rendu |

Le GIF prend une seule palette de 256 couleurs pour tout le clip. Garde-le court et petit : un GIF de tout un niveau pèse bien plus qu'un MP4 du même niveau

## Où va la vidéo

Par défaut, la vidéo va dans `recordings/<level id>/` dans le dossier de données du jeu, nommée d'après le niveau et l'heure de l'export. `{{ui:editor_video-export_output_folder}}` ouvre ce dossier. `{{ui:editor_video-export_output_choose}}` enregistre la vidéo suivante n'importe où ailleurs

Les enregistrements restent quand tu supprimes le niveau. Ils ne font pas partie d'un transfert de profil, sauf si tu coches `{{ui:settings_profile-transfer_category-recordings}}`

## Son

Le son de la vidéo n'est pas enregistré depuis les haut-parleurs, et tu n'entends rien pendant un export.

Avec `{{ui:editor_video-export_engine-audio}}` activé (par défaut) et des effets sur les pistes, le son du niveau joue en temps réel pendant le rendu des images, et le son propre au jeu est enregistré, effets compris. L'export dure au moins la longueur de la plage : un ordinateur rapide attend la fin du son. Désactivé, les pistes sont mixées à part, avec leurs images clés de volume et de panoramique mais sans leurs effets. `{{ui:editor_video-export_container_audio}}` mixe toujours à part

Sous l'aperçu, la fenêtre montre deux timelines, `{{ui:editor_video-export_track_frames}}` et `{{ui:editor_video-export_track_sound}}` : elles avancent indépendamment. Sur un niveau lourd, le son en parallèle peut saccader. Active alors `{{ui:editor_video-export_sound-after-frames}}` : le son est enregistré après la dernière image, et l'export prend plus longtemps, de la longueur de la plage

> [!warning] Avertissement
> Ne ferme pas le jeu pendant le rendu d'une vidéo. La fenêtre le rappelle pendant toute la durée

## Ce qui n'est pas dans la vidéo

- les effets sur les pistes audio, mais seulement avec `{{ui:editor_video-export_engine-audio}}` désactivé ou dans `{{ui:editor_video-export_container_audio}}`. La fenêtre prévient quand le niveau en a
- un arrière-plan transparent
- un enregistrement de ta façon de jouer : seul le bot peut jouer dans la vidéo

À lire ensuite : [[13_export-and-protection]], [[7_audio]]
