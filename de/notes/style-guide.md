---
title: Styleguide
date: 2026-10-13
tags: [contributor]
---

# Styleguide

Schreib einfach: ein Satz, ein Gedanke, Zahlen statt Adjektiven. Ein Bindestrich mit Leerzeichen statt eines langen Strichs, keine Semikolons, kein Punkt am Ende eines Absatzes

Der Text berichtet, er verkauft nicht. Jede Emotion wird zuerst in eine Liste, eine Tabelle oder eine Zahl verwandelt.
Eine Seite, die nach Marketing, Expertengehabe oder einem freundlichen Assistenten klingt, ist gescheitert, auch wenn jeder Fakt darin stimmt

## Zuerst einfach

Diese Regel steht über allen anderen

Ein Text kann ganz ohne Füllwörter auskommen und trotzdem schwer zu lesen sein. Jeder Satz stimmt, aber sie sind zu einem einzigen dichten Argument verkettet, und der Leser muss alles auf einmal im Kopf behalten

Seiten für Einsteiger werden so geschrieben, dass man sie überfliegen kann. Das sind die Seiten für Spieler, die ersten Seiten für Levelautoren, der Schnellstart, die FAQ, die Hilfe und die Startseite jedes Abschnitts. Referenz- und SDK-Seiten dürfen dichter sein, aber für ihre Sätze gelten dieselben Regeln

1. **Nur, was der Leser jetzt braucht.** Frag dich vor jedem Satz: Handelt der Leser anders, nachdem er ihn gelesen hat? Wenn nicht, streich ihn oder verschieb ihn auf die ausführliche Seite. Grenzfälle, Plattformvorbehalte, interne Gründe, wie die Website selbst funktioniert - nichts für eine Einsteigerseite
2. **Ein Satz, ein Gedanke.** Keine Ketten aus Nebensätzen, verbunden durch Doppelpunkte, "weil", "also", "während", keine Klammern in Klammern. Zwei kurze Sätze sind besser als ein langer. Ein Satz darf innerhalb eines Absatzes in einer eigenen Zeile stehen: mit einem Punkt am Ende, außer dem letzten. Im Chinesischen und Japanischen ist ein Satz in einer eigenen Zeile ein eigener Absatz, mit einer Leerzeile davor
3. **Die allgemeine Regel, nicht die Ausnahmen.** "Die Zahlen stimmen meistens überein" statt dreier Sätze darüber, wann sie abweichen. Die Ausnahme steht auf der ausführlichen Seite, hinter `Mehr - [[page]]` (im Englischen `More - [[page]]`, im Chinesischen `更多：[[page]]`, im Japanischen `詳細：[[page]]`, im Spanischen `Más - [[page]]`, im Portugiesischen `Mais - [[page]]`, im Französischen `Plus - [[page]]`)
4. **Navigation vor Erklärung.** Eine Startseite ist eine kurze Einleitung und eine Tabelle Name -> Link oder Zeilen wie `Alles, was du herunterladen kannst - [[download]]`. Beschreibende Spalten wie "was es ist" und "Status" braucht es nicht, wenn der Link es schon sagt
5. **Sag, was wichtig ist, nicht wie es funktioniert.** "Diese Zahl ist wichtiger als alle anderen" plus ein Link, statt den Mechanismus zu beschreiben
6. **Status in einem Wort.** `In Entwicklung`, `Nicht verfügbar`, `Aktuelle Version - gv 1.0.0`. Kein "zum Zeitpunkt des Schreibens", kein "nicht vor"
7. **Schreib eine Abkürzung aus, wo sie zum ersten Mal vorkommt.** Zum Beispiel eine Spalte `gv` -> `Spielversion`
8. **Sprich mit dem Leser.** Frage und Antwort sind in Ordnung: `Dir gefällt die Dokumentation nicht? Dann kannst du helfen, sie zu schreiben`. `Vielleicht möchtest du...` ist auch in Ordnung
9. **Einfache Wörter.** Ein Fachbegriff erscheint nur, wenn der Leser ihm in der Oberfläche des Spiels begegnet. Dann steht er in Backticks, genau so, wie das Spiel ihn zeigt

