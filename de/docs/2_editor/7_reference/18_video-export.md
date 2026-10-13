---
title: Videoexport
date: 2026-10-03
tags: [level_author]
---

# Videoexport

Der Editor rendert das offene Level mit dem ffmpeg auf deinem Computer in eine Videodatei. Gerendert wird offline, Frame für Frame, also ist das Video exakt, egal wie langsam der Rechner ist

Der Export funktioniert unter Windows, macOS und Linux. Auf Smartphones ist er nicht verfügbar

## Wo es zu finden ist

- `{{ui:editor_video-export_open}}` in der Seitenspalte der Leveleinstellungen
- der Befehl `{{ui:cmd_editor_export-video}}` in der Befehlspalette

Das Fenster öffnet sich über dem Editor. Aus den Leveleinstellungen geöffnet, kehrt es beim Schließen zu ihnen zurück. Während ein Video rendert, lässt sich das Fenster nicht schließen: `{{ui:editor_video-export_stop}}` beendet das Rendern

## ffmpeg installieren

ffmpeg gehört nicht zum Spiel. Installiere es einmal, und das Fenster findet es von selbst. Nötig ist Version `{{v:ffmpeg.min-version}}` oder neuer. Eine ältere wird abgelehnt, und das Fenster nennt die gefundene Version

| System | Installationsbefehl |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | das Paket deiner Distribution, zum Beispiel `sudo apt install ffmpeg` |

> [!warning] Warnung
> Manche Linux-Distributionen liefern ein ffmpeg, das älter als `{{v:ffmpeg.min-version}}` ist (Ubuntu 24.04 liefert 6.1). Installiere dann einen neueren Build von der ffmpeg-Website und zeige dem Fenster den Weg dorthin

Das Fenster sucht ffmpeg in dieser Reihenfolge:
1. die Datei, die du mit `{{ui:editor_video-export_ffmpeg_choose}}` gewählt hast. Dann wird nichts anderes gesucht
2. der Pfad in der Umgebungsvariable `BH_FFMPEG`
3. `tools/ffmpeg` im Datenordner des Spiels
4. jeder Ordner in `PATH`
5. die Ordner, in die die üblichen Installer schreiben

`{{ui:editor_video-export_ffmpeg_auto}}` vergisst die gewählte Datei und sucht erneut. `{{ui:editor_video-export_ffmpeg_check}}` wiederholt die Prüfung, zum Beispiel direkt nach der Installation

Dein ffmpeg kann Hardware-Encoder enthalten (NVIDIA, AMD, Intel, Apple). Das Fenster probiert jeden an einer Zehntelsekunde Schwarz aus und verwendet nur die, die auf diesem Computer tatsächlich funktionieren

## Optionen des Fensters

