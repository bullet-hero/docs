---
title: Mobile Geräte
date: 2026-10-02
tags: [level_author]
---

# Mobile Geräte

Auf dem Handy verdeckt ein Finger den Bildschirm, und die Ränder gehören dem System. Halte Wichtiges von den Rändern fern und teste auf einem schwachen Handy: Vollbild-Halbtransparenz bremst es zuerst

Handys sind ebenso ein Ziel wie der PC.
Ein Level, das nur auf dem PC spielbar ist, ist nur halb fertig

## Ein Finger statt einer Maus

**Ein Finger verdeckt den Bildschirm.** Eine Maus ist ein Punkt, ein Finger ist ein Fleck, unter dem nichts zu sehen ist.
Bau kein Muster, bei dem man genau dort hinsehen muss, wo der Spieler ist. Am PC funktioniert das, auf dem Handy ist es ein toter Winkel

**Die Steuerung ist anders.** Am PC gibt der Cursor das Ziel vor, und die Figur bewegt sich dorthin. Auf dem Handy ist die Präzision geringer, und ein Finger hat mehr Trägheit.
Eine Lücke, die man mit der Maus beim ersten Versuch schafft, wird auf dem Handy zu einer eigenen Prüfung

**Mach eine schmale Lücke zeitlich kurz,** nicht räumlich schmal

## Ränder und Bildschirmform

> [!caution] Vorsicht
> Die Ränder gehören dem System: die Kameraaussparung, abgerundete Ecken, Navigationsgesten. Die Oberfläche des Spiels hält sich vom unsicheren Bereich fern, der Levelinhalt nicht. Halte Wichtiges von den Rändern fern, vor allem vom oberen

**Seitenverhältnis.** Ein Handy hat etwa 20:9, deutlich schmaler und länger als das, woran du arbeitest.
Sieh dir das Level mindestens einmal im Gerätesimulator in dieser Form an, bevor du es für fertig hältst

> [!caution] Vorsicht
> Der Gerätesimulator zeigt Proportionen und Aussparungen, sagt aber nichts über die Leistung. Ein Durchlauf auf einem echten schwachen Gerät ist mehr wert als jede Überlegung

## Was ein Handy zuerst bremst

Der Reihe nach:
1. Bildschirmfüllende Halbtransparenz in mehreren Ebenen
2. Post-Processing, vor allem Bloom. Seine Kosten wachsen mit der Auflösung, nicht mit der Zahl der Objekte
3. Große Texturen. Ein 4096er-Bild belegt 64 MB Speicher, bevor irgendetwas gezeichnet wird. Ein Viertel davon nur, wenn die eigenen Einstellungen des Spielers es komprimieren
4. Effekte mit vielen Partikeln
5. Und erst dann die Zahl der Formen

## Kantenglättung

Kantenglättung ist eine Einstellung des Spielers, keine des Levels.
Sie erklärt aber, warum sich dasselbe Level auf zwei ähnlichen Handys unterschiedlich verhält:
- `{{ui:enum_anti-aliasing-type_msaa}}` wird pro Sample berechnet. Seine Kosten wachsen mit halbtransparentem Overdraw, genau dort, wo ein schwaches Handy ohnehin kämpft
- `{{ui:enum_anti-aliasing-type_fxaa}}` ist ein Durchgang über den Bildschirm, seine Kosten hängen von nichts ab

Weiter: [[4_composition-and-camera|Komposition und Kamera]], [[1_level-budget|Levelbudget]]