```
Vorher (richtig, aber schwer):
Die Zahlen folgen einander nicht. `gv` und `sv` begannen einmal gleich und dürfen jetzt frei auseinanderlaufen: Eine Änderung am SDK muss die Spielversion nicht verschieben, und ein Update des Spiels muss die SDK-Version nicht verschieben

Nachher:
Die Versionsnummern müssen einander nicht folgen, aber in den meisten Fällen stimmen sie überein.
Versionen werden außerdem gemeinsam erhöht, und ein gemeinsames Update trägt dieselbe Version
```

## Zeichensetzung

Die Zeichensetzung folgt den Regeln der Sprache, mit zwei bewussten Abweichungen. Beide sind verpflichtend

**Keine langen Striche.** Geviertstrich und Halbgeviertstrich werden gar nicht verwendet. Wo ein Strich nötig ist, schreib einen Bindestrich mit Leerzeichen davor und danach

```
Vorher:   Bullet Hero — weniger ein Spiel als ein Player für Animationen
Nachher:  Bullet Hero - weniger ein Spiel als ein Player für Animationen
```

Chinesisch und Japanisch verwenden überhaupt keinen Strich: kein `——`, kein `—` und nicht einmal einen Bindestrich mit Leerzeichen. Schreib stattdessen ein Komma, einen Doppelpunkt oder einen neuen Satz (`，` und `：` im Chinesischen, `、` und `：` im Japanischen)

```
Vorher:   Bullet Hero——与其说是游戏，不如说是动画播放器
Nachher:  Bullet Hero与其说是游戏，不如说是动画播放器

Vorher:   Bullet Hero——ゲームというより、アニメーションのプレイヤー
Nachher:  Bullet Heroはゲームというより、アニメーションのプレイヤー
```

**Kein Punkt am Ende eines Absatzes.** Punkte zwischen Sätzen innerhalb eines Absatzes bleiben. Der letzte Satz eines Absatzes, ein Listenpunkt, eine Tabellenzelle und eine Überschrift bekommen keinen Punkt. Frage- und Ausrufezeichen bleiben

**Achte auf die Zeilenumbrüche.** Markdown fügt Zeilen ohne Leerzeile dazwischen zu einem Absatz zusammen. Eine Zeile ohne Punkt, auf die eine weitere Zeile folgt, wird zu zwei aneinandergeklebten Sätzen

Deshalb endet im Englischen, Russischen, Spanischen, Deutschen, Portugiesischen und Französischen innerhalb eines Absatzes jede Zeile, auf die eine weitere folgt, mit einem Punkt. Setz vor jeden eigenständigen Gedanken eine Leerzeile

**Im Chinesischen und Japanischen ist ein Absatz eine Zeile im Quelltext.** Markdown macht aus einem Zeilenumbruch innerhalb eines Absatzes ein Leerzeichen, und dieses Leerzeichen erscheint zwischen chinesischen oder japanischen Sätzen und stört die Suche. Deshalb wird chinesischer und japanischer Text nie von Hand umbrochen, und ein Satz, der in einer eigenen Zeile stehen muss, ist ein eigener Absatz. Jeder eigenständige Gedanke bekommt eine Leerzeile davor

Weitere Zeichen:

- **Der Doppelpunkt** ist das Arbeitszeichen zum Erklären und Aufzählen, verwende ihn ruhig oft
- **Das Semikolon** wird nie verwendet. Schreib stattdessen einen Punkt oder einen eigenen Listenpunkt. Auch Chinesisch verwendet kein `；`: Schreib zwei Sätze oder ein `，`. Japanisch ebenso: zwei Sätze oder ein `、`
- **Ausrufezeichen** sind selten, höchstens eines pro langem Text
- **Anführungszeichen** sind im Englischen, Russischen, Spanischen, Deutschen, Portugiesischen und Französischen nur gerade `"Anführungszeichen"`, nie `«»` (im Deutschen auch nie `„“`). Chinesisch verwendet die vollbreiten `“”`, Japanisch `「」`, Koreanisch gerade wie das Englische
- **Klammern** passen gut für eine kurze Randbemerkung, einen Vorbehalt oder einen trockenen Witz

