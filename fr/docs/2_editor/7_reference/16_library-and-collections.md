---
title: Bibliothèque et collections
date: 2026-10-02
tags: [level_author]
---

# Bibliothèque et collections

Les collections contiennent les ressources que tu réutilises d'un niveau à l'autre. Un niveau ne renvoie jamais à une collection : l'import copie la ressource à l'intérieur, et le niveau se joue partout

## Ce qu'est une collection

**Une collection** est un dossier de ressources réutilisables. Elle peut contenir des ressources de sept types :

| Type | Comment il est stocké |
|---|---|
| prefabs, thèmes, formes, effets | des données, un fichier par entrée |
| textures, polices, audio | des fichiers multimédias |

Une collection n'est pas liée à un niveau. Elle se trouve sur ton appareil et est disponible dans n'importe quel niveau que tu ouvres

## Sources

La bibliothèque montre des ressources de trois sources. Chacune est une pastille de filtre au-dessus de la liste :

| Pastille | Ce que c'est | Modifiable |
|---|---|---|
| `{{ui:editor_library-source_library}}` | la bibliothèque de l'appareil : `resources/prefabs`, `themes`, `shapes`, `effects` | oui |
| `{{ui:editor_library-source_local}}` | tes propres collections, `resources/collections` | oui |
| `{{ui:editor_library-source_workshop}}` | les collections que tu suis par un abonnement dans le Steam Workshop, lues sur place. Versions Steam seulement | non |

Une collection en lecture seule se modifie ainsi : ses entrées sont copiées dans une de tes collections

## L'onglet "Bibliothèque"

`{{ui:settings_editor-settings_library}}` est le dernier onglet de l'écran d'accueil de l'éditeur, après `{{ui:settings_editor-settings_community}}`

