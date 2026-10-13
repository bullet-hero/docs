---
title: Guide de style
date: 2026-10-13
tags: [contributor]
---

# Guide de style

Écris simplement : une phrase, une idée, des nombres plutôt que des adjectifs. Un trait d'union entouré d'espaces au lieu d'un tiret long, pas de points-virgules, pas de point à la fin d'un paragraphe

Le texte rend compte, il ne vend pas. Chaque émotion est d'abord transformée en liste, en tableau ou en nombre.
Une page qui sonne comme du marketing, une posture d'expert ou un assistant aimable est ratée, même si chaque fait qu'elle contient est juste

## La simplicité d'abord

Cette règle passe avant toutes les autres

Un texte peut ne contenir aucun remplissage et rester pourtant difficile à lire. Chaque phrase est vraie, mais elles s'enchaînent en un seul raisonnement dense, et le lecteur doit tout garder en tête à la fois

Les pages pour débutants s'écrivent pour pouvoir être parcourues en diagonale. Ce sont les pages pour les joueurs, les premières pages pour les auteurs de niveaux, le démarrage rapide, la FAQ, l'aide et la page d'accueil de chaque section. Les pages de référence et du SDK peuvent être plus denses, mais les mêmes règles s'appliquent à leurs phrases

1. **Seulement ce dont le lecteur a besoin maintenant.** Avant chaque phrase, demande-toi : le lecteur agira-t-il autrement après l'avoir lue ? Sinon, coupe-la ou déplace-la vers la page détaillée. Les cas limites, les réserves propres à une plateforme, les raisons internes, le fonctionnement du site lui-même - pas pour une page de débutant
2. **Une phrase, une idée.** Pas de chaînes de propositions reliées par des deux-points, "parce que", "donc", "alors que", pas de parenthèses dans des parenthèses. Deux phrases courtes valent mieux qu'une longue. Une phrase peut être seule sur sa ligne à l'intérieur d'un paragraphe : avec un point à la fin, sauf la dernière. En chinois et en japonais, une phrase seule sur sa ligne est un paragraphe à part, précédé d'une ligne vide
3. **La règle générale, pas les exceptions.** "Les nombres coïncident en général" au lieu de trois phrases sur les cas où ils divergent. L'exception vit sur la page détaillée, derrière `Plus - [[page]]` (en anglais `More - [[page]]`, en chinois `更多：[[page]]`, en japonais `詳細：[[page]]`, en espagnol `Más - [[page]]`, en portugais `Mais - [[page]]`)
4. **La navigation avant l'explication.** Une page d'accueil, c'est une courte introduction et un tableau nom -> lien, ou des lignes comme `Everything you can download - [[download]]`. Les colonnes descriptives comme "ce que c'est" et "statut" sont inutiles quand le lien le dit déjà
5. **Dis ce qui compte, pas comment ça marche.** "Ce nombre compte plus que tous les autres" plus un lien, au lieu de décrire le mécanisme
6. **Le statut en un mot.** `In development`, `Not available`, `Current version - gv 1.0.0`. Pas de "au moment de la rédaction", pas de "pas avant"
7. **Développe une abréviation à sa première apparition.** Par exemple, une colonne `gv` -> `game version`
8. **Parle au lecteur.** Une question et sa réponse, c'est bien : `Don't like the documentation? Then you can help write it`. `You may want to...` convient aussi
9. **Des mots simples.** Un terme n'apparaît que si le lecteur le rencontrera dans l'interface du jeu. Il est alors entre backticks, exactement comme le jeu l'affiche

```
Before (correct, but heavy):
The numbers do not follow each other. `gv` and `sv` once started equal and are now free to diverge: an SDK change does not have to move the game version, and a game update does not have to move the SDK version

After:
The version numbers do not have to follow each other, but in most cases they match.
Versions are also bumped together, and a shared update carries the same version
```

## Ponctuation

La ponctuation suit les normes de la langue, avec deux écarts délibérés. Les deux sont obligatoires

**Pas de tirets longs.** Le tiret cadratin et le tiret demi-cadratin ne sont pas utilisés du tout. Partout où un tiret est nécessaire, écris un trait d'union entouré d'espaces

```
Before:  Bullet Hero — less a game than a player for animations
After:   Bullet Hero - less a game than a player for animations
```

Le chinois et le japonais n'utilisent aucun tiret : ni `——`, ni `—`, ni même un trait d'union entouré d'espaces. Écris à la place une virgule, un deux-points ou une nouvelle phrase (`，` et `：` en chinois, `、` et `：` en japonais)

```
Before:  Bullet Hero——与其说是游戏，不如说是动画播放器
After:   Bullet Hero与其说是游戏，不如说是动画播放器