## Chinesisch, Japanisch, Koreanisch, Spanisch, Deutsch und Portugiesisch

Die Regeln oben gelten für jede Sprache ohne Ausnahme. Chinesisch fügt einige Punkte hinzu:

- **Sprich den Leser mit `你` an,** nie mit `您`. Ratschlag ist `建议`, die Meinung des Autors ist `我`, nie `开发者` oder `我们`
- **Vollbreite Zeichensetzung** `，。：？！（）` und Anführungszeichen `“”`. Code, Dateinamen und alles in Backticks behalten die ASCII-Zeichensetzung
- **Kein Leerzeichen zwischen Hanzi und lateinischen Buchstaben oder Ziffern,** so wie das Spiel selbst es schreibt: `在Bullet Hero中`, `60帧`
- **In lateinischen Buchstaben bleiben:** Produkt- und Formatnamen (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), Dateiendungen, Tasten, Feldnamen
- **Begriffe kommen aus `game/zh-glossary.md`.** Jeder Begriff hat eine Schreibweise, und Zeilen mit der Markierung `strict` werden immer befolgt. Eine UI-Bezeichnung wird aus dem Wert ihres Schlüssels in `game/zh.yaml` zitiert
- **Callout-Titel** sind 建议, 提示, 须知, 警告, 注意 (`> [!tip] 建议`)

Japanisch fügt diese Punkte hinzu:

- **Schreib im Register です/ます.** Der Leser wird nicht mit einem Pronomen benannt, nie `あなた`: Bau den Satz so, dass das Subjekt auch ohne klar ist. Ratschlag ist `〜することをおすすめします` oder `推奨`, die Meinung des Autors ist `私`, nie `開発者` oder `私たち`
- **Vollbreite Zeichensetzung** `、。：？！（）` und Eckklammern `「」`. Ein Zitat im Zitat ist `『』`. Code, Dateinamen und alles in Backticks behalten die ASCII-Zeichensetzung
- **Lehnwörter werden in Katakana geschrieben,** mit dem abschließenden `ー`: `インスペクター`, `レイヤー`. So schreibt sie der japanische Unity-Editor
- **Kein Leerzeichen zwischen Kana oder Kanji und lateinischen Buchstaben oder Ziffern,** so wie das Spiel selbst es schreibt: `Bullet Heroでは`, `60フレーム`
- **In lateinischen Buchstaben bleiben:** Produkt- und Formatnamen (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), Dateiendungen, Tasten, Feldnamen
- **Begriffe kommen aus `game/ja-glossary.md`.** Jeder Begriff hat eine Schreibweise, und Zeilen mit der Markierung `strict` werden immer befolgt. Eine UI-Bezeichnung wird aus dem Wert ihres Schlüssels in `game/ja.yaml` zitiert
- **Zeichensetzung gehört außerhalb der Fettmarkierung:** Schreib `**太字**。本文`, nie `**太字。**本文`. In der zweiten Form kann Markdown das `**` nicht schließen, und die Sternchen werden so gedruckt, wie sie sind
- **Callout-Titel** sind 推奨, ヒント, 補足, 警告, 注意 (`> [!tip] 推奨`)

Koreanisch fügt diese Punkte hinzu:

- **Schreib im Register 합니다체** (`-ㅂ니다`/`-습니다`). Der Leser wird nicht mit einem Pronomen benannt, nie `당신`. Ratschlag ist `권장합니다`, die Meinung des Autors ist `저`, nie `개발자` oder `저희`
- **Die Zeichensetzung ist ASCII, und Wörter werden durch Leerzeichen getrennt,** wie im Englischen, daher gelten die Regeln oben zu Strich, Punkt und Anführungszeichen wie geschrieben
- **Lehnwörter werden in Hangul geschrieben,** so wie der koreanische Unity-Editor sie schreibt: `레이어`, `인스펙터`
- **Keine nackte Partikel nach einem lateinischen Wort, Code oder einem Platzhalter,** dessen Endlaut der Satz nicht kennen kann: Schreib die Paarform `을(를)`, `이(가)` oder formuliere um
- **In lateinischen Buchstaben bleiben:** Produkt- und Formatnamen (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), Dateiendungen, Tasten, Feldnamen
- **Begriffe kommen aus `game/ko-glossary.md`.** Jeder Begriff hat eine Schreibweise, und Zeilen mit der Markierung `strict` werden immer befolgt. Eine UI-Bezeichnung wird aus dem Wert ihres Schlüssels in `game/ko.yaml` zitiert
- **Zeichensetzung oder Code am Ende einer Fettmarkierung bricht die Fettung, wenn eine Partikel folgt:** Schreib `**이름**을`, nie `**"이름"**을`
- **Callout-Titel** sind 권장, 팁, 참고, 경고, 주의 (`> [!tip] 권장`)

