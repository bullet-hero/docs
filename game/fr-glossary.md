# French term base

The terms `fr.yaml` (standard French) is translated with. Every value in `fr.yaml` follows this table: a thing is
named the same way on every screen, in every hint, in every tooltip.

- **`strict`** rows are checked by the game's tests: whenever the English value of a key contains the `en` term (a
  whole word, any case, tags ignored, a plural `s`/`es` included), its French value must contain the `fr` term.
- The check is a plain substring match, accents included, so a `strict` cell is the part every form of the term
  shares: `niveau` covers `niveaux`. Where the plural moves a word (`images clés`) or the noun and the verb part ways
  (`aimantation`, `aimanter`, `ancrage`, `ancré`), the cell is the shared part and the note gives the full term. Where
  no such part is a word anyone would recognise, the row is `loose`.
- **`loose`** rows are guidance: a common word whose best translation depends on the sentence around it. Follow them
  unless the sentence reads wrong, and never use a `loose` row's `fr` for a different concept.
- A row whose `fr` is the same Latin text as `en` means "keep it in Latin" - product names, formats, keys.
- Loanwords follow the French Unity editor and the French-speaking rhythm-game communities (osu!, Geometry Dash): a
  French word where they use one (`calque`, `image clé`, `piste`), the English word where they keep it (`prefab`,
  `gizmo`, `checkpoint`, `hitbox`, `timeline`).
- One file for France, Belgium, Switzerland and Canada: `tu`, a button is an infinitive, sentence case, and the
  vocabulary of French software (`fichier`, `paramètres`, `enregistrer`, `souris`, `écran`).
- The French cells and notes follow French typography: a no-break space (U+00A0) before `? ! :`, the straight `'`,
  straight quotes.

The canonical meanings are the [glossary](../en/docs/2_editor/7_reference/1_glossary.md). To propose a change, open an
issue or a pull request that edits this table and every `fr.yaml` value that uses the term, in one change.

Punctuation, labels and the rest of the house style for French: `Assets/Addressables/TEXT-STYLE.md`, section 14, in
the game's repository.