Before:  Bullet Hero——ゲームというより、アニメーションのプレイヤー
After:   Bullet Heroはゲームというより、アニメーションのプレイヤー
```

**Pas de point à la fin d'un paragraphe.** Les points entre les phrases à l'intérieur d'un paragraphe restent. La dernière phrase d'un paragraphe, un élément de liste, une cellule de tableau et un titre ne prennent pas de point. Les points d'interrogation et d'exclamation restent

**Attention aux retours à la ligne.** Markdown fusionne en un seul paragraphe les lignes qui ne sont pas séparées par une ligne vide. Une ligne sans point suivie d'une autre ligne donne deux phrases collées

Donc en anglais, en russe, en espagnol, en portugais et en français, à l'intérieur d'un paragraphe, chaque ligne suivie d'une autre ligne se termine par un point. Mets une ligne vide avant chaque idée distincte

**En chinois et en japonais, un paragraphe est une seule ligne dans la source.** Markdown transforme un retour à la ligne à l'intérieur d'un paragraphe en espace, et cette espace apparaît entre des phrases chinoises ou japonaises et gêne la recherche. Le texte chinois et japonais n'est donc jamais coupé à la main, et une phrase qui doit être seule sur sa ligne est un paragraphe à part. Chaque idée distincte est précédée d'une ligne vide

Autres signes :

- **Le deux-points** est le signe de travail pour expliquer et énumérer, utilise-le librement
- **Le point-virgule** n'est jamais utilisé. Écris à la place un point ou un élément de liste séparé. Le chinois n'utilise pas non plus `；` : écris deux phrases ou une `，`. De même en japonais : deux phrases ou un `、`
- **Les points d'exclamation** sont rares, un au maximum par texte long
- **Les guillemets** en anglais, en russe, en espagnol, en portugais et en français sont uniquement des guillemets droits `"quotes"`, jamais `«»`. Le chinois utilise les `“”` pleine chasse, le japonais `「」`, le coréen des guillemets droits comme l'anglais
- **Les parenthèses** conviennent pour une courte remarque, une réserve ou une plaisanterie pince-sans-rire

## Chinois et japonais

Les règles ci-dessus s'appliquent à toutes les langues sans exception. Le chinois ajoute quelques points :

- **Adresse-toi au lecteur avec `你`,** jamais `您`. Le conseil est `建议`, l'opinion de l'auteur est `我`, jamais `开发者` ni `我们`
- **Ponctuation pleine chasse** `，。：？！（）` et guillemets `“”`. Le code, les noms de fichiers et tout ce qui est entre backticks gardent la ponctuation ASCII
- **Pas d'espace entre les hanzi et les lettres latines ou les chiffres,** comme le jeu lui-même l'écrit : `在Bullet Hero中`, `60帧`
- **Restent en lettres latines :** les noms de produits et de formats (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), les extensions de fichiers, les touches, les noms de champs
- **Les termes viennent de `game/zh-glossary.md`.** Chaque terme a une seule graphie, et les lignes marquées `strict` sont toujours suivies. Un libellé de l'interface est cité depuis la valeur de sa clé dans `game/zh.yaml`
- **Les titres des encadrés** sont 建议, 提示, 须知, 警告, 注意 (`> [!tip] 建议`)

Le japonais ajoute ces points :

- **Écris dans le registre です/ます.** Le lecteur n'est pas désigné par un pronom, jamais `あなた` : construis la phrase pour que le sujet soit clair sans lui. Le conseil est `〜することをおすすめします` ou `推奨`, l'opinion de l'auteur est `私`, jamais `開発者` ni `私たち`
- **Ponctuation pleine chasse** `、。：？！（）` et guillemets en coin `「」`. Une citation dans une citation est `『』`. Le code, les noms de fichiers et tout ce qui est entre backticks gardent la ponctuation ASCII
- **Les emprunts s'écrivent en katakana,** en gardant le `ー` final : `インスペクター`, `レイヤー`. C'est ainsi que les écrit l'éditeur Unity en japonais
- **Pas d'espace entre les kana ou les kanji et les lettres latines ou les chiffres,** comme le jeu lui-même l'écrit : `Bullet Heroでは`, `60フレーム`
- **Restent en lettres latines :** les noms de produits et de formats (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), les extensions de fichiers, les touches, les noms de champs
- **Les termes viennent de `game/ja-glossary.md`.** Chaque terme a une seule graphie, et les lignes marquées `strict` sont toujours suivies. Un libellé de l'interface est cité depuis la valeur de sa clé dans `game/ja.yaml`
- **La ponctuation se place en dehors des marqueurs de gras :** écris `**太字**。本文`, jamais `**太字。**本文`. Dans la seconde forme, Markdown ne peut pas fermer les `**`, et les astérisques s'affichent tels quels
- **Les titres des encadrés** sont 推奨, ヒント, 補足, 警告, 注意 (`> [!tip] 推奨`)

Le coréen ajoute ces points :

- **Écris dans le registre 합니다체** (`-ㅂ니다`/`-습니다`). Le lecteur n'est pas désigné par un pronom, jamais `당신`. Le conseil est `권장합니다`, l'opinion de l'auteur est `저`, jamais `개발자` ni `저희`
- **La ponctuation est ASCII et les mots sont séparés par des espaces,** comme en anglais, donc les règles sur le tiret, le point et les guillemets ci-dessus s'appliquent telles quelles
- **Les emprunts s'écrivent en hangeul** comme les écrit l'éditeur Unity en coréen : `레이어`, `인스펙터`
- **Pas de particule seule après un mot latin, du code ou un espace réservé** dont la phrase ne peut pas connaître le son final : écris la forme double `을(를)`, `이(가)` ou reformule
- **Restent en lettres latines :** les noms de produits et de formats (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), les extensions de fichiers, les touches, les noms de champs
- **Les termes viennent de `game/ko-glossary.md`.** Chaque terme a une seule graphie, et les lignes marquées `strict` sont toujours suivies. Un libellé de l'interface est cité depuis la valeur de sa clé dans `game/ko.yaml`
- **Une ponctuation ou du code à la fin du gras casse le gras quand une particule suit :** écris `**이름**을`, jamais `**"이름"**을`
- **Les titres des encadrés** sont 권장, 팁, 참고, 경고, 주의 (`> [!tip] 권장`)

L'espagnol ajoute ces points :

- **Un espagnol neutre, un seul texte pour l'Espagne et l'Amérique latine.** Le lecteur est `tú`, au singulier, jamais `usted`, `vosotros` ni `ustedes`. Le conseil est `se recomienda` ou `conviene`, jamais `te recomendamos`, l'opinion de l'auteur est `yo`, jamais `los desarrolladores` ni `nosotros`
- **Un vocabulaire qui se lit de la même façon des deux côtés de l'Atlantique :** `archivo` et non `fichero`, `equipo` ou `PC` et non `ordenador` ou `computadora`, `teléfono` ou `móvil` et non `celular`, `hacer clic` sur l'écran et `pulsar` une touche
- **Aucun adjectif qui s'accorde avec le genre du lecteur** (`listo`/`lista`) : reformule pour l'éviter
- **Les deux écarts s'appliquent par-dessus la typographie espagnole :** un trait d'union entouré d'espaces ` - ` au lieu de la raya (aussi dans les incises et les dialogues), des guillemets droits au lieu de `«»`, pas de point qui ferme un paragraphe, un élément de liste, une cellule de tableau ou un titre. Pas de `;`
- **`¿…?` et `¡…!` portent toujours les deux signes**
- **Les titres en casse de phrase** (`## Cómo funciona el ajuste`), jamais en Title Case. Une majuscule garde son accent (`Á`, `É`)
- **Restent non traduits :** les noms de produits et de formats (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), les extensions de fichiers, les touches, les noms de champs
- **Les termes viennent de `game/es-glossary.md`.** Chaque terme a une seule graphie, et les lignes marquées `strict` sont toujours suivies. Un libellé de l'interface est cité depuis la valeur de sa clé dans `game/es.yaml`
- **Les titres des encadrés** sont Recomendación, Consejo, Conviene saber, Advertencia, Precaución (`> [!tip] Recomendación`). `More - [[page]]` s'écrit `Más - [[page]]`