| Option | Was sie tut |
|---|---|
| `{{ui:editor_video-export_container}}`, `{{ui:editor_video-export_codec}}` | die Art der Datei und wie sie komprimiert wird, siehe die Formate unten |
| `{{ui:editor_video-export_resolution}}` | die Größe des Videos. Breite und Höhe sind gerade Zahlen von `{{v:video-export.min-size}}` bis `{{v:video-export.max-size}}` |
| `{{ui:editor_video-export_fps}}` | Frames pro Sekunde des Videos, bis `{{v:video-export.max-fps}}`. Hängt nicht von der eigenen Framerate des Levels ab. Unter `{{v:video-export.min-simulation-rate}}` wird jeder Frame in mehreren Schritten simuliert, damit der Bot so spielt wie im Spiel |
| `{{ui:editor_video-export_range}}` | das ganze Level, der Schleifenbereich der Zeitleiste oder ein eigener Start- und Endframe |
| `{{ui:editor_video-export_quality}}` | wie viel Platz das Video einnimmt. Ausgeblendet bei Formaten, die ohnehin verlustfrei sind |
| `{{ui:editor_video-export_full-chroma}}` | Farbe für jedes Pixel statt für jedes zweite. Schärfere dünne farbige Linien, eine größere Datei |
| `{{ui:editor_video-export_seed}}` | der Seed für den Zufall des Levels. `0` behält den Seed, den der Editor gerade verwendet |
| `{{ui:editor_video-export_preroll}}` | wie viele Sekunden vor dem Start gespielt, aber nicht aufgenommen werden, damit Effekte schon ihre Vorgeschichte haben. Standardmäßig `{{v:video-export.default-preroll}}`, bis `{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | standardmäßig `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}` oder `{{ui:enum_bot-kind_none}}` für ein Video ohne Avatar. Treffer bewirken während eines Exports nichts |
| `{{ui:editor_video-export_post-processing}}`, `{{ui:editor_video-export_effects}}` | dieselben Schalter wie im Editor, nur für das Video |
| `{{ui:editor_video-export_audio}}` | die Spuren des Levels im Video |

Jede Option hat im Fenster ihr eigenes `?`

Die Oberfläche des Editors, das Raster, Gizmos, die Auswahl und die Kameragrenzen kommen nie ins Video. Die Kamera des Levels bestimmt den Bildausschnitt, und schwarze Balken füllen alles, was ihr Seitenverhältnis nicht abdeckt

## Rendergeschwindigkeit

Das Video hängt nicht davon ab, wie schnell dein Computer ist. Levelzeit und Bot rücken pro gerendertem Frame um genau einen Frame des Videos vor, also rendert ein langsamer Rechner dasselbe Video, nur später

`{{ui:enum_bot-kind_warm}}` berechnet seine ganze Route vor dem ersten Frame, und das Fenster zeigt, wie weit er ist. Findet er keine Route, stoppt der Export und verlangt einen anderen Bot

## Formate

Ein Format besteht aus zwei Entscheidungen: `{{ui:editor_video-export_container}}` und `{{ui:editor_video-export_codec}}`. Aufgelistet sind nur die Paare, die dein ffmpeg erzeugen kann. Die Zeile darunter sagt, welcher Ton zum Paar gehört und welche Datei du bekommst

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | Ton | Gut für |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264, HEVC, AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | Verschicken und Hochladen überallhin |
| `{{ui:editor_video-export_container_mkv}}` | H.264, HEVC, AV1, VP9, FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | Archivieren, FFV1 ganz ohne Verlust |
| `{{ui:editor_video-export_container_mov}}` | H.264, HEVC, ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | Schnitt in Premiere, DaVinci Resolve, Final Cut |
| `{{ui:editor_video-export_container_webm}}` | VP9, AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | das Web |
| `{{ui:editor_video-export_container_gif}}`, `{{ui:editor_video-export_container_webp}}`, `{{ui:editor_video-export_container_apng}}` | - | kein Ton | kurze Schleifenclips für Chats und Seiten |
| `{{ui:editor_video-export_container_sequence}}` | PNG, JPEG, WebP, TIFF | `audio.wav` neben den Frames | jedes Schnittprogramm importiert es |
| `{{ui:editor_video-export_container_audio}}` | WAV, FLAC, MP3, Opus | das Format selbst | nur der Ton des Levels, nichts wird gerendert |

GIF verwendet für den ganzen Clip eine Palette mit 256 Farben. Halte es kurz und klein: Ein GIF eines ganzen Levels wiegt weit mehr als ein MP4 davon

## Wohin das Video geht

Standardmäßig landet das Video in `recordings/<level id>/` im Datenordner des Spiels, benannt nach dem Level und der Zeit des Exports. `{{ui:editor_video-export_output_folder}}` öffnet diesen Ordner. `{{ui:editor_video-export_output_choose}}` speichert das nächste Video an einem beliebigen anderen Ort

Aufnahmen bleiben erhalten, wenn du das Level löschst. Sie gehören nicht zu einer Profilübertragung, außer du hakst `{{ui:settings_profile-transfer_category-recordings}}` an

## Ton

Der Ton des Videos wird nicht von den Lautsprechern aufgenommen, und während eines Exports hörst du nichts

Mit eingeschaltetem `{{ui:editor_video-export_engine-audio}}` (der Standard) und Effekten auf den Spuren läuft der Ton des Levels in Echtzeit, während die Frames rendern, und der eigene Ton des Spiels wird aufgenommen, Effekte eingeschlossen. Der Export dauert mindestens so lange wie der Bereich: Ein schneller Computer wartet, bis der Ton fertig ist. Ausgeschaltet werden die Spuren getrennt gemischt, mit ihren Keyframes für Lautstärke und Panorama, aber ohne ihre Effekte. `{{ui:editor_video-export_container_audio}}` mischt immer getrennt

Unter der Vorschau zeigt das Fenster zwei Zeitleisten, `{{ui:editor_video-export_track_frames}}` und `{{ui:editor_video-export_track_sound}}`: Sie bewegen sich unabhängig voneinander. Bei einem schweren Level kann der parallele Ton stocken. Schalte dann `{{ui:editor_video-export_sound-after-frames}}` ein: Der Ton wird nach dem letzten Frame aufgenommen, und der Export dauert um die Länge des Bereichs länger

> [!warning] Warnung
> Schließe das Spiel nicht, während ein Video rendert. Das Fenster sagt das während des ganzen Vorgangs

## Was nicht im Video ist

- die Effekte auf Audiospuren, aber nur mit ausgeschaltetem `{{ui:editor_video-export_engine-audio}}` oder in `{{ui:editor_video-export_container_audio}}`. Das Fenster warnt, wenn das Level welche hat
- ein transparenter Hintergrund
- eine Aufnahme deines eigenen Spiels: Im Video kann nur der Bot spielen

Weiterlesen: [[13_export-and-protection]], [[7_audio]]