| en | fr | kind | note |
|---|---|---|---|
| Level | niveau | strict | Tout ce qui forme une partie : objets, audio, événements et ressources propres. Le "level" du son est autre chose : "volume" ou "niveau du signal" |
| Object | objet | strict | Ce que l'auteur crée sur la timeline, avec son propre intervalle, sa transformation et son parent |
| Rect | objet vide | loose | Objet qui ne dessine rien : seulement transformation, intervalle et enfants. Comme en ru, deux mots : le type est "objet vide", la forme géométrique est "rectangle" |
| Shape | forme | loose | Géométrie réelle que dessine un objet, pas une texture. Le jeu en génère environ 500 lui-même |
| Collider | collider | strict | Ce contre quoi un objet entre en collision. Peut différer de ce qu'il dessine. En anglais, comme dans la documentation française d'Unity. Masculin, pluriel "colliders" |
| Prefab | prefab | strict | Modèle réutilisable d'objets, placé dans un niveau autant de fois que nécessaire. En anglais, comme dans Unity. Masculin, pluriel "prefabs" |
| Prefab Mode | mode prefab | strict | Modifier le contenu propre d'un modèle au lieu du niveau qui l'entoure |
| Effect | effet | loose | Objet qui crée ses propres objets à chaque image à partir de quelques paramètres. Bloom, Vignette, etc. sont des "effets de post-traitement", jamais "effet" tout court |
| Inframe Object | objet d'image | loose | Objet créé par un effet. Le moteur le gère : on ne peut ni le sélectionner ni le modifier |
| Theme | thème | strict | Palette à laquelle le niveau renvoie par index : recolorer est une modification, pas cent. Une chanson n'est jamais un "thème" ici, c'est un "morceau" |
| Frame | image | strict | Unité de temps du niveau, comme dans "images par seconde". L'image est une cellule, le temps est la limite entre deux cellules. Jamais "cadre" ni "trame". Une image au sens d'illustration se dit plutôt "texture" ou "illustration", pour ne pas brouiller le terme |
| Keyframe | clé | strict | Terme complet "image clé", pluriel "images clés" : la cellule est "clé" parce que les deux formes la partagent et parce qu'elle distingue Keyframe de Frame. Valeur fixée par l'auteur à une image, interpolée entre deux |
| Key | image clé | loose | Abréviation de keyframe : "image clé". La touche du clavier est "touche", la clé de localisation est "clé" |
| Track | piste | strict | Rangée d'images clés d'une propriété animable : position, rotation, volume. Audio Track est "piste audio" |
| Timeline | timeline | strict | En anglais, comme la fenêtre Timeline d'Unity en français et les logiciels de montage. Féminin, "la timeline", pluriel "timelines", que la cellule couvre. Axe d'images sur lequel on édite le niveau, un onglet par type de contenu. Ni "chronologie" ni "ligne de temps", qui ferait entrer "temps" en collision avec Beat |
| Span | intervalle | loose | Quand un objet existe : image de début et durée, pas image de fin. Masculin. Le verbe span ("couvrir") ne se traduit pas par "intervalle" |
| Playhead | tête de lecture | strict | L'image affichée en ce moment. Comme dans les logiciels audio et vidéo en français |
| Ease | lissage | strict | Comment la valeur passe de l'image clé précédente à celle-ci. Ce n'est ni Curve ("courbe") ni l'antialiasing |
| Marker | marqueur | strict | Point nommé sur la règle du niveau, pour revenir à l'endroit exact |
| Checkpoint | checkpoint | strict | Là où une mort ramène le joueur. En anglais, comme dans la communauté de Geometry Dash et comme en ru, qui garde aussi l'emprunt. Pluriel "checkpoints" |
| Anchor | ancr | strict | Bord qui suit le bord du parent : si le parent rétrécit, l'enfant bouge avec lui. La cellule est la racine "ancr", que partagent "ancre", "ancrage", "ancré" et "ancrer" |
| Layer | calque | strict | Ordre de dessin relatif au parent : le calque de l'enfant s'ajoute à celui du parent. Comme dans Unity en français |
| Pivot | pivot | loose | Point autour duquel l'objet tourne et se met à l'échelle, dans son propre rectangle |
| Gizmo | gizmo | strict | Poignées de glissement dessinées sur l'objet sélectionné dans la vue. En anglais, comme dans Unity |
| Snapping | aimant | strict | Terme complet "aimantation". Attirer un glissement vers quelque chose : vers le contenu avec l'aimant, vers la musique avec l'interrupteur de pulsation. La cellule est "aimant", que partagent "aimant", "aimantation" et "aimanter" |
| Snap | aimant | strict | Comme Snapping : le verbe est "aimanter", "s'aimanter". Fit est "ajuster", jamais "aimanter" |
| Beat | pulsation | strict | La grille propre à la musique : l'auteur la fixe et rien ne la lit pendant le jeu. Pas "temps", qui se confond avec le temps du niveau, ni "battement" |
| Beat Segment | segment | strict | Terme complet "segment de pulsation". Partie à tempo constant avec son propre tempo, sa phase et sa longueur de mesure. Pas "intervalle", qui est Span |
| BPM | BPM | strict | Pulsations par minute. En latin, comme dans les communautés de jeux de rythme |
| Tap | appui | loose | Un appui pour marquer le tempo. Sur l'écran tactile aussi "appui" |
| Generator | générateur | strict | Automatisation de la création : produit du contenu du niveau à partir de quelques paramètres |
| Modifier | modificateur | strict | Générateur qui modifie ou supprime ce qui existe déjà au lieu d'ajouter. La touche du clavier est Modifier Key |
| Seed | graine | strict | Le nombre d'où vient chaque valeur aléatoire du niveau : la même graine reproduit exactement la même chose. Comme dans Minecraft en français |
| Raw Data | données brutes | strict | Tout le modèle enregistré sous forme d'arbre modifiable. Rien n'y est validé, exprès |
| Recommendation | Recommandation | strict | Une des cinq étiquettes : `<b>Recommandation :</b>`, espace insécable avant les deux-points, et la phrase qui suit commence par une minuscule |
| Tip | Conseil | strict | Une des cinq étiquettes : `<b>Conseil :</b>`, espace insécable avant les deux-points, et la phrase qui suit commence par une minuscule |
| Worth knowing | Bon à savoir | strict | Une des cinq étiquettes : `<b>Bon à savoir :</b>`, espace insécable avant les deux-points, et la phrase qui suit commence par une minuscule |
| Warning | Avertissement | strict | Une des cinq étiquettes : `<b>Avertissement :</b>`, espace insécable avant les deux-points, et la phrase qui suit commence par une minuscule |
| Caution | Attention | strict | Une des cinq étiquettes : `<b>Attention :</b>`, espace insécable avant les deux-points, et la phrase qui suit commence par une minuscule. Hors étiquette, "caution" devient aussi "attention" ("avec attention"), jamais "prudence" |
| More | Plus | loose | La dernière ligne de liens d'une aide, `More:`, devient `Plus :` |
| Bullet Hero | Bullet Hero | strict | Nom du produit. Ne se traduit pas |
| Steam | Steam | loose |  |
| JSON | JSON | strict | Nom de format. Ne se traduit pas |
| MSAA | MSAA | strict | Sigle technique. Ne se traduit pas |
| FXAA | FXAA | strict | Sigle technique. Ne se traduit pas |
| HDR | HDR | loose |  |
| VFX | VFX | loose |  |
| URL | URL | loose |  |
| Ctrl | Ctrl | loose | Les touches restent en latin |
| Shift | Shift | loose | En latin, pas "Maj" |
| Enter | Enter | loose | En latin, pas "Entrée" |
| Hierarchy | hiérarchie | strict | Panneau de l'éditeur qui liste les objets par relation parent-enfant. Comme la fenêtre Hiérarchie d'Unity |
| Inspector | inspecteur | strict | Panneau de l'éditeur avec les propriétés de la sélection. Comme dans Unity |
| Viewport | vue | strict | Zone de l'éditeur qui montre l'écran du niveau. La catégorie de commandes View est "Affichage", pas "Vue", et Preview est "aperçu" |
| Command Palette | palette de commandes | strict | Fenêtre qui cherche et exécute une commande par son nom. Comme dans VS Code en français |
| Command | commande | loose |  |
| Selection | sélection | loose |  |
| Select | sélectionner | loose |  |
| Marquee | sélection rectangulaire | strict | Sélectionner en faisant glisser un rectangle |
| Apply | appliquer | loose |  |
| Reset | réinitialiser | loose |  |
| Cancel | annuler | loose | Comme dans toute interface en français, le même verbe que Undo |
| Confirm | confirmer | loose |  |
| OK | OK | loose | Le bouton OK reste "OK" dans une interface en français |
| Save | enregistrer | loose | "enregistrer", jamais "sauvegarder" : la sauvegarde est Backup |
| Load | charger | loose |  |
| Open | ouvrir | loose |  |
| Close | fermer | loose |  |
| Exit | quitter | loose |  |
| Create | créer | loose |  |
| Add | ajouter | loose |  |
| Remove | retirer | loose | Distinct de Delete ("supprimer") : Remove sort quelque chose d'une liste, Delete l'efface |
| Delete | supprimer | loose |  |
| Duplicate | dupliquer | loose |  |
| Copy | copier | loose |  |
| Paste | coller | loose |  |
| Cut | couper | loose |  |
| Undo | annuler | loose | Comme dans toute interface en français |
| Redo | rétablir | loose |  |
| History | historique | loose | Distinct de Story ("histoire") |
| Edit | modifier | loose | Comme catégorie de menu, "Édition" |
| Rename | renommer | loose |  |
| Move | déplacer | loose |  |
| Import | importer | loose |  |
| Export | exporter | loose |  |
| Archive | archive | loose | Conteneur portable d'un niveau ou d'une collection. Jamais "fichier" tout court, qui est File |
| Folder | dossier | loose |  |
| File | fichier | loose | "fichier", jamais "document" |
| Search | rechercher | loose | Comme nom, "recherche" |
| Filter | filtrer | loose | Comme nom, "filtre" |
| Refresh | actualiser | loose |  |
| Toggle | basculer | loose | Un interrupteur afficher/masquer peut dire "Afficher/masquer" |
| Show | afficher | loose |  |
| Hide | masquer | loose |  |
| Hidden | masqué | loose |  |
| Visible | visible | loose |  |
| Enabled | activé | loose |  |
| Disabled | désactivé | loose |  |
| On | activé | loose | État d'un interrupteur |
| Off | désactivé | loose |  |
| None | aucun | loose | S'accorde avec le nom auquel il renvoie ("aucune" pour une forme) |
| Auto | automatique | loose |  |
| Custom | personnalisé | loose |  |
| Default | par défaut | loose |  |
| All | tout | loose |  |
| Nothing | rien | loose |  |
| Current | actuel | loose |  |
| Active | actif | loose |  |
| Global | global | loose |  |
| Local | local | loose |  |
| Parent | parent | loose |  |
| Child | enfant | loose |  |
| Root | racine | loose |  |
| Fold | replier | loose |  |
| Unfold | déplier | loose |  |
| Flatten | aplatir | loose |  |
| Transform | transformation | loose |  |
| Position | position | loose |  |
| Rotation | rotation | loose |  |
| Scale | échelle | loose |  |
| Size | taille | loose |  |
| Offset | décalage | loose |  |
| Angle | angle | loose |  |
| Radius | rayon | loose |  |
| Width | largeur | loose |  |
| Height | hauteur | loose |  |
| Min | min | loose |  |
| Max | max | loose |  |
| Step | pas | loose |  |
| Random | aléatoire | loose |  |
| Rnd | aléat. | loose | Abréviation de "aléatoire" dans les étiquettes courtes |
| From | de | loose |  |
| To | à | loose |  |
| Value | valeur | loose |  |
| Type | type | loose |  |
| Name | nom | loose |  |
| Mode | mode | loose |  |
| Count | nombre | loose |  |
| Speed | vitesse | loose |  |
| Velocity | vitesse | loose |  |
| Gravity | gravité | loose |  |
| Particle | particule | loose |  |
| Orbital | orbital | loose |  |
| Lifetime | durée de vie | loose |  |
| Color | couleur | loose |  |
| Alpha | alpha | loose |  |
| Opacity | opacité | loose |  |
| Opaque | opaque | loose |  |
| Transparent | transparent | loose |  |
| Gradient | dégradé | loose |  |
| Texture | texture | loose |  |
| Font | police | loose |  |
| Text | texte | loose |  |
| Localized Text | texte localisé | loose |  |
| Language | langue | loose |  |
| Audio | audio | loose |  |
| Audio Track | piste audio | loose |  |
| Volume | volume | loose |  |
| Music | musique | loose |  |
| Sound | son | loose |  |
| Resource | ressource | loose |  |
| Resources | ressources | loose |  |
| Metadata | métadonnées | loose |  |
| Meta | méta | loose |  |
| License | licence | loose |  |
| Author | auteur | loose |  |
| Artist | artiste | loose |  |
| Settings | paramètres | loose | Jamais "réglages", que contient Preset ("préréglage") |
| Editor | éditeur | loose |  |
| Game | jeu | loose |  |
| Player | joueur | loose |  |
| Avatar | avatar | loose |  |
| Dash | dash | loose | En anglais, comme dans la communauté de Geometry Dash |
| Hitbox | hitbox | loose |  |
| Damage | dégâts | loose |  |
| Health | santé | loose |  |
| Death | mort | loose |  |
| Camera | caméra | loose |  |
| Zoom | zoom | loose |  |
| Pan | panoramique | loose |  |
| Shake | tremblement | loose |  |
| Grid | grille | loose |  |
| Ruler | règle | loose |  |
| Loop | boucle | loose |  |
| Play | lire | loose | Lire dans l'éditeur, c'est "lire", jouer le niveau, c'est "jouer" |
| Pause | mettre en pause | loose | Comme nom, "pause" |
| Stop | arrêter | loose |  |
| Preview | aperçu | loose |  |
| Render | rendu | loose |  |
| Post-processing | post-traitement | loose |  |
| Post | post-traitement | loose | Abréviation de post-processing |
| Bloom | bloom | loose |  |
| Vignette | vignette | loose |  |
| Chromatic Aberration | aberration chromatique | loose |  |
| Lens Distortion | distorsion de l'objectif | loose |  |
| Film Grain | grain de film | loose |  |
| Grain | grain | loose |  |
| Motion Blur | flou de mouvement | loose |  |
| Blur | flou | loose |  |
| Color Curves | courbes de couleur | loose |  |
| Curve | courbe | loose | Ce n'est pas Ease ("lissage") |
| Lift Gamma Gain | Lift/Gamma/Gain | loose | Commandes de la correction colorimétrique, en anglais |
| Shadows Midtones Highlights | ombres/tons moyens/hautes lumières | loose |  |
| White Balance | balance des blancs | loose |  |
| Analog Glitch | glitch analogique | loose |  |
| Digital Glitch | glitch numérique | loose |  |
| Glitch | glitch | loose |  |
| Gamma | gamma | loose |  |
| Background | arrière-plan | loose |  |
| Framerate | images par seconde | loose | Ou "fréquence d'images" là où la place manque pour une unité |
| Fixed Framerate | fréquence fixe de simulation | loose | Comme en ru, deux sens : dans les paramètres, la fréquence de mise à jour de la simulation, ailleurs, "fréquence d'images fixe" |
| Collision | collision | loose |  |
| Screen Limit | limite de l'écran | loose |  |
| Cursor | curseur | loose |  |
| Control | contrôle | loose |  |
| Controls | contrôles | loose | Pas "commandes", qui est Command |
| Keybinding | attribution des touches | loose |  |
| Shortcut | raccourci | loose |  |
| Button | bouton | loose |  |
| Interface | interface | loose |  |
| Screen | écran | loose |  |
| Window | fenêtre | loose |  |
| Panel | panneau | loose |  |
| Tab | onglet | loose |  |
| Menu | menu | loose |  |
| Tool | outil | loose |  |
| Library | bibliothèque | loose |  |
| Bot | bot | loose |  |
| Tutorial | tutoriel | loose |  |
| Sandbox | bac à sable | loose |  |
| Hint | aide | loose | Le texte d'aide d'un champ ou d'une fenêtre. Jamais "indice", ni "piste" (Track), ni "conseil" (Tip) |
| Glossary | glossaire | loose |  |
| Validation | validation | loose |  |
| Rules | règles | loose |  |
| Format | format | loose |  |
| Version | version | loose |  |
| Desktop | ordinateur | loose | La plateforme. Le bureau de Windows est "bureau" |
| Mobile | mobile | loose |  |
| Alignment | alignement | loose | Distinct de Placement ("placement") |
| Align | aligner | loose |  |
| Center | centre | loose |  |
| Left | gauche | loose |  |
| Right | droite | loose |  |
| Top | haut | loose |  |
| Bottom | bas | loose |  |
| Horizontal | horizontal | loose |  |
| Vertical | vertical | loose |  |
| Linear | linéaire | loose |  |
| Appearing | apparition | loose |  |
| Scissors | ciseaux | loose |  |
| Edges | bords | loose | Comme en ru, deux sens : l'outil qui déplace les bords d'un intervalle est "bords", les arêtes d'une forme sont "arêtes" |
| Point | point | loose |  |
| Continue | continuer | loose |  |
| Next | suivant | loose |  |
| Back | retour | loose |  |
| Loading | chargement | loose |  |
| Progress | progression | loose |  |
| Statistics | statistiques | loose |  |
| Preset | préréglage | loose |  |
| Clipboard | presse-papiers | loose |  |
| Console | console | loose |  |
| Ping | localiser | loose | Montrer quelque chose dans la vue, la timeline et la hiérarchie |
| Override | remplacement | loose |  |
| Placement | placement | loose |  |
| Template | modèle | loose |  |
| Clip | clip | loose |  |
| Slip | glisser le contenu | loose | Comme en ru : déplacer le contenu dans son intervalle sans déplacer l'intervalle |
| Slot | emplacement | loose |  |
| Beat Grid | grille de pulsations | loose |  |
| Bar | mesure | loose | En musique. La barre de progression est "barre" |
| Tempo | tempo | loose |  |
| Tap Tempo | tempo par appuis | loose |  |
| Stereo Pan | panoramique stéréo | loose |  |
| Font Size | taille de police | loose |  |
| Word Wrap | retour à la ligne automatique | loose |  |
| Backup | sauvegarde | loose | Jamais pour Save, qui est "enregistrer" |
| Branch | branche | loose |  |
| Fit | ajuster | loose | Jamais "aimanter", qui est Snap |
| Finding | problème | loose | Ce que la validation trouve dans un niveau |
| Fix | corriger | loose |  |
| Group | groupe | loose |  |
| Id | ID | loose |  |
| Mipmap | mipmap | loose |  |
| Sampling | échantillonnage | loose |  |
| Tiling | mosaïque | loose |  |
| Wrapping | hors des bords | loose | Ce qu'une texture montre au-delà de ses bords, comme en ru |
| Pixel art | pixel art | loose |  |
| Drawing | dessin | loose |  |
| Emission Shape | forme d'émission | loose |  |
| Over Lifetime | au cours de la vie | loose |  |
| Forces | forces | loose |  |
| Scatter | dispersion | loose |  |
| Spread | ouverture | loose |  |
| Tangent | tangente | loose |  |
| Clamp | limiter | loose |  |
| Ping Pong | aller-retour | loose |  |
| Temperature | température | loose |  |
| Tint | teinte | loose |  |
| Modifier Key | touche de modification | loose | Aucune valeur de en.yaml ne la nomme aujourd'hui. Si une la nomme, la règle strict de Modifier y exige "modificateur" |
| Dead Zone | zone morte | loose |  |
| Sensitivity | sensibilité | loose |  |
| Stick | stick | loose |  |
| Shoulder | bouton supérieur | loose |  |
| Gamepad | manette | loose |  |
| Touchscreen | écran tactile | loose |  |
| Motion Sensor | capteur de mouvement | loose |  |
| Handedness | main dominante | loose |  |
| Double Tap | double appui | loose |  |
| Workshop | Workshop | loose | Comme dans Steam en français |
| Story | histoire | loose |  |
| Wave | vague | loose |  |
| Immortal | immortel | loose | Qualifie un mode, jamais le joueur, pour ne pas accorder au genre |
| Dodge | esquive | loose |  |
| Zen | zen | loose |  |
| Clears | réussites | loose | Combien de fois un niveau a été terminé |
| Hits | impacts | loose |  |
| Profile | profil | loose |  |
| Frame Hierarchy | hiérarchie de l'image | loose | Suit Hierarchy ("hiérarchie") et Frame ("image"), tous deux strict |
| Stop Frame | image d'arrêt | loose |  |
| Runtime Seed | graine d'exécution | loose |  |
| Level Logo | couverture du niveau | loose | L'image affichée dans la liste des niveaux |
| Post-processing effect | effet de post-traitement | loose |  |
| Audio effect | effet audio | loose | "effet" tout court, c'est seulement l'objet Effect |
| Chorus | chorus | loose |  |
| Compressor | compresseur | loose |  |
| Distortion | distorsion | loose |  |
| Echo | écho | loose |  |
| Flange | flanger | loose |  |
| Highpass | passe-haut | loose |  |
| Lowpass | passe-bas | loose |  |
| Normalize | normaliser | loose |  |
| Param EQ | EQ paramétrique | loose |  |
| Pitch Shifter | changement de hauteur | loose |  |
| Reverb | réverbération | loose |  |
| Emitter | émetteur | loose |  |
| Variant | variante | loose |  |
| Fader | fader | loose |  |
| Signal level | niveau du signal | loose | Le "level" des aides des effets audio. LocalizationGlossaryTests l'exclut |
| Swatch | échantillon | loose |  |
| Device library | bibliothèque partagée de l'appareil | loose |  |
| Collection | collection | strict | Dossier de ressources réutilisables : prefabs, thèmes, formes, effets, textures, polices, audio. Rien à voir avec les collections de Steam. Strict, car "collections" contient "collection". La collection des règles de validation (une structure de données) n'a pas à être "collection", et LocalizationGlossaryTests exclut ces clés |
| Anti-aliasing | antialiasing | loose | En anglais, comme dans les paramètres graphiques des jeux en français. Jamais "lissage", qui est Ease |
| Overlay | superposition | loose |  |
| Scrub | balayage | loose |  |
| Gradient stop | point de couleur | loose |  |
| Link to a docs page | titre de la page | loose | Un lien vers la documentation porte le titre français de la page liée |
| Difficulty | Difficulté | loose | Niveaux de difficulté : les balles comme une météo, de quelques gouttes à l'effondrement. L'image compte, pas le mot littéral |
| Auto (difficulty) | Auto | loose |  |
| Drizzle (difficulty) | Bruine | loose |  |
| Rain (difficulty) | Pluie | loose |  |
| Downpour (difficulty) | Averse | loose |  |
| Hail (difficulty) | Grêle | loose |  |
| Barrage (difficulty) | Rafale | loose |  |
| Onslaught (difficulty) | Assaut | loose |  |
| Deluge (difficulty) | Déluge | loose |  |
| Inferno (difficulty) | Enfer | loose |  |
| Singularity (difficulty) | Singularité | loose |  |