Le portugais ajoute ces points :

- **Un portugais du Brésil, le code `pt` ne porte pas de région.** Le lecteur est `você` avec des verbes à la troisième personne, jamais `tu`, `o senhor` ni `vocês`. Le conseil est `recomenda-se` ou `vale a pena`, jamais `recomendamos`, l'opinion de l'auteur est `eu`, jamais `os desenvolvedores` ni `nós`
- **Le vocabulaire du Brésil, jamais celui de l'Europe :** `arquivo` et non `ficheiro`, `tela` et non `ecrã`, `salvar` et non `guardar`, `mouse` et non `rato`, `celular` et non `telemóvel`, `baixar` et non `transferir`. `estar` suivi du gérondif (`está carregando`), jamais `estar a` suivi de l'infinitif
- **Aucun adjectif qui s'accorde avec le genre du lecteur** (`pronto`/`pronta`) : reformule pour l'éviter
- **Les deux écarts s'appliquent par-dessus la typographie portugaise :** un trait d'union entouré d'espaces ` - ` au lieu du travessão, des guillemets droits au lieu de `«»` ou `“”`, pas de point qui ferme un paragraphe, un élément de liste, une cellule de tableau ou un titre. Pas de `;`
- **Les titres en casse de phrase** (`## Como funciona o encaixe`), jamais en Title Case. Une majuscule garde son accent (`É`, `Ã`)
- **Restent non traduits :** les noms de produits et de formats (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), les extensions de fichiers, les touches, les noms de champs
- **Les termes viennent de `game/pt-glossary.md`.** Chaque terme a une seule graphie, et les lignes marquées `strict` sont toujours suivies. Un libellé de l'interface est cité depuis la valeur de sa clé dans `game/pt.yaml`
- **Les titres des encadrés** sont Recomendação, Dica, Vale saber, Aviso, Cuidado (`> [!tip] Recomendação`). `More - [[page]]` s'écrit `Mais - [[page]]`