Spanisch fügt diese Punkte hinzu:

- **Neutrales Spanisch, ein Text für Spanien und Lateinamerika.** Der Leser ist `tú`, Singular, nie `usted`, `vosotros` oder `ustedes`. Ratschlag ist `se recomienda` oder `conviene`, nie `te recomendamos`, die Meinung des Autors ist `yo`, nie `los desarrolladores` oder `nosotros`
- **Wortschatz, der sich auf beiden Seiten des Atlantiks gleich liest:** `archivo` statt `fichero`, `equipo` oder `PC` statt `ordenador` oder `computadora`, `teléfono` oder `móvil` statt `celular`, `hacer clic` auf dem Bildschirm und `pulsar` bei einer Taste
- **Kein Adjektiv, das sich nach dem Geschlecht des Lesers richtet** (`listo`/`lista`): Formuliere darum herum
- **Die zwei Abweichungen gelten auch für die spanische Typografie:** ein Bindestrich mit Leerzeichen ` - ` statt der Raya (auch bei Einschüben und Dialogen), gerade Anführungszeichen statt `«»`, kein Punkt am Ende eines Absatzes, eines Listenpunkts, einer Tabellenzelle oder einer Überschrift. Kein `;`
- **`¿…?` und `¡…!` haben immer beide Zeichen**
- **Überschriften und Titel in Satzschreibung** (`## Cómo funciona el ajuste`), nie in Title Case. Ein Großbuchstabe behält seinen Akzent (`Á`, `É`)
- **Nicht übersetzt:** Produkt- und Formatnamen (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), Dateiendungen, Tasten, Feldnamen
- **Begriffe kommen aus `game/es-glossary.md`.** Jeder Begriff hat eine Schreibweise, und Zeilen mit der Markierung `strict` werden immer befolgt. Eine UI-Bezeichnung wird aus dem Wert ihres Schlüssels in `game/es.yaml` zitiert
- **Callout-Titel** sind Recomendación, Consejo, Conviene saber, Advertencia, Precaución (`> [!tip] Recomendación`). `More - [[page]]` wird `Más - [[page]]` geschrieben

Deutsch fügt diese Punkte hinzu:

- **Standarddeutsch für Deutschland,** keine österreichische oder schweizerische Variante. Der Leser ist `du`, kleingeschrieben (`du`, `dein`, `dich`), nie `Sie` oder `ihr`. Ratschlag ist `es empfiehlt sich` oder `am besten`, nie `wir empfehlen`, die Meinung des Autors ist `ich`, nie `die Entwickler` oder `wir`
- **Der übliche Wortschatz deutscher Software:** `Datei`, `Einstellungen`, `speichern`, `herunterladen`. `ß`, wo die Rechtschreibung es verlangt, nie das große `ẞ`
- **Lehnwörter so, wie das Glossar sie führt** (`Keyframe`, `Prefab`, `Hitbox`, `Beat`): großgeschrieben, mit deutschem Artikel
- **Die zwei Abweichungen gelten auch für die deutsche Typografie:** ein Bindestrich mit Leerzeichen ` - ` statt des Gedankenstrichs, gerade Anführungszeichen statt `„“` oder `»«`, kein Punkt am Ende eines Absatzes, eines Listenpunkts, einer Tabellenzelle oder einer Überschrift. Kein `;`
- **Überschriften und Titel in deutscher Satzschreibung:** das erste Wort und jedes Nomen groß, sonst nichts (`## Wie das Einrasten funktioniert`), nie englische Title Case
- **Nicht übersetzt:** Produkt- und Formatnamen (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), Dateiendungen, Tasten, Feldnamen
- **Begriffe kommen aus `game/de-glossary.md`.** Jeder Begriff hat eine Schreibweise, und Zeilen mit der Markierung `strict` werden immer befolgt. Eine UI-Bezeichnung wird aus dem Wert ihres Schlüssels in `game/de.yaml` zitiert
- **Callout-Titel** sind Empfehlung, Tipp, Gut zu wissen, Warnung, Vorsicht (`> [!tip] Empfehlung`). `More - [[page]]` wird `Mehr - [[page]]` geschrieben

