---
title: Datenschutzerklärung des Spiels
date: 2026-10-03
tags: [legal]
---

# Datenschutzerklärung des Spiels

Bullet Hero erhebt, übermittelt, speichert auf keinem Server, verkauft oder teilt keinerlei personenbezogene Daten. Es gibt keine Konten, keine Anmeldung, keine Werbung, keine Analyse, keine Absturzberichte, kein Tracking und keine Werbe-ID. Alles, was sich das Spiel über dich merkt, bleibt auf deinem eigenen Gerät

Vier Dinge können dein Gerät verlassen, und keines davon geht an den Entwickler:

- ein Level, das du öffnest, kann auf eine Datei verweisen, die auf einer fremden Website liegt, und beim Laden wird diese Website kontaktiert ([[game-privacy-policy#Netzwerkzugriff]])
- ein Level, das du bewusst mit jemandem teilst, gelangt dorthin, wohin du es schickst ([[game-privacy-policy#Levels, die du teilst]])
- in den Steam-Builds spricht das Spiel über den Steam-Client mit dem Steam Workshop ([[game-privacy-policy#Steam Workshop]])
- in den Steam-Builds zeigt das Spiel über den Discord-Client deine aktuelle Aktivität auf Discord an ([[game-privacy-policy#Discord Rich Presence]])

| | |
|---|---|
| Gültig ab | 3. Oktober 2026 |
| Version der Erklärung | 1.3 |
| Anwendung | Bullet Hero: `com.vertoker.BulletHero` auf Android, `com.vertoker.Bullet-Hero` auf iOS sowie die Desktop-Builds für Windows, Linux und macOS |
| Entwickler | vertoker, ein einzelner Entwickler |
| Kontakt | [kostyachurakov@gmail.com](mailto:kostyachurakov@gmail.com) |

Diese Erklärung gilt nur für das Spiel. Die Website hat eine eigene Erklärung - [[privacy-policy]]. Auch der Server wird eine eigene Erklärung bekommen, die geschrieben wird, sobald es den Server gibt

## Für wen diese Erklärung gilt

Diese Erklärung gilt für jeden Build von Bullet Hero, auf jeder Plattform und in jedem Store, über den er vertrieben wird, und für jede Version des Spiels, der keine neuere Erklärung beigefügt ist

Wenn ein Store (Google Play, der App Store, Steam, RuStore, VK Play oder ein anderer) eigene Daten über deinen Kauf, deine Installation oder deine Nutzung der Anwendung erhebt, gilt für diese Erhebung die Datenschutzerklärung dieses Stores und nicht diese hier. Der Entwickler erhält von diesen Stores nur das, was sie jedem Entwickler zeigen: zusammengefasste, anonyme Statistiken zu Installationen und Abstürzen, die sich nicht auf einen einzelnen Spieler zurückführen lassen

## Was auf deinem Gerät gespeichert wird

Das Spiel schreibt Folgendes in seinen eigenen Anwendungsspeicher und liest es beim nächsten Start wieder ein:

- **Einstellungen**: Grafik, Audio, Steuerung, Tastenbelegung, Oberfläche und Spracheinstellungen
- **Fortschritt und Statistik**: Versuche, Bestleistungen, Tode, Spielzeit und ähnliche Aufzeichnungen, sowohl für das ganze Gerät als auch pro Level
- **Levels**: die Levels, die du erstellst, importierst oder herunterlädst, einschließlich ihrer Audiodateien, Bilder und anderer Medien, sowie ihre automatischen Sicherungen
- **Diagnoseprotokolle**: die eigene Protokolldatei der Engine, lokal geschrieben, damit sich ein Problem auf dem Gerät untersuchen lässt, auf dem es aufgetreten ist

Nichts davon wird irgendwohin übermittelt, und nichts davon wird bei einem Dienst des Entwicklers gesichert. Wo es liegt, hängt von der Plattform ab:

- **Android und iOS**: der private Speicher des Spiels. Andere Anwendungen können ihn nicht lesen, und er wird zusammen mit dem Spiel gelöscht, wenn du es deinstallierst
- **Windows, Linux und macOS**: der Ordner für Anwendungsdaten in deinem Benutzerprofil, der Standardort der Engine. Andere Programme, die unter deinem Konto laufen, können ihn lesen, wie jede deiner Dateien, und er bleibt nach der Deinstallation des Spiels erhalten, bis du diesen Ordner löschst

Das Spiel bietet außerdem unter `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` ausdrückliche Steuerelemente, um gespeicherte Statistiken und Sicherungen ohne Deinstallation zu löschen

Das Spiel fordert keinen Zugriff auf deine Kontakte, Fotos, Kamera, Mikrofon, Standort, Kalender, Anrufliste, die Liste installierter Anwendungen oder eine andere sensible Ressource an, und es fragt überhaupt keine Laufzeitberechtigungen ab

## Netzwerkzugriff

Bullet Hero hat keinen Server. Der Entwickler betreibt keinen Dienst, mit dem sich das Spiel verbindet, und erhält deshalb keine Daten daraus

Ein Level ist ein Ordner mit Dateien, und sein Autor kann eine dieser Dateien auf eine Internetadresse verweisen lassen, statt sie im Ordner mitzuliefern. Wenn du ein solches Level öffnest, lädt das Spiel diese Datei von der Website herunter, die ihr Autor gewählt hat. Diese Website sieht dann, was jede Website sieht, wenn eine Datei bei ihr angefragt wird, vor allem deine IP-Adresse und die technischen Details der Anfrage. Der Entwickler kontrolliert diese Anfragen nicht, beobachtet sie nicht, und es wird kein Protokoll davon geführt

Davon abgesehen, vom Steam Workshop in den Steam-Builds ([[game-privacy-policy#Steam Workshop]]) und von Discord Rich Presence in den Steam-Builds ([[game-privacy-policy#Discord Rich Presence]]), stellt das Spiel keine eigenen Netzwerkanfragen

## Steam Workshop

Die Steam-Builds nutzen den Steam Workshop über den Steam-Client, der auf deinem Computer läuft. Builds für alle anderen Stores starten Steam nie: Der Code, der mit Steam spricht, wird nur in die Steam-Builds kompiliert

Das Spiel fragt Steam, welche Workshop-Objekte dein Konto abonniert hat, damit es sie als Levels und Sammlungen auflisten kann. Der Steam-Client lädt sie herunter. Wenn du ein Level oder eine Sammlung veröffentlichst, übergibt das Spiel es zusammen mit dem Titel, der Beschreibung, dem Vorschaubild, den Inhaltsbeschreibungen und der Sichtbarkeit, die du festgelegt hast, an den Steam-Client, und Steam speichert es unter deinem Steam-Konto auf seinen Servern. Ein öffentliches Objekt kann jeder auf Steam sehen, bis du es dort entfernst

All das läuft zwischen dem Steam-Client und den Servern von Valve und unterliegt der eigenen Datenschutzerklärung von Steam und dem Steam-Nutzervertrag (Steam Subscriber Agreement). Der Entwickler erhält daraus nichts über das hinaus, was Steam jedem Entwickler über ein Workshop-Objekt zeigt

## Discord Rich Presence

Die Steam-Builds können in deinem Discord-Profil anzeigen, was du im Spiel tust: das Menü, den Leveleditor, die Sandbox oder das Level, das du spielst, und wie lange schon. Ein Level wird nur dann mit Namen und seinen Autoren angezeigt, wenn es bereits öffentlich ist - ein Objekt im Steam Workshop oder ein Level, das mit dem Spiel ausgeliefert wird. Jedes andere Level wird nur als eigenes Level angezeigt, und das Level, das du bearbeitest, wird nie genannt. Das funktioniert nur, solange die Discord-App auf demselben Computer läuft. Builds für alle anderen Stores haben keine Discord-Integration: Der Code, der mit Discord spricht, wird nur in die Steam-Builds kompiliert

Das Spiel übergibt diese Aktivität an den Discord-Client auf deinem Gerät, nie an einen eigenen Server. Der Discord-Client veröffentlicht sie dann unter deinem Discord-Konto, und deine Freunde und Server auf Discord können sie sehen. Das Spiel meldet sich nicht bei Discord an, liest weder deine Nachrichten noch deine Server oder deine Freundesliste und sendet nichts in deinem Namen

Was mit dieser Aktivität auf der Seite von Discord geschieht, unterliegt der [Datenschutzerklärung von Discord](https://discord.com/privacy). Der Entwickler erhält daraus nichts. Du kannst deine Aktivität jederzeit in Discord ausblenden: `User Settings` -> `Activity Privacy`

## Levels, die du teilst

Levels sind von Grund auf portabel: Ein Level lässt sich als gewöhnliche Archivdatei exportieren und auf jedem Weg, den du wählst, an eine andere Person schicken. Eine solche Datei gelangt direkt von dir zum Empfänger oder über den Dienst, mit dem du sie verschickst. Sie läuft nicht über den Entwickler, und der Entwickler behält keine Kopie davon

Ein Level, das du erstellst, kann deine eigene Musik, Bilder und Texte enthalten und, wenn du sie hineinschreibst, deinen Namen oder Nickname. Alles, was du in ein Level legst, ist für jeden sichtbar, dem du dieses Level gibst. Was du hineinnimmst, entscheidest allein du

Ein Level kann optional mit einer Passphrase geschützt werden. Mit dieser Passphrase wird der Inhalt des Levels auf deinem Gerät verschlüsselt, und sie wird nie auf die Festplatte geschrieben, nie protokolliert und nie übermittelt. Wenn du sie verlierst, kann weder der Entwickler noch sonst jemand den Inhalt des Levels wiederherstellen

## Kinder

Das Spiel erhebt von niemandem personenbezogene Daten, auch nicht von Kindern. Es enthält keine Werbung, keine In-App-Käufe, keinen Chat und keine andere Kommunikationsfunktion und keinen Mechanismus, über den ein Kind dem Entwickler oder einem anderen Spieler über das Spiel selbst persönliche Informationen preisgeben könnte

Da Levels als Dateien geteilt werden und beliebige, von ihrem Autor gewählte Texte, Bilder und Audiodateien enthalten können, bleiben Eltern und Erziehungsberechtigte für die Levels verantwortlich, die ein Kind von anderen Personen bekommt

## Komponenten von Drittanbietern

Das Spiel ist mit der Engine Unity gebaut. **Die datenerhebenden Dienste von Unity selbst (Unity Analytics, Unity Ads, Unity In-App Purchasing, Unity Cloud Diagnostics, die Diagnose der Engine, Hardwarestatistiken, Absturzberichte und Leistungsberichte) sind in diesem Projekt alle deaktiviert**, und die Pakete, die sie bereitstellen, sind nicht im Build enthalten. Es ist keinerlei SDK für Werbung, Analyse, Attribution oder Absturzberichte vorhanden

## Deine Rechte

Regelwerke wie die DSGVO, die UK-DSGVO, der CCPA/CPRA und das russische Föderale Gesetz Nr. 152-FZ geben dir das Recht auf Auskunft über deine personenbezogenen Daten, auf ihre Berichtigung und Löschung sowie auf Widerspruch gegen ihre Verarbeitung

Da der Entwickler keinerlei personenbezogene Daten über dich besitzt, gibt es auf der Seite des Entwicklers nichts einzusehen, zu berichtigen, zu exportieren oder zu löschen, und für die Ausübung dieser Rechte ist kein Antrag nötig. Die in [[game-privacy-policy#Was auf deinem Gerät gespeichert wird]] beschriebenen Daten stehen unter deiner eigenen Kontrolle: Du kannst sie im Speicherordner des Spiels auf deinem Gerät einsehen, im Spiel selbst leeren oder durch Deinstallation der Anwendung vollständig entfernen. Mit jeder Frage zu dieser Erklärung kannst du dich trotzdem an die oben genannte Kontaktadresse wenden

## Speicherdauer

Der Entwickler speichert keine personenbezogenen Daten und hat deshalb keine Speicherdauer anzugeben. Daten auf deinem Gerät bleiben so lange erhalten, wie du sie dort behältst

## Änderungen dieser Erklärung

Diese Erklärung ändert sich, wenn sich das Spiel ändert, höchstwahrscheinlich dann, wenn ein eigener Server des Spiels, Spielerkonten oder Multiplayer hinzukommen, die es heute alle nicht gibt. Bei einer Änderung werden das Gültigkeitsdatum und die Version der Erklärung oben auf dieser Seite aktualisiert, und der vorherige Text bleibt im öffentlichen Versionsverlauf dieser Seite verfügbar. Nutzt du das Spiel nach einer Änderung weiter, gilt für diese Nutzung die aktualisierte Erklärung

## Kontakt

Fragen zu dieser Erklärung oder allgemein zum Datenschutz in Bullet Hero gehen an die Kontaktadresse oben auf dieser Seite