Le français ajoute ces points :

- **Le français tel qu'il s'écrit en France, lu de la même façon en Belgique, en Suisse et au Canada.** Le lecteur est `tu`, jamais `vous`. Le conseil est `il vaut mieux` ou `mieux vaut`, jamais `nous te recommandons`, l'opinion de l'auteur est `je`, jamais `les développeurs` ni `nous`
- **Le vocabulaire des logiciels en français :** `fichier`, `paramètres`, `enregistrer`, `souris`, `écran`, `cliquer` sur l'écran et `appuyer sur` une touche
- **Aucun adjectif qui s'accorde avec le genre du lecteur** (`prêt`/`prête`) : reformule pour l'éviter
- **Les deux écarts s'appliquent par-dessus la typographie française :** un trait d'union entouré d'espaces ` - ` au lieu du tiret (aussi dans les incises), des guillemets droits au lieu de `«»`, l'apostrophe droite `'`, pas de point qui ferme un paragraphe, un élément de liste, une cellule de tableau ou un titre. Pas de `;`
- **Une espace insécable (U+00A0) avant `?`, `!` et `:`,** et avant `%` après un nombre, jamais une espace normale et jamais aucune. Le code et tout ce qui est entre backticks gardent leur propre texte
- **Les titres en casse de phrase** (`## Comment fonctionne l'aimantation`), jamais en Title Case. Une majuscule garde son accent (`É`, `À`)
- **Restent non traduits :** les noms de produits et de formats (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), les extensions de fichiers, les touches, les noms de champs
- **Les termes viennent de `game/fr-glossary.md`.** Chaque terme a une seule graphie, et les lignes marquées `strict` sont toujours suivies. Un libellé de l'interface est cité depuis la valeur de sa clé dans `game/fr.yaml`
- **Les titres des encadrés** sont Recommandation, Conseil, Bon à savoir, Avertissement, Attention (`> [!tip] Recommandation`). `More - [[page]]` s'écrit `Plus - [[page]]`

## Mise en page

- **Des paragraphes courts,** d'une à trois lignes
- **Une liste à puces** pour toute énumération de plus de deux éléments. Les listes numérotées seulement pour les étapes et les choix
- **Un tableau** partout où trois choses ou plus sont comparées sur plusieurs propriétés
- **L'italique** (`*text*`) pour les termes, les noms de produits et les genres : *musical bullet hell*, *Geometry Dash*. On ne peut pas compter sur l'italique dans les polices chinoises et japonaises, donc dans ces langues l'italique ne va que sur les noms de produits écrits en lettres latines, et l'insistance passe par le gras
- **Le gras** pour insister sur un mot ou pour ouvrir un paragraphe par son sujet
- **Les backticks** pour tout ce qui est technique : fichiers, champs, formats, valeurs, touches, commandes
- **Une version, c'est toujours son préfixe plus le nombre, entre backticks :** `gv 1.0.0`, `sv 1.1.0`, `fv 1.0.0`, `bv 1.0.0`, `mg 2`. Jamais un `1.0.0` nu, ni "version 1.0.0" ou "SDK 1.0.0" sans le préfixe. Les backticks ne fonctionnent pas dans `title` et `# H1`, donc là c'est `gv 1.0.0` en texte brut. Les versions de choses tierces (Unity, paquets NuGet) ne sont pas les nôtres et s'écrivent telles quelles
- **Pas d'emoji**

