---
title: Textures et polices
date: 2026-10-02
tags: [level_author]
---

# Textures et polices

Si une forme fait l'affaire, prends une forme : elle n'a pas de fichier, ne coûte pas de mémoire et ne pose pas de question de droits. Fais une texture à la taille de sa place à l'écran, pas plus de {{v:texture.mobile-max-side}} pour un niveau mobile et {{v:texture.desktop-max-side}} dans tous les cas

Arrondis la taille de la texture à la puissance de deux supérieure

## Formats et taille

Tout ce que le moteur sait décoder à partir des octets d'un fichier se charge. En pratique, ce sont `png` et `jpg`

Le jeu ne limite pas la taille du fichier, c'est le matériel qui le fait :

| Appareil | Plus grand côté |
|---|---|
| Android, garanti | 4096 |
| Android, en général | 8192-16384 |
| PC de bureau | jusqu'à 32768 |

## Mémoire

**La vraie limite, c'est la mémoire.** En mémoire, une texture est stockée en pixels bruts, quel que soit le poids du fichier.
Un `png` prend 4 octets par pixel. Un `jpg` en prend 3, car il n'a pas de transparence

| Taille | Mémoire (`png`) |
|---|---|
| 512 sur 512 | 1 Mo |
| 1024 sur 1024 | 4 Mo |
| 2048 sur 2048 | 16 Mo |
| 4096 sur 4096 | 64 Mo |
| 8192 sur 8192 | 256 Mo |

> [!caution] Attention
> Une texture de 8192, c'est un quart de gigaoctet pour une seule illustration. Sur un téléphone, ce n'est pas de la lenteur, c'est un plantage

## Ce que décide le joueur

Trois options des paramètres graphiques de chaque joueur décident de la mémoire que prend une texture :
- si les textures sont compressées au chargement. La compression divise les chiffres ci-dessus par 4 à 8
- le plus grand côté d'une texture en mémoire. La moitié du côté - un quart de la mémoire
- s'il faut construire des mipmaps, des copies réduites pour dessiner en petit

Un téléphone compresse les textures et les plafonne à {{v:texture.mobile-max-side}} par défaut. Un PC de bureau garde la texture entière et la plafonne à {{v:texture.desktop-max-side}}

**Ta part, ce sont les champs de la texture, avant tout ce qu'elle représente.** Ils se trouvent à côté de la texture dans la liste des ressources.
Une photo supporte le mieux la réduction et la compression. Un dessin aux bords nets les supporte moins bien

Une texture de type `{{ui:enum_texture-kind_pixel-art}}` n'a jamais de mipmaps, quelle que soit la préférence de l'appareil. Elle démarre aussi sans compression ni lissage, et les champs `{{ui:level_resources_texture-compression}}` et `{{ui:level_resources_texture-sampling}}` peuvent changer cela

## Mipmaps

Les mipmaps empêchent une petite texture de scintiller. Ce sont des copies réduites, dessinées à la place de la texture entière tant qu'elle est petite à l'écran.
Elles coûtent un tiers de mémoire en plus

Sans mipmaps, une texture réduite ne se lisse pas, elle ondule. Un joueur peut les désactiver, et le type `{{ui:enum_texture-kind_pixel-art}}` n'en a jamais

Une texture de 4096 qui occupe 200 pixels à l'écran coûte 256 fois la mémoire de la même texture réduite à 256 à l'avance

## Les formes avant les textures

Une forme est moins chère qu'une texture en tout : pas de fichier, pas de mémoire, pas de question de droits.
Les formes intégrées sont de la vraie géométrie, pas une illustration sur un rectangle. Elles n'ont pas de marges transparentes qui sont dessinées puis jetées

Cela se voit sur un téléphone. Sur une puce mobile de milieu de gamme, une scène de 1000 objets passe 95-97 % du temps du GPU à colorier des pixels.
Une forme couvre 29,4 % de son rectangle. Le reste d'un quad texturé est du gaspillage transparent

Une texture est nécessaire quand il faut précisément une illustration : un logo, une photo, un dessin fait main.
Pour une forme géométrique, prends une forme. Si celle qu'il te faut n'existe pas, dessine-la dans la fenêtre `{{ui:hint_level_shape-editor_header}}`

## Polices

Les polices se chargent en `ttf`, `otf`, `ttc`. Sans police propre, le texte est dessiné avec ce que le système a sous la main, et cela diffère d'un appareil à l'autre

`{{ui:settings_level-settings_fontcache}}`, c'est l'ensemble des caractères préparés à l'avance pour le dessin. Un générateur le reconstruit à partir du texte que contient le niveau.
Lance le générateur une fois que le texte ne change plus

Ensuite : [[1_level-budget]], [[2_mobile-devices]]
