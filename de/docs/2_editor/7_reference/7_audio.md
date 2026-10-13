---
title: Audio
date: 2026-10-02
tags: [level_author]
---

# Audio

Der Klang einer Audiospur läuft durch eine Kette aus 11 Effekten, von Normalisieren und Kompressor bis Echo und Hall. Kette, Geschwindigkeit und Lautstärke stellt man im Audiospur-Inspector ein

## Audiospur-Inspector

Zeigt den Clip der ausgewählten Audiospur, ihre Geschwindigkeit, die Lautstärke des Faders und die Effektkette.
Die Effekte: Tiefpass, Hochpass, Echo, Hall, Chorus, Tonhöhenverschiebung, Verzerrung, Flanger, Kompressor, Normalisieren und ein parametrischer Equalizer

`{{ui:field_common_speed}}` und `{{ui:editor_inspector-audio_volume}}` sind Regler, keine Eingabefelder. So ist der erlaubte Bereich sichtbar

> [!caution] Vorsicht
> **Die Lautstärke hier ist ein Fader.** Die per Keyframes gesetzte Lautstärke ist eine eigene Spur auf der lokalen Zeitleiste. Beim Abspielen werden beide multipliziert

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Normalisieren

Zieht das Signal ständig zu einer Ziellautheit hin. So klingen Clips aus verschiedenen Quellen ohne manuelles Nachregeln gleich laut.
Setz es ein, wenn die Spuren des Levels nicht zusammen abgemischt wurden