## Encadrés

Un paragraphe qui a un but concret devient un encadré. Il y en a exactement cinq, et le titre s'écrit dans la langue de la page :

| Encadré | Titre anglais | Titre russe | Titre chinois | Titre japonais | Titre coréen | Titre espagnol | Titre portugais | Titre français | Ce qu'il introduit |
|---|---|---|---| --- |---|---|---|---|---|
| `> [!tip] Recommendation` | Recommendation | Рекомендация | 建议 | 推奨 | 권장 | Recomendación | Recomendação | Recommandation | fais comme ça |
| `> [!tip]` | Tip | Подсказка | 提示 | ヒント | 팁 | Consejo | Dica | Conseil | un raccourci, une astuce, une voie plus rapide |
| `> [!info]` | Worth knowing | Интересно | 须知 | 補足 | 참고 | Conviene saber | Vale saber | Bon à savoir | du contexte qui explique une décision |
| `> [!warning]` | Warning | Предупреждение | 警告 | 警告 | 경고 | Advertencia | Aviso | Avertissement | cela coûtera du temps ou de la qualité |
| `> [!caution]` | Caution | Внимание | 注意 | 注意 | 주의 | Precaución | Cuidado | Attention | cela détruit du travail ou publie un niveau cassé |

**Deux encadrés au maximum par page,** car un troisième cesse d'être lu comme une insistance. Les pages de référence peuvent en avoir deux par section. Une page sur quelque chose qui n'existe pas encore s'ouvre par un `> [!warning]` sur son statut, et celui-ci ne compte pas dans la limite

## Voix

- **Adresse-toi au lecteur avec "you"** en anglais (en russe, le "вы" formel en minuscule, en chinois `你`, en espagnol `tú`, jamais `usted`, en portugais `você`, en français `tu`, jamais `vous`). Le japonais ne désigne pas le lecteur par un pronom et n'utilise jamais `あなた`
- **Le projet parle de façon impersonnelle,** jamais en tant que "les développeurs" ou "nous". Un conseil s'écrit "it is recommended" en anglais (en russe "рекомендуется", en chinois `建议`, en japonais `〜することをおすすめします` ou `推奨`, en espagnol `se recomienda` ou `conviene`, en portugais `recomenda-se` ou `vale a pena`, en français `il vaut mieux` ou `mieux vaut`), et un fait a pour sujet la chose elle-même : "Le jeu ne livre aucune texture"
- **L'opinion ou la décision de l'auteur est à la première personne,** "I recommend" en anglais (en russe "я рекомендую", en chinois `我建议`, en japonais `私は〜をおすすめします`). Le jeu est fait par une seule personne, donc "je" est honnête ici. Seulement pour un vrai jugement ou une vraie décision, pas pour de simples faits
- **Les notes de `notes/` peuvent parler à la première personne,** car une note est le compte rendu de son auteur
- **Pas d'historique dans la documentation.** Une page de documentation décrit comment les choses fonctionnent maintenant. "Avant, c'était X" relève d'une note
- **Pas de prétention à être meilleur.** Une comparaison n'est permise que si elle aide le lecteur à comprendre plus vite
- **Indique les limites de ce qui est connu.** "Très probablement", "pas encore connu". Une fausse assurance est pire que l'ignorance
- **Chaque jugement s'accompagne de sa raison.** Un adjectif sans raison est un défaut
- **Des nombres plutôt que des adjectifs.** Secondes, images, mégaoctets, versions, nombres d'objets
- **L'ironie est sèche et rare,** une courte remarque entre parenthèses. Les pages de référence n'en contiennent presque pas
- **Pas de grossièretés** dans aucune langue, y compris les mots de substitution vulgaires
- **N'invente jamais** une adresse, un nombre ou un fait. Sans source, dis que c'est inconnu

