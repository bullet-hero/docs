---
title: Politique de licence des niveaux des joueurs
date: 2026-10-14
tags: [legal]
---

# Politique de licence des niveaux des joueurs

Chaque niveau créé par un joueur est distribué sous CC BY-NC : avec attribution et uniquement à des fins non commerciales. Une ressource externe est autorisée sous une licence ouverte acceptée ou avec l'autorisation directe de son auteur

> [!warning] Avertissement
> Les informations de cette page seront retravaillées plus tard - les conditions, la liste des licences acceptées et la manière d'enregistrer une autorisation peuvent encore changer

Bullet Hero permet aux joueurs de créer leur propre contenu (UGC, user-generated content, contenu généré par les utilisateurs), et ce contenu doit être placé sous licence. L'approche est proche de celle de *Geometry Dash*, à une différence près : là où *Geometry Dash* traite d'une seule piste musicale, cette politique couvre **toutes** les ressources externes d'un niveau

## La licence du niveau

Chaque niveau créé par un joueur est distribué sous **CC BY-NC** :

- **CC** - une licence Creative Commons
- **BY** - l'attribution est obligatoire : les auteurs sont crédités
- **NC** - uniquement à des fins non commerciales

Cette licence couvre le contenu original propre au niveau : sa disposition, son timing et ses images clés, son code personnalisé et le travail créatif qui consiste à assembler le tout en un niveau fini. **Elle ne modifie pas la licence des ressources externes intégrées au niveau**

Chaque ressource externe conserve sa propre licence ou autorisation, enregistrée séparément pour chaque ressource (voir plus bas). La CC BY-NC du niveau est une enveloppe autour de ressources qui, chacune de leur côté, peuvent déjà être redistribuées de cette manière

**Un niveau n'est éligible à la distribution sous CC BY-NC que si chacune de ses ressources externes remplit l'option A ou l'option B.** Si une seule ne la remplit pas, le niveau ne peut pas être distribué par les services web officiels de Bullet Hero (le serveur officiel, OWS)

Je n'empêche pas la libre distribution des niveaux par des canaux non officiels. Je suis catégoriquement opposé à l'utilisation commerciale des niveaux

## Ressources externes

Les ressources externes recouvrent un large éventail de données :

- musique et audio : `.mp3`, `.wav`, `.ogg`
- textures et images : `.png`, `.jpg`, `.jpeg`
- polices : `.ttf`, `.otf`
- textes et octets : toutes données

Chaque ressource externe doit remplir l'une des deux options ci-dessous

### Option A - une licence ouverte

La ressource est disponible sous une licence identique à CC BY-NC ou plus permissive (voir la liste des licences acceptées plus bas). La ressource conserve sa **propre** licence d'origine : elle n'est pas convertie en CC BY-NC, elle permet déjà la redistribution publique non commerciale qu'exige CC BY-NC, donc l'inclure dans un niveau sous CC BY-NC est cohérent

La licence d'origine et la source de la ressource doivent être indiquées dans le fichier de métadonnées du niveau. La SIL OFL l'exige déjà pour les polices, et ici l'exigence s'applique à chaque ressource, pour que toute personne qui télécharge le niveau puisse voir à quelles conditions chaque partie a été utilisée

### Option B - l'autorisation directe de l'auteur

L'auteur de la ressource donne l'autorisation de l'utiliser spécifiquement dans Bullet Hero. Un "oui, vas-y" en privé ne suffit pas à lui seul : un niveau marqué CC BY-NC est redistribué publiquement, l'autorisation doit donc couvrir cela explicitement, et pas seulement ton usage personnel. Une autorisation valable accorde les trois points suivants :

1. Le droit d'utiliser la ressource dans un niveau de Bullet Hero
2. Le droit pour le niveau obtenu, cette ressource comprise, d'être librement redistribué **à des fins non commerciales** par des tiers via les services de Bullet Hero (OWS, Steam Workshop, NOWS), avec attribution à l'auteur
3. Un usage uniquement non commercial, énoncé explicitement