Es wirkt auf die Gesamtlautheit. Die Dynamik innerhalb einer Spur ändert der [[7_audio#Kompressor|Kompressor]]

- `Lowest Volume` verhindert, dass Stille und Rauschen zu einem Zischen hochgezogen werden
- `Maximum Amp` begrenzt, wie stark es anheben kann

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Kompressor

Drückt die lauten Stellen herunter, damit die leisen höher klingen können. Eine komprimierte Spur ist unter allem anderen im Level hörbar und übersteuert nicht.
Meist rettet er einen Song, der hinter seinen eigenen Effekten untergeht

- `Threshold` - wo er zu arbeiten beginnt
- `Attack` und `Release` - wie schnell er zupackt und loslässt. Zu schnell, und du schneidest die Anschläge ab oder bekommst hörbares Pumpen
- `Make Up Gain` gibt die Lautstärke zurück, die er weggenommen hat

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Tiefpass

Lässt die Tiefen durch und schneidet alles oberhalb von `Cutoff Freq` ab. Klingt wie unter Wasser oder durch eine Wand

Senk die Grenzfrequenz: die Spur verliert zuerst ihre Luft, dann ihre Klarheit und am Ende alles außer dem Bass.
Am oberen Ende des Bereichs ist der Filter fast durchlässig. Die Spur klingt wie die Datei

> [!tip] Tipp
> Die Effektkette gehört zur **Spur** und wird nicht mit Keyframes animiert. Sie kann sich nicht sanft über die Zeit ändern. Schneide die Spur dort, wo die Änderung nötig ist, und stelle die Hälften unterschiedlich ein

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Hochpass

Das Spiegelbild des Tiefpasses: lässt die Höhen durch und schneidet alles unterhalb von `Cutoff Freq` ab

Heb die Grenzfrequenz an: die Spur wird dünn wie ein winziger Lautsprecher oder ein Telefonat.
Meist lässt man damit etwas klein klingen, bevor sich alles öffnet

> [!tip] Tipp
> Die Effektkette gehört zur **Spur** und wird nicht mit Keyframes animiert. Sie kann sich nicht sanft über die Zeit ändern. Schneide die Spur dort, wo die Änderung nötig ist, und stelle die Hälften unterschiedlich ein

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Parametrischer EQ

Ein parametrisches Band: hebt einen gewählten Teil des Spektrums an oder senkt ihn ab.
Anders als [[7_audio#Tiefpass|Tiefpass]] und [[7_audio#Hochpass|Hochpass]] kann er auch hinzufügen. Deshalb schafft man damit eher Platz im Mix, als einen Effekt zu erzeugen

- `Center Freq` - wo das Band sitzt
- `Octave Range` - die Breite des Bands. Schmal für eine genaue Korrektur, breit für eine allgemeine Färbung
- `Frequency Gain` unter 1 senkt ab, über 1 hebt an

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Verzerrung

Kappt die Wellenform. Der Klang füllt sich mit Obertönen, die er nicht hatte: schmutzig, übersteuert, wütend.
Der einfachste Effekt hier: ein Regler, `Level` - wie hart das Kappen zubeißt

Als Nebenwirkung glättet er die Dynamik. Eine stark verzerrte Spur verliert ihre leisen Stellen.
Wo ein Abschnitt unerbittlich klingen soll, ist das nützlich. Wo nicht, zerstört es

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Echo

Wiederholt das Signal in gleichen Abständen. Jede Wiederholung ist leiser als die vorige.
Ein Echo ist rhythmisch, und die Wiederholungen lassen sich zählen. Das unterscheidet es vom verwaschenen Ausklang des [[7_audio#Hall|Halls]]: du hörst einzelne Kopien, keinen Raum

- `Delay` - der Abstand zwischen den Kopien in Millisekunden
- `Decay` - welcher Anteil jeder Kopie in die nächste übergeht

Nimm die Verzögerung aus dem Tempo des Songs, dann landet das Echo auf dem Beat, statt ihn zu verschmieren

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Hall

Setzt die Spur in einen Raum. Zuerst kommen die frühen Reflexionen von den nahen Wänden, dann ein abklingender Ausklang.
Das ist der größte Effekt hier: seine Felder beschreiben einen Raum, keine Wiederholung. Wiederholungen sind Sache des [[7_audio#Echo|Echos]]

Den Grundklang bestimmen drei Felder:
- `Decay Time` - wie groß der Raum ist
- `Room` - wie viel davon zu hören ist
- `Room HF` - senk es ab, und die Wände klingen weich und schluckend

Der Rest ist Feinabstimmung. Geh dazu über, wenn diese drei Felder stimmen

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Chorus

Legt drei leicht verzögerte Kopien mit schwankender Tonhöhe über das Signal. Eine Quelle klingt wie mehrere.
Das Ergebnis ist Breite und Fülle, keine Wiederholung. Die Verzögerungen sind zu kurz, um einzeln gehört zu werden

Die drei Kopien unterscheiden ihn vom [[7_audio#Flanger|Flanger]], bei dem eine Kopie wandert

- `Rate` - die Geschwindigkeit des Schwankens
- `Depth` - die Spannweite des Schwankens
- `Feedback` - heb es an, und der Klang rückt in Richtung Flanger

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Flanger

Mischt eine sehr kurze, schwankende Verzögerung des Signals in das Signal selbst. Bei Frequenzen, die mit der Verzögerung wandern, löschen sich die beiden gegenseitig aus.
Diese wandernde Kerbe ist das Rauschen eines Düsentriebwerks. Der Effekt entsteht durch Auslöschung, nicht durch eine Kopie

Er gehört zur selben Familie wie der [[7_audio#Chorus|Chorus]]. Aber es gibt eine Kopie, und die Verzögerung ist kürzer, also hörst du ein Wandern, keine Breite

Die Kerbe ist am tiefsten, wenn `Dry Mix` und `Wet Mix` nah beieinander eingestellt sind

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Tonhöhenverschiebung

Ändert die Tonhöhe der Spur, ohne ihre Geschwindigkeit zu ändern.
Darum geht es: das Timing des Levels hängt am Song. Die Spur lässt sich also nicht einfach neu abtasten, wie es das eigene Feld `{{ui:field_common_speed}}` der Spur tut

- `Pitch` - ein Multiplikator. 1 ändert nichts, 2 hebt um eine Oktave an
- `FFT Size` und `Overlap` tauschen Qualität gegen Kosten

Bei einer großen Verschiebung hört man dem Klang die Bearbeitung trotzdem an

> [!tip] Tipp
> Die Effektkette gehört zur **Spur** und wird nicht mit Keyframes animiert. Sie kann sich nicht sanft über die Zeit ändern. Schneide die Spur dort, wo die Änderung nötig ist, und stelle die Hälften unterschiedlich ein

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld auf seinen Standard zurück, `{{ui:field_common_mix-level}}` eingeschlossen. Dessen Standard ist die Untergrenze von -80 dB, das Zurücksetzen schaltet den Effekt also auch ab

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]
