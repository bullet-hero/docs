---
title: Politique de confidentialité du jeu
date: 2026-10-17
tags: [legal]
---

# Politique de confidentialité du jeu

Le développeur de Bullet Hero ne collecte, ne reçoit, ne vend et ne partage aucune donnée personnelle. Le jeu n'a ni comptes qui lui soient propres, ni publicité, ni analyse d'audience, ni rapports de plantage, ni pistage, ni identifiant publicitaire. Tout ce que le jeu retient de toi reste sur ton propre appareil, sauf ce que tu laisses une boutique conserver pour toi sous ton propre compte auprès de cette boutique

Les choses suivantes peuvent quitter ton appareil, et aucune d'elles ne va au développeur 

- un niveau que tu ouvres peut faire référence à un fichier hébergé sur un site web tiers, et son chargement contacte ce site ([[game-privacy-policy#Accès au réseau]])
- un niveau ou un fichier de profil que tu partages délibérément avec quelqu'un d'autre va là où tu l'envoies ([[game-privacy-policy#Les niveaux que tu partages]])
- dans les builds Steam, le jeu communique avec le Steam Workshop par l'intermédiaire du client Steam ([[game-privacy-policy#Steam Workshop]])
- dans les builds Steam, le jeu conserve une copie de tes données enregistrées dans Steam Cloud et signale tes succès à Steam ([[game-privacy-policy#Steam Cloud et succès]])
- dans les builds Steam, le jeu affiche ton activité en cours sur Discord par l'intermédiaire du client Discord ([[game-privacy-policy#Discord Rich Presence]])
- dans le build Google Play, le jeu signale tes succès à Google Play Jeux et s'adresse à Google Play pour les mises à jour et les évaluations ([[game-privacy-policy#Google Play]])
- dans le build RuStore, le jeu s'adresse à l'application RuStore pour les mises à jour et les évaluations ([[game-privacy-policy#RuStore]])
- sur un ordinateur, un programme d'IA que tu connectes à l'éditeur de niveaux voit le niveau que tu as ouvert ([[game-privacy-policy#Assistant IA dans l'éditeur]])

| | |
|---|---|
| Date d'entrée en vigueur | 17 octobre 2026 |
| Version de la politique | 1.4 |
| Application | Bullet Hero  `com.vertoker.BulletHero` sur Android, `com.vertoker.Bullet-Hero` sur iOS, et les builds pour ordinateur sous Windows, Linux et macOS |
| Développeur | vertoker, développeur individuel |
| Contact | [kostyachurakov@gmail.com](mailto:kostyachurakov@gmail.com) |

Cette politique couvre uniquement le jeu. Le site web a sa propre politique - [[privacy-policy]]. Le serveur aura lui aussi sa propre politique, rédigée quand le serveur existera

## À qui cette politique s'applique

Cette politique couvre chaque build de Bullet Hero, sur chaque plateforme et dans chaque boutique par laquelle il est distribué, ainsi que chaque version du jeu à laquelle aucune politique plus récente n'est rattachée

Lorsqu'une boutique (Google Play, l'App Store, Steam, RuStore, VK Play ou toute autre) collecte ses propres données sur ton achat, ton installation ou ton utilisation de l'application, cette collecte est régie par la politique de confidentialité de cette boutique et non par la présente. Le développeur ne reçoit de ces boutiques que ce qu'elles choisissent de montrer à tout développeur  des statistiques agrégées et anonymes sur les installations, les plantages et les succès, qui ne permettent pas de remonter jusqu'à un joueur en particulier

## Ce qui est stocké sur ton appareil

Le jeu écrit les éléments suivants dans son propre stockage d'application et les relit au lancement suivant 

- **Paramètres**  préférences de graphismes, d'audio, de contrôles, d'attribution des touches, d'interface et de langue
- **Progression et statistiques**  tentatives, meilleurs résultats, morts, temps de jeu et données similaires, à la fois pour l'ensemble de l'appareil et par niveau
- **Succès**  les succès que tu as débloqués et à quel moment
- **Niveaux**  les niveaux que tu crées, importes ou télécharges, y compris leur audio, leurs images et leurs autres médias, ainsi que leurs sauvegardes automatiques et, si tu utilises l'assistant IA, ses notes dans le dossier `ai` du niveau
- **Skins de l'avatar**  les skins que tu crées ou importes, et celle que tu portes
- **Profil de performances de l'appareil**  si tu lances le test de charge, ses mesures de temps ainsi que le modèle de l'appareil, le nom de la puce graphique et la taille de l'écran. Il sert uniquement à évaluer à quel point un niveau est lourd sur cet appareil et ne quitte jamais l'appareil  ni un transfert de profil ni Steam Cloud ne l'emportent
- **État local**  les paramètres de l'assistant IA de l'éditeur, l'état de la dernière synchronisation Steam Cloud et, sur Android, le moment où le jeu t'a demandé pour la dernière fois de le noter
- **Journaux de diagnostic**  le fichier journal propre au moteur, écrit localement pour qu'un problème puisse être examiné sur l'appareil où il s'est produit

Rien de tout cela n'est envoyé au développeur, et rien de tout cela n'est sauvegardé sur un service exploité par le développeur. Seul Steam Cloud, dans les builds Steam, en conserve une copie sous ton compte Steam ([[game-privacy-policy#Steam Cloud et succès]]). L'emplacement dépend de la plateforme 

- **Android et iOS**  le stockage privé du jeu. Les autres applications ne peuvent pas le lire, et il est supprimé avec le jeu quand tu le désinstalles
- **Windows, Linux et macOS**  le dossier des données d'application dans ton profil utilisateur, l'emplacement standard du moteur. Les autres programmes qui s'exécutent sous ton compte peuvent le lire, comme n'importe lequel de tes fichiers, et il reste en place après la désinstallation du jeu jusqu'à ce que tu supprimes ce dossier. Le programme de désinstallation fourni avec les builds gratuits (`unins000`) ne supprime que les fichiers propres au jeu et laisse ce dossier intact

Le jeu propose aussi, dans `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}`, des commandes explicites pour supprimer les statistiques et les sauvegardes stockées sans désinstaller le jeu

Le jeu ne demande pas l'accès à tes contacts, photos, caméra, microphone, position, agenda, journal d'appels, liste des applications installées ni à aucune autre ressource sensible, et il ne demande aucune autorisation à l'exécution

## Accès au réseau

Bullet Hero n'a pas de serveur. Le développeur n'exploite aucun service auquel le jeu se connecte, et ne reçoit donc aucune donnée de sa part

Un niveau est un dossier de fichiers, et son auteur peut faire pointer l'un de ces fichiers vers une adresse internet au lieu de l'inclure dans le dossier. Quand tu ouvres un tel niveau, le jeu télécharge ce fichier depuis le site web choisi par son auteur. Ce site voit alors ce que voit tout site web auquel on demande un fichier, notamment ton adresse IP et les détails techniques de la requête. Le développeur ne contrôle ni n'observe ces requêtes, et aucune trace n'en est conservée

En dehors de cela, le jeu n'effectue de requêtes réseau que par l'intermédiaire de la boutique ou de l'application avec laquelle il est fourni, et uniquement dans le build de cette boutique 

- les builds Steam  le Steam Workshop, Steam Cloud et les succès Steam par l'intermédiaire du client Steam, et Discord Rich Presence par l'intermédiaire du client Discord
- le build Google Play  les succès Google Play Jeux, la vérification des mises à jour et la demande d'évaluation par l'intermédiaire de Google Play sur le téléphone
- le build RuStore  la vérification des mises à jour et la demande d'évaluation par l'intermédiaire de l'application RuStore sur le téléphone

Aucun autre build n'effectue ces requêtes  le code propre à chaque boutique n'est compilé que dans le build de cette boutique. L'assistant IA de l'éditeur n'écoute que sur l'adresse de bouclage locale de l'ordinateur et ne peut pas être atteint depuis le réseau ([[game-privacy-policy#Assistant IA dans l'éditeur]])

## Steam Workshop

Les builds Steam utilisent le Steam Workshop par l'intermédiaire du client Steam qui tourne sur ton ordinateur. Les builds pour toutes les autres boutiques ne lancent jamais Steam  le code qui communique avec lui n'est compilé que dans les builds Steam

Le jeu demande à Steam à quels éléments du Workshop ton compte est abonné, afin de pouvoir les afficher comme niveaux et collections. C'est le client Steam qui les télécharge. Quand tu choisis de publier un niveau ou une collection, le jeu le remet au client Steam avec le titre, la description, l'image d'aperçu, les descripteurs de contenu et la visibilité que tu as définis, et Steam le stocke sur ses serveurs sous ton compte Steam. Un élément public peut être vu par n'importe qui sur Steam jusqu'à ce que tu l'en retires

Tout cela transite entre le client Steam et les serveurs de Valve et est régi par la politique de confidentialité de Steam et par l'Accord de souscription Steam. Le développeur n'en reçoit rien au-delà de ce que Steam montre à tout développeur au sujet d'un élément du Workshop

## Steam Cloud et succès

Dans les builds Steam, le jeu conserve une copie de tes paramètres, statistiques, succès, niveaux, bibliothèque et skins de l'avatar dans Steam Cloud, sous ton compte Steam. Il lit cette copie au lancement et y écrit les modifications pendant que tu joues et quand tu quittes le jeu, par l'intermédiaire du client Steam. Les paramètres de graphismes et de contrôles, les sauvegardes, les rapports d'erreur, les enregistrements vidéo, le profil de performances de l'appareil et l'état local de l'éditeur n'y vont jamais. Steam Cloud peut être désactivé pour le jeu dans ses propriétés sur Steam, et le jeu conserve alors tout uniquement sur cet ordinateur

Chaque succès que tu débloques est aussi signalé à Steam, qui l'affiche sur ton profil Steam selon tes paramètres de confidentialité Steam

Les deux sont stockés sur les serveurs de Valve et sont régis par la politique de confidentialité de Steam et par l'Accord de souscription Steam. Le développeur n'en reçoit rien au-delà de ce que Steam montre à tout développeur, comme la part des joueurs qui ont débloqué chaque succès

## Discord Rich Presence

Les builds Steam peuvent afficher dans ton profil Discord ce que tu fais dans le jeu  le menu, l'éditeur de niveaux, le bac à sable ou le niveau auquel tu joues, et depuis combien de temps. Un niveau n'est nommé, avec ses auteurs, que s'il est déjà public - un élément du Steam Workshop ou un niveau livré avec le jeu. Tout autre niveau apparaît seulement comme un niveau personnalisé, et le niveau que tu modifies n'est jamais nommé. Cela ne fonctionne que tant que l'application Discord tourne sur le même ordinateur. Les builds pour toutes les autres boutiques n'ont aucune intégration Discord  le code qui communique avec Discord n'est compilé que dans les builds Steam

Le jeu remet cette activité au client Discord sur ton appareil, jamais à un serveur qui lui serait propre. Le client Discord la publie ensuite sous ton compte Discord, et tes amis et tes serveurs Discord peuvent la voir. Le jeu ne se connecte pas à Discord, ne lit ni tes messages, ni tes serveurs, ni ta liste d'amis, et n'envoie rien en ton nom

Ce qu'il advient de cette activité du côté de Discord est régi par la [politique de confidentialité de Discord](https://discord.com/privacy). Le développeur n'en reçoit rien. Tu peux masquer ton activité à tout moment dans Discord  `User Settings` -> `Activity Privacy`

## Google Play

Le build Google Play utilise trois services de Google Play sur ton téléphone 

- **Google Play Jeux**  si ta session Google Play Jeux est ouverte, chaque succès que tu débloques y est aussi signalé, sous ton compte Google, et affiché dans ton profil Google Play Jeux. Le jeu demande seulement à Google Play Jeux si ta session est ouverte et quels succès sont déjà débloqués. Il ne lit ni ton nom, ni tes amis, ni quoi que ce soit d'autre de ton compte. L'ouverture de session est gérée par Google Play Jeux lui-même, et sans elle les succès restent uniquement dans le jeu
- **Mises à jour**  à l'ouverture du menu principal, le jeu demande à Google Play si une version plus récente est disponible, et Google Play la télécharge en arrière-plan
- **Évaluation**  après un niveau réussi, à partir du troisième et au plus une fois tous les 60 jours, le jeu demande à Google Play d'afficher sa fenêtre d'évaluation. L'apparition de la fenêtre, et ce que tu y écris, relèvent de Google Play  le jeu ne voit jamais ta note ni ton avis

Ce que Google fait de ces données est régi par les [règles de confidentialité de Google](https://policies.google.com/privacy). Le développeur n'en reçoit rien au-delà de ce que Google Play montre à tout développeur, comme les avis publiés et la part des joueurs qui ont débloqué chaque succès

## RuStore

Le build RuStore utilise l'application RuStore sur ton téléphone pour deux choses, et uniquement tant que cette application est installée 

- **Mises à jour**  à l'ouverture du menu principal, le jeu demande à RuStore si une version plus récente est disponible, et RuStore la télécharge en arrière-plan
- **Évaluation**  après un niveau réussi, à partir du troisième et au plus une fois tous les 60 jours, le jeu demande à RuStore d'afficher sa fenêtre d'évaluation. L'apparition de la fenêtre, et ce que tu y écris, relèvent de RuStore  le jeu ne voit jamais ta note ni ton avis

Ce que RuStore fait de ces données est régi par les documents propres à RuStore. Le développeur n'en reçoit rien au-delà de ce que RuStore montre à tout développeur

## Assistant IA dans l'éditeur

Sous Windows, Linux et macOS, l'éditeur de niveaux peut laisser un programme d'assistant IA modifier le niveau ouvert. Cette fonction reste désactivée tant que tu n'actives pas `{{ui:settings_game-editor_mcp-enabled}}` dans `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor_mcp_title}}`. Tant qu'elle est activée, le jeu n'écoute que sur l'adresse de bouclage locale de l'ordinateur, n'accepte qu'un seul programme à la fois et ne le laisse entrer qu'avec un jeton aléatoire écrit dans un fichier du stockage du jeu. Rien en dehors de cet ordinateur ne peut s'y connecter

Le programme que tu connectes relève de ton propre choix et ne fait pas partie du jeu. Il peut lire le niveau ouvert, ses ressources et sa musique, ainsi que des images de l'aire de jeu, et il peut les envoyer à quiconque exploite son modèle d'IA. Ce qu'il en advient là-bas est régi par les conditions et la politique de confidentialité propres à ce programme. Le développeur n'en reçoit rien

## Les niveaux que tu partages

Les niveaux sont portables par conception  un niveau peut être exporté sous forme de fichier d'archive ordinaire et envoyé à une autre personne par le moyen de ton choix. Ce fichier circule directement entre toi et le destinataire, ou par le service que tu utilises pour l'envoyer. Il ne passe pas par le développeur, et le développeur n'en garde aucune copie

Il en va de même pour les autres fichiers que le jeu peut écrire pour que tu les déplaces  un fichier de profil créé avec `{{ui:settings_profile-transfer_title}}`, qui contient tes niveaux, tes statistiques, tes paramètres, ta bibliothèque et tes skins de l'avatar, et une skin de l'avatar exportée seule

Un niveau que tu crées peut contenir ta propre musique, tes images et ton texte, et, si tu les y mets, ton nom ou ton pseudonyme. Tout ce que tu places dans un niveau est visible par toutes les personnes à qui tu donnes ce niveau. Décider de ce que tu y inclus ne relève que de toi. Si tu utilises l'assistant IA, les notes qu'il garde dans le dossier `ai` du niveau accompagnent les exports du niveau et ses publications sur le Workshop, sauf si `{{ui:settings_level-settings_metadata-level-ai-share}}` est décoché, et un export protégé par un mot de passe ne les emporte jamais

Un niveau peut, en option, être protégé par une phrase de passe. Cette phrase de passe sert à chiffrer le contenu du niveau sur ton appareil et n'est jamais écrite sur le disque, jamais journalisée et jamais transmise. Si tu la perds, ni le développeur ni personne d'autre ne peut récupérer le contenu du niveau

## Enfants

Le jeu ne collecte aucune donnée personnelle auprès de qui que ce soit, enfants compris. Il ne contient ni publicité, ni achats intégrés, ni chat, ni aucune autre fonction de communication, ni aucun mécanisme par lequel un enfant pourrait divulguer des informations personnelles au développeur ou à un autre joueur par le jeu lui-même

Comme les niveaux peuvent être partagés sous forme de fichiers et peuvent contenir des textes, des images et de l'audio arbitraires choisis par leur auteur, les parents et les tuteurs restent responsables des niveaux qu'un enfant obtient d'autres personnes

## Composants tiers

Le jeu est construit avec le moteur Unity. **Les services de collecte de données propres à Unity (Unity Analytics, Unity Ads, Unity In-App Purchasing, Unity Cloud Diagnostics, les diagnostics du moteur, les statistiques matérielles, les rapports de plantage et les rapports de performances) sont tous désactivés dans ce projet**, et les paquets qui les fournissent ne sont pas inclus dans le build. Aucun SDK de publicité, d'analyse d'audience, d'attribution ou de rapports de plantage, de quelque sorte que ce soit, n'est présent

Le build d'une boutique contient la bibliothèque propre à cette boutique, et aucun autre build ne la contient  Steamworks (par l'intermédiaire de Facepunch.Steamworks) dans les builds Steam, Google Play Games Services et les bibliothèques Google Play d'évaluation et de mise à jour intégrée à l'application dans le build Google Play, le SDK RuStore d'évaluation et de mise à jour de l'application dans le build RuStore. Chacune d'elles ne communique qu'avec son propre service, comme décrit ci-dessus

## Tes droits

Des réglementations telles que le RGPD, le RGPD du Royaume-Uni (UK GDPR), le CCPA/CPRA et la loi fédérale russe n° 152-FZ t'accordent des droits d'accès, de rectification, d'effacement et d'opposition au traitement de tes données personnelles

Comme le développeur ne détient absolument aucune donnée personnelle te concernant, il n'y a rien à consulter, rectifier, exporter ou supprimer du côté du développeur, et aucune demande n'est nécessaire pour exercer ces droits. Les données décrites dans [[game-privacy-policy#Ce qui est stocké sur ton appareil]] sont sous ton propre contrôle  elles peuvent être examinées dans le dossier de stockage du jeu sur ton appareil, effacées depuis le jeu ou supprimées entièrement en désinstallant l'application. Une copie qu'une boutique conserve sous ton compte (Steam Cloud, les succès sur Steam ou dans Google Play Jeux) est détenue par cette boutique, et ces droits s'exercent sur elle auprès de cette boutique, selon sa propre politique. Tu peux toujours écrire à l'adresse de contact ci-dessus pour toute question sur cette politique

## Conservation des données

Le développeur ne conserve aucune donnée personnelle et n'a donc aucune durée de conservation à déclarer. Les données stockées sur ton appareil sont conservées aussi longtemps que tu les y gardes. Une copie qu'une boutique conserve sous ton compte est conservée par cette boutique selon sa propre politique

## Modifications de cette politique

Cette politique changera si le jeu change, très probablement lorsque seront ajoutés le serveur propre au jeu, les comptes joueurs ou le multijoueur, dont aucun n'existe aujourd'hui. Lorsqu'elle change, la date d'entrée en vigueur et la version de la politique en haut de cette page sont mises à jour, et le texte précédent reste disponible dans l'historique public des versions de cette page. Continuer à utiliser le jeu après une modification signifie que la politique mise à jour s'applique à cette utilisation

## Contact

Les questions sur cette politique, ou sur la confidentialité dans Bullet Hero en général, sont à adresser à l'adresse de contact en haut de cette page
