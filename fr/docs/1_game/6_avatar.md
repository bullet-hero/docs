---
title: Avatar et déplacement
date: 2026-10-14
tags: [advanced_player]
---

# Avatar et déplacement

L'avatar marche à {{v:avatar.move-speed}} unités par seconde, et un dash le porte sur {{v:avatar.dash-distance}} unités en {{v:avatar.dash-time}} s. La hitbox est un cercle de rayon {{v:avatar.hitbox-radius}} unité, plus petit que le carré dessiné de {{v:avatar.body-size}} unité

Cette page est la source de vérité pour l'avatar. Le jeu et les deux bots sont construits sur ces chiffres, et le SDK les enregistre comme constantes `AvatarRules`. Un code qui contredit cette page est un bug dans le code

Les distances sont en unités du monde. La caméra par défaut fait exactement {{v:camera.default-height}} unités de haut (`ValueRules.DefaultZoom`), donc une unité vaut un dixième de la hauteur de l'écran, et le corps de l'avatar fait une demi-unité de large.
Le zoom de la caméra change ce que tu vois, mais pas les chiffres ci-dessous

## Les chiffres

| Quoi | Valeur | En clair |
|---|---|---|
| Vitesse de marche | `{{v:avatar.move-speed}}` u/s | traverse l'écran de haut en bas en deux tiers de seconde |
| Vitesse du dash | `{{v:avatar.dash-speed}}` u/s | {{v:avatar.dash-to-walk-ratio}} fois plus rapide que la marche |
| Durée du dash | `{{v:avatar.dash-time}}` s | |
| Distance du dash | `{{v:avatar.dash-distance}}` unités | vitesse × durée, trois quarts de la hauteur de l'écran |
| Temps de recharge du dash | `{{v:avatar.dash-cooldown}}` s | compté depuis le début du dash |
| Invulnérabilité du dash | `{{v:avatar.dash-invulnerability}}` s | aussi depuis le début, elle dure donc {{v:avatar.dash-invulnerability-margin}} s de plus que le mouvement lui-même |
| Dash le plus court | `{{v:avatar.arrival-distance}}` unité | la même que la distance d'arrivée, plus près et tu es déjà sur la cible |
| Vitesse de recul | `{{v:avatar.knockback-speed}}` u/s | {{v:avatar.knockback-to-walk-ratio}} fois plus rapide que la marche, [[7_damage]] |
| Durée du recul | `{{v:avatar.knockback-time}}` s | aucun contrôle pendant ce temps |
| Délai après dégâts | `{{v:avatar.damage-timeout}}` s | chaque coup suivant dans ce délai est ignoré |
| Taille du corps | `{{v:avatar.body-size}}` unité | le carré dessiné |
| Hitbox | rayon `{{v:avatar.hitbox-radius}}` unité | {{v:avatar.hitbox-scale}} du corps, volontairement plus petite que ce que tu vois |
| Apparition et disparition | `{{v:avatar.spawn-time}}` s | grandit en apparaissant et rétrécit jusqu'à un point |
| Effet de la taille du joueur sur la vitesse | total, `{{v:avatar.size-speed-influence}}` | un avatar plus grand se déplace proportionnellement plus vite. C'est la piste de taille du joueur du niveau, pas le zoom de la caméra |
| Vitesse de rotation | `{{v:avatar.turn-speed}}` /s | cosmétique : l'orientation du corps |
| Distance d'arrivée | `{{v:avatar.arrival-distance}}` unité | plus près que cela du curseur, on considère que tu es dessus |

Ce qui en découle, et c'est ce qui décide d'une esquive :

| Quoi | Valeur |
|---|---|
| Dash le plus court : distance | `{{v:avatar.arrival-distance}}` unité |
| Dash le plus court : durée | bien moins d'une image |
| Dash le plus court : recharge et invulnérabilité | bien moins d'une image, chacune |
| Dashs les plus fréquents | pas plus souvent qu'une image sur deux |
| Distance du recul | `{{v:avatar.knockback-distance}}` unités |

Ce qui se passe lors d'un coup - [[7_damage]]

## Déplacement

Tu contrôles l'avatar d'une de deux façons, et le jeu ne les mélange jamais :
- **Direction** : WASD, un stick de manette, le gyroscope. L'avatar va là où tu pousses, à la vitesse de marche. Un stick poussé à mi-course donne la moitié de la vitesse, et il n'y a pas d'autre "marche lente"
- **Curseur** : la souris ou un doigt. L'avatar poursuit le point au lieu de s'y téléporter. Il se déplace à sa propre vitesse de marche et reste en retard sur une souris rapide

Le déplacement est instantané dans les deux cas : ni accélération, ni glissade, ni inertie. Tu t'arrêtes à la même image que celle où tu arrêtes de bouger

## Le dash

L'invulnérabilité dure {{v:avatar.dash-invulnerability-margin}} s de plus que le mouvement. C'est cette marge après l'atterrissage qui permet de passer *à travers* un obstacle en dash

Tu diriges pendant un dash. Le dash va là où tu le demandes : selon la direction maintenue ou vers le point visé, et cela peut changer en plein dash. Un dash sans direction maintenue ne va nulle part

Avec un curseur, le dash va là où tu pointes et s'y arrête :

| Distance au curseur | Ce qui se passe |
|---|---|
| plus de {{v:avatar.dash-distance}} unités | un dash complet vers lui. Tu t'arrêtes avant le curseur |
| de {{v:avatar.arrival-distance}} à {{v:avatar.dash-distance}} unités | un dash raccourci qui s'arrête pile sur le curseur |
| moins de {{v:avatar.arrival-distance}} unité | pas de dash |