Portugiesisch fügt diese Punkte hinzu:

- **Brasilianisches Portugiesisch, der Code `pt` trägt keine Region.** Der Leser ist `você` mit Verben in der dritten Person, nie `tu`, `o senhor` oder `vocês`. Ratschlag ist `recomenda-se` oder `vale a pena`, nie `recomendamos`, die Meinung des Autors ist `eu`, nie `os desenvolvedores` oder `nós`
- **Brasilianischer Wortschatz, nie europäischer:** `arquivo` statt `ficheiro`, `tela` statt `ecrã`, `salvar` statt `guardar`, `mouse` statt `rato`, `celular` statt `telemóvel`, `baixar` statt `transferir`. `estar` mit Gerundium (`está carregando`), nie `estar a` mit Infinitiv
- **Kein Adjektiv, das sich nach dem Geschlecht des Lesers richtet** (`pronto`/`pronta`): Formuliere darum herum
- **Die zwei Abweichungen gelten auch für die portugiesische Typografie:** ein Bindestrich mit Leerzeichen ` - ` statt des Travessão, gerade Anführungszeichen statt `«»` oder `“”`, kein Punkt am Ende eines Absatzes, eines Listenpunkts, einer Tabellenzelle oder einer Überschrift. Kein `;`
- **Überschriften und Titel in Satzschreibung** (`## Como funciona o encaixe`), nie in Title Case. Ein Großbuchstabe behält seinen Akzent (`É`, `Ã`)
- **Nicht übersetzt:** Produkt- und Formatnamen (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), Dateiendungen, Tasten, Feldnamen
- **Begriffe kommen aus `game/pt-glossary.md`.** Jeder Begriff hat eine Schreibweise, und Zeilen mit der Markierung `strict` werden immer befolgt. Eine UI-Bezeichnung wird aus dem Wert ihres Schlüssels in `game/pt.yaml` zitiert
- **Callout-Titel** sind Recomendação, Dica, Vale saber, Aviso, Cuidado (`> [!tip] Recomendação`). `More - [[page]]` wird `Mais - [[page]]` geschrieben

Französisch fügt diese Punkte hinzu:

- **Französisch, wie es in Frankreich geschrieben wird,** in Belgien, der Schweiz und Kanada genauso gelesen. Der Leser ist `tu`, nie `vous`. Ratschlag ist `il vaut mieux` oder `mieux vaut`, nie `nous te recommandons`, die Meinung des Autors ist `je`, nie `les développeurs` oder `nous`
- **Der übliche Wortschatz französischer Software:** `fichier`, `paramètres`, `enregistrer`, `souris`, `écran`, `cliquer` auf dem Bildschirm und `appuyer sur` bei einer Taste
- **Kein Adjektiv, das sich nach dem Geschlecht des Lesers richtet** (`prêt`/`prête`): Formuliere darum herum
- **Die zwei Abweichungen gelten auch für die französische Typografie:** ein Bindestrich mit Leerzeichen ` - ` statt des Tiret (auch bei Einschüben), gerade Anführungszeichen statt `«»`, der gerade Apostroph `'`, kein Punkt am Ende eines Absatzes, eines Listenpunkts, einer Tabellenzelle oder einer Überschrift. Kein `;`
- **Ein geschütztes Leerzeichen (U+00A0) vor `?`, `!` und `:`,** auch vor `%` nach einer Zahl, nie ein normales Leerzeichen und nie gar keins. Code und alles in Backticks behält seinen eigenen Text
- **Überschriften und Titel in Satzschreibung** (`## Comment fonctionne l'aimantation`), nie in Title Case. Ein Großbuchstabe behält seinen Akzent (`É`, `À`)
- **Nicht übersetzt:** Produkt- und Formatnamen (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), Dateiendungen, Tasten, Feldnamen
- **Begriffe kommen aus `game/fr-glossary.md`.** Jeder Begriff hat eine Schreibweise, und Zeilen mit der Markierung `strict` werden immer befolgt. Eine UI-Bezeichnung wird aus dem Wert ihres Schlüssels in `game/fr.yaml` zitiert
- **Callout-Titel** sind Recommandation, Conseil, Bon à savoir, Avertissement, Attention (`> [!tip] Recommandation`). `More - [[page]]` wird `Plus - [[page]]` geschrieben