L'autorisation peut prendre n'importe quelle forme qu'un modérateur peut vérifier : un e-mail, un message privé ou une déclaration publique (par exemple sur Twitter/X). Sers-toi du modèle ci-dessous comme point de départ et conserve la réponse de l'auteur comme preuve

### Modèle de demande d'autorisation

Remplis les champs à compléter et adapte le ton si besoin, mais garde intacts les points 1 à 3 : ce sont eux qui rendent l'autorisation valable pour une distribution sous CC BY-NC. Le modèle est donné en anglais, comme dans la politique d'origine. Si l'auteur parle une autre langue, traduis le modèle en conservant les trois points

```
Subject: Permission to use "<TRACK/RESOURCE NAME>" in a Bullet Hero level

Hi <AUTHOR NAME>,

My name is <YOUR NAME / HANDLE>, I'm creating a level for Bullet Hero (a rhythm/
bullet-hell game - <link to game/project if available>) and I'd love to use your
work "<TRACK/RESOURCE NAME>" (<link to the original>) in it.

Specifically, I'm asking your permission to:
1. Use "<TRACK/RESOURCE NAME>" inside my Bullet Hero level.
2. Allow the level (including your work) to be shared/redistributed for FREE and
   NON-COMMERCIALLY by anyone who downloads it, through Bullet Hero's official and
   unofficial services (including its official server, Steam Workshop, and any
   community-run servers).
3. Credit you as "<HOW YOU WANT TO BE CREDITED>" wherever the level shows attribution.

To be clear, this permission is for non-commercial use only - the level will not be
sold, and no one (including me) will make money from it or from your work through it.

If you're fine with this, a simple reply confirming points 1-3 is all I need - I'll
keep this email/message as proof of permission. If you'd rather I credit you
differently, or you want to set any other condition, just let me know.

Thanks a lot either way!
<YOUR NAME / HANDLE>
```

Comment rédiger une telle demande et ce qui compte comme preuve sont expliqués plus en détail dans [[6_asking-permission]], où se trouve aussi une version russe du modèle

## Services externes

Le jeu peut fonctionner avec plusieurs services externes :

| Service | Description |
|---|---|
| Official Web Services (OWS) | le serveur par défaut, disponible sur toutes les plateformes |
| Steam Workshop | disponible sur PC |
| Non-official web services (NOWS) | des services que n'importe qui peut créer et exploiter comme il l'entend |

Tous les outils pour faire tourner ton propre serveur sont prévus en open source sous licence MIT. Aucun serveur n'existe encore. Plus d'informations sur les serveurs dans [[4_server/index]]

## Licences acceptées (option A)

Une ressource externe acceptée porte l'une de ces licences courantes, identique à celle du niveau ou plus permissive :