## Ouverture de page

**L'ouverture répond, elle n'annonce pas.** Elle ne décrit pas la page ("ce qu'est X, comment fonctionne Y et où se trouve Z"), elle donne une réponse courte à la question pour laquelle la page existe. Une telle ouverture est utile à elle seule, même si le lecteur ne va pas plus loin

**L'essentiel va dans le premier paragraphe.** C'est aussi la description dans les listes, la recherche et les aperçus de liens : coupée à 200 caractères, sans liens ni mise en forme. La réponse peut se poursuivre dans le deuxième et le troisième paragraphe

**Ne découpe pas une page courte.** S'il y a peu de contenu, l'ouverture se fond dans le corps au lieu d'être répétée sur une ligne à part en haut

```
Before:
Where to report a bug or ask a question, and what to write so the bug can be reproduced

After:
Game bugs go to the releases issues, questions to Discord. Attach the version string from the settings and the steps that lead to the bug
```

## Structure d'une page

1. `# H1` et une ouverture qui répond à la question de la page
2. Le corps ne répète pas l'ouverture, il donne les détails, les cas et les étapes
3. Des sections `##`, un sujet chacune : l'affirmation, puis le mécanisme ou les étapes, puis la conclusion
4. Là où c'est pertinent, des conseils concrets ou des liens "à lire ensuite" à la fin
5. La fin ne résume jamais la page

Une page de guide se lit en 2 à 4 minutes, soit environ 2000 à 3500 caractères. Une page de référence peut être plus longue, mais chaque section tient debout seule

## Ce qui trahit le texte de quelqu'un d'autre

- un tiret long, un point à la fin d'un paragraphe, un point-virgule
- "Ce n'est pas juste X, c'est tout un Y"
- les effets de style en trois temps : "plus rapide, moins cher, plus fiable"
- les entrées en matière creuses : "dans le monde d'aujourd'hui", "plongeons dans le sujet", "ce n'est un secret pour personne"
- un paragraphe final qui répète ce qui a déjà été dit
- des adjectifs enthousiastes sans raison : "incroyable", "extraordinaire", "un outil puissant"
- les formules de politesse creuses et les excuses au lecteur
- des tournures symétriques écrites pour le rythme plutôt que pour le sens
- des conseils génériques que personne n'a vérifiés avec ce jeu

## Avant et après

**Un paragraphe d'ouverture**

```
Before:
In today's world of level design, the Bullet Hero editor holds a special place — it's not just a
tool, it's a whole ecosystem. Let's dive in and see why.

After:
The editor builds a level from objects that live on a stretch of time and move along keyframes. Below is how it is arranged and in what order to work with it
```

**Un jugement**

```
Before:
The Blob format is an amazing solution that dramatically speeds up loading and makes your workflow more productive.

After:
`Blob` loads faster than `Json`, but it cannot be read by eye or diffed in git. Keep a level in `Json` while you work on it and convert it to `Blob` before publishing
```

**Quelque chose qui n'existe pas encore**

```
Before:
The official server will offer a convenient way to share your levels with the whole world.

After:
There is no official server yet. The protocol the game will use to talk to it has not been designed, so this page describes only what has already been decided
```

## Liste de vérification avant une pull request

1. La page peut être parcourue en diagonale : une idée par phrase, les détails plus bas sur la page ou sur leur propre page
2. Pas de tirets cadratins ni demi-cadratins (le chinois et le japonais n'utilisent aucun tiret)
3. Aucun paragraphe, élément de liste ou titre ne se termine par un point
4. Pas de lignes collées : chaque idée distincte est son propre paragraphe ou séparée par un point dans la ligne. Un paragraphe chinois ou japonais est une seule ligne dans la source
5. Pas de points-virgules, pas d'emoji, un point d'exclamation au maximum
6. Pas de grossièretés
7. Les virgules, les deux-points et les accords suivent la norme, pas de fautes de frappe
8. Chaque jugement a sa raison à côté
9. Les nombres, les noms de champs et les liens viennent d'une source
10. Pas de "les développeurs" ni de "nous" dans `docs/` : le conseil est impersonnel, "je" seulement pour l'opinion ou la décision de l'auteur
11. Deux encadrés au maximum
12. L'ouverture après le H1 répond à la question de la page (l'essentiel dans les 200 premiers caractères), ne décrit pas la page et n'est pas répétée plus bas
13. La fin ne résume pas la page