## Gestaltung

- **Kurze Absätze,** eine bis drei Zeilen
- **Eine Aufzählung** für jede Aufzählung mit mehr als zwei Elementen. Nummerierte Listen nur für Schritte und Auswahlmöglichkeiten
- **Eine Tabelle** überall dort, wo drei oder mehr Dinge nach mehreren Eigenschaften verglichen werden
- **Kursiv** (`*text*`) für Begriffe, Produktnamen und Genres: *musical bullet hell*, *Geometry Dash*. Auf Kursivschrift ist in chinesischen und japanischen Schriften kein Verlass, deshalb steht sie in diesen Sprachen nur auf Produktnamen in lateinischen Buchstaben, und betont wird fett
- **Fett**, um ein Wort zu betonen oder einen Absatz mit seinem Thema zu eröffnen
- **Backticks** für alles Technische: Dateien, Felder, Formate, Werte, Tasten, Befehle
- **Eine Version ist immer ihr Präfix plus die Nummer, in Backticks:** `gv 1.0.0`, `sv 1.1.0`, `fv 1.0.0`, `bv 1.0.0`, `mg 2`. Nie eine nackte `1.0.0`, "Version 1.0.0" oder "SDK 1.0.0" ohne Präfix. In `title` und `# H1` funktionieren Backticks nicht, dort steht also schlicht `gv 1.0.0`. Versionen fremder Dinge (Unity, NuGet-Pakete) sind nicht unsere und werden so geschrieben, wie sie sind
- **Keine Emoji**

## Callouts

Ein Absatz mit einem konkreten Zweck wird zu einem Callout. Es gibt genau fünf, und der Titel wird in der Sprache der Seite geschrieben:

| Callout | Englischer Titel | Russischer Titel | Chinesischer Titel | Japanischer Titel | Koreanischer Titel | Spanischer Titel | Deutscher Titel | Portugiesischer Titel | Französischer Titel | Was er einleitet |
|---|---|---|---|---| --- |---|---|---|---|---|
| `> [!tip] Recommendation` | Recommendation | Рекомендация | 建议 | 推奨 | 권장 | Recomendación | Empfehlung | Recomendação | Recommandation | mach es so |
| `> [!tip]` | Tip | Подсказка | 提示 | ヒント | 팁 | Consejo | Tipp | Dica | Conseil | eine Abkürzung, ein Trick, ein schnellerer Weg |
| `> [!info]` | Worth knowing | Интересно | 须知 | 補足 | 참고 | Conviene saber | Gut zu wissen | Vale saber | Bon à savoir | Kontext, der eine Entscheidung erklärt |
| `> [!warning]` | Warning | Предупреждение | 警告 | 警告 | 경고 | Advertencia | Warnung | Aviso | Avertissement | das kostet Zeit oder Qualität |
| `> [!caution]` | Caution | Внимание | 注意 | 注意 | 주의 | Precaución | Vorsicht | Cuidado | Attention | das zerstört Arbeit oder liefert ein kaputtes Level aus |

**Höchstens zwei Callouts pro Seite,** denn ein dritter wirkt nicht mehr als Betonung. Referenzseiten dürfen zwei pro Abschnitt haben. Eine Seite über etwas, das es noch nicht gibt, beginnt mit einem `> [!warning]` zu seinem Status, und dieser zählt nicht zur Grenze

## Stimme