Une étroite colonne de boutons choisit le type :
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`, `{{ui:editor_library_kind-themes}}`, `{{ui:editor_library_kind-shapes}}`, `{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`, `{{ui:editor_library_kind-fonts}}`, `{{ui:field_common_audio}}`

À sa droite, le titre de la page (à gauche) et ses boutons (à droite) se tiennent sur une seule rangée. La liste est en dessous.
Une liste vide le dit en son milieu

Sur les pages des sept types, de `{{ui:editor_library_kind-prefabs}}` à `{{ui:field_common_audio}}`, `{{ui:editor_library_copy-target}}` occupe une rangée à part, sur toute la largeur, sous le titre. Les pastilles des sources se tiennent dans la rangée en dessous

Une fenêtre de la bibliothèque (la fiche d'une collection, l'image d'une texture, la fenêtre de partage) se ferme avec la croix dans son coin. Il n'y a pas de bouton `{{ui:editor_library_close}}`

Chaque ligne est un bouton. Appuyer dessus fait l'action principale de son type :

| Type | Appui sur une ligne |
|---|---|
| collection | ouvre sa page |
| thème, forme, effet | ouvre l'éditeur |
| texture | montre l'image et sa taille |
| prefab, police, audio | rien. Une ligne audio a son propre bouton de lecture |

Les petits boutons à droite d'une ligne sont les autres actions, et l'icône de corbeille supprime ou retire

`{{ui:editor_library_open-folder}}` montre le dossier de la page actuelle dans le gestionnaire de fichiers du système. Disponible seulement sur Windows, macOS et Linux

### Collections

`{{ui:editor_library_open-folder}}` et `{{ui:editor_library_refresh}}` se tiennent à droite du titre de la page. `Nouvelle collection` et `{{ui:editor_library_import-archive}}` sont dans une rangée à part en dessous, alignés à droite

- `Nouvelle collection` crée une collection vide et ouvre sa fiche
- `{{ui:editor_library_import-archive}}` ajoute une collection depuis un fichier `.zip` ou `.tar.gz`, ou depuis une archive protégée par mot de passe : un `.zip` avec son propre mot de passe, `.zip.gpg` ou `.tar.gz.gpg`. Si cette collection est déjà sur l'appareil, le jeu demande s'il faut la remplacer

Une archive protégée par mot de passe ouvre la fenêtre `{{ui:editor_library_passphrase-title}}` : `{{ui:editor_library_passphrase-needed}}`. Saisis le mot de passe et appuie sur `{{ui:editor_library_open}}`.
Un mauvais mot de passe affiche `{{ui:editor_library_passphrase-wrong}}`
- `{{ui:editor_library_open-folder}}` ouvre `resources/collections`
- `{{ui:editor_library_refresh}}` relit les dossiers

Tes propres collections ont `{{ui:editor_library_edit}}` et l'icône de corbeille. La corbeille demande d'abord, puis supprime la collection avec tous ses fichiers

### Fiche d'une collection

`{{ui:editor_library_edit}}` ouvre une fenêtre avec la fiche de la collection :
- `{{ui:editor_library_field-name}}`, `{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`, séparés par des virgules
- `{{ui:editor_library_field-license}}` : `{{ui:editor_library_license-unspecified}}` ou l'une des licences courantes
- `{{ui:editor_library_set-cover}}` choisit une image png. La ligne à côté indique s'il y a une couverture

`{{ui:editor_save_text}}` écrit la fiche. `{{ui:editor_cancel_text}}`, la croix ou un clic hors de la fenêtre abandonne les changements

### Page d'une collection

| Élément | Ce qu'il fait |
|---|---|
| `{{ui:settings_common_back}}` | revient à la liste |
| `{{ui:editor_library_edit}}` | ouvre la fiche. Seulement pour tes propres collections |
| `{{ui:editor_share_share}}` | ouvre la fenêtre de partage : `{{ui:editor_share_archive}}` en `.zip` ou `.tar.gz`, avec ou sans mot de passe, et dans la version Steam aussi `{{ui:editor_share_steam}}` pour une de tes collections |
| `{{ui:editor_library_open-folder}}` | ouvre le dossier propre à la collection |
| `{{ui:editor_library_delete}}` | supprime la collection, en demandant d'abord |

En dessous se trouve le contenu. Une ligne ouvre l'entrée de la même façon que la page de son type, et l'icône de corbeille retire l'entrée de la collection

Une collection en lecture seule affiche `{{ui:editor_library_read-only}}`

Plus sur `{{ui:editor_share_share}}` - [[17_publishing]]

### Prefabs, thèmes, formes, effets

Chacune de ces pages montre chaque entrée de chaque source. Les pastilles restreignent la liste

`{{ui:editor_library_copy-target}}` choisit une de tes collections. Par défaut, c'est `{{ui:editor_library_copy-target-none}}`. Une fois une cible choisie, chaque ligne venue d'ailleurs reçoit `{{ui:editor_library_copy-to}}`

Un thème, une forme ou un effet s'ouvre dans le même éditeur que dans les paramètres du niveau. `{{ui:editor_save_text}}` écrit la modification là où vit l'entrée : dans `{{ui:editor_library-source_library}}` ou dans ta collection.
Une entrée du Workshop s'ouvre en lecture seule, et `{{ui:editor_save_text}}` est désactivé. Pour la modifier, copie-la dans une de tes collections

`{{ui:editor_library_new-entry}}` crée un nouveau thème, une nouvelle forme ou un nouvel effet dans l'éditeur. L'entrée est enregistrée dans la collection cible, ou dans `{{ui:editor_library-source_library}}` si aucune cible n'est choisie. Les prefabs se créent dans un niveau, et ils n'ont pas de `{{ui:editor_library_new-entry}}`

Les entrées que tu peux modifier ont l'icône de corbeille, et elle demande d'abord

Chaque ligne a `{{ui:editor_share_share}}`. Le bouton emballe l'entrée avec tout ce dont elle a besoin (par exemple les formes, les textures et les prefabs imbriqués d'un prefab) dans un `.zip` ou un `.tar.gz`, avec ou sans mot de passe, sous forme de collection d'une seule entrée. Le destinataire importe ce fichier par `{{ui:editor_library_import-archive}}`, comme n'importe quelle collection

`{{ui:editor_library_open-folder}}` ouvre le dossier de la bibliothèque de l'appareil pour ce type, par exemple `resources/themes`

### Textures, polices, audio

Ces pages montrent les fichiers de toutes les collections. Il n'y a pas de bibliothèque personnelle pour les fichiers, donc ces types ne vivent que dans des collections

- une ligne de texture montre l'image
- une ligne audio a un bouton de lecture. Une seule piste joue à la fois, et elle s'arrête quand tu quittes la page
- une ligne de police n'a pas d'aperçu

`{{ui:editor_library_add-file}}` place un fichier de l'appareil dans la collection cible, donc sans cible le bouton est désactivé. Une texture est en png ou jpg, une police en ttf ou otf, l'audio en mp3, wav ou ogg.
Si la collection a déjà un fichier avec les mêmes octets, rien n'est ajouté, et le jeu le dit

Les lignes ont `{{ui:editor_library_copy-to}}` et l'icône de corbeille

### Ce qu'une copie emporte

Une copie emporte tout ce dont l'entrée a besoin : les formes, les textures, les polices et les prefabs imbriqués d'un prefab, la forme des particules d'un effet.
Les informations d'auteur de ces ressources les accompagnent aussi

## L'onglet "Collections"

`{{ui:editor_library_kind-collections}}` est un onglet des paramètres du niveau, juste après `{{ui:editor_library_kind-prefabs}}`. En haut, il y a deux modes : `Importer` et `{{ui:editor_collections_mode-build}}`

### Import

1. L'onglet montre une liste de collections. Appuie sur celle qu'il te faut
2. Coche les entrées qu'il te faut. `{{ui:editor_collections_select-all}}` et `{{ui:editor_collections_select-none}}` cochent tout ou décochent tout
3. La ligne `Selected: N, dependencies added: M` montre ce qui entrera dans le niveau. Les dépendances s'ajoutent d'elles-mêmes
4. Appuie sur `Importer`

Tout l'import est une seule étape d'annulation

Les textures, les polices et l'audio reçoivent de nouveaux ID dans le niveau, et leurs fichiers sont copiés dans le dossier du niveau sous un nom unique.
Un fichier que le niveau possède déjà octet pour octet n'est pas copié une seconde fois : l'import prend la texture, la police ou la piste propre au niveau

### Construire une collection

1. `{{ui:editor_collections_target}}` choisit `Une nouvelle collection` ou une des tiennes. Une nouvelle prend son nom dans le champ `{{ui:editor_library_field-name}}`
2. Coche les ressources du niveau, de n'importe lequel des sept types
3. Appuie sur `{{ui:editor_collections_build}}`

Une nouvelle collection reçoit les auteurs du niveau

Une collection ne peut pas être construite à partir d'un niveau protégé. Plus - [[13_export-and-protection]]

## Choix des ressources et recherche

La recherche et les fenêtres de choix de ressources ont un niveau `{{ui:settings_editor-settings_library}}` pour les prefabs, les thèmes, les formes et les effets. Il montre toutes les sources.
Les fenêtres de choix sont les champs de forme, de collider, d'effet et de thème, ainsi que `{{ui:cmd_editor_place-prefab}}`

Choisir une entrée de la bibliothèque l'importe dans le niveau avec ses dépendances et l'assigne. Un conflit pose la même question que dans l'onglet "Collections"

Les navigateurs de bibliothèque dans les onglets de ressources du niveau fonctionnent de la même façon et montrent les pastilles des sources. Plus - [[11_level-resources]]

## Conflits

Une entrée importée peut déjà être dans le niveau avec le même ID :
- même contenu - rien à faire
- contenu différent - la fenêtre `{{ui:editor_resource-conflict_title}}` s'ouvre

La fenêtre liste chaque conflit, chacun avec un interrupteur `{{ui:editor_resource-conflict_copy}}` :

| Choix | Résultat |
|---|---|
| garder (interrupteur désactivé) | la version du niveau reste et est utilisée |
| `{{ui:editor_resource-conflict_copy}}` | la version de la collection est ajoutée sous un nouvel ID. Tout ce qui est importé avec elle renvoie à la copie |

`{{ui:editor_resource-conflict_all-keep}}` et `{{ui:editor_resource-conflict_all-copy}}` règlent tous les interrupteurs d'un coup. `Importer` applique le choix, `{{ui:editor_cancel_text}}` n'importe rien

Aucune version ne l'emporte en silence. Chaque conflit avec un contenu différent se tranche dans cette fenêtre

## Paternité

Les fiches sur les ressources d'un niveau couvrent les thèmes, les effets, les formes et les prefabs, ainsi que les textures, les polices et l'audio.
L'import copie les fiches nécessaires dans le niveau, donc la paternité arrive avec la ressource

Plus - [[4_resource-record]]

## Sur le disque

Les collections vivent dans `resources/collections/<collection-guid>/` dans le dossier de données du jeu. C'est le même dossier `resources` à côté de `levels` où vit la bibliothèque de l'appareil. Plus - [[4_level-folder-and-backups]]

| Chemin | Ce qu'il contient |
|---|---|
| `collection.json` ou `collection.blob` | le manifeste : nom, description, auteurs, licence, les entrées de textures, de polices et d'audio, et les informations d'auteur de tout ce qui est à l'intérieur |
| `cover.png` | la couverture, facultative |
| `prefabs/`, `themes/`, `shapes/`, `effects/` | un `<guid>.json` ou `<guid>.blob` par entrée, les mêmes fichiers que dans la bibliothèque de l'appareil |
| `media/` | les fichiers de textures, de polices et d'audio |

Une collection se transmet sous forme d'archive : `{{ui:editor_share_share}}` sur sa page, `{{ui:editor_library_import-archive}}` dans la liste.
Une archive qui n'est pas une collection est refusée

À lire ensuite : [[17_publishing]], [[2_reuse]], [[4_resource-record]]
