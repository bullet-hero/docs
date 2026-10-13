# German term base

The terms `de.yaml` (standard German) is translated with. Every value in `de.yaml` follows this table: a thing is
named the same way on every screen, in every hint, in every tooltip.

- **`strict`** rows are checked by the game's tests: whenever the English value of a key contains the `en` term (a
  whole word, any case, tags ignored, a plural `s`/`es` included), its German value must contain the `de` term.
- The check is a plain substring match, any case, umlauts included, so a `strict` cell is the part every form of the
  term and its usual compounds share: `Ebene` covers `Ebenen` and `Objektebene`, `Anker` covers `verankert`, `rast`
  covers `einrasten` and `rastet ein`. Where the full term is longer (`Beat-Segment`), the cell is the shared part and
  the note gives the full term. Where an umlaut or a stem change leaves no shared part anyone would recognise as a
  word, the row is `loose`.
- **`loose`** rows are guidance: a common word whose best translation depends on the sentence around it. Follow them
  unless the sentence reads wrong, and never use a `loose` row's `de` for a different concept.
- A row whose `de` is the same Latin text as `en` means "keep it in Latin" - product names, formats, keys.
- Loanwords follow the German Unity editor and the German-speaking rhythm-game communities (osu!, Geometry Dash): a
  German word where they use one (`Ebene`, `Zeitleiste`, `Abspielkopf`), the English word where they keep it
  (`Keyframe`, `Prefab`, `Gizmo`, `Checkpoint`, `Hitbox`, `Beat`). A kept English noun is capitalised and takes a
  German article (`das Level`, `der Keyframe`, `das Prefab`).
- Standard German as written in Germany: `du` in lowercase, never `Sie`, a button is an infinitive (`Speichern`,
  `Übernehmen`), German capitalisation (the first word and every noun, never English Title Case), `ß` where the
  spelling has it (`Größe`).

The canonical meanings are the [glossary](../en/docs/2_editor/7_reference/1_glossary.md). To propose a change, open an
issue or a pull request that edits this table and every `de.yaml` value that uses the term, in one change.

Punctuation, labels and the rest of the house style for German: `Assets/Addressables/TEXT-STYLE.md`, section 13, in
the game's repository.