- **Sprich den Leser mit "du" an** (im Russischen mit dem förmlichen "вы", kleingeschrieben, im Chinesischen mit `你`, im Spanischen mit `tú`, nie `usted`, im Deutschen mit `du`, kleingeschrieben, nie `Sie`, im Portugiesischen mit `você`, im Französischen mit `tu`, nie `vous`). Japanisch benennt den Leser nicht mit einem Pronomen und verwendet nie `あなた`
- **Das Projekt spricht unpersönlich,** nie als "die Entwickler" oder "wir". Ratschlag ist "es empfiehlt sich" (im Englischen "it is recommended", im Russischen "рекомендуется", im Chinesischen `建议`, im Japanischen `〜することをおすすめします` oder `推奨`, im Spanischen `se recomienda` oder `conviene`, im Deutschen auch `am besten`, im Portugiesischen `recomenda-se` oder `vale a pena`, im Französischen `il vaut mieux` oder `mieux vaut`), und ein Fakt hat die Sache selbst als Subjekt: "Das Spiel liefert überhaupt keine Texturen mit"
- **Die Meinung oder Entscheidung des Autors steht in der ersten Person,** "ich empfehle" (im Russischen "я рекомендую", im Chinesischen `我建议`, im Japanischen `私は〜をおすすめします`). Das Spiel macht eine Person, deshalb ist "ich" hier ehrlich. Nur für ein echtes Urteil oder eine echte Entscheidung, nicht für schlichte Fakten
- **Notizen in `notes/` dürfen in der ersten Person sprechen,** denn eine Notiz ist der Bericht ihres Autors
- **Keine Geschichte in der Dokumentation.** Eine Dokumentationsseite beschreibt, wie die Dinge jetzt funktionieren. "Früher war es X" ist eine Notiz
- **Keine Behauptungen, besser zu sein.** Ein Vergleich ist nur erlaubt, wenn er dem Leser hilft, schneller zu verstehen
- **Nenne die Grenzen des Wissens.** "Höchstwahrscheinlich", "noch nicht bekannt". Falsche Gewissheit ist schlimmer als Nichtwissen
- **Jedes Urteil kommt mit seinem Grund.** Ein Adjektiv ohne Grund ist ein Mangel
- **Zahlen statt Adjektiven.** Sekunden, Frames, Megabyte, Versionen, Objektzahlen
- **Ironie ist trocken und selten,** eine kurze Randbemerkung in Klammern. Referenzseiten haben fast keine
- **Keine Kraftausdrücke** in keiner Sprache, auch keine derben Ersatzwörter
- **Erfinde nie** eine Adresse, eine Zahl oder einen Fakt. Ohne Quelle sag, dass es unbekannt ist

## Seiteneinstieg

**Der Einstieg antwortet, er kündigt nicht an.** Er beschreibt nicht die Seite ("was X ist, wie Y funktioniert und wo Z liegt"), er gibt eine kurze Antwort auf die Frage, für die es die Seite gibt. So ein Einstieg ist für sich allein nützlich, auch wenn der Leser nicht weiterliest

**Der Kern gehört in den ersten Absatz.** Er ist auch die Beschreibung in Listen, in der Suche und in Linkvorschauen: nach 200 Zeichen abgeschnitten, ohne Links und Formatierung. Die Antwort darf im zweiten und dritten Absatz weitergehen

**Teile eine kurze Seite nicht auf.** Gibt es wenig Inhalt, verschmilzt der Einstieg mit dem Text, statt ihn als eigene Zeile obendrauf zu wiederholen

```
Vorher:
Wo man einen Bug meldet oder eine Frage stellt und was man schreibt, damit sich der Bug nachstellen lässt

Nachher:
Bugs im Spiel gehören in die Issues von releases, Fragen auf Discord. Füge die Versionszeile aus den Einstellungen und die Schritte bei, die zum Bug führen
```

## Aufbau einer Seite

1. `# H1` und ein Einstieg, der die Frage der Seite beantwortet
2. Der Text wiederholt den Einstieg nicht, er liefert die Details, Fälle und Schritte
3. `##`-Abschnitte, jeder zu einem Thema: die Aussage, dann der Mechanismus oder die Schritte, dann das Fazit
4. Wo es passt, konkrete Ratschläge oder Links zum Weiterlesen am Ende
5. Das Ende erzählt die Seite nie nach

