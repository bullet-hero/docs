---
title: "Couleur, thèmes et post-traitement"
date: 2026-10-02
tags: [level_author]
---

# Couleur, thèmes et post-traitement

Fais passer la couleur du contenu par une référence au thème, garde les couleurs littérales pour ce qui est vraiment unique. Active le post-traitement sur un sommet puis désactive-le, sinon les projectiles perdent leurs bords

## Références au thème et couleurs littérales

Une couleur peut être définie de deux façons :
- **une couleur littérale** - une valeur saisie directement dans l'objet
- **une référence au thème** - "prends tel emplacement du thème actif". Le thème actif est défini par une piste d'images clés

La différence apparaît au deuxième passage. Avec des références, changer la palette, c'est une modification du thème. Avec des littérales, c'est une modification de chaque objet

Le fond prend aussi sa couleur dans le thème. Comment fonctionnent les emplacements et les clés de thème - [[6_themes]]

> [!caution] Attention
> Vérifie le contraste sur chaque thème, pas seulement sur celui où tu as travaillé. Un niveau qui change de thème au drop doit rester lisible dans les deux. Des projectiles sombres parfaitement lisibles sur un thème clair disparaissent sur un thème sombre

## Post-traitement

L'ensemble standard d'URP plus deux effets de glitch. Tout est sur des clés, donc chaque paramètre peut être animé

> [!caution] Attention
> C'est le chemin le plus rapide vers un niveau auquel personne ne peut jouer. Un bloom au maximum transforme n'importe quel objet lumineux en tache, et un projectile perd son bord. L'aberration chromatique écarte les bords. Un glitch plus long qu'une mesure est une interférence, pas un style. Le bloom n'a pas de seuil : chaque pixel brille, donc un fond sombre tire vers le gris à mesure que l'intensité monte

Trois règles gardent le post-traitement du côté du style :
- active un effet sur un sommet puis désactive-le, ne le laisse pas en toile de fond
- n'active pas un effet qui nuit à la lisibilité des projectiles là où il faut les esquiver
- tu as dû plisser les yeux après avoir activé un effet ? Désactive-le. Le joueur ne plissera pas les yeux, il quittera

## Antialiasing

L'antialiasing est un paramètre du joueur, pas le tien.
Un niveau qui n'a le bon aspect que dans un seul mode n'a pas le bon aspect pour tout le monde

| Mode | Ce qu'il fait |
|---|---|
| `{{ui:enum_anti-aliasing-type_msaa}}` | par défaut. Lisse exactement les bords de la géométrie, et chaque forme est de la vraie géométrie |
| `{{ui:enum_anti-aliasing-type_fxaa}}` | coûte un passage sur l'écran, quelle que soit la quantité que le niveau dessine par-dessus lui-même |
| `TAA`, `STP` | non proposés : ils laissent une traînée derrière les objets rapides, et une traînée derrière un projectile rend le niveau plus difficile à lire |

À lire ensuite : [[1_readability-and-fairness|Lisibilité et équité]], [[1_level-budget|Budget du niveau]]