| en | de | kind | note |
|---|---|---|---|
| Level | Level | strict | Alles, was eine Partie ausmacht: Objekte, Audio, Ereignisse und eigene Ressourcen. "das Level", Plural "Levels", zusammengesetzt "Leveleditor". Das "level" beim Ton ist etwas anderes: "Lautstärke" oder "Signalpegel" |
| Object | Objekt | strict | Was der Autor auf der Zeitleiste erstellt, mit eigener Spanne, Transformation und eigenem Elternobjekt. "Objekt" steckt auch in "Elternobjekt" und "Objektebene" |
| Rect | leeres Objekt | loose | Objekt, das nichts zeichnet: nur Transformation, Spanne und Kinder. Wie in ru zwei Wörter: der Typ ist "leeres Objekt", die geometrische Form ist "Rechteck" |
| Shape | Form | loose | Echte Geometrie, die ein Objekt zeichnet, kein Bild. Das Spiel erzeugt rund 500 davon selbst |
| Collider | Collider | strict | Womit ein Objekt kollidiert. Muss nicht dem entsprechen, was es zeichnet. Englisch, wie in Unity. "der Collider", Plural "Collider" |
| Prefab | Prefab | strict | Wiederverwendbare Vorlage aus Objekten, die beliebig oft in ein Level gesetzt wird. Englisch, wie in Unity. "das Prefab", Plural "Prefabs" |
| Prefab Mode | Prefab-Modus | strict | Den eigenen Inhalt einer Vorlage bearbeiten statt des umgebenden Levels |
| Effect | Effekt | loose | Objekt, das in jedem Frame aus wenigen Parametern eigene Objekte erzeugt. Bloom, Vignette usw. sind "Post-Processing-Effekte", nie nur "Effekt" |
| Inframe Object | Frame-Objekt | loose | Von einem Effekt erzeugtes Objekt. Die Engine verwaltet es: nicht auswählbar, nicht bearbeitbar |
| Theme | Theme | strict | Palette, auf die das Level per Index verweist: Umfärben ist eine Änderung, nicht hundert. "das Theme", Plural "Themes". Ein Lied ist hier nie "Theme", sondern "Song" |
| Frame | Frame | strict | Zeiteinheit des Levels. Ein Frame ist eine Zelle, die Zeit ist die Grenze zwischen zwei Zellen. "der Frame", nie "Bild" |
| Keyframe | Keyframe | strict | Vom Autor in einem Frame festgelegter Wert, dazwischen wird interpoliert. Englisch, wie in Unity. "der Keyframe", Plural "Keyframes" |
| Key | Keyframe | loose | Kurzform von Keyframe. Die Taste der Tastatur ist "Taste", der Lokalisierungsschlüssel ist "Schlüssel" |
| Track | Spur | strict | Reihe von Keyframes einer animierbaren Eigenschaft: Position, Drehung, Lautstärke. Plural "Spuren", Audio Track ist "Audiospur". Das Verb "track" (verfolgen) ist nie "Spur" |
| Timeline | Zeitleiste | strict | Achse aus Frames, auf der das Level bearbeitet wird, ein Tab pro Inhaltsart. Plural "Zeitleisten" |
| Span | Spanne | loose | Wann ein Objekt existiert: Startframe und Dauer, kein Endframe. Das Verb span ("umfassen") ist nie "Spanne". Nicht "Segment", das ist Beat Segment |
| Playhead | Abspielkopf | strict | Der Frame, der gerade angezeigt wird |
| Ease | Easing | strict | Wie der Wert vom vorigen Keyframe zu diesem übergeht. "das Easing". Nicht Curve ("Kurve") und nicht Kantenglättung |
| Marker | Marker | strict | Benannter Punkt auf dem Lineal des Levels, um genau dorthin zurückzuspringen. "der Marker", Plural "Marker" |
| Checkpoint | Checkpoint | strict | Wohin ein Tod den Spieler zurückbringt. Englisch, wie in der Geometry-Dash-Community und wie in ru. "der Checkpoint", Plural "Checkpoints" |
| Anchor | Anker | strict | Kante, die der Kante des Elternobjekts folgt: schrumpft das Elternobjekt, wandert das Kind mit. "Anker" steckt auch in "verankert" und "Verankerung" |
| Layer | Ebene | strict | Zeichenreihenfolge relativ zum Elternobjekt: die Ebene des Kindes wird zu der des Elternobjekts addiert. Plural "Ebenen", wie im deutschen Unity |
| Pivot | Drehpunkt | loose | Punkt, um den sich das Objekt dreht und skaliert, innerhalb seines eigenen Rahmens |
| Gizmo | Gizmo | strict | Ziehgriffe, die im Viewport über dem ausgewählten Objekt gezeichnet werden. Englisch, wie in Unity. "das Gizmo", Plural "Gizmos" |
| Snapping | Einrasten | strict | Ein Ziehen an etwas ausrichten: mit dem Magneten an den Inhalt, mit dem Beat-Schalter an die Musik. Das Partizip "eingerastet" enthält "Einrasten" nicht, dort deckt Snap ("rast") ab. Settings ist "Einstellungen" |
| Snap | rast | strict | Wie Snapping. Die Zelle ist "rast", das "einrasten", "rastet ein" und "eingerastet" teilen. Achtung: "Raster" (Grid) und "Kontrast" enthalten "rast" auch, zählen aber nicht als Einrasten. Fit ist "Einpassen", nie "einrasten" |
| Beat | Beat | strict | Das eigene Raster der Musik: der Autor legt es fest, im Spiel liest es nichts. "der Beat", Plural "Beats". Nicht "Takt", das ist Bar |
| Beat Segment | Segment | strict | Voller Begriff "Beat-Segment". Abschnitt mit konstantem Tempo, eigener Phase und Taktlänge. Nicht "Spanne", das ist Span |
| BPM | BPM | strict | Beats pro Minute. Lateinisch, wie in den Rhythmusspiel-Communities |
| Tap | Tippen | loose | Ein Antippen beim Einklopfen des Tempos, auf dem Touchscreen ebenso. Enthält "Tipp" (Tip), ist aber kein Tipp |
| Generator | Generator | strict | Automatisiertes Erstellen: erzeugt Levelinhalt aus wenigen Parametern. Plural "Generatoren" |
| Modifier | Modifikator | strict | Generator, der Vorhandenes bearbeitet oder entfernt, statt hinzuzufügen. Plural "Modifikatoren". Die Taste ist Modifier Key ("Modifikatortaste") |
| Seed | Seed | strict | Die Zahl, aus der jeder Zufallswert des Levels entsteht: derselbe Seed ergibt genau dasselbe. "der Seed" |
| Raw Data | Rohdaten | strict | Das ganze gespeicherte Modell als bearbeitbarer Baum. Hier wird absichtlich nichts validiert |
| Recommendation | Empfehlung | strict | Eines der fünf Labels: `<b>Empfehlung:</b>`, der folgende Satz beginnt klein, außer das erste Wort ist ein Nomen |
| Tip | Tipp | strict | Eines der fünf Labels: `<b>Tipp:</b>`, der folgende Satz beginnt klein, außer das erste Wort ist ein Nomen |
| Worth knowing | Gut zu wissen | strict | Eines der fünf Labels: `<b>Gut zu wissen:</b>`, der folgende Satz beginnt klein, außer das erste Wort ist ein Nomen |
| Warning | Warnung | strict | Eines der fünf Labels: `<b>Warnung:</b>`, der folgende Satz beginnt klein, außer das erste Wort ist ein Nomen |
| Caution | Vorsicht | strict | Eines der fünf Labels: `<b>Vorsicht:</b>`, der folgende Satz beginnt klein, außer das erste Wort ist ein Nomen |
| More | Mehr | loose | Die letzte Linkzeile einer Hilfe, `More:`, ist `Mehr:` |
| Bullet Hero | Bullet Hero | strict | Produktname. Wird nicht übersetzt |
| Steam | Steam | loose |  |
| JSON | JSON | strict | Formatname. Wird nicht übersetzt |
| MSAA | MSAA | strict | Technisches Kürzel. Wird nicht übersetzt |
| FXAA | FXAA | strict | Technisches Kürzel. Wird nicht übersetzt |
| HDR | HDR | loose |  |
| VFX | VFX | loose |  |
| URL | URL | loose |  |
| Ctrl | Ctrl | loose | Tasten bleiben lateinisch, nicht "Strg" |
| Shift | Shift | loose | Lateinisch, nicht "Umschalt" |
| Enter | Enter | loose | Lateinisch, nicht "Eingabe" |
| Hierarchy | Hierarchie | strict | Editorbereich, der die Objekte nach Eltern-Kind-Beziehung auflistet. Das Hierarchy-Fenster von Unity heißt "Hierarchie" |
| Inspector | Inspector | strict | Editorbereich mit den Eigenschaften der Auswahl. Englisch, wie in Unity. "der Inspector" |
| Viewport | Viewport | strict | Editorbereich, der den Bildschirm des Levels zeigt. "der Viewport". Die Befehlskategorie View ist "Ansicht" |
| Command Palette | Befehlspalette | strict | Fenster, das einen Befehl nach Namen sucht und ausführt. Wie in VS Code auf Deutsch |
| Command | Befehl | loose |  |
| Selection | Auswahl | loose |  |
| Select | Auswählen | loose |  |
| Marquee | Rechteckauswahl | strict | Auswählen durch Aufziehen eines Rechtecks |
| Apply | Übernehmen | loose |  |
| Reset | Zurücksetzen | loose |  |
| Cancel | Abbrechen | loose |  |
| Confirm | Bestätigen | loose |  |
| OK | OK | loose | Die OK-Schaltfläche bleibt im Deutschen "OK" |
| Save | Speichern | loose |  |
| Load | Laden | loose |  |
| Open | Öffnen | loose |  |
| Close | Schließen | loose |  |
| Exit | Beenden | loose |  |
| Create | Erstellen | loose |  |
| Add | Hinzufügen | loose |  |
| Remove | Entfernen | loose | Anders als Delete ("Löschen"): Remove nimmt etwas aus einer Liste, Delete löscht es |
| Delete | Löschen | loose |  |
| Duplicate | Duplizieren | loose |  |
| Copy | Kopieren | loose |  |
| Paste | Einfügen | loose |  |
| Cut | Ausschneiden | loose |  |
| Undo | Rückgängig | loose |  |
| Redo | Wiederholen | loose |  |
| History | Verlauf | loose | Anders als Story ("Geschichte") |
| Edit | Bearbeiten | loose | Als Menükategorie ebenfalls "Bearbeiten" |
| Rename | Umbenennen | loose |  |
| Move | Verschieben | loose |  |
| Import | Importieren | loose |  |
| Export | Exportieren | loose |  |
| Archive | Archiv | loose | Tragbarer Container eines Levels oder einer Sammlung. Nie nur "Datei", das ist File |
| Folder | Ordner | loose |  |
| File | Datei | loose |  |
| Search | Suchen | loose | Als Nomen "Suche" |
| Filter | Filtern | loose | Als Nomen "Filter" |
| Refresh | Aktualisieren | loose |  |
| Toggle | Umschalten | loose | Ein Schalter für Anzeigen und Ausblenden darf "Ein-/Ausblenden" heißen |
| Show | Anzeigen | loose |  |
| Hide | Ausblenden | loose |  |
| Hidden | ausgeblendet | loose |  |
| Visible | sichtbar | loose |  |
| Enabled | aktiviert | loose |  |
| Disabled | deaktiviert | loose |  |
| On | An | loose | Zustand eines Schalters |
| Off | Aus | loose |  |
| None | Keine | loose | Richtet sich nach dem Nomen ("kein" für einen Effekt, "keine" für eine Form) |
| Auto | Automatisch | loose |  |
| Custom | Benutzerdefiniert | loose |  |
| Default | Standard | loose |  |
| All | Alle | loose |  |
| Nothing | Nichts | loose |  |
| Current | Aktuell | loose |  |
| Active | Aktiv | loose |  |
| Global | Global | loose |  |
| Local | Lokal | loose |  |
| Parent | Elternobjekt | loose | Kurz auch "Eltern" |
| Child | Kindobjekt | loose | Kurz auch "Kind" |
| Root | Wurzel | loose |  |
| Fold | Einklappen | loose |  |
| Unfold | Aufklappen | loose |  |
| Flatten | Auflösen | loose | Eine Verschachtelung auf eine Ebene bringen |
| Transform | Transformation | loose |  |
| Position | Position | loose |  |
| Rotation | Drehung | loose |  |
| Scale | Skalierung | loose |  |
| Size | Größe | loose |  |
| Offset | Versatz | loose |  |
| Angle | Winkel | loose |  |
| Radius | Radius | loose |  |
| Width | Breite | loose |  |
| Height | Höhe | loose |  |
| Min | Min. | loose |  |
| Max | Max. | loose |  |
| Step | Schritt | loose |  |
| Random | Zufällig | loose |  |
| Rnd | Zuf. | loose | Kurzform von "zufällig" in kurzen Labels |
| From | Von | loose |  |
| To | Bis | loose |  |
| Value | Wert | loose |  |
| Type | Typ | loose |  |
| Name | Name | loose |  |
| Mode | Modus | loose |  |
| Count | Anzahl | loose |  |
| Speed | Geschwindigkeit | loose | In kurzen Feld- und Spaltenbeschriftungen "Tempo" (Spielertempo, Kurven nach Tempo), weil "Geschwindigkeit" nicht passt. In Fließtext "Geschwindigkeit" |
| Velocity | Geschwindigkeit | loose |  |
| Gravity | Schwerkraft | loose |  |
| Particle | Partikel | loose |  |
| Orbital | Orbital | loose |  |
| Lifetime | Lebensdauer | loose |  |
| Color | Farbe | loose |  |
| Alpha | Alpha | loose |  |
| Opacity | Deckkraft | loose |  |
| Opaque | Deckend | loose |  |
| Transparent | Transparent | loose |  |
| Gradient | Verlauf | loose |  |
| Texture | Textur | loose |  |
| Font | Schriftart | loose |  |
| Text | Text | loose |  |
| Localized Text | Lokalisierter Text | loose |  |
| Language | Sprache | loose |  |
| Audio | Audio | loose |  |
| Audio Track | Audiospur | loose |  |
| Volume | Lautstärke | loose |  |
| Music | Musik | loose |  |
| Sound | Sound | loose |  |
| Resource | Ressource | loose |  |
| Resources | Ressourcen | loose |  |
| Metadata | Metadaten | loose |  |
| Meta | Meta | loose |  |
| License | Lizenz | loose |  |
| Author | Autor | loose |  |
| Artist | Künstler | loose |  |
| Settings | Einstellungen | loose | Enthält kein "rast", kollidiert also nicht mit Snap |
| Editor | Editor | loose |  |
| Game | Spiel | loose |  |
| Player | Spieler | loose |  |
| Avatar | Avatar | loose |  |
| Dash | Dash | loose | Englisch, wie in der Geometry-Dash-Community |
| Hitbox | Hitbox | loose |  |
| Damage | Schaden | loose |  |
| Health | Leben | loose |  |
| Death | Tod | loose |  |
| Camera | Kamera | loose |  |
| Zoom | Zoom | loose |  |
| Pan | Schwenken | loose |  |
| Shake | Erschütterung | loose | Kameraerschütterung, auch in Spur- und Foldout-Namen. Nicht "Beben" oder "Wackeln" |
| Grid | Raster | loose | Enthält "rast", ist aber kein Einrasten (Snap) |
| Ruler | Lineal | loose |  |
| Loop | Schleife | loose |  |
| Play | Abspielen | loose | Im Editor "Abspielen", das Level spielen ist "Spielen" |
| Pause | Pausieren | loose | Als Nomen "Pause" |
| Stop | Stoppen | loose |  |
| Preview | Vorschau | loose |  |
| Render | Rendering | loose |  |
| Post-processing | Post-Processing | loose |  |
| Post | Post-Processing | loose | Kurzform von Post-processing |
| Bloom | Bloom | loose |  |
| Vignette | Vignette | loose |  |
| Chromatic Aberration | Chromatische Aberration | loose |  |
| Lens Distortion | Linsenverzerrung | loose |  |
| Film Grain | Filmkörnung | loose |  |
| Grain | Körnung | loose |  |
| Motion Blur | Bewegungsunschärfe | loose |  |
| Blur | Unschärfe | loose |  |
| Color Curves | Farbkurven | loose |  |
| Curve | Kurve | loose | Nicht Ease ("Easing") |
| Lift Gamma Gain | Lift/Gamma/Gain | loose | Regler der Farbkorrektur, englisch |
| Shadows Midtones Highlights | Tiefen/Mitteltöne/Lichter | loose |  |
| White Balance | Weißabgleich | loose |  |
| Analog Glitch | Analoger Glitch | loose |  |
| Digital Glitch | Digitaler Glitch | loose |  |
| Glitch | Glitch | loose |  |
| Gamma | Gamma | loose |  |
| Background | Hintergrund | loose |  |
| Framerate | Framerate | loose |  |
| Fixed Framerate | Feste Simulationsrate | loose | Wie in ru zwei Bedeutungen: in den Einstellungen die Aktualisierungsrate der Simulation, anderswo "feste Framerate" |
| Collision | Kollision | loose |  |
| Screen Limit | Bildschirmgrenze | loose |  |
| Cursor | Cursor | loose |  |
| Control | Steuerung | loose |  |
| Controls | Steuerung | loose |  |
| Keybinding | Tastenbelegung | loose |  |
| Shortcut | Tastenkürzel | loose |  |
| Button | Schaltfläche | loose | Am Gamepad "Taste" |
| Interface | Oberfläche | loose |  |
| Screen | Bildschirm | loose |  |
| Window | Fenster | loose |  |
| Panel | Bereich | loose |  |
| Tab | Tab | loose |  |
| Menu | Menü | loose |  |
| Tool | Werkzeug | loose |  |
| Library | Bibliothek | loose |  |
| Bot | Bot | loose |  |
| Tutorial | Tutorial | loose |  |
| Sandbox | Sandbox | loose |  |
| Hint | Hilfe | loose | Der Hilfetext eines Felds oder Fensters. Nie "Spur" (Track) und nie "Tipp" (Tip) |
| Glossary | Glossar | loose |  |
| Validation | Validierung | loose |  |
| Rules | Regeln | loose |  |
| Format | Format | loose |  |
| Version | Version | loose |  |
| Desktop | Desktop | loose |  |
| Mobile | Mobil | loose |  |
| Alignment | Ausrichtung | loose | Anders als Placement ("Platzierung") |
| Align | Ausrichten | loose |  |
| Center | Mitte | loose |  |
| Left | Links | loose |  |
| Right | Rechts | loose |  |
| Top | Oben | loose |  |
| Bottom | Unten | loose |  |
| Horizontal | Horizontal | loose |  |
| Vertical | Vertikal | loose |  |
| Linear | Linear | loose |  |
| Appearing | Erscheinen | loose |  |
| Scissors | Schere | loose |  |
| Edges | Ränder | loose | Wie in ru zwei Bedeutungen: das Werkzeug, das die Ränder einer Spanne verschiebt, ist "Ränder", die Kanten einer Form sind "Kanten" |
| Point | Punkt | loose |  |
| Continue | Fortsetzen | loose |  |
| Next | Weiter | loose |  |
| Back | Zurück | loose |  |
| Loading | Wird geladen | loose |  |
| Progress | Fortschritt | loose |  |
| Statistics | Statistik | loose |  |
| Preset | Preset | loose | Englisch, kurz genug für Schaltflächen |
| Clipboard | Zwischenablage | loose |  |
| Console | Konsole | loose |  |
| Ping | Lokalisieren | loose | Etwas im Viewport, auf der Zeitleiste und in der Hierarchie zeigen |
| Override | Überschreibung | loose |  |
| Placement | Platzierung | loose |  |
| Template | Vorlage | loose |  |
| Clip | Clip | loose |  |
| Slip | Inhalt verschieben | loose | Wie in ru: den Inhalt innerhalb seiner Spanne verschieben, ohne die Spanne zu bewegen |
| Slot | Slot | loose |  |
| Beat Grid | Beat-Raster | loose |  |
| Bar | Takt | loose | In der Musik. Der Fortschrittsbalken ist "Balken" |
| Tempo | Tempo | loose |  |
| Tap Tempo | Tap-Tempo | loose |  |
| Stereo Pan | Stereo-Panorama | loose |  |
| Font Size | Schriftgröße | loose |  |
| Word Wrap | Zeilenumbruch | loose |  |
| Backup | Sicherung | loose |  |
| Branch | Zweig | loose |  |
| Fit | Einpassen | loose | Nie "einrasten", das ist Snap |
| Finding | Befund | loose | Was die Validierung in einem Level findet |
| Fix | Beheben | loose |  |
| Group | Gruppe | loose |  |
| Id | ID | loose |  |
| Mipmap | Mipmap | loose |  |
| Sampling | Abtastung | loose |  |
| Tiling | Kachelung | loose |  |
| Wrapping | Randverhalten | loose | Was eine Textur jenseits ihrer Ränder zeigt, wie in ru |
| Pixel art | Pixel-Art | loose |  |
| Drawing | Zeichnung | loose |  |
| Emission Shape | Emissionsform | loose |  |
| Over Lifetime | Über Lebensdauer | loose |  |
| Forces | Kräfte | loose |  |
| Scatter | Streuung | loose |  |
| Spread | Öffnung | loose |  |
| Tangent | Tangente | loose |  |
| Clamp | Begrenzen | loose |  |
| Ping Pong | Hin und zurück | loose |  |
| Temperature | Temperatur | loose |  |
| Tint | Tönung | loose |  |
| Modifier Key | Modifikatortaste | loose | Muss "Modifikator" enthalten: das englische "Modifier" darin löst die strict-Zeile Modifier aus |
| Dead Zone | Totzone | loose |  |
| Sensitivity | Empfindlichkeit | loose |  |
| Stick | Stick | loose |  |
| Shoulder | Schultertaste | loose |  |
| Gamepad | Gamepad | loose |  |
| Touchscreen | Touchscreen | loose |  |
| Motion Sensor | Bewegungssensor | loose |  |
| Handedness | Händigkeit | loose |  |
| Double Tap | Doppeltippen | loose |  |
| Workshop | Workshop | loose | Wie im deutschen Steam |
| Story | Geschichte | loose |  |
| Wave | Welle | loose |  |
| Immortal | Unsterblich | loose |  |
| Dodge | Ausweichen | loose |  |
| Zen | Zen | loose |  |
| Clears | Abschlüsse | loose | Wie oft ein Level geschafft wurde |
| Hits | Treffer | loose |  |
| Profile | Profil | loose |  |
| Frame Hierarchy | Frame-Hierarchie | loose | Folgt Hierarchy ("Hierarchie") und Frame ("Frame"), beide strict |
| Stop Frame | Stopp-Frame | loose |  |
| Runtime Seed | Laufzeit-Seed | loose |  |
| Level Logo | Levelbild | loose | Das Bild in der Levelliste |
| Post-processing effect | Post-Processing-Effekt | loose |  |
| Audio effect | Audioeffekt | loose | "Effekt" allein ist nur das Effect-Objekt |
| Chorus | Chorus | loose |  |
| Compressor | Kompressor | loose |  |
| Distortion | Verzerrung | loose |  |
| Echo | Echo | loose |  |
| Flange | Flanger | loose |  |
| Highpass | Hochpass | loose |  |
| Lowpass | Tiefpass | loose |  |
| Normalize | Normalisieren | loose |  |
| Param EQ | Parametrischer EQ | loose |  |
| Pitch Shifter | Tonhöhenverschiebung | loose |  |
| Reverb | Hall | loose |  |
| Emitter | Emitter | loose |  |
| Variant | Variante | loose |  |
| Fader | Fader | loose |  |
| Signal level | Signalpegel | loose | Das "level" der Hilfen zu Audioeffekten. LocalizationGlossaryTests nimmt es aus |
| Swatch | Farbfeld | loose |  |
| Device library | Gemeinsame Gerätebibliothek | loose |  |
| Collection | Sammlung | loose | Ordner mit wiederverwendbaren Ressourcen: Prefabs, Themes, Formen, Effekte, Texturen, Schriftarten, Audio. Nichts mit Steam-Sammlungen zu tun. Loose, weil die collection der Validierungsregeln (eine Datenstruktur) nicht "Sammlung" sein muss, LocalizationGlossaryTests nimmt diese Schlüssel aus |
| Anti-aliasing | Kantenglättung | loose | Nie "Easing", das ist Ease |
| Overlay | Overlay | loose |  |
| Scrub | Ziehen | loose | Den Abspielkopf über die Zeitleiste ziehen |
| Gradient stop | Farbmarke | loose |  |
| Link to a docs page | Seitentitel | loose | Ein Link zur Dokumentation trägt den deutschen Titel der verlinkten Seite |