Eine Anleitungsseite braucht 2 bis 4 Minuten zum Lesen, etwa 2000 bis 3500 Zeichen. Eine Referenzseite darf länger sein, aber jeder Abschnitt steht für sich

## Was einen fremden Text verrät

- ein langer Strich, ein Punkt am Ende eines Absatzes, ein Semikolon
- "Das ist nicht nur X, das ist ein ganzes Y"
- Dreierfiguren als Schmuck: "schneller, billiger, zuverlässiger"
- leere Einstiege: "in der heutigen Welt", "tauchen wir ein", "es ist kein Geheimnis, dass"
- ein Schlussabsatz, der wiederholt, was schon gesagt wurde
- begeisterte Adjektive ohne Grund: "unglaublich", "erstaunlich", "ein mächtiges Werkzeug"
- höfliche Füllsätze und Entschuldigungen beim Leser
- symmetrische Formulierungen, die für den Rhythmus statt für den Sinn geschrieben sind
- allgemeine Ratschläge, die niemand an diesem Spiel überprüft hat

## Vorher und nachher

**Ein Einstiegsabsatz**

```
Vorher:
In der heutigen Welt des Leveldesigns nimmt der Editor von Bullet Hero einen besonderen Platz ein — er ist nicht nur ein
Werkzeug, er ist ein ganzes Ökosystem. Tauchen wir ein und sehen wir uns an, warum.

Nachher:
Der Editor baut ein Level aus Objekten, die auf einem Zeitabschnitt leben und sich entlang von Keyframes bewegen. Unten steht, wie er aufgebaut ist und in welcher Reihenfolge man mit ihm arbeitet
```

**Ein Urteil**

```
Vorher:
Das Blob-Format ist eine erstaunliche Lösung, die das Laden drastisch beschleunigt und deinen Arbeitsablauf produktiver macht.

Nachher:
`Blob` lädt schneller als `Json`, lässt sich aber weder mit bloßem Auge lesen noch in git vergleichen. Halte ein Level in `Json`, solange du daran arbeitest, und wandle es vor dem Veröffentlichen in `Blob` um
```

**Etwas, das es noch nicht gibt**

```
Vorher:
Der offizielle Server wird eine bequeme Möglichkeit bieten, deine Levels mit der ganzen Welt zu teilen.

Nachher:
Einen offiziellen Server gibt es noch nicht. Das Protokoll, über das das Spiel mit ihm sprechen wird, ist noch nicht entworfen, deshalb beschreibt diese Seite nur, was bereits entschieden ist
```

## Checkliste vor einem Pull Request

1. Die Seite lässt sich überfliegen: ein Gedanke pro Satz, Details weiter unten auf der Seite oder auf einer eigenen Seite
2. Keine Geviertstriche und keine Halbgeviertstriche (Chinesisch und Japanisch verwenden gar keinen Strich)
3. Kein Absatz, kein Listenpunkt und keine Überschrift endet mit einem Punkt
4. Keine aneinandergeklebten Zeilen: Jeder eigenständige Gedanke ist ein eigener Absatz oder innerhalb der Zeile durch einen Punkt abgetrennt. Ein chinesischer oder japanischer Absatz ist eine Zeile im Quelltext
5. Keine Semikolons, keine Emoji, höchstens ein Ausrufezeichen
6. Keine Kraftausdrücke
7. Kommas, Doppelpunkte und Kongruenz folgen der Norm, keine Tippfehler
8. Jedes Urteil hat seinen Grund daneben
9. Zahlen, Feldnamen und Links kommen aus einer Quelle
10. Kein "die Entwickler" oder "wir" in `docs/`: Ratschläge sind unpersönlich, "ich" nur für die Meinung oder Entscheidung des Autors
11. Höchstens zwei Callouts
12. Der Einstieg nach der H1 beantwortet die Frage der Seite (der Kern innerhalb der ersten 200 Zeichen), beschreibt die Seite nicht und wird unten nicht wiederholt
13. Das Ende erzählt die Seite nicht nach