- La famille Creative Commons
  - CC BY-NC (Attribution - Pas d'utilisation commerciale) - identique à celle du niveau
  - CC BY (Attribution) - plus permissive que CC BY-NC
  - CC0 (domaine public) - la meilleure option, à utiliser dès que possible
- Apache, MIT - prévues pour le texte et le code, et plus permissives que CC BY-NC
- GPL - prévue pour le texte et le code, acceptée uniquement par un service dont le profil l'autorise. Ce n'est pas le cas du serveur officiel, voir plus bas
- SIL OFL (Open Font License) - doit être indiquée dans le fichier de métadonnées

> [!info] Bon à savoir
> Le profil de publication `standard`, sur lequel repose le serveur officiel, accepte CC0, CC BY, CC BY-NC, SIL OFL, MIT, Apache 2.0 et l'Unlicense, mais pas la famille GPL. Une œuvre sous GPL redistribuée via l'App Store entre en conflit avec les conditions d'Apple, donc un catalogue contenant de telles œuvres ne pourrait pas être servi sur iOS plus tard

Licences courantes qui ne sont **pas** acceptées :

- Propriétaire ("All Rights Reserved", tous droits réservés) - évidemment pas acceptée
- La famille Creative Commons
  - CC BY-SA (Attribution - Partage dans les mêmes conditions) - techniquement autorisée, mais une musique synchronisée avec un niveau compte comme une adaptation de celle-ci, et l'adaptation d'une œuvre ShareAlike doit porter la même licence. Le niveau devrait passer en CC BY-SA, qu'OWS n'accepte pas, donc la réponse est non
  - CC BY-ND (Attribution - Pas de modification) - une musique synchronisée avec un niveau compte comme une adaptation de celle-ci, et cette licence interdit de partager des adaptations. Un tel morceau ne peut être publié qu'avec l'autorisation de son auteur (option B)
  - CC BY-NC-SA (Attribution - Pas d'utilisation commerciale - Partage dans les mêmes conditions)
  - CC BY-NC-ND (Attribution - Pas d'utilisation commerciale - Pas de modification)

À la publication, le jeu compare la licence du niveau aux licences de sa musique. Un morceau NoDerivatives sans autorisation enregistrée, une licence du niveau qu'un morceau ShareAlike n'admet pas et deux morceaux ShareAlike qui exigent des licences différentes apparaissent dans le rapport de publication

## Où trouver des ressources acceptées

### Audio et musique

Gratuites à coup sûr :

- [ccMixter](https://ccmixter.org/) - parfait, contenu sous CC BY et CC BY-NC
- [Freesound](https://freesound.org/) - parfait, tout le contenu sous CC0, CC BY et CC BY-NC
- [Incompetech](https://incompetech.com/) - parfait, tout le contenu sous CC BY
- [Teknoaxe](https://teknoaxe.com/) - parfait, tout le contenu sous CC BY
- [Kenney Assets](https://kenney.nl/) - tous les sons sous CC0

Gratuites, mais chaque entrée mérite un coup d'œil :

- [SoundImage](https://soundimage.org/)
- [Pixabay](https://pixabay.com)
- [GoodKid](https://goodkidofficial.com/creators/) - aucune licence n'est déclarée, mais d'après leur FAQ, c'est du CC BY sans mention de l'auteur. Utilise-le comme du CC BY
- NCS - uniquement si le niveau garde la licence CC BY-NC par défaut

Nécessitent une vérification manuelle de la licence :

- [OpenGameArt](https://opengameart.org/) - si la licence ne peut pas être identifiée, la ressource ne peut pas être utilisée
- [FMA](https://freemusicarchive.org/home) - toutes sortes de licences CC, vérifie chacune avec attention
- SoundBible

Douteuses :

- Zapsplat
- [Play On Loop](https://www.playonloop.com/music-licensing/) - une condition : le jeu ne doit pas être un projet commercial

### Textures et images

Gratuites à coup sûr :

- [Poly Haven](https://polyhaven.com/)
- [AmbientCG](https://ambientcg.com/)
- [Kenney Assets](https://kenney.nl/)
- [Pexels](https://www.pexels.com/)
- [Unsplash](https://unsplash.com/)

Gratuites, mais chaque entrée mérite un coup d'œil :

- [Pixabay](https://pixabay.com)

Nécessitent une vérification manuelle de la licence :

- [OpenGameArt](https://opengameart.org/)
- [Rawpixel](https://www.rawpixel.com/) - uniquement la "Personal License" et la "Public Domain License", voir [la page des licences](https://www.rawpixel.com/services/licenses)
- itch.io
- Wikimedia Commons

### Polices

Gratuites à coup sûr :

- Google Fonts

## Le mot de la fin

Bullet Hero n'est pas un gros jeu. J'essaie de rester humain envers la communauté et je te demande d'en faire autant. Une bonne communauté se construit ensemble