Un dash raccourci est le même dash à plus petite échelle. Trajet, invulnérabilité et recharge rétrécissent ensemble : un dash deux fois plus court protège deux fois moins longtemps et se recharge deux fois plus vite. Il ne revient jamais moins cher. Deux demi-dashs coûtent exactement autant qu'un dash complet et couvrent la même distance

Un dash qui n'a pas lieu ne coûte rien : la recharge ne démarre pas, rien n'est dépensé. Un joueur en mode direction qui ne maintient rien obtient la même réponse - pas de dash

Le corps prend un bleu plus profond pendant le dash, puis revient à sa couleur normale dans les {{v:avatar.dash-tint-fade}} s qui suivent. Rien d'autre ne change la couleur du corps, pas même un coup - le dash est ton propre mouvement, donc lui seul le fait

La traînée du dash et ce bleu dépendent de la longueur du dash : un dash complet les montre en entier, le plus court à `{{v:avatar.dash-effect-min}}` de cela, et tout ce qui est entre les deux proportionnellement. Un dash court projette ses particules plus lentement, donc la traînée paraît exactement aussi longue que le dash

### Deux styles, un même budget

- En mode `{{ui:field_common_direction}}`, un dash va toujours sur les {{v:avatar.dash-distance}} unités complètes. Une distance fiable sans viser, mais pas d'arrêt à mi-chemin non plus
- Avec un curseur, tu choisis la longueur et tu peux t'arrêter pile sur un point. Un dash court veut dire une protection plus courte et une image vulnérable de plus par dash. Pointe loin et le dash complet revient

En ligne droite, les deux couvrent la même distance dans le même temps. Aucun style n'est plus fort : l'un donne la précision, l'autre la simplicité

### Enchaîner les dashs

**Un dash maintenu n'est pas une invulnérabilité.** Recharge et protection ont la même durée, donc un bouton maintenu donne une chaîne continue de dashs. Mais entre deux dashs il y a toujours exactement une image où un coup peut t'atteindre, à n'importe quelle fréquence d'images, sur un téléphone lent comme sur un PC rapide.
La chaîne la plus serrée, c'est un dash pas plus souvent qu'une image sur deux

## La hitbox

L'anneau de points sur l'avatar est dessiné exactement le long de la hitbox. Une balle a frôlé le contour sans rien faire ? C'est voulu

Pendant l'invulnérabilité (en dash ou juste après un coup), il n'y a pas de hitbox du tout

Le même anneau montre tes vies : un point allumé est une vie en réserve

La visibilité de l'anneau se règle dans `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_hitbox-ring-opacity}}`. `0` le masque, mais les niveaux sont équilibrés pour quelqu'un qui le voit

Le corps est une grille de {{v:avatar.grid-cells}} carrés, {{v:avatar.grid-side}} sur 5. Quand la santé baisse, les carrés du bord vers le centre ne disparaissent pas mais s'estompent : un carré perdu reste comme un fantôme pâle, donc la grille montre toujours les {{v:avatar.grid-cells}}, et la santé se lit au nombre encore allumé.

C'est l'apparence de la skin classique. Une skin peut changer la grille, la forme de chaque case et les couleurs - [[16_skins]]
Les carrés fantômes sont assez transparents pour laisser voir l'anneau de la hitbox sous le corps.
À santé nulle, exactement un carré est allumé - le dernier.
Toute perte de santé s'affiche en `{{v:avatar.health-loss-time}}` s, tout regain en `{{v:avatar.health-gain-time}}` s, quel que soit le nombre de vies.
Si tu désactives `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics_avatar-render}}`, le corps devient un seul carré qui s'estompe. C'est pour les appareils faibles

## Arrivée et départ

L'avatar grandit dans le niveau en `{{v:avatar.spawn-time}}` s et rétrécit jusqu'à un point en `{{v:avatar.spawn-time}}` s à la mort. Dans les deux cas, il ne répond pas aux entrées, et pendant l'apparition il ne peut pas être touché

## Mise à l'échelle

Un niveau peut animer la taille et la vitesse de l'avatar avec ses propres pistes. Il peut aussi retirer le contrôle pour un moment ou désactiver les collisions

- Les vitesses de marche, de dash et de recul sont multipliées par un seul nombre. Donc à demi-vitesse, le dash est aussi deux fois plus court ({{v:avatar.half-speed-dash-distance}} unités)
- Un avatar plus grand se déplace proportionnellement plus vite, parce que ses esquives ont grandi aussi. La taille ici est la taille propre de l'avatar, venant de la piste de taille du joueur. Le zoom de la caméra ne change ni la vitesse, ni les distances, ni les fenêtres : l'avatar parcourt {{v:avatar.move-speed}} unités par seconde quoi que fasse la caméra
- La hitbox est une fraction du corps dessiné, donc elle grandit et rétrécit avec l'avatar
- La visée du dash utilise la distance actuelle, pas les 7,5 du tableau. Sur un niveau à demi-vitesse, un curseur à {{v:avatar.half-speed-dash-distance}} unités demande déjà un dash complet, et le seuil de {{v:avatar.arrival-distance}} unité devient {{v:avatar.half-speed-arrival-distance}}, parce que le dash au-dessus est aussi deux fois plus court
- Les fenêtres en secondes ne changent pas d'échelle : recharge, invulnérabilité, délai après dégâts, apparition. Seule la longueur du dash lui-même met à l'échelle ses deux propres fenêtres

Les bots suivent les mêmes règles, [[9_bots]]
