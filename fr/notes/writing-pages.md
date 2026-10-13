---
title: Rédiger les pages
date: 2026-10-13
tags: [contributor]
---

# Rédiger les pages

Les pages sont des fichiers markdown dans le dépôt ouvert bullet-hero/docs. Une modification arrive sous forme de pull request : un fork, une branche, la modification dans chaque langue, une vérification par rapport au guide de style

## Dépôts

Tous les dépôts du projet se trouvent dans l'organisation [bullet-hero](https://github.com/bullet-hero). Les dépôts ouverts :

| Dépôt | Ce qu'il contient |
|---|---|
| [bullet-hero/releases](https://github.com/bullet-hero/releases) | les releases contiennent chaque build public du jeu, les issues contiennent les bugs et les demandes des joueurs sur le jeu |
| [bullet-hero/sdk](https://github.com/bullet-hero/sdk) | le code du SDK, les issues contiennent les bugs et les demandes sur le SDK |
| [bullet-hero/docs](https://github.com/bullet-hero/docs) | ces pages et leurs traductions |
| [bullet-hero/backend](https://github.com/bullet-hero/backend) | le serveur, vide pour l'instant |

Le code du jeu (`bullet-hero/game`) et celui du site (`bullet-hero/frontend`) sont fermés

Cette page porte sur bullet-hero/docs

## Comment envoyer une modification

1. Fais un fork de [bullet-hero/docs](https://github.com/bullet-hero/docs) et crée une branche
2. Modifie ou ajoute des pages au format décrit plus bas
3. Modifie la page dans chaque langue, ou indique dans la pull request quelles langues ont encore besoin de la modification. Plus - [[translating]]
4. Vérifie le texte par rapport au [[style-guide]]
5. Ouvre une pull request avec une courte description de ce qui a changé et pourquoi

**Les faits viennent du jeu, du SDK ou de leur documentation.** Les nombres, les noms de champs, les noms de fichiers, les raccourcis et les adresses ne sont jamais devinés. Un doute sur la véracité de quelque chose ? Dis-le dans la pull request, pas sur la page

Une modification acceptée apparaît sur [bullethero.space](https://bullethero.space/) en quelques minutes : chaque push sur `master` reconstruit le site

> [!tip] Conseil
> Tu ne peux pas construire le site toi-même, car son code est fermé. L'aperçu le plus proche est Obsidian : un lien qu'Obsidian ne trouve pas ne sera pas trouvé non plus sur le site

## Comment fonctionne le dépôt

- **Uniquement du markdown.** Il n'a ni build propre ni scripts
- **C'est un coffre [Obsidian](https://obsidian.md/).** Ouvre le dossier racine du dépôt comme coffre, et les liens, les intégrations et les aperçus fonctionnent comme sur le site. N'importe quel autre éditeur markdown convient aussi
- **C'est un sous-module du site.** Le site inclut le dépôt comme son dossier `content/`, compile les pages lors de son build et les prérend toutes. Le site est construit à partir du dernier `master` de ce dépôt

## Qu'est-ce qui va où

| Chemin | Ce qu'il contient | Adresse sur le site |
|---|---|---|
| `<lang>/docs/1_game/` | pour les joueurs : l'installation, le jeu, les paramètres, les mécaniques | `/docs/game` |
| `<lang>/docs/2_editor/` | pour les auteurs de niveaux : le guide et la référence de l'éditeur | `/docs/editor` |
| `<lang>/docs/3_sdk/` | pour les développeurs : le SDK ouvert et le format des niveaux | `/docs/sdk` |
| `<lang>/docs/4_server/` | pour les hébergeurs de serveurs : serveurs officiels et communautaires | `/docs/server` |
| `<lang>/docs/5_changelog/` | le journal des modifications, une page par version du jeu | `/docs/changelog` |
| `<lang>/notes/` | articles, communauté, règles de rédaction, documents publics et politiques, par date | `/notes/<name>` |
| `<lang>/tags/` | pages des tags | `/tags/<tag>` |
| `<lang>/download.md` | la page de téléchargement | `/download` |
| `assets/` | images pour toutes les langues | intégrées aux pages |

`<lang>` est un dossier de langue : `en`, `ru`, `zh`, `zh-Hant`, `ja`, `ko`, `es`, `pt` ou `fr`. Un fichier en dehors de `docs/`, `notes/`, `tags/` et `download.md` ne devient pas une page

**La documentation décrit comment les choses fonctionnent maintenant.** Un historique des changements, une opinion ou un essai est une note dans `notes/`

## Noms de fichiers et ordre

- **L'ordre dans le menu latéral est fixé par un préfixe `N_`** sur chaque fichier et dossier dans `docs/` : `1_`, `2_` et ainsi de suite, jusqu'à `10_` et au-delà
- **Le préfixe n'arrive jamais dans l'adresse.** `1_game/3_controls.md` s'ouvre à `/docs/game/controls`
- **`index.md` n'a pas de préfixe.** C'est la page d'accueil de son dossier. Elle prend la position du dossier et donne son nom au groupe du menu latéral
- **Pour changer l'ordre, renomme les fichiers.** Active "Automatically update internal links" dans Obsidian, et il corrige chaque lien tout seul
- **Un nom sans son préfixe est unique dans une langue.** Si deux fichiers aboutissent à la même adresse, le build du site le signale
- **Un nom avec son préfixe est identique dans toutes les langues.** `en/docs/2_editor/4_craft/3_difficulty-curve.md` et `ru/docs/2_editor/4_craft/3_difficulty-curve.md` sont la même page
- **`notes/` n'a ni préfixes ni sous-dossiers.** Ne renomme jamais `notes/cookie-policy` : le bandeau des cookies du site renvoie vers elle

## Frontmatter, titre et description

Chaque page commence ainsi :

```md
---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

One line that says what the page is, up to 200 characters, no markup
```

- **`title`, le H1 et la description sont écrits dans la langue de la page.** L'exemple ci-dessus vient de la version anglaise
- **Le frontmatter, c'est `title`, `date` et `tags`.** Rien d'autre n'est lu. `date`, au format `YYYY-MM-DD`, est la date de la dernière mise à jour, pas de la création. Quand tu modifies un fichier, mets `date` au jour de la modification
- **`# H1` est obligatoire et égal à `title`.** Le site n'affiche que le corps de la page, donc le H1 est le titre visible
- **Le premier paragraphe après le H1 est la description** dans les listes, la recherche et les aperçus de liens. Il est coupé à 200 caractères. Écris-le sur une seule ligne, sans liens ni mise en forme. Il répond brièvement à la question de la page au lieu de décrire ce qu'elle contient, [[style-guide#Ouverture de page]]
- **Les sections sont des `##`, les sous-sections des `###`.** Elles produisent les ancres et la table des matières. Les niveaux plus profonds ne sont pas nécessaires

## Tags d'audience

Chaque page de documentation a de 1 à 3 tags de cette liste. Les tags s'écrivent en `snake_case` sans `#`. Le site les affiche sur la page

| Tag | Sur le site | Pour qui |
|---|---|---|
| `player` | [[player]] | un joueur ordinaire |
| `advanced_player` | [[advanced_player]] | un joueur qui s'intéresse aux mécaniques |
| `level_author` | [[level_author]] | crée des niveaux dans l'éditeur |
| `developer` | [[developer]] | construit quelque chose sur le SDK ou étend le jeu |
| `server_host` | [[server_host]] | fait tourner un serveur pour soi et ses amis |
| `server_advanced` | [[server_advanced]] | un gros hébergeur de serveur, prêt à étendre ou à écrire un serveur |
| `contributor` | [[contributor]] | modifie les textes et les traductions de ce dépôt |

Les notes de `notes/` utilisent à la place des tags thématiques, actuellement `legal` ([[legal]])

Le lecteur ne voit jamais le code du tag. Le libellé vient de la page du tag `<lang>/tags/<code>.md` :

- son `title` est le libellé
- son premier paragraphe décrit l'audience
- le site ajoute lui-même la liste des pages portant ce tag

Un nouveau tag a besoin d'une telle page dans chaque langue

Pour mentionner un tag dans le texte, fais un lien vers sa page : `[[level_author]]`. Le lien affiche le libellé dans la langue du lecteur

## Liens

| Quoi | Comment |
|---|---|
| Une autre page | `[[3_difficulty-curve]]`, par le nom de fichier complet avec son préfixe |
| Une section d'une page | `[[3_difficulty-curve#Anchor]]` |
| Une page d'accueil de dossier | `[[2_editor/4_craft/index]]`, avec le chemin, car chacune de ces pages s'appelle `index` |
| Un site externe | `[text](https://…)`, avec l'adresse complète et le schéma |

Les liens mènent à une adresse sans langue, donc une même source fonctionne dans toutes les langues. `[[cookie-policy]]` envoie un lecteur anglophone vers la page anglaise, un lecteur russophone vers la page russe, un lecteur sinophone vers la page chinoise, un lecteur japonais vers la page japonaise, un lecteur coréen vers la page coréenne, un lecteur hispanophone vers la page espagnole, un lecteur lusophone vers la page portugaise et un lecteur francophone vers la page française

Ne fais de liens que vers des pages qui existent. Le build du site signale chaque lien qu'il n'a pas pu résoudre

## Images

Les images se trouvent dans `assets/` à la racine du dépôt et s'intègrent avec `![[file.png]]`

Un seul dossier sert toutes les langues. Le texte dessiné sur une image n'est pas traduit avec la page

## Encadrés

| Syntaxe | Couleur | Usage |
|---|---|---|
| `> [!note]`, `> [!info]`, `> [!tip]` | bleu | contexte, raccourci, recommandation |
| `> [!warning]`, `> [!caution]` | jaune | coûte du temps ou de la qualité, détruit du travail |
| `> [!danger]`, `> [!bug]` | rouge | rendus, mais le guide de style ne les utilise pas |

Quel encadré choisir, son titre et la limite de deux par page - [[style-guide]]

## Nombres, versions et libellés de l'interface

Un nombre que le jeu fixe - la vitesse de l'avatar, une valeur par défaut des paramètres, une limite de taille - et la version actuelle ne sont pas tapés dans la page. Ils se trouvent dans `values.yaml` à la racine du dépôt, et la page écrit un espace réservé que le site remplit lors du build :

- `\{{v:avatar.move-speed}}` est une valeur de `values.yaml`. Le site l'écrit comme la langue de la page écrit les nombres, `0.15` en anglais et `0,15` en russe
- `\{{ui:menu_main_sandbox-btn}}` est un libellé de l'interface tiré de `game/<lang>.yaml`, dans la langue de la page
- `\{{` est une paire d'accolades littérale

Une clé qui n'existe pas arrête le build du site, donc un nouveau nombre va d'abord dans `values.yaml`. Une version citée comme un moment de l'histoire ("depuis `gv 1.0.0`") reste du texte. Obsidian affiche l'espace réservé tel qu'il est écrit

## Code et autres balisages

- **La coloration syntaxique** n'existe que pour `ts`, `tsx`, `js`, `json`, `csharp`, `bash`, `yaml`, `css` et `md`. Les autres langages s'affichent en texte brut
- **Les tableaux GFM, les listes de tâches, les notes de bas de page et les `==highlights==`** fonctionnent
- **Ni MDX ni JSX.** `{` et `<` s'affichent tels quels
