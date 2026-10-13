---
title: Assistant IA
date: 2026-10-13
tags: [level_author]
---

# Assistant IA

Un client IA qui parle MCP peut modifier le niveau ouvert dans l'éditeur pendant que tu regardes. Chaque lot de l'IA est une seule étape d'annulation, et l'IA ne peut ni publier, ni supprimer de fichiers, ni écrire par-dessus un autre niveau

Le jeu sur Windows, Linux et Mac est livré avec un serveur MCP pour cela. L'IA modifie à travers les mêmes opérations que toi, donc chaque changement apparaît tout de suite dans la vue et arrive dans l'historique comme les tiens

N'importe quel client qui parle MCP fonctionne, par exemple une application de chat ou un assistant de programmation. Rien dans le jeu n'est lié à une IA en particulier

## Connecter un client

1. Ouvre `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`
2. Coche `{{ui:settings_game-editor_mcp-enabled}}`. La ligne d'état sous les paramètres affiche le port sur lequel l'éditeur écoute
3. Appuie sur `{{ui:settings_game-editor_mcp-copy-config}}`. Le presse-papiers contient maintenant la configuration du client avec les deux chemins remplis
4. Colle-la dans les paramètres des serveurs MCP de ton client
5. Ouvre un niveau dans l'éditeur, ou demande à l'IA d'ouvrir elle-même l'éditeur ou un niveau

La configuration copiée ressemble à ceci :

```json
{ "mcpServers": { "bullet-hero": { "command": "<path to BH.MCP>", "args": ["--endpoint", "<path to endpoint.json>"] } } }
```

Le fichier du serveur `BH.MCP` se trouve à côté du jeu :

| Système | Fichier du serveur |
|---|---|
| Windows | `<game folder>/BH.MCP.exe` |
| Linux | `<game folder>/BH.MCP` |
| Mac | `<game>.app/Contents/Resources/mcp/osx-arm64/BH.MCP`, sur Intel `osx-x64` au lieu de `osx-arm64` |

Seul cet ordinateur peut se connecter, et un seul client à la fois.
Les téléphones et les tablettes n'ont pas de section MCP : l'assistant est réservé à l'ordinateur

Plusieurs copies du jeu peuvent tourner en même temps. L'IA travaille dans la dernière lancée jusqu'à ce que tu lui demandes d'en changer, et elle peut toutes les lister. Chaque copie n'accepte toujours qu'un client. Pour plusieurs copies, laisse `{{ui:settings_game-editor_mcp-port}}` à `0`, car deux copies ne peuvent pas écouter sur un même port

## Ce que l'IA peut et ne peut pas faire

L'IA peut faire presque tout ce que tu peux faire :
- lire le niveau : la hiérarchie, les objets, les images clés, les événements et les ressources
- créer, changer et supprimer des objets, des images clés, des marqueurs, des checkpoints, des pistes audio et la grille de pulsations
- lancer des générateurs, empaqueter et placer des prefabs, travailler en mode prefab
- importer une texture, une police ou un fichier audio dans le niveau
- remplir la fiche d'attribution d'une texture, d'une police ou d'un fichier audio après l'import : titre, description, lien, sources et auteurs - [[4_resource-record]]
- utiliser les thèmes, les polices et les sons d'interface prédéfinis du jeu. `resources_list` les marque comme ceux du jeu, et ils n'ont pas besoin d'import. Le jeu n'est livré avec aucun effet prédéfini : un effet que l'IA place est soit un effet que le niveau contient déjà, soit un nouvel effet qu'elle crée
- dessiner n'importe quel contour comme une forme du niveau à partir de ses coins, colorer une forme avec un dégradé, définir la police et l'alignement d'un texte, créer et modifier les thèmes du niveau
- annuler et rétablir, enregistrer le niveau ouvert, ouvrir un autre niveau, en créer un nouveau
- lancer et mettre en pause la lecture, comme le fait ton bouton de lecture
- faire passer le jeu à un autre écran, comme l'éditeur, un niveau ou les paramètres, avec les mêmes arguments qu'un lancement - [[12_launch-arguments]]
- démarrer le jeu quand il ne tourne pas, si le serveur se trouve à côté du jeu installé et que MCP est déjà activé

Une partie lancée ainsi compte dans tes statistiques comme n'importe quelle autre, donc l'IA n'en lance une que si tu le lui demandes

Elle ne peut pas :
- publier sur le Steam Workshop
- supprimer un niveau ou un fichier quelconque
- écrire par-dessus un autre niveau ou un autre fichier. Un import dont le nom de fichier est déjà pris est refusé
- ouvrir un niveau en lecture seule, ou un niveau protégé dont tu n'as pas saisi le mot de passe pendant cette session
- ouvrir un autre niveau tant que celui qui est ouvert a des modifications non enregistrées

**Un lot de l'IA est une étape de l'historique.** Il apparaît dans l'onglet `{{ui:settings_level-settings_history}}` comme `{{ui:op_group_ai-batch}}` avec la légende propre de l'IA. Un seul `Ctrl+Z` retire le lot entier. Plus sur l'historique - [[10_level-settings#Historique]]

**L'IA ne met jamais deux objets sur un même calque pendant qu'ils jouent tous les deux.** Si un lot le faisait, elle remonte l'objet le plus tardif au calque libre suivant dans la même étape et le signale. Le contenu des prefabs fait exception : il peut partager des calques avec le reste du niveau

Le premier lot de l'IA qui change un niveau passe son `{{ui:settings_level-settings_metadata-level-ai-generated}}` à `{{ui:enum_ai-generation_yes}}`, dans la même étape. Annuler le lot l'annule aussi. Plus - [[2_metadata-and-sharing#Génération par IA]]

## Tu as la priorité

L'IA ne se bat jamais avec toi pour l'éditeur :
- pendant que tu fais glisser une poignée de gizmo ou que tu balaies la timeline, les modifications de l'IA sont refusées, et elle attend puis réessaie
- l'IA ne prend la tête de lecture que lorsque tu ne fais rien : ni en lecture, ni en glissement, ni en saisie, ni en enregistrement
- l'éditeur lance la lecture d'un niveau dès son ouverture, donc l'IA peut la mettre en pause pour regarder des images. Un niveau que l'IA ouvre ou crée elle-même reste en pause. Si tu regardes la lecture exprès, l'IA demande avant de mettre en pause
- si tu touches l'éditeur pendant que l'IA regarde une image, l'IA s'arrête tout de suite. La tête de lecture reste là où tu l'as mise
- pendant un parcours de l'historique, l'IA ne peut pas modifier non plus

Tant qu'un client est connecté, la vue affiche `AI` dans son coin supérieur droit, sous les boutons de recherche. Sa couleur indique l'état : vert - connecté, ambre - l'IA travaille, rouge - le dernier appel de l'IA s'est terminé par une erreur.
Après la déconnexion du client, le badge reste {{v:mcp.badge-hold-seconds}} secondes, pour qu'une IA qui se reconnecte à chaque étape ne clignote pas. Il se masque en même temps que les outils de la vue.
Survole-le pour lire l'état en mots : `{{ui:editor_agent-badge_connected}}`, et pendant que l'IA travaille, la légende de ce qu'elle fait.
La croix à côté déconnecte le client et le refuse, et le badge disparaît

Un arrêt n'est pas enregistré. Désactiver puis réactiver `{{ui:settings_game-editor_mcp-enabled}}` ou redémarrer le jeu l'efface

## Ce que voit l'IA

L'IA regarde le niveau de deux façons :
- **un schéma.** Un rendu de n'importe quelle image du niveau, calculé hors écran. Il ne déplace pas la tête de lecture. Il montre les formes et les hitboxes, mais ni les textes ni les effets
- **une capture.** De vrais pixels, exactement comme le niveau se dessine, pris à travers ta tête de lecture. Pendant un instant, la tête de lecture saute à cette image et les superpositions de l'éditeur se masquent. Puis la tête de lecture revient là où tu l'as laissée, sauf si `{{ui:settings_game-editor_mcp-follow-ai}}` est activé. Le rendu est cadré par la caméra du niveau, pas par la caméra de l'éditeur. Pour regarder un détail de près, l'IA peut à la place cadrer un rectangle du monde. Le niveau ne change pas

Un arrêt sur image d'un effet après un saut est proche de ce que montre une lecture continue, mais pas toujours identique

L'IA ne peut pas entendre la musique. Elle transforme le morceau en nombres : tempo, pulsations, mesures, sections, volume de chaque bande.
C'est une estimation avec un indice de confiance, et elle peut se tromper, par exemple de la moitié ou du double du tempo. La grille de pulsations que tu as fixée dans le niveau prime sur l'estimation de l'IA.
Une grille de pulsations que l'IA propose à partir de l'analyse arrondit un tempo à moins de 0,01 % d'un nombre entier à ce nombre, et son décalage est toujours plus court qu'une mesure. Une proposition sur une partie du morceau prend le tempo propre à cette partie, donc un morceau dont le tempo change reçoit un segment par tempo

Alors, quand le timing compte, l'IA peut te demander d'écouter. Elle joue dans l'éditeur un passage de {{v:mcp.max-play-seconds}} secondes au plus, et cela déplace aussi la tête de lecture. Touche l'éditeur, et la lecture s'arrête là où elle en est

Tant que le son de l'éditeur est coupé, l'IA ne joue rien et te demande de rétablir le son

Les actions propres de l'IA ne produisent aucun son d'interface : une annulation, un enregistrement ou un refus qu'elle provoque est silencieux. Seul ce qu'elle joue exprès s'entend

## Le dossier ai

L'IA garde sa mémoire du niveau dans le dossier `ai` à l'intérieur du dossier du niveau. La session suivante, avec n'importe quel client, le lit en premier et reprend là où la précédente s'est arrêtée

Ce qu'il contient :
- `CONTEXT.md` - le brief, la musique, le plan des sections, les décisions, tes remarques et les questions ouvertes
- d'autres fichiers que l'IA décide de garder, `.md` ou `.json` uniquement
- `manifest.json` - si le dossier voyage avec le niveau. L'IA ne peut pas le changer

Le dossier n'apparaît que lorsque l'IA a pour la première fois quelque chose à écrire. Un fichier contient jusqu'à {{v:mcp.ai-file-max-kb}} Ko, le dossier entier jusqu'à {{v:mcp.ai-folder-max-mb}} Mo. Ce sont de simples fichiers texte : tu peux les lire, les modifier ou les supprimer toi-même

> [!warning] Avertissement
> Le dossier `ai` ne fait pas partie de l'historique du niveau. `Ctrl+Z` n'annule pas ce que l'IA y a écrit

**Le dossier voyage avec le niveau par défaut** : dans une archive exportée et dans un envoi sur le Steam Workshop. Pour le garder chez toi, décoche `{{ui:settings_level-settings_metadata-level-ai-share}}` dans l'onglet `{{ui:settings_level-settings_metadata}}` des paramètres du niveau. La case apparaît une fois que le dossier existe. Elle est enregistrée dans un fichier tout de suite, donc `Ctrl+Z` ne l'annule pas non plus

Un mode d'export avec mot de passe n'emporte jamais le dossier, quoi que dise la case. Plus - [[13_export-and-protection#Exporter le niveau]]

Une copie du niveau sur cet appareil emporte le dossier, puisqu'une copie n'est pas un partage

## Paramètres

Ils se trouvent tous dans `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}` et ne sont conservés que sur cet appareil :
- `{{ui:settings_game-editor_mcp-enabled}}` - si un client peut se connecter ou non. Désactivé par défaut
- `{{ui:settings_game-editor_mcp-port}}` - le port sur lequel l'éditeur écoute. `0` en choisit un libre à chaque démarrage
- `{{ui:settings_game-editor_mcp-follow-ai}}` - activé : après une capture, la tête de lecture reste sur l'image que l'IA a regardée, en pause
- `{{ui:settings_game-editor_mcp-reveal-edits}}` - après chaque modification de l'IA, sélectionne et localise ce qu'elle a créé ou changé
- `{{ui:settings_game-editor_mcp-operation-delay}}` - combien de temps l'éditeur attend entre deux opérations de l'IA, pour que tu puisses les suivre. `0` applique chacune tout de suite

Chaque paramètre et sa valeur par défaut - [[14_editor-settings#Agent IA]]

Suite : [[4_not-losing-work]], [[13_export-and-protection]]
