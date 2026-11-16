# Satisim – Fluid-, Partikel- & Mandelbrot-Simulationsspiel

## Ziel des Projekts
Ein interaktives Simulations-Spiel (später Desktop-App), in dem man mit Werten, Szenarien, Farben und
Geschwindigkeiten spielen kann. Drei Modi: **Fluid**, **Partikel**, **Mandelbrot** – am Ende in einer App per Moduswechsel.
Es soll sich „satisfying“ anfühlen: hohe Auflösung, flüssig (60+ FPS), kräftige Farben, knackige Sounds, Lofi-Musik.
Ein **Chill-Modus ohne Ziel** ist wichtiger als ein klassisches Spiel mit Punkten.

## Über den Nutzer
- Programmieranfänger (etwas Unity-Erfahrung), nutzt Windows, arbeitet neu mit Claude Code.
- Erklärungen in einfachen Worten, Fachbegriffe beim ersten Auftreten kurz erklären. Antworten auf Deutsch.
- In kleinen Schritten arbeiten, nur das tun, was im jeweiligen Schritt verlangt ist; kurz erklären, was und warum
  geändert wurde; bei Unklarheiten nachfragen statt raten. Nach jedem Ausbauschritt auf Feedback warten.

## Technische Leitlinien
- Web-Technik: HTML, JavaScript, WebGL2 – **kein Framework**, keine Build-Tools. Später Desktop-App (Tauri oder Electron).
- Alles Rechenintensive auf die GPU (Shader).
- Mehrere Modi in einer App: **Fluid**, **Mandelbrot**, **Partikel** und **Flüssigkeit (Partikel)** (Abschnitte „Modi“,
  „Partikel-Modus“ und „Flüssigkeits-Modus (Partikel)“ unten).
- Jede Eingabe muss innerhalb eines Frames sichtbar werden. Bewegungen und Parameteränderungen immer weich
  interpolieren (Easing, Trägheit).
- FPS-Zähler und einstellbare Qualitätsstufe (Auflösung, Partikelzahl) für schwächere Geräte.
- Option, schnelles Blinken/Flackern zu reduzieren.
- Git: Commits mit Autor `ErfinderJojo <erfinder-jojo@posteo.de>` (lokal im Repo konfiguriert).

## Ideensammlung (für später – nicht alles auf einmal!)
(✅ = umgesetzt, ⬜ = offen)

**Fluid:** ✅ Farbe mit der Maus malen, die verwirbelt (Stable Fluids nach Jos Stam). ✅ Regler für Viskosität,
Wirbelstärke, Schwerkraft, Verblassen. ✅ Hindernisse zeichnen, um die die Flüssigkeit herumfließt.

**Partikel:** ✅ Anziehung/Abstoßung durch die Maus. ✅ Kräfte wie schwarze Löcher, Magnete, Wind, Orbits.
✅ Trails und Glow. ✅ Explosionen bei Klick. ✅ Schwarmverhalten (Flocking). ✅ Farbe nach Tempo/Alter, eigener
Partikel-Klang, Auto-Play mit unsichtbaren Kräften.

**Mandelbrot:** ✅ Zoom per Scrollen/Ziehen mit Trägheit, ✅ Julia-Sets live mit Mausposition, ✅ animierte Farbpaletten,
✅ automatische Zoom-Fahrt zu schönen Stellen, ✅ tiefer Zoom bis 10³⁰-fach (Bezugsbahn statt Float32-Grenze).
⬜ Zwei-Finger-Zoom auf Touch-Geräten, ⬜ weitere Farbgebungen, ⬜ tiefe Mini-Mandelbrote als Ziel der Zoom-Fahrt.

**Modusübergreifend:** ✅ Paletten-Presets (Neon, Sunset, Ozean, Lava …) mit sanftem Überblenden. ⬜ Presets/Szenarien
speichern und teilen. ✅ Idle-Modus/Screensaver (Auto-Play). ⬜ Screenshot-, Wallpaper- und Video-Export. ⬜ Optional kleine
Sammelziele („entdecke 10 Muster“). ✅ Moduswechsel Fluid/Mandelbrot/Partikel/Flüssigkeit, ⬜ Desktop-App (Tauri oder Electron).

**Satisfying-Faktoren:** ✅ Audio-Feedback per Web Audio API (selbst synthetisiert, Pentatonik, Lautstärke/Tonhöhe abhängig
von Geschwindigkeit, ✅ im Mandelbrot-Modus von der Zoomtiefe, ✅ im Partikel-Modus von Tempo und Dichte der Partikel). ✅ Lofi-Musik (generativ: Akkorde,
Vinyl-Knistern, sanfte Drums, reagiert auf Interaktion). ✅ Wenig UI: minimalistisches, ausblendbares Panel (⬜ Radialmenü).
✅ Bloom/Glow, dunkler Hintergrund, kontrastreiche Paletten. ✅ Option „Flackern reduzieren“.

**Looks:** ✅ Palette, Regenbogen, Geschwindigkeit, Wirbel, Feuer / Glut, Metallic, Glas / Kristall, Wasser,
Seifenblase / Ölfilm, Tinte & Aquarell, Marmorpapier (Ebru), Galaxie / Nebel / Aurora.

## Aktueller Stand
- Alles in **einer Datei**: `index.html` (HTML, CSS, JavaScript, GLSL-Shader). Öffnen per Doppelklick im Browser.
- **Vier Modi in einer App:** Fluid, Mandelbrot, Partikel und Flüssigkeit (Partikel). Umschalten mit `Tab`
  (Umschalt + `Tab` = zurück) oder im Panel-Abschnitt „Modus“, mit weicher Überblendung (0,8 s). Panel, Paletten,
  Bloom, Flacker-Reduktion, Qualität, FPS, Ton und Auto-Play gibt es nur einmal – sie gelten für alle Modi (Abschnitt
  „Modi“ unten). Ein Modus, der nicht zu sehen ist, kostet nichts und behält seinen Zustand.
- **Flüssigkeits-Modus (Partikel)** (Abschnitt unten, **Schritte 1–3 von 6 fertig**): bis 44.000 einzelne Partikel im
  Bild, die sich wie Wasser verhalten (fallen, schwappen, spritzen, Tropfen halten zusammen). Nachbarsuche über ein
  feines Raster auf der GPU, Physik nach „Position Based Fluids“, Regler für Schwerkraft/Fallrichtung, Viskosität,
  Zusammenhalt, Steifigkeit, Dichte. Dargestellt über die vorhandenen Looks (Start: „Wasser“) plus Look „Partikel“.
  **Noch offen:** Schritt 4 Interaktion (Maus, Spritzer, Hahn, Leeren, Hindernisse), Schritt 5 Presets (Wasser, Öl,
  Honig, Gel, Quecksilber), Schritt 6 Ton, Auto-Play, Flacker-Reduktion bei Spritzern, Panel-Feinschliff.
- **Mandelbrot-Modus** (Abschnitt unten): Zoom per Scrollen/Klick, Ziehen mit Trägheit, Julia-Sets live per Maus
  (Taste `J`), wandernde Farben in der aktiven Palette, 7 „schöne Stellen“ mit Flug dorthin, Zoom-Fahrt als Auto-Play,
  Töne passend zur Zoomtiefe, scharf bis 10³⁰-fachem Zoom.
- **Partikel-Modus** (Abschnitt unten, alle 5 Schritte fertig): bis 2,1 Millionen Partikel auf der GPU, Maus zieht
  an/stößt ab, Spuren und Glow, platzierbare Kräfte (Schwarzes Loch, Magnet +/−, Wind, Orbit), Explosion bei Klick,
  Schwarmverhalten (Schalter, Taste `S`), Farbe nach Wolken/Tempo/Alter (Taste `C`), eigener Klang, Auto-Play mit
  unsichtbaren Kräften.
- Fluid-Modus nach Stable Fluids auf der GPU (WebGL2 + `EXT_color_buffer_float`): Vorticity Confinement (Wirbel),
  Viskosität (Jacobi-Diffusion), Druck-Lösung (Jacobi), Gradienten-Subtraktion, Advektion.
- Farbe wird als „Dichte + Position auf der Palette“ gespeichert (R = Dichte, G/B = Dichte·cos/sin des Palettenwinkels);
  erst beim Anzeigen wird eingefärbt – durch den aktiven **Look** (siehe unten). Dadurch blendet ein Palettenwechsel
  das ganze Bild sanft um.
- Looks (Farbdarstellungen), 12 Stück (dazu **Partikel**, nur im Flüssigkeits-Modus): **Palette** (1), **Regenbogen** (2), **Geschwindigkeit** (3), **Wirbel** (4),
  **Feuer / Glut** (5), **Metallic** (6), **Glas / Kristall** (7), **Wasser** (8), **Seifenblase / Ölfilm** (9),
  **Tinte & Aquarell** (0), **Marmorpapier (Ebru)**, **Galaxie / Nebel / Aurora** – wählbar im Panel-Abschnitt „Look“,
  mit den Zifferntasten `1`–`9` und `0` (die ersten zehn) oder durch Weiterschalten mit `←`/`→` (auch `,`/`.` und `[`/`]`),
  womit alle Looks per Tastatur erreichbar sind (Details im Abschnitt „Look-System“ unten).
- **Oberflächen-Baustein** (Höhenfeld + Neigung) – genutzt von Metallic, Glas / Kristall, Wasser, Seifenblase / Ölfilm,
  Tinte & Aquarell, Marmorpapier und Galaxie.
- **Bloom (Glow)** als Nachbearbeitungs-Schritt nach dem Look – funktioniert mit allen Looks (Details im Abschnitt
  „Bloom“ unten). Panel-Abschnitt „Bloom“: Schalter „Glow“, Regler Bloom-Intensität/-Schwelle/-Weichheit.
- Ausblendbares Einstellungs-Panel (Zahnrad oben rechts bzw. Taste `H`): Regler für Pinselgröße (30–300 %, wirkt nur auf
  das eigene Malen, nicht auf Auto-Play; Pinsel-Ring zeigt die echte Größe, beim Ziehen Vorschau-Ring in der Bildmitte),
  Viskosität, Wirbelstärke, Verblassen, **Schwerkraft** und **Fallrichtung**
  (Doppelklick = Standardwert); Paletten Neon, Sunset, Ozean, Lava. Reglerwerte und Paletten werden weich interpoliert,
  die Akzentfarben der Oberfläche folgen der aktiven Palette.
- Qualität als Regler mit 6 Stufen: Niedrig/Mittel/Hoch/Ultra/**Extrem**/**Maximum** (Extrem/Maximum = Supersampling der
  Farbe bis 1,5×/2× Bildschirmauflösung, Strömungsraster bis 512, bis 70 Druck-Iterationen; im Mandelbrot-Modus:
  Fraktal-Auflösung 0,5×/0,75×/1×/1×/1,5×/2× Bildschirm, höchstens 2000–10000 Durchgänge). Schalter „Automatisch anpassen“:
  Ziel ist die volle Bildschirmfrequenz (höchste gemessene FPS ≈ Hz); senkt bei < 85 % davon, erhöht bei > 95 %.
  Manuelles Verstellen schaltet Auto ab, Doppelklick auf den Regler wieder an. Beim Wechsel wird das Bild in die neue
  Auflösung übernommen (kein Reset). Physik ist auf `REF_RESOLUTION` normiert, damit sie sich auf jeder Stufe gleich anfühlt.
- Hinweis: Nutzer hat einen 144-Hz-Monitor und eine starke GPU – FPS-Anzeige zeigt dort korrekt konstant 144 (V-Sync).
- FPS-Anzeige oben links (Zahl, Farbpunkt, Mini-Diagramm der letzten 60 Bilder), ein/aus mit `F` oder Schalter im Panel.
- UI-Prinzipien für Immersion: Glas-Optik, federnde Animationen, eigener leuchtender Pinsel-Cursor in Malfarbe,
  UI tritt beim Malen zurück (wird transparent) und kommt beim Darüberfahren zurück, kurze Meldungen („Toasts“) als Feedback,
  Leeren blendet sanft aus.
- **Auto-Play:** startet beim ersten Öffnen (Oberfläche bleibt sichtbar) und nach `IDLE_SECONDS` (30 s) ohne Eingabe als
  Bildschirmschoner (Oberfläche und Cursor blenden ganz aus, Hinweis unten). Drei unsichtbare Pinsel auf überlagerten
  Sinusbahnen, die Farbe an- und abschwellend abgeben; alle 3–7 s ein sanfter Farbstoß; alle 25 s nächste Palette.
  Jede Eingabe (Taste, Klick, Scrollen, Mausbewegung > 12 px) beendet es; Pinsel blenden weich aus. Taste `A` startet/stoppt
  sofort, Schalter „Bei Inaktivität starten“ im Panel. Der Rahmen (Start, Ende, Palettenwechsel) ist für alle Modi
  derselbe; im Mandelbrot-Modus ist der Inhalt die Zoom-Fahrt.
- **Ton & Musik** (Abschnitt „Ton & Musik“ unten): Klänge beim Malen und Klicken, generative Lofi-Musik, Panel-Abschnitt
  „Ton“ (Schalter Ton, Schalter Musik, Regler Lautstärke), Taste `M` = stumm. Startet erst nach dem ersten Klick/Tastendruck.
- **Flacker-Reduktion** (Abschnitt unten): Schalter „Flackern reduzieren“ im Panel-Abschnitt „Qualität“.
- **Schwerkraft & Hindernisse** (Abschnitt unten): Regler Schwerkraft/Fallrichtung, Werkzeuge Farbe/Hindernis/Radierer.
- Bedienung in jedem Modus: `Tab` = Modus wechseln, `H` = Panel, `F` = FPS, `Q` = eine Qualitätsstufe höher (schaltet
  Auto ab), `A` = Auto-Play, `M` = stumm.
- Bedienung Fluid: Maus bewegen = malen, Klick = Farbklecks, Leertaste = leeren, `1`–`9`/`0` = Look wählen,
  `←`/`→` = Look weiterschalten, `W` = Hindernis-Stift an/aus, `E` = Radierer an/aus, `X` = alle Hindernisse löschen,
  rechte Maustaste ziehen = Hindernis zeichnen (mit Umschalt-Taste = radieren).
- Bedienung Mandelbrot: Scrollen = Zoom zur Maus, Ziehen = verschieben, Klick = hinein, Rechtsklick = heraus,
  `↑`/`↓` = Zoom, `J` = Julia-Set an/aus (dort: Maus wählt die Form, Klick = Form festhalten/lösen), `1`–`7` = Flug zu
  einer schönen Stelle, `←`/`→` = vorige/nächste Stelle, Leertaste = zurück zur Übersicht.
- Bedienung Partikel: Maus bewegen = Kraft folgt der Maus, Klick = Explosion, Maustaste halten = Kraft umgekehrt,
  `R` = Anziehen ↔ Abstoßen, Leertaste = neu verteilen, `1`–`5` = Kraft an der Maus setzen (Schwarzes Loch, Magnet +,
  Magnet −, Wind, Orbit), gesetzte Kraft ziehen = verschieben, Rechtsklick oder `Entf` = löschen, `X` = alle löschen,
  Mausrad über einer Kraft = Reichweite, `S` = Schwarm an/aus, `C` = Farbe wechseln (Wolken → Tempo → Alter).
- Bedienung Flüssigkeit (Partikel), Stand Schritt 3: Leertaste = neu einfüllen, `1`–`9`/`0` = Look wählen, `←`/`→` =
  Look weiterschalten. (Maus-Interaktion kommt in Schritt 4.)
- Noch nicht umgesetzt: Presets speichern/teilen, Export, Desktop-App; Flüssigkeits-Modus Schritte 4–6.
- Testen: Die Seite läuft per Doppelklick. Zum automatischen Prüfen (FPS, GPU-Zeit per `EXT_disjoint_timer_query_webgl2`,
  alle Stufen × alle Looks) wurde sie über einen kleinen lokalen Server geladen (`python -m http.server`). Innerhalb
  eines Seitenaufrufs ist die Simulation bei gleichem Ablauf bitgenau wiederholbar (Prüfsumme der Farb-Textur) – gut für
  Vorher/Nachher-Vergleiche. Zwischen zwei Seitenaufrufen traten zwei verschiedene Prüfsummen auf (Ursache ungeklärt);
  alte und neue Version lieferten aber beide genau dieselben zwei Werte. Der Umbau auf mehrere Modi und der
  Mandelbrot-Modus wurden so geprüft: Fluid-Prüfsumme und fertige Bilder von 7 Looks bitgenau wie vorher.
  Die GPU-Zeitmessung schwankt auf dem Testrechner stark (gleiche Stelle 4–14 ms je nach Durchlauf) – verlässlich
  sind nur direkte Vergleiche hintereinander mit vielen Wiederholungen.

## Bloom (Nachbearbeitung / Post-Processing)
- Reihenfolge pro Frame: Simulation (`step`) → Look → Hindernisse (Überlagerung) → Helligkeits-Bremse der
  Flacker-Reduktion (nur wenn an) → **Bloom** → Bildschirm. Der Bloom verändert die Simulation nicht und
  arbeitet nur mit dem fertigen Bild des Looks, daher funktioniert er automatisch mit allen (auch zukünftigen) Looks –
  und genauso mit jedem Modus: `render()` fragt den aktiven Modus nach seinem Bild (`draw`) und seinem Bloom-Anteil
  (`bloomShare`), alles danach ist für alle Modi gleich.
- **Bloom-Anteil pro Look:** Ein Look kann `bloom: 0..1` angeben (Standard 1). Die Papier-Looks (Tinte & Aquarell,
  Marmorpapier) haben `bloom: 0` – helles Papier würde sonst glühen und die Farbe wegbleichen. Beim Look-Wechsel wird
  der Anteil weich überblendet; bei `bloom: 0` tritt der Panel-Abschnitt „Bloom“ zurück (abgeblendet).
- Ablauf (`render()` / `applyBloom(intensity, src)`; `src` = Szenen-Textur oder das gebremste Bild): Look zeichnet in die Szenen-Textur `scene` (volle Auflösung) statt direkt auf den
  Bildschirm → `bloomPrefilter` filtert helle Bereiche (Schwelle mit weichem Knick) und verkleinert auf
  Bildschirm / `bloomDiv` → `bloomDown` halbiert mehrfach (`bloomLevels`, Mip-Kette) → `bloomUp` setzt von klein nach groß
  wieder zusammen und **mischt** jede Stufe mit der weicheren (`bloomUpLevels`, Mischverhältnis = Weichheit, energieerhaltend)
  → `bloomFinal` legt den Glow auf.
- `bloomFinal`: Glow × Intensität × `CONFIG.BLOOM_GAIN` (6), farbtreu begrenzt (als Ganzes skaliert, nie über Weiß), dann
  **„Aufhellen“** (`max(Bild, Glow)`). Dadurch bleichen helle Flächen nicht aus und dunkle Bereiche bleiben dunkel; der Glow
  zeigt sich als Schein in dunkler Umgebung. (Erste Version mit „Screen“-Mischung hat volle, helle Bilder pastellig
  ausgebleicht – nicht wieder einführen.) Die Verstärkung ist nötig, weil Looks nur Helligkeit ≤ 1 liefern (kein HDR).
- Weichgezeichnet wird nur in verkleinerten Texturen. Qualitätsstufen: `bloomDiv` 4 (Niedrig/Mittel) bzw. 2 (ab Hoch),
  `bloomLevels` 4/5/6/7/8/8; die Kette endet früher, wenn eine Stufe kleiner als 4 px würde.
- Puffer (`ensureBloomBuffers`) werden automatisch neu angelegt, wenn sich Fenstergröße oder Qualitätsstufe ändert.
- Ist Bloom aus bzw. Intensität ≈ 0, zeichnet der Look wie früher direkt auf den Bildschirm (keine Zusatzkosten).
- Regler (alle weich interpoliert, Doppelklick = Standard): Bloom-Intensität 0–200 % (Standard 100 %, 0 = aus),
  Bloom-Schwelle 0–100 % (Standard 40 %), Bloom-Weichheit 0–100 % (Standard 80 % → Mischverhältnis 0,4 + 0,55·Weichheit).
  Schalter „Glow“ blendet weich ein/aus (`PARAMS.bloomOn`), Regler werden bei „aus“ abgeblendet.
- Gemessen: Bloom-Kette ≈ 0,23 ms GPU-Zeit pro Frame bei 674×1322 px (Stufe Maximum); stabil 60 FPS auf allen Stufen.

## Look-System (Farbdarstellungen)
- Looks verändern **nur die Darstellung, nie die Simulation**. Jeder Look ist ein Eintrag in der Liste `LOOKS`
  (`index.html`): `{ name, usesPalette?, params?, smoothCurl?, surface?, surfaceBlur?, foam?, bloom?, only?, sprites?, glsl }`. `glsl` enthält genau eine Funktion
  `vec3 look(LookInput L)` (darf eigene Hilfsfunktionen davor definieren).
- **Looks für mehrere Modi (Fluid und Flüssigkeit):** Jeder Modus, der die Looks benutzt, hat einen eigenen
  „Look-Stand“ (`makeLooks(index, source)` → `fluidLooks`, `liquidLooks`; im Modus-Objekt als `looks`): gewählter Look,
  laufende Überblendung, eigener Schaum-Puffer und die Datenquelle `source` (`id`, `dye`, `velocity`, `curl`,
  `simScale`, optional `sprites` + `updateSprites()`). Die bisherigen Variablen `lookIndex`, `prevLook`, `lookFade`,
  `foamBuf` … gelten immer für den Stand, der gerade „eingelegt“ ist (`useLooks(L)`; der vorige wird dabei
  zurückgeschrieben). `drawLook`, `updateSurface`, `updateFoam`, `updateCurlSmooth` lesen nur noch über
  `looks.source`. `drawLooks(L, target, dt, time)` zeichnet das Bild eines Stands, `lookBloomShare(L)` seinen
  Bloom-Anteil, `setLook`/`cycleLook`/`lookKeys` gelten für den Stand des aktiven Modus, `showLooks()` stellt das Panel
  beim Moduswechsel darauf ein. Jeder Modus merkt sich so seinen eigenen Look. Geprüft: Fluid-Bilder von 10 Looks
  bitgenau wie vor dem Umbau (Metallic/Glas/Ölfilm dafür mit `envAngle = filmPhase = 0`, sie hängen sonst von der Zeit ab).
- `only: 'liquid'` → den Look gibt es nur in diesem Modus (Knopf dort sichtbar, Weiterschalten überspringt ihn sonst).
  `sprites: true` → der Look liest `uSprites` (Bild der einzelnen Partikel), das die Quelle mit `updateSprites()`
  zeichnet, solange der Look zu sehen ist. Beides nutzt bisher nur der Look **Partikel**.
- `LookInput`: `L.uv` (Bildposition 0..1), `L.density` (Farbmenge), `L.t` (Palettenposition 0..1), `L.dye` (Rohdaten).
  Gemeinsame Hilfen im `lookHeader`: `palette(t)`, `hsv2rgb(hsv)`, `brightness(density)`, `dyeColor(L)` (eingemalte
  Farbe wie im Look „Palette“), `uTime` (eigene Uhr `lookTime`, läuft bei „Flackern reduzieren“ langsamer),
  `uCalm` (0..1, Schalter „Flackern reduzieren“ – Looks mit eigenem Flackern/Funkeln schwächen es damit ab),
  `speedAt(uv)` (Tempo), `curlAt(uv)` (rohe Drehung, ±), `curlSmoothAt(uv)` (geglättete Drehung).
  `lookMain` liest die Farb-Textur und ruft `look()` auf.
- Werte sind auf die Bezugsgröße (`REF_RESOLUTION`) normiert (`uSimScale`), damit Looks auf jeder Qualitätsstufe gleich
  aussehen. Gemessene Größenordnungen: Tempo typisch ≈ 25, schnell ≈ 150; geglättete Drehung ruhig ≈ 1–4,
  Auto-Play ≈ 4–37, gemalter Strich bis ≈ 30–75.
- `params: [...]` → Panel zeigt unter den Look-Knöpfen nur die genannten Look-Regler (Zeilen mit `class="look-param"
  data-param="…"`; sie klappen weich auf/zu und gelten gemeinsam für alle Looks, die sie nutzen). Vorhanden:
  `sensitivity` „Empfindlichkeit“ (`uSensitivity`, 0,2–5×), `dyeMix` „Farbstoff-Anteil“ (`uDyeMix`, 0–100 %),
  `heat` „Hitze“ (`uHeat`), `flicker` „Flackern“ (`uFlicker`), `ember` „Glutfarbe“ (`uEmber`).
  Neuer Look-Regler = Zeile im HTML + Eintrag in `PARAMS` + Uniform im `lookHeader` + Übergabe in `drawLook` + `bindSlider`.
- Looks dürfen Werte > 1,0 ausgeben: Bei aktivem Bloom landen sie unbegrenzt in der Szenen-Textur und erzeugen stärkeren
  Glow; ohne Bloom werden sie am Bildschirm zu Weiß begrenzt.
- `smoothCurl: true` → vor dem Zeichnen wird die Wirbel-Textur der Simulation (nur gelesen!) per `curlDownsample` auf
  ein kleines Bild (48 px kurze Seite) heruntergerechnet und dabei gemittelt (`curlSmooth`). Entfernt das kleinteilige
  Pixelrauschen der Wirbelverstärkung; läuft nur, wenn ein sichtbarer Look es braucht.
- Jeder Look wird beim Start zu einem eigenen Shader-Programm (`programs['look' + i]`) übersetzt; nur der aktive wird
  gezeichnet (1 Vollbild-Durchgang). Beim Wechsel werden 0,6 s lang beide gezeichnet und weich überblendet.
  `drawLook(i, alpha, time, target)` zeichnet in `target` (Szenen-Textur bei aktivem Bloom, sonst `null` = Bildschirm).
- Auswahl: Abschnitt „Look“ im Panel (Knöpfe werden automatisch aus `LOOKS` erzeugt), Zifferntasten `1`–`9` und `0`
  (zehnter Look) sowie Weiterschalten mit `←`/`→`, `,`/`.` oder `[`/`]` (`cycleLook`, läuft im Kreis). `[`/`]` werden
  über `e.key` erkannt, weil sie auf deutschen Tastaturen AltGr brauchen; Pfeiltasten gelten nicht, solange ein Regler
  den Tastaturfokus hat.
  Nutzt ein Look die Palette nicht (`usesPalette` fehlt), wird die Paletten-Auswahl im Panel abgeblendet.
- **Neuen Look hinzufügen = nur einen Eintrag in `LOOKS` ergänzen.**
- Fertig: **Palette** (bisherige Darstellung), **Regenbogen** (Farbton aus √Dichte, Verlauf wandert langsam mit der Zeit),
  **Geschwindigkeit** (Tempo → dunkles Blau → Violett → Pink → Gelb → Weiß), **Wirbel** (geglättete Drehung: eine
  Richtung Blau→Cyan, andere Magenta→Orange, ruhig = dunkel). Geschwindigkeit hat die Look-Regler Empfindlichkeit und
  Farbstoff-Anteil; Wirbel nur Empfindlichkeit – dort ist die Flüssigkeit selbst bewusst unsichtbar (schwarz), nur die
  Wirbel leuchten (Nutzerwunsch: eingemalte Farbe wirkte im Wirbel-Look verwirrend).
- **Feuer / Glut** (Taste `5`): Hitze = `(1 − exp(−Dichte·2,5)) · (1 + 0,8·Tempo-Anteil) · Hitze-Regler` – Tempo macht nur
  vorhandene Glut heißer (ohne Farbe bleibt es schwarz). Verlauf Schwarz → dunkles Rot → Rot → Orange → Gelb → Weiß mit
  weichen Übergängen; über Hitze 1 werden Werte > 1,0 ausgegeben (bis ≈ 1,8 gemessen), die der Bloom kräftig leuchten
  lässt (Szenen-Textur ist RGBA16F; ohne Bloom werden sie am Bildschirm einfach weiß). Kalte Bereiche per
  `smoothstep(0,02; 0,1)` komplett schwarz. Flackern: zwei Lagen weiches Rauschen („Value Noise“), die langsam nach oben
  ziehen – moduliert die Hitze um ±45 %·Flackern, kein Blinken. Look-Regler (`params: ['heat', 'flicker', 'ember']`):
  **Hitze** 0,2–3× (Standard 1×), **Flackern** 0–100 % (Standard 50 %, 0 = aus), **Glutfarbe** 0–1 (Standard 0,5;
  Anzeige Glut/Mitte/Feuer; skaliert die Hitze mit 0,65…1,4 → rötliche Glut ↔ gelbweißes Feuer). Nutzt die Palette nicht.
  Gemessen: Auto-Play-Schlieren Dichte ≈ 0,2–0,6 (→ Rot bis Gelb), frisch gemalte Striche ≈ 1+ (→ Weiß/HDR).
- **Spiegelnde Oberflächen – gemeinsame Hilfen im `lookHeader`** (von Metallic und Glas genutzt, nicht kopieren):
  `softbox(...)`, `studio(r, soft)` (Studio-Umgebung, dreht mit `uEnvAngle`), `fresnelSchlick(f0, cosT)`,
  `studioSpecular(n, gloss)` (Glanzlicht Lampe oben links).
- **Weiches Rauschen – gemeinsamer Baustein `noiseGLSL`** (im `lookHeader` und im Schaum-Shader eingebunden): `hash(p)`,
  `noise(p)` („Value Noise“, 0..1), `fbm(p)` (4 Lagen Rauschen übereinander, 0..1). Genutzt von Feuer, Wasser, Ölfilm,
  den Papier-Looks, Galaxie und dem Schaum-Puffer.
- **Papier – gemeinsame Hilfen im `lookHeader`** (Tinte & Aquarell, Marmorpapier): `paperFibers(q)` (Körnung 0..1, steht
  still) und `paperColor(q, fibers, grain)` (warmes Weiß mit Körnung und leichten Wolken). Geteilter Regler
  `paperGrain` „Papierstruktur“ (0–100 %, Standard 50 %).
- **Metallic** (Taste `6`, `surface: true`, `surfaceBlur: 0.02`): Spiegelung einer im Code erzeugten Studio-Umgebung
  (`studio(r, soft)`): Horizont hell (≈ 0,4 – bewusst knapp unter der Bloom-Schwelle, damit mit Bloom nur die
  Lichtflächen glühen, nicht der ganze Metallkörper), nach oben und unten dunkler, aber nie schwarz (Himmel oben ≈ 0,14,
  Boden ≈ 0,12 – sonst sind spiegelnde Stellen nicht vom schwarzen Hintergrund zu unterscheiden; gemessen: dunkelster
  Metall-Bildpunkt ≈ 0,12), Horizont um 0,15 rad abgesenkt
  (flache Stellen spiegeln den hellen Bereich darüber); drei weiche, längliche Softboxen (Helligkeit 2–3, also > 1 → Bloom).
  Reflexionsrichtung `reflect(-v, n)` mit `n = surfaceNormal(uv, Wölbung · 0,5)` (halbe Wölbung, sonst glitzern kleine Wellen),
  Fresnel nach Schlick (`f0 = Metallfarbe`, an steilen Flanken heller/farbneutraler), scharfes Glanzlicht (Blinn-Phong,
  Lampe oben links). Maske `smoothstep(0,02; 0,15; Höhe)`: ohne Farbe dunkel, zum Rand weich auslaufend.
  Umgebung dreht sich um die senkrechte Achse (`envAngle` wird in `render()` aufsummiert → weich bei Reglerwechsel).
  Look-Regler (`params: ['metal', 'bump', 'gloss', 'envSpin']`): **Metall-Typ** (Chrom/Gold/Kupfer/Rosé, rastet ein, Farbe
  blendet weich über; Standard Chrom), **Wölbung** (Regler `bump`), **Glanz** 0–100 %
  (Standard 60 %: Kantenweichheit der Softboxen + Schärfe/Stärke des Glanzlichts), **Umgebung drehen** 0–100 %
  (Standard 20 %, 0 = aus). Nutzt die Palette nicht. Gemessen: Baustein ≈ 0,1 ms + Look ≈ 0,13 ms (Stufe Maximum) →
  läuft auf jeder Qualitätsstufe; keine besondere Stufe nötig.
- **Glas / Kristall** (Taste `7`, `surface: true`, `surfaceBlur: 0.012`, `usesPalette: true`): Hinter der Flüssigkeit ein
  im Code erzeugtes, ruhiges Hintergrundmuster (`bgPattern`, 14 Zellen pro Bildschirmhöhe, kantengeglättet über `fwidth`):
  **Gitter** (helle Linien auf farbigem Grund), **Streifen** (diagonal, orange/blau), **Punkte** (bunte Punkte auf dunklem
  Grund), **Farbverlauf** (Regenbogen). Brechung: Versatz `−n.xy · (0,4 + Höhe) · Brechung · 0,06` (dicke, steile Stellen
  stärker). Farbsäume: R/G/B mit Faktor `1 ± Farbsäume · (0,15 + 0,45 · Rand)` verschoben → **genau 3 Musterabfragen pro
  Pixel**. Tönung: Muster × gemalte Farbe (`palette(L.t)`) plus leichte Eigenfarbe (× 0,22), dicker = satter (sonst wäre die
  Farbe über dunklen Musterstellen nicht sichtbar). Fresnel (`f0 = 0,06`) mischt die Studio-Spiegelung ein, dazu
  `studioSpecular(n, 0,85)`. Ohne Flüssigkeit: Muster unverzerrt, × 0,3 abgedunkelt, weicher Übergang
  `smoothstep(0,02; 0,2; Höhe)`. Look-Regler (`params: ['refract', 'chroma', 'tint', 'bgType', 'bgBright']`):
  **Brechung** 0–3× (Standard 1×), **Farbsäume** 0–100 % (Standard 50 %, 0 = aus), **Tönung** 0–100 % (Standard 60 %),
  **Hintergrund** Gitter/Streifen/Punkte/Farbverlauf (rastet ein, blendet weich über; Standard Gitter),
  **Hintergrund-Helligkeit** 10–150 % (Standard 70 %). Umgebung dreht mit dem Metallic-Regler „Umgebung drehen“ mit.
  Gemessen (Stufe Maximum, 674×1322): Baustein ≈ 0,26 ms + Look ≈ 0,31 ms; alle Stufen fehlerfrei, 60 FPS.
- **Wasser** (Taste `8`, `surface: true`, `surfaceBlur: 0.012`, `usesPalette: true`): Tiefe = Höhe × (0,7…1,5 je nach
  Tiefenfarbe); Verlauf helles Türkis → Blau (0,04; 0,30; 0,62) → tiefes Dunkelblau, Regler verschiebt Flach- und Tieffarbe
  Richtung Ozean. Gemalte Farbe färbt mit 20 % ein. **Lichtmuster** („Caustics“): Produkt zweier langsam wandernder
  Rauschgraten-Lagen (`caustic(q)`, 7 Zellen pro Bildschirmhöhe, durch `n.xy · 1,5` leicht verzerrt), in flachem Wasser
  stärker. Fresnel (`f0 = 0,02`) spiegelt die Studio-Umgebung an flachen Winkeln; Sonnenreflexe =
  `studioSpecular(n, Glanz) · (0,8…2)` (> 1 → Bloom). **Schaum** kommt aus dem mitgetragenen Schaum-Puffer (siehe
  Abschnitt „Schaum-Puffer“): `smoothstep(0,15; 0,5; Schaumwert)` → weiches Weiß (0,88; 0,93; 0,95) mit max. 85 % Deckkraft;
  die Körnung steckt im Puffer selbst (kein festes Bildschirm-Rauschen mehr). Rand:
  `smoothstep(0,01; 0,25; Höhe)` gegen dunklen Hintergrund (0; 0,008; 0,02). Look-Regler
  (`params: ['depthTone', 'waves', 'gloss', 'foam', 'foamLife', 'foamGrain', 'caustics']`): **Tiefenfarbe** 0–1 (Standard
  0,4; Anzeige Karibik/Mitte/Ozean), **Wellen** 0–3× (Standard 1×, = Stärke von `surfaceNormal`), **Glanz** (geteilter
  Regler `gloss` aus Metallic), **Schaum** 0–100 % (Menge, Standard 50 %, 0 = aus), **Schaum-Haltbarkeit** 0–100 %
  (Standard 50 %), **Schaum-Körnung** fein/mittel/grob (Standard mittel), **Lichtmuster** 0–100 % (Standard 60 %, 0 = aus).
  Gemessen (Stufe Maximum, 674×1274): Baustein ≈ 0,22 ms + Look ≈ 0,36 ms; alle Stufen fehlerfrei, 60 FPS.
- **Seifenblase / Ölfilm** (Taste `9`, `surface: true`, `surfaceBlur: 0.02`): Schillerfarben eines dünnen Films
  (Interferenz): `thinFilm(d) = 0,5 − 0,5·cos(2π·d·(1; 1,18; 1,44))` – Rot/Grün/Blau schwingen verschieden schnell mit
  der Filmdicke `d`; sehr dicke Stellen (d > 3) werden pastelliger. Filmdicke =
  `(√Höhe · 2,8 + (fbm − 0,5) · 0,8) · Filmdicke-Regler · (0,55 + 0,45·n.z)` – die Wurzel bringt auch dünne Schleier
  schnell über das farblose Silber-Weiß der dünnsten Schicht; die Schlieren (`fbm`) wandern mit `filmPhase` (in `render()`
  aufsummiert → weich bei Reglerwechsel). Der Film spiegelt die Studio-Umgebung, aber nur deren **Helligkeit**, begrenzt
  auf 1,6 (`Farbe · (0,45 + 0,6 · Licht)`), plus `studioSpecular · 0,35`; Normale mit halber Wölbung. (Erste Version mit
  voller Umgebungsfarbe und voller Wölbung brannte großflächig weiß aus.) Rand `smoothstep(0,01; 0,12; Höhe)` gegen fast
  schwarzen Hintergrund. Look-Regler (`params: ['filmThick', 'iridescence', 'filmFlow', 'gloss']`): **Filmdicke**
  0,3–3× (Standard 1×), **Schillern** 0–100 % (Standard 85 %, 0 = farblos), **Fließen** 0–100 % (Standard 40 %, 0 = still),
  **Glanz** (geteilter Regler). Gemessen (Stufe Maximum, 1086×1205): Baustein ≈ 0,23 ms + Look ≈ 0,49 ms.
- **Tinte & Aquarell** (Taste `0`, `surface: true`, `surfaceBlur: 0.015`, `usesPalette: true`, `bloom: 0`): helles Papier,
  die Farbe **schluckt Licht** (Lasur): `Papier · exp(−(1 − Pigment + 0,06) · Farbmenge · Deckkraft · 1,1)`.
  Pigment = Mischung aus blauschwarzer Tinte (0,05; 0,06; 0,14) und `palette(L.t)` (Regler Stil). Farbmenge =
  `−log(1 − Deckung)`; Deckung = Mischung aus scharfer Dichte (`heightFrom`, mit kleinem Faser-Versatz abgefragt →
  ausgefranste Ränder) und geglättetem Höhenfeld (Regler Verlaufen). **Trocknungsränder:** an steilen Stellen
  dünner Farbe mehr Pigment (`+2,2 · Steilheit · (1 − Deckung)`), innen etwas weniger. Körnung: Pigment setzt sich in den
  Tälern der Papierstruktur ab (`± 35 % · Papierstruktur`). Look-Regler
  (`params: ['inkStyle', 'inkOpacity', 'inkEdge', 'inkBleed', 'paperGrain']`): **Stil** 0–1 (Anzeige
  Tinte/Mischung/Aquarell, Standard 0,75), **Deckkraft** 0,3–3× (Standard 1×), **Ränder** 0–100 % (Standard 60 %),
  **Verlaufen** 0–100 % (Standard 50 %), **Papierstruktur**. Gemessen (Maximum): Baustein ≈ 0,27 ms + Look ≈ 0,58 ms.
- **Marmorpapier (Ebru)** (`surface: true`, `surfaceBlur: 0.008`, `usesPalette: true`, `bloom: 0`): Höhenlinien der
  Farbmenge werden zu Bändern: `x = Farbmenge · Bänder` (Farbmenge = halb scharfe, halb geglättete Höhe); Band 0 ist
  blankes Papier, jedes weitere Band nimmt die nächste Palettenfarbe (`palette(t + Band · 0,2)`, leicht entsättigt),
  abwechselnd kräftig und gedeckt (× 0,62). Die Palettenposition wird in 5 klare Farbflächen eingeteilt. Bandkanten
  sind über `fwidth` kantengeglättet (Kantenschärfe 100 % = 1,5 Bildpunkte breit, 0 % = halbe Bandbreite). **Adern:**
  feine helle Linien (0,95; 0,89; 0,74) genau auf den Bandgrenzen. Leichtes Relief aus `surfaceNormal` nur auf der Farbe
  (auf dem leeren Papier sah es fleckig aus), Papierkörnung auch auf der Farbe. Look-Regler
  (`params: ['marbleBands', 'marbleVeins', 'marbleSharp', 'paperGrain']`): **Bänder** 2–16 (Standard 7), **Adern**
  0–100 % (Standard 70 %), **Kantenschärfe** 0–100 % (Standard 85 %), **Papierstruktur**. Weil die Farbe verblasst,
  wandern die Bänder langsam nach innen. Gemessen (Maximum): Baustein ≈ 0,76 ms + Look ≈ 0,53 ms.
- **Galaxie / Nebel / Aurora** (`surface: true`, `surfaceBlur: 0.02`, `usesPalette: true`,
  `foam: { amount: 'stardust', life: 0.85, grain: 0 }`): Regler **Stil** rastet auf drei Varianten ein (Zwischenwerte
  blenden über, es werden nur die sichtbaren berechnet): **Galaxie** (Gas in Palettenfarben, durch `fbm`-Wolken
  moduliert, dunkle Staubbänder, weißglühender Kern `Gas⁴ · 1,4` > 1 → Bloom), **Nebel** (zwei Gasfarben, die in Wolken
  ineinander übergehen, leuchtende Fäden aus Rauschgraten, weicher Schein aus dem Höhenfeld), **Aurora** (Dichte wird
  mit 6 Messpunkten senkrecht verschmiert – Startpunkt pro Bildpunkt per `hash` verschoben, sonst sieht man Stufen –,
  senkrechte Strahlen aus gestrecktem Rauschen, Farbe dünn = grün → türkis → dicht = violett, 25 % Palettenfarbe).
  **Sternenhimmel:** zwei Lagen (`starLayer`: pro Gitterzelle höchstens ein Stern, zufällig groß/hell, funkelt sehr
  langsam; `uCalm` schaltet das Funkeln ab), scheint durch dünnes Gas. **Sternenstaub:** der mitgetragene Schaum-Puffer
  mit eigenen Einstellungen (`smoothstep(0,3; 1; Wert) · 1,6`) – winzige Lichtpunkte, die mit dem Gas treiben.
  Look-Regler (`params: ['spaceMode', 'spaceGlow', 'nebula', 'stars', 'stardust']`): **Stil** Galaxie/Nebel/Aurora,
  **Leuchtkraft** 0,2–3× (Standard 1×), **Struktur** 0–100 % (Standard 60 %), **Sterne** 0–100 % (Standard 60 %),
  **Sternenstaub** 0–100 % (Standard 50 %). Gemessen (Maximum): Baustein ≈ 0,2 ms + Schaum ≈ 0,27 ms + Look ≈ 0,93 ms.
- Der frühere Prüf-Look „Oberfläche (Test)“ ist entfernt. Sein Regler „Wölbung“ (`bump`) gehört jetzt nur noch zu
  Metallic; „Sättigung“ gibt es nicht mehr als Regler (fester Wert `CONFIG.SURFACE_SATURATION` = 2).
- Alle 12 Looks × 6 Qualitätsstufen laufen fehlerfrei mit 60 FPS (gemessen bei 1086×1205).
- Weitere Look-Ideen sind nicht geplant; neue Looks sind nur noch über Panel-Knöpfe und `←`/`→` erreichbar
  (Zifferntasten reichen für die ersten zehn).

## Schaum-Puffer (Looks „Wasser“ und „Galaxie“, mitgetragen)
- **Einstellungen pro Look** (`foamSettings(i)`): `foam: true` → die Schaum-Regler (Menge `foam`, Haltbarkeit `foamLife`,
  Körnung `foamGrain`, Look „Wasser“); `foam: { amount, life, grain }` → eigene Werte, jeweils eine Zahl 0..1 oder der
  Name eines Reglers in `PARAMS` (Galaxie: Menge vom Regler „Sternenstaub“, Haltbarkeit 0,85, feinste Körnung).
  Ein Look mit `foam` braucht auch `surface: true` (der Schaum-Shader liest das Höhenfeld). Wechselt der Look, der den
  Puffer benutzt (`foamOwner`), wird der Puffer geleert.
- Eigener Doppelpuffer `foamBuf` (R16F, 1 Kanal), Größe = Bildschirm / `QUALITY[].foamDiv` (Niedrig 4, Mittel/Hoch/Ultra 2,
  Extrem/Maximum 1). Funktion `updateFoam(dt, time)`, aufgerufen in `render()` direkt nach `updateSurface()` – **nur**,
  wenn ein sichtbarer Look `foam: true` hat (auch während der Look-Überblendung), sonst null Kosten.
- Pro Frame: 1) **Mitführen** mit dem vorhandenen Shader `advection` (derselbe wie für die Farbe, keine Kopie) und
  denselben Strömungs-Einheiten (`velocity.texel · sim/REF`); die Abklingrate ist der Zerfall:
  `dissipation = 3 + (0,05 − 3) · Haltbarkeit`. 2) **Neuer Schaum** per Shader `foamSource`: Quelle =
  `max(0,9·Tempo + 0,4·Wirbel + 0,4·Steilheit − 0,45, 0)` (Tempo `1 − exp(−v/120)`, Wirbel `1 − exp(−|curl|/60)`,
  Steilheit aus `surfaceNormal`) × Bläschen-Rauschen (2 Lagen, `uGrain` = 200…50 Bläschen pro Bildschirmhöhe, driftet nur
  langsam) × Menge × dt × 14 → Körnung wird beim Entstehen „eingebrannt“ und schwimmt mit. Nur wo Flüssigkeit ist
  (Maske `smoothstep(0,02; 0,15; Dichte)`), begrenzt auf max. 1,5.
- Puffer wird bei Größen-/Qualitätsänderung neu angelegt (leer) und beim (Wieder-)Sichtbarwerden des Looks geleert
  (`foamWasActive`).
- Gemeinsame GLSL-Bausteine dafür (keine Kopien): `densityGLSL`, `noiseGLSL` (hash/noise), `surfaceGLSL`
  (heightAt/surfaceNormal + Uniforms) – werden von `lookHeader` UND `foamSource` eingebunden; Uniforms setzt `bindSurface(u, unit)`.
- **Simulation unverändert, geprüft:** 1) Alle 9 Simulations-Puffer (Farbe A/B, Geschwindigkeit A/B, Druck A/B, Wirbel,
  Divergenz, Geschwindigkeit-vorher) sind nach 10× Schaum-Schritt bitgenau gleich. 2) A/B-Test mit 30 gleichen
  Pinsel-Schritten: mittlere Abweichung „mit vs. ohne Schaum“ (6,13–6,22) = „ohne vs. ohne“ (6,08–6,20). Hinweis: Die
  Simulation ist auf der GPU nicht bitgenau reproduzierbar (Rundungen von 16-Bit-Zahlen, z. B. 0,016 nach einem Pinselstrich);
  die Wirbelverstärkung schaukelt das chaotisch auf – daher kein bitgenauer A/B-Vergleich möglich.
- Gemessen: Schaum-Schritt ≈ 0,04–0,36 ms GPU-Zeit je nach Stufe; alle Stufen und Fenstergrößen fehlerfrei, 60 FPS.

## Oberflächen-Baustein (Höhenfeld → Neigung)
- Wiederverwendbar für alle Looks mit `surface: true` (Metallic, Glas, Wasser, Ölfilm …), kein Code-Kopieren nötig.
- Eigener Render-Schritt `updateSurface()` (nur Darstellung, liest `dye.read`, schreibt nie in die Simulation), läuft nur,
  wenn ein sichtbarer Look ihn braucht (auch während der Look-Überblendung):
  1. `surfaceHeight`: Höhe = `1 − exp(−Dichte · Sättigung)` (weich gesättigt; Sättigung = fester Wert
     `CONFIG.SURFACE_SATURATION` = 2), 4 Messpunkte gemittelt. Die Dichte kommt aus
     derselben GLSL-Funktion wie bei allen Looks: `densityFrom(dye)` (String `densityGLSL`, auch von `lookMain` benutzt).
  2. `surfaceBlur`: trennbarer Gauß-Weichzeichner (9 Punkte, waagrecht + senkrecht). Radius = Glättung × Bildschirmhöhe
     → auf jeder Qualitätsstufe gleich glatt. Glättung = `surfaceBlur` des aktiven Looks (optional, z. B. Metallic 0,02)
     oder Standard `CONFIG.SURFACE_BLUR` (0,006). Ergebnis liegt in `surfaceA`.
  - Bei starker Glättung wird das Höhenfeld automatisch kleiner gerechnet (`div = max(surfaceDiv, Schritt/1,5)`), damit die
    9 Messpunkte höchstens ~1,5 Pixel auseinander liegen – sonst entsteht ein Rautenmuster. Spart zugleich Rechenzeit.
- Puffer `surfaceA`/`surfaceB`: R32F (falls `OES_texture_float_linear` vorhanden, sonst R16F) – 32 Bit verhindern
  Treppenstufen in der Neigung. Größe = Bildschirm / `QUALITY[].surfaceDiv` (Niedrig 4, Mittel/Hoch 2, ab Ultra 1);
  werden bei Fenster- oder Qualitätsänderung automatisch neu angelegt. `createFBO` hat dafür einen optionalen `type`-Parameter.
- Shader-Hilfen im gemeinsamen Baustein `surfaceGLSL` (eingebunden in `lookHeader` und `foamSource`, Uniforms über
  `bindSurface(u, unit)`): `heightAt(uv)` (0..1), `heightFrom(density)` (dieselbe Höhenformel für eine einzelne,
  ungeglättete Dichte – passt genau zum Höhenfeld) und `surfaceNormal(uv, strength)` – zentrale Differenzen zu den
  Nachbarpunkten im Abstand 1,5 × Blur-Schritt (`uSurfaceStep`), seitenverhältnis-korrigiert (`uAspect`),
  `normalize(vec3(−Steigung · strength · 0,12, 1))`. `strength` ist Parameter, damit jeder Look seine eigene Wölbung nutzt.
- Gemessen (674×1322 px, Höhenfeld in voller Auflösung, Stufe Maximum): Baustein ≈ 0,46 ms GPU-Zeit pro Frame, damaliger Test-Look
  ≈ 0,1 ms. Grob hochgerechnet ≈ 2 ms bei 2560×1440 auf Ultra+. Wird es zu teuer: Stufe „Hoch“ rechnet das Höhenfeld in
  halber Auflösung (≈ ¼ der Kosten) und sieht durch die Glättung fast gleich aus.
  Hinweis: Es gibt 12 Looks – Zifferntasten für die ersten zehn, `←`/`→` und die Panel-Knöpfe für alle.

## Ton & Musik (Web Audio API)
- Alles wird im Code erzeugt, **keine Audiodateien**. Browser erlauben Ton erst nach einer echten Eingabe; deshalb baut
  `initAudio()` die ganze Ton-Anlage erst beim ersten `pointerdown`/`pointerup`/`keydown`/`touchend` auf (Mausbewegung
  allein reicht dem Browser nicht – der Starthinweis sagt „Klick = Ton an“). Vorher tun alle Ton-Funktionen nichts.
  Tab im Hintergrund → `ctx.suspend()`, sonst knistert es weiter.
- Signalweg: Klänge → `sfxBus`; Musik → `musicBus` → `musicFilter` (Tiefpass) → `musicOut`; Knistern → `musicOut`;
  Echo (`audio.echo`: Verzögerung 3 Schritte, Rückkopplung 0,32, gedämpft) → alles in `master` (Lautstärke² · 1,6, Stumm)
  → Kompressor → Lautsprecher. `aset(param, wert)` steuert Werte weich an und nur bei Änderung.
- Bausteine: `tone(freq, t, {type, peak, attack, hold, decay, dest})` (Oszillator mit Hüllkurve), `noiseHit(t, {...})`
  (gefiltertes Rauschen), `pluck(freq, t, peak, pan, dest, decay)` (gezupfter Ton: Sinus + kurzer Oberton bei 4×, mit
  Links/Rechts-Position und Echo). Tonleiter: Dur-Pentatonik C D E G A (`SCALE`, `scaleFreq(i)` ab C3 = 130,81 Hz).
- **Klänge:** `audioPaint(speed, dist, x)` beim Malen – Pinsel-Rauschen (Bandpass 400–3000 Hz, Lautstärke und Klangfarbe
  folgen dem Tempo) plus ein gezupfter Ton pro 0,07 Bildbreiten Weg (höchstens ~12/s); Tonhöhe = Stufe
  `3 + Tempo · 10 ± 1,5` (schneller = höher, über zwei Oktaven), Lautstärke `0,05 + 0,15 · Tempo`; Tempo = 1 bei
  3 Bildbreiten pro Sekunde. `audioClick(x, y)`: „Plop“ (Sinus fällt von 2,5·f auf 0,5·f) plus zwei gezupfte Töne, oben im
  Bild = höher. `audioClear()`: Wischen (Rauschen 2600 → 220 Hz). `audioTock()`: Hindernis-Stift setzt auf.
  `audioBurst()`: leiser tiefer Ton bei Farbstößen im Auto-Play.
- **Lofi-Musik** (`MUSIC`, `scheduleMusicStep`): 74 BPM, 16 Schritte pro Takt, Swing 16 %; wird in `updateAudio()` jeweils
  0,25 s im Voraus eingeplant. Akkordfolgen A = Fmaj7–Em7–Dm9–Cmaj9, B = Am7–Dm9–G7sus–Cmaj9, gespielt A A B A.
  Akkorde: pro Ton Sinus + leicht verstimmtes Dreieck (E-Piano-artig), langsames „Leiern“ (0,35 Hz, ±7 Cent) wie eine
  alte Kassette. Bass (Sinus) auf Schritt 0 und 10. Schlagzeug: Bassdrum (0, 10, manchmal 7), Snare (4, 12), Hi-Hat
  (Achtel). Melodie: einzelne Pentatonik-Töne. Vinyl-Knistern: 5-Sekunden-Schleife aus leisem Rauschen und Knacksern.
- **Reaktion auf Interaktion:** `audio.energy` (0..1) steigt beim Malen/Klicken und klingt in ~6 s ab (im Auto-Play
  mindestens 0,2). Mehr Energie → Musik-Filter öffnet sich (800 → 4200 Hz, dumpf ↔ offen), Schlagzeug kräftiger
  (40 → 100 %), mehr Hi-Hats, Melodietöne häufiger (5 % → 45 % pro Achtel).
- Panel-Abschnitt „Ton“: Schalter **Ton (Klänge beim Malen)**, Schalter **Musik (Lofi)**, Regler **Lautstärke**
  (`PARAMS.volume`, Standard 60 %), Hinweiszeile. Taste `M` = stumm (`setMuted`).
- **Partikel-Modus:** `audioBlast(x, y, Stärke)` (Explosion: tiefer Ton fällt von 140 auf 40 Hz, dazu Rauschen
  2800 → 160 Hz und zwei gezupfte Töne, der zweite 0,6 s später), `audioGather(Dichte, x)` („Sammeln“: Dichte an der
  Maus-Kraft → Stufe `round(log2(1 + max(Dichte − 1,5; 0)) · 2,5)`; bei jedem Stufenwechsel ein leiser, tiefer
  gezupfter Ton, höchstens ~7/s), `audioSwallow(n)` („Verschlucken“ am Schwarzen Loch: leiser Tropfen, der nach unten
  wegkippt, etwa 3–4/s, unregelmäßig). Das mittlere Tempo der Partikel hebt `audio.energy` (bis 0,75) → die Musik
  öffnet sich bei Schwarm und Explosionen. Die Zahlen dafür liefert `partStat` (Abschnitt „Partikel-Modus“).
- Geprüft (per Analyser am Ausgang): Tonhöhen stimmen (131/262/330/440 Hz), schnelles Malen ≈ 3× so laut wie langsames,
  Stumm und Schalter ergeben Stille, 60 FPS bleiben. **Nicht geprüft: wie es klingt** – das kann nur ein Mensch hören.

## Flacker-Reduktion
- Schalter „Flackern reduzieren“ (Panel-Abschnitt „Qualität“, `PARAMS.calm`, blendet weich ein/aus). Voreingestellt an,
  wenn im Betriebssystem „Bewegung reduzieren“ gewählt ist (`prefers-reduced-motion`).
- **Helligkeits-Bremse** (`applyCalm`, Shader `calmLimit`): Nachbearbeitung zwischen Look und Bloom. Jeder Bildpunkt darf
  sich pro Sekunde höchstens um `CONFIG.CALM_RATE` (2,5) ändern (voller Blitz Schwarz → Weiß dauert 0,4 s); langsame
  Änderungen kommen unverändert durch. Braucht das zuletzt gezeigte Bild (`calmBuf`, Bildschirmgröße). Wirkt dadurch
  automatisch bei **allen** (auch zukünftigen) Looks und bei Klick-Blitzen. Ist Bloom aus, wird das gebremste Bild direkt
  auf den Bildschirm kopiert.
- Zusätzlich an der Quelle: Looks dämpfen eigenes Flackern über `uCalm` (Feuer: Flackern × 0,15; Galaxie: kein
  Sternfunkeln), die Look-Uhr `lookTime` läuft mit 40 % Tempo, Klick-Klecks × 0,4, Farbstöße im Auto-Play × 0,5 (Menge
  und Kraft), Cursor-Puls kleiner, Glow × 0,65.
- Gemessen: Feuer-Flackern (Simulation eingefroren) mittlere Änderung pro Bild 0,0008 → 0,0001 (−88 %); Klick-Blitz
  größter Helligkeitssprung in einem Bild 0,133 → 0,011 (−92 %), Anteil der Bildpunkte mit Sprung > 10 %: 27 % → 0 %.
  Kosten ≈ 0,12 ms GPU-Zeit (Stufe Maximum). Nebenwirkung: schnell bewegte helle Kanten ziehen kurz nach.

## Schwerkraft & Hindernisse (ändern die Simulation)
- **Standardwerte = unveränderte Simulation:** Schwerkraft 0 → kein zusätzlicher Rechenschritt; ohne Hindernisse
  (`obstaclesExist = false`) laufen die unveränderten Shader-Programme. Geprüft: gleicher fester Ablauf in der Version
  davor und danach → **bitgenau gleiche Prüfsumme** der Farb-Textur (siehe Hinweis unter „Testen“ im aktuellen Stand); außerdem „Hindernis-Variante mit leerer
  Hindernis-Textur“ = „ohne Hindernisse“ (Abweichung 0) und gleiche Zahl an Zeichenschritten pro `step` (7 + Druck-Durchgänge).
- **Schwerkraft** (Shader `gravity`, in `step()` nach der Wirbelverstärkung, nur bei Regler > 0): Die Farbe ist „schwer“ –
  `Geschwindigkeit += Fallrichtung · Stärke² · CONFIG.GRAVITY (800) · min(Dichte, 2) · dt`. Farbige Flüssigkeit sinkt durch
  klare hindurch und sammelt sich am Rand/auf Hindernissen (eine gleichmäßige Kraft auf alles hätte in einem
  geschlossenen Becken keine Wirkung). Regler **Schwerkraft** 0–100 % (Standard aus) und **Fallrichtung** −180…180°
  (0 = unten in der Reglermitte, 90 = rechts, ±180 = oben; Anzeige mit Pfeil; tritt zurück, solange Schwerkraft aus ist).
  Gemessen bei 50 %: mittleres Tempo ≈ 42, Spitze ≈ 300.
- **Hindernisse:** Textur `obstacles` (R8, kurze Seite `CONFIG.OBSTACLE_RES` = 384, 1 = Hindernis), unabhängig von der
  Qualitätsstufe, bleibt bei Qualitäts-/Größenwechsel erhalten. Shader-Varianten `divergenceObs`, `pressureObs`,
  `gradientSubtractObs`, `advectionObs` entstehen aus **demselben Quelltext** plus `#define OBSTACLES` (`obstacleDefs`:
  `solid(uv)`, `freeAt(uv)`): Hindernis-Nachbarn zählen wie der Bildrand (Strömung prallt ab, kein Druckgefälle in die
  Wand), im Hindernis sind Geschwindigkeit und Farbe 0.
- Zeichnen: `obstacleStroke(x, y)` (Shader `obstacleBrush`) zieht eine dicke Linie vom letzten Punkt; Breite = Pinsel-Ring,
  mindestens 2 % der Bildhöhe (dünnere Wände wären auf niedriger Stufe undicht). `clearObstacles()` leert alles und
  schaltet zurück auf die unveränderte Simulation. Anzeige: `drawObstacles(target)` (Shader `obstacleDraw`) legt die
  Hindernisse nach dem Look über das Bild – dunkle Fläche mit hellem Rand, dunkler als die Bloom-Schwelle; sieht in jedem
  Look gleich aus (Looks bleiben unverändert).
- **Bedienung:** Panel-Abschnitt „Hindernisse“ mit Werkzeugen **Farbe / Hindernis / Radierer** (`setTool`) und Knopf
  „Alle Hindernisse löschen“. Bei Hindernis/Radierer malt die Maus keine Farbe; gezeichnet wird mit gedrückter
  Maustaste, der Cursor-Ring wird eckig (Radierer: gestrichelt). Tasten `W` (Hindernis-Stift an/aus), `E` (Radierer
  an/aus), `X` (alle löschen). Schnellweg ohne Werkzeugwechsel: **rechte Maustaste ziehen = Hindernis**, mit
  Umschalt-Taste = radieren. Leertaste leert nur die Farbe, Hindernisse bleiben.
- Gemessen (Stufe Maximum): `step` 1,67 ms → 2,86 ms mit Hindernissen + Schwerkraft; Anzeige ≈ 0,03 ms; alle Stufen und
  Looks 60 FPS.

## Modi (Moduswechsel)
- Ein Modus ist ein Objekt in der Liste `MODES` (`index.html`, Abschnitt „Modi“) mit fester Schnittstelle:
  `id`, `name`, `hint`, `autoplayHint`, `enter()`, `leave()`, `update(dt, now)` (Eingaben verarbeiten, rechnen),
  `draw(target, dt, time)` (Bild zeichnen; `target` = Szenen-Textur oder `null` = Bildschirm), `bloomShare()` (0..1),
  `autoplayStart()`, `autoplayStop()`, `autoplay(dt)`, `pointerMove/Down/Up(e)`, `pointerLeave()`, `key(e, bracket)`,
  `qualityInfo(q)`; optional `wheel(e)`, `idle()` (true = es wird gerade nichts Teures gerechnet → die
  Auto-Qualität schaltet dann nicht hoch), `label` (kurzer Name für den Modus-Knopf) und `looks` (Look-Stand, falls
  der Modus die Looks benutzt – siehe „Look-System“).
- Panel-Teile dürfen zu mehreren Modi gehören: `data-mode="fluid liquid"` (der Abschnitt „Look“ und seine
  Tastenhinweise). Die Regel dafür entsteht aus allen vorkommenden `data-mode`-Werten (`display: none !important`,
  sonst gewinnt bei den Look-Knöpfen die Regel `#looks button`).
- **Geteilt, ohne Code-Kopien:** Hauptschleife `frame()`, `render()` (Helligkeits-Bremse, Bloom), `easeParams`
  (alle Regler in `PARAMS`), Paletten (GLSL-Baustein `paletteGLSL` mit `palette(t)`, von Looks und Mandelbrot
  eingebunden), Qualität/Auto-Qualität, FPS, Ton (`audio…`-Funktionen), Auto-Play-Rahmen (`updateAutoplay` → ruft
  `autoplay(dt)` des aktiven Modus), Panel, Regler (`bindSlider`), Cursor-Ring (`showCursor`), Hinweise und Toasts.
  Alle Eingaben auf der Zeichenfläche und alle Tasten, die nicht für jeden Modus gelten, gehen an den aktiven Modus.
- **Panel:** Abschnitte und Tastenkürzel mit `data-mode="id"` sind nur in ihrem Modus zu sehen (die CSS-Regel dafür
  wird aus `MODES` erzeugt; `body` trägt die Klasse `mode-id`). Die Knöpfe im Abschnitt „Modus“ entstehen aus der Liste.
- **Überblendung** (`setMode(i)`, `CONFIG.MODE_FADE` = 0,8 s): alter Modus zeichnet in die Szenen-Textur, neuer in
  eine zweite (`sceneB`, nur währenddessen angelegt), Shader `fade` legt den neuen weich darüber; der Bloom-Anteil
  wird mit überblendet. Währenddessen laufen `update` und `draw` beider Modi. Wechsel zurück mitten in der
  Überblendung läuft von der aktuellen Stelle rückwärts. Beim Wechsel: leises Wischen, Hinweis des Modus für 6 s,
  Auto-Qualität pendelt sich neu ein.
- **Neuer Modus = ein Objekt in `MODES` + Panel-Abschnitte mit `data-mode="…"`.** Mehr ist nicht nötig (so wurde der
  Partikel-Modus eingehängt, ohne Fluid oder Mandelbrot anzufassen).
- Fluid als Modus: `updateFluid` (Pinsel, Cursor, `step`), `drawFluid` (Looks, Hindernisse), `fluidBloomShare`,
  `fluidAutoplay`, `fluidPointerDown`, `fluidKey` – der Inhalt dieser Funktionen ist unverändert.
- Geprüft: 12 Looks × 6 Stufen fehlerfrei mit 57–60 FPS; Prüfsumme der Farb-Textur und fertige Bilder (7 Looks mit
  Bloom) bitgenau wie vor dem Umbau; 36 Moduswechsel (alle Stufen, mit/ohne Flacker-Reduktion und Bloom) 60 FPS.

## Mandelbrot-Modus
- **Rechnung:** Für jeden Bildpunkt wird z → z² + c wiederholt und gezählt, nach wie vielen Durchgängen z „ausbricht“
  (|z| > 256). Mandelbrot: c = Bildpunkt, Start z = 0. Julia: c fest, Start z = Bildpunkt. Gespeichert wird der
  „glatte“ Zähler (ohne Stufen), −1 = gehört zur Menge (schwarz).
- **Zwei Schritte pro Bild:** 1) *Zählen* (teuer) in den Puffer `fracData` (R32F, Größe = Bildschirm ×
  `QUALITY[].fscale`) – läuft nur, wenn sich Ausschnitt, Julia-Form oder Durchgänge geändert haben (`frac.dataKey`);
  steht das Bild still, kostet es fast nichts. 2) *Färben* (billig, Shader `fracColor`) – läuft immer, deshalb können
  die Farben wandern. Weicht die Fraktal-Auflösung vom Bildschirm ab, wird über `fracColorBuf` weich skaliert
  (über 1 = Supersampling).
- **Farben** (`fracColor`): Palettenposition = `1,2 · asinh((Zähler − kleinster Zähler im Bild) / 30) · Farbdichte` +
  wandernde Verschiebung (`frac.phase`). Der kleinste Zähler kommt aus einem winzigen Zähl-Bild (16×16, `fracTiny` →
  Shader `fracMin` → 1 Bildpunkt `fracStat`, alles auf der GPU). Dadurch sieht das Muster in jeder Tiefe ähnlich aus,
  und beim Hineinzoomen fließen die Farben von selbst. Helligkeit: flache Farbverläufe (weit weg vom Rand) dunkel,
  Strukturen hell; Relief (Licht von links oben) aus der Steigung der Farbbänder; ganz nah am Rand glüht es über 1,0
  auf → Bloom. (Erste Fassungen waren überall hell bzw. in dichten Bereichen weiß-pastellig – nicht wieder einführen.)
  Regler: **Farbdichte** 0,2–4×, **Farb-Tempo** 0–100 % (Standard 35 %), **Leuchten** (60 %), **Relief** (50 %),
  **Details** 0,5–3× (Faktor auf die Durchgänge).
- **Durchgänge** (`fracIterations`): `100 + 40 · (log2 Zoom)^1,4`, begrenzt durch `QUALITY[].iter`
  (2000/3000/4500/6000/8000/10000), mal „Details“, höchstens 24000. Großzügig, weil nur Bildpunkte teuer sind, die bis
  zum Schluss nicht ausbrechen. Reicht es nicht, bleiben Stellen schwarz → Regler „Details“.
- **Ausschnitt** (`frac.M` Mandelbrot, `frac.J` Julia): Bildmitte `x`, `y` als BigInt-Festkommazahlen (200 Binärstellen
  hinter dem Komma, Hilfen `fx(zahl)` und `fxNum(bigint)`), Zoom `lz` als natürlicher Logarithmus (0 = Übersicht) mit
  Ziel `lzT`. Scrollen/Klick setzt `lzT`, `lz` läuft weich hinterher, die Stelle unter der Maus bleibt stehen. Ziehen
  verschiebt sofort; nach dem Loslassen läuft der Ausschnitt mit Trägheit aus (`frac.vel`). Grenzen: Zoom
  0,6× … 10³⁰×, Bildmitte bleibt in der Nähe der Menge.
- **Julia-Set** (`setJulia`, Taste `J`): Der Punkt unter der Maus im Mandelbrot-Ausschnitt wird zum Parameter c
  (läuft weich hinterher); eine kleine Karte unten links zeigt den Mandelbrot-Ausschnitt mit einem Ring bei c. Klick
  hält die Form fest bzw. löst sie. Der Übergang ist eine echte Verwandlung (`frac.k` 0 → 1 in 1,1 s): Startwert
  z = k · Julia-Punkt, c = (1 − k) · Mandelbrot-Punkt + k · c.
- **Schöne Stellen** (`SPOTS`): Punkte genau auf dem Rand der Menge (Misiurewicz-Punkte: ihre Bahn mündet nach k
  Schritten in einen Kreislauf der Länge p) – dort hört das Muster beim Hineinzoomen nie auf – plus die Mitte eines
  Mini-Mandelbrots. Beim Start rechnet `refineSpot` jede Position per Newton-Verfahren auf alle 60 Stellen nach.
  Zieltiefe je Stelle: so tief, bis ein Bildpunkt im Schnitt ≈ 800 Durchgänge braucht, höchstens 10²⁰-fach
  (Seepferdchen-Tal 6 · 10¹², Vierfach-Spirale 2 · 10¹⁰, Dreifach-Spirale 9 · 10⁴, Elefanten-Tal/Verzweigung/Zepter
  10²⁰, Mini-Mandelbrot 33-fach). Gefunden wurden die Punkte per Suche in der Nähe gut aussehender Stellen.
- **Flug** (`fracFlyTo`, `updateFracFlight`): erst herauszoomen, bis das Ziel nahe der Bildmitte liegt (Tempo 1,5 pro
  Sekunde im Logarithmus), dann hinein (0,6 ≈ 1,8-fach pro Sekunde), das Ziel rückt dabei weich in die Mitte; Tempo
  ändert sich weich. **Zoom-Fahrt** = Auto-Play: besucht die Stellen in zufälliger Reihenfolge, 4 s Pause am Ziel. Im
  Julia-Bild wandert stattdessen c auf einem Kreis (Radius 0,7885). „Flackern reduzieren“ macht alles 40 % langsamer.
- **Ton:** `audioZoom` – ein gezupfter Pentatonik-Ton pro Stück Zoom (alle 0,35 ≈ 1,4-fach), Tonhöhe folgt der
  Tiefe (Übersicht hoch, tief im Bild tief), vier wechselnde Stufen ergeben eine kleine Melodie, Lautstärke nach
  Zoom-Tempo; beim Zoomen von Hand zusätzlich leises Rauschen. Julia-Form verändern klingt wie Malen (`audioPaint`),
  Ankunft an einer Stelle: drei aufsteigende Töne (`audioArrive`). **Nicht geprüft: wie es klingt.**
- Nicht umgesetzt: Zwei-Finger-Zoom auf Touch-Geräten (ein Finger zieht, Tippen zoomt hinein).

### Tiefer Zoom (Bezugsbahn / „Perturbation“)
- **Problem:** Die Grafikkarte rechnet mit 32-Bit-Zahlen (ca. 7 Stellen). Gemessen weicht die direkte Rechnung schon
  bei 8.000-fachem Zoom um bis zu einen halben Bildpunkt ab, ab etwa 20.000-fach wird das Bild klötzchenhaft.
- **Lösung:** Ein Punkt (Bezugspunkt, meist die Bildmitte) wird im JavaScript mit vielen Stellen gerechnet; seine
  Bahn (alle z nacheinander) geht als Textur an die Grafikkarte (`fracRef`, RG32F, 1024 Punkte pro Zeile). Jeder
  Bildpunkt rechnet nur seinen Abstand d zur Bahn Z: `neues d = (2·Z + d)·d + dc`. Winzige Zahlen sind in 32 Bit
  sehr genau (7 Stellen bezogen auf den Abstand). „Rebasing“: Wird z kleiner als d (oder ist die Bahn zu Ende), wird
  d = z gesetzt und am Bahnanfang weitergerechnet – das hält d klein. Bahn A startet am Bezugspunkt, Bahn B bei 0
  (für Julia und die Verwandlung; beim Mandelbrot sind beide gleich).
- **Bezugsbahn** (`fracPrepareRef`): bis 67 Millionen-fach mit normalen Zahlen (`orbitDouble`), darüber mit BigInt
  (`orbitBig`, Stellenzahl = Zoom + 48 Binärstellen). Neu gerechnet wird nur, wenn der Bezugspunkt mehr als ¾ Bild
  von der Mitte entfernt ist, mehr Durchgänge nötig sind, der Zoom deutlich tiefer wurde oder sich die Julia-Form
  ändert. Bei einem Flug ist das Ziel selbst der Bezugspunkt → eine Rechnung pro Flug.
- **Abkürzungen** (ohne sie kostete das Zählen in der Tiefe 9–20 ms statt 2–5 ms):
  1. bis ca. 1.800-fach (`FRACTAL.PLAIN_LZ`) direkte Rechnung (Shader `fracPlain`);
  2. gemeinsame erste Durchgänge überspringen (`fracSeries`, „Series Approximation“: Abstand als Reihe mit drei
     Gliedern, im JavaScript vorgerechnet – im Seepferdchen-Tal bei 6 · 10¹²-fach 508 von ≈ 630 Durchgängen);
  3. ist der Abstand größer als 0,01, rechnet der Bildpunkt den Rest wieder direkt;
  4. Kreislauf-Erkennung für Punkte in der Menge: wiederholt sich der Stand exakt, wird abgebrochen (Ergebnis
     bleibt dasselbe; bildfüllendes Mini-Mandelbrot 30 ms → 1 ms, kostet an dichten Stellen ≈ 20 % mehr).
- **Geprüft** gegen eine langsame BigInt-Vergleichsrechnung an 99–168 Stichproben je Bild, bis 4,6 · 10²⁸-fach, auch
  Julia tief und Bezugspunkt außerhalb der Mitte: An ruhigen Stellen stimmen 81–99 % auf 0,02 genau, keine weicht um
  mehr als 0,5 ab (Ausnahme: 1 von 135 in einem Bild). Abweichungen gibt es nur an „chaotischen“ Stellen direkt am
  Rand, wo schon 1/100 Bildpunkt Verschiebung das Ergebnis ändert. Keine gleichen Nachbar-Bildpunkte (keine Klötzchen).
- **Kosten** (Testrechner, 1351×1205, Stufe Ultra, nur der Zähl-Schritt; Färben ≈ 0,1–0,4 ms): Übersicht 0,5 ms,
  Julia 0,35 ms, Seepferdchen 8.000× 2,4 ms, Vierfach-Spirale 14.000× 4 ms (etwa so teuer wie die direkte Rechnung vor
  dem tiefen Zoom: 2,0 bzw. 6,0 ms), Seepferdchen 6 · 10¹²× 1,9 ms, Vierfach-Spirale 2 · 10¹⁰× 4 ms, Elefanten-Tal 10²⁰× 0,9 ms,
  Verzweigung 10²⁸× 0,35 ms. Bezugsbahn im JavaScript: 0,1–0,7 ms, beim freien Hineinscrollen bis 2,2 ms, etwa 3-mal
  pro Sekunde. Flüge (25 s und 50 s) und freies Hineinzoomen bis 10¹⁷-fach: 60 FPS, kein Bild über 25 ms.
  Alle 10 Testbilder × 6 Stufen: 57–60 FPS, außer der dichtesten Stelle (Vierfach-Spirale) auf Maximum mit 50–52 FPS.
- **Bekannte Grenzen:** Schwarze Flächen dicht an ihrem eigenen Rand bleiben teuer (z. B. eine Knospe am
  Mini-Mandelbrot bildfüllend: 23 FPS auf Ultra) – dort greift keine Abkürzung, die Auto-Qualität senkt die Stufe.
  Während der Verwandlung Mandelbrot ↔ Julia aus großer Tiefe wird die Bezugsbahn in jedem Bild neu gerechnet
  (gemessen 56 FPS, zwei Bilder über 25 ms).

## Partikel-Modus (alle 5 Schritte fertig)
- **Ausbauplan:** 1 Grundsystem ✅ · 2 Kräfte ✅ · 3 Explosionen ✅ · 4 Schwarmverhalten (Ausrichtung, Abstand,
  Zusammenhalt) ✅ · 5 Look und Gefühl (Farbe nach Tempo/Alter mit Paletten, eigener Klang, Auto-Play mit unsichtbaren
  Kräften, Panel-Feinschliff) ✅. Commits: `f07c1e4`, `63afdbc`, `b70d80e`, `bc630dc` (Schritt 4), `e22be53` (Schritt 5).
- Code: Abschnitt `// ---------- Partikel-Modus ----------` in `index.html` (vor `// ----- Moduswechsel -----`),
  Konstanten in `PARTICLES`, Zustand in `part`, Modus-Objekt `MODES.push({ id: 'particles', … })`.

### Technik
- **Zustand auf der GPU:** Jedes Partikel ist ein Bildpunkt einer RGBA32F-Textur (`part.state`, Doppelpuffer, NEAREST):
  xy = Position (0..1), zw = Tempo. Seitenlänge `QUALITY[].pside` = 192/320/512/724/1024/1448 → 37 Tsd., 102 Tsd.,
  262 Tsd., 524 Tsd., 1,05 Mio., 2,1 Mio. Partikel. Beim Stufenwechsel übernimmt `partResize` die vorhandenen Partikel
  (neue werden zufällig verteilt), `partInit` verteilt neu (Leertaste).
- **Rechnen** (`partStep`, ein Vollbild-Durchgang über die Zustands-Textur): Kräfte → Tempo → Position. Einheiten sind
  „Bildhöhen“ (seitenverhältnis-korrigiert), damit Kreise rund bleiben. Das Tempo nähert sich mit
  `v = Wind + (v − Wind) · exp(−Bremsung · dt)` einem Mediums-Tempo an (Bremsung = `5 · 0,02^Trägheit`) – das ist die
  „Trägheit“. Ein Strömungsfeld (Regler „Strömung“) aus weichem Rauschen schiebt die Partikel nur mit
  (`p += (v + Strömung) · dt`, kein Einfluss aufs Tempo), wirbelfrei aus einem Potenzial berechnet, am Rand ausgeblendet.
  Weiche Wand 5 % vor dem Rand (`WALL`) plus Abprallen (`BOUNCE`).
- **Zeichnen:** Punkte per `gl_VertexID` (leeres VAO, kein Vertex-Puffer), additiv in den Spuren-Puffer
  (`part.trail`, RGBA16F). Spuren: Der Puffer wird jedes Bild multiplikativ abgedunkelt (`partFade`,
  `blendFunc(ZERO, SRC_COLOR)`), Lebensdauer = `Spuren² · 2,5` s. **Bewegungsunschärfe:** Jeder Punkt wird an einer
  zufälligen Stelle auf seiner Strecke vom letzten zum neuen Ort gezeichnet (Sprünge > 0,2, z. B. nach dem Verschlucken,
  ausgenommen) → durchgehende Linien statt Perlenketten. Punktgröße = `clamp(0,8 · √(Bildpunkte/Partikel); 1,2; 2,6) ·
  Größe`; die Helligkeit pro Partikel ist so normiert, dass das Bild bei jeder Partikelzahl/Größe/Spurlänge gleich hell
  wirkt. Farbe: siehe „Farbe“ unten.
- **Anzeigen** (`partShow`): Farbtreue Tonwert-Kompression (`L / (1 + L)`, Farbton bleibt) mit Überschuss > 1 in sehr
  dichten Bereichen → nur dort Glow über den gemeinsamen Bloom. Darüber die Zeichen der gesetzten Kräfte und der
  Explosionsblitz. Der Rest (Flacker-Bremse, Bloom) ist der gemeinsame `render()`-Weg.
- **Zufall:** PCG-Ganzzahl-Hash (`partHashGLSL`, `floatBitsToUint`) statt des üblichen `sin`-Hashs.
- **Maus-Kraft** = ein Magnet, der der Maus weich folgt (`FOLLOW` 16/s) und weich ein-/ausblendet (`LEVEL`). Anziehen:
  `Abstand · Stärke · exp(0,5 − 0,5·r²/R²) / R`, mit einem **Kern** pro Partikel (0,15…1,55 · R, zufällig), in dem die
  Anziehung in Abstoßung kippt, plus leichter Drehung (`SWIRL`) → kreisende Wolke wie eine Galaxienscheibe. Abstoßen:
  begrenzte Blase `(1 − r²/R²)²`, Radius = Reichweite × 1,2. Umschalten: `R`, Panel-Knöpfe, oder Maustaste halten
  (solange gehalten umgekehrt; weicher Wechsel). Zeigt die Maus auf eine gesetzte Kraft, ruht die Maus-Kraft.
- **Gesetzte Kräfte** (`FORCE_TYPES`, höchstens `MAX_FORCES` = 12, Uniform-Felder `uF[12]`/`uG[12]`, `bindForces` – von
  Rechnen und Anzeigen gemeinsam genutzt): **Schwarzes Loch** (1/r² weich begrenzt, Kreisbahn-Wind × 0,85 → Spirale;
  innerhalb `HORIZON` · R wird das Partikel verschluckt und taucht zufällig irgendwo neu auf), **Magnet +/−** (wie die
  Maus), **Wind** (bläst in eine Richtung, Regler „Windrichtung“), **Orbit** (zieht auf einen Ring mit Radius
  R · (0,8…1,2) und lässt die Partikel darauf kreisen). Regler Stärke/Reichweite/Windrichtung gelten für die ausgewählte
  Kraft (ist keine ausgewählt: Werte für die nächste). Zeichen: schwarze Scheibe mit Ring, Ring mit +/−, Pfeil, Punkt mit
  Kreis; Reichweiten-Kreis, solange ausgewählt oder unter der Maus.
- **Gedränge** (Dichte-Raster): Partikel wissen nichts voneinander. Damit Kräfte sie nicht alle auf einen grellen Punkt
  ziehen, wird vor jedem Schritt gezählt, wie viele in jedem Feld eines groben Rasters liegen (`partGrid`: jedes Partikel
  als Punkt additiv in eine R16F-Textur, 128 Felder an der kurzen Seite, danach 2× weichgezeichnet). Über dem Doppelten
  des Durchschnitts (`CROWD`) drückt es die Partikel auseinander: `−∇ log(1 + Überschuss) · PRESSURE` (wie ein Gas).
  Ist der Schwarm an, übernimmt das Schwarm-Raster (siehe unten) diese Aufgabe mit.
- **Explosionen** (höchstens `MAX_BLASTS` = 4, `uBlast[4]`, `bindBlasts`): Druckwelle als Ring, der mit `BLAST_SPEED`
  (1,6 Bildhöhen/s) nach außen läuft, breiter und schwächer wird (`exp(−t/0,4)`) und die Partikel nach außen
  schleudert; ab ≈ 0,5 s holt eine sanfte Kraft sie zurück (weit entfernte stärker), nach 3,2 s ist alles vorbei.
  Anzeige: kurzer Blitz im Zentrum plus feiner Ring auf der Welle. Regler „Explosion (Klick)“ 0–250 % (0 = aus).
- **Flacker-Reduktion:** Explosion schwächer (× 0,7), Blitz und Ring breiter, langsamer und × 0,2 so hell, Partikel-Uhr
  langsamer; dazu die gemeinsame Helligkeits-Bremse.
- **Panel** (vier Abschnitte): „Partikel“ (Anziehen/Abstoßen, Maus-Kraft, Reichweite, Explosion, Trägheit, Strömung,
  Knopf „Neu verteilen“), „Schwarm“ (Schalter, Ausrichtung, Abstand, Zusammenhalt, Schwarm-Tempo – abgeblendet, solange
  der Schwarm aus ist), „Kräfte“ (Knöpfe aus `FORCE_TYPES`, Stärke, Reichweite, Windrichtung, Infozeile, Löschen, Alle
  löschen; Panel-Knöpfe setzen die Kraft nahe der Bildmitte), „Aussehen“ (Farbe: Wolken/Tempo/Alter, Lebensdauer – nur
  bei „Alter“ aufgeklappt –, Spuren, Größe, Helligkeit).

### Schwarm (Schritt 4)
- **Nachbarsuche über ein Raster statt Paar für Paar:** Bei 2 Millionen Partikeln wären das Billionen Paare. Stattdessen
  wird jedes Partikel als Punkt additiv in ein Raster gezeichnet (`partGridV`, `part.gridV`, 128 Felder an der kurzen
  Seite): Rot = Anzahl, Grün/Blau = Summe der Tempos, Alpha = Summe der Geschwindigkeiten. Summe / Anzahl = mittlere
  Bewegung der Partikel dort. Daraus entstehen drei verkleinerte, geglättete Fassungen (`part.levels`, ½, ¼, ⅛, jede
  mittelt über 4×4 Felder der vorigen; Shader `partGridBlur`). Jedes Partikel liest in `partStep`:
  `uNear` = `levels[NEAR_LEVEL]` (64 Felder, nahe Umgebung ≈ 2 % der Bildhöhe) und `uWide` = `levels[WIDE_LEVEL]`
  (32 Felder, weitere Umgebung ≈ 6 %).
- **Die drei Regeln** (nur wenn `uSwarm.w` > 0, d. h. Schwarm an): **Ausrichtung** `acc += (mittleres Tempo der Nachbarn −
  v) · ALIGN (6/s)`; **Abstand** `acc −= ∇ log(1 + Dichte nah) · SEPARATE (0,08)`; **Zusammenhalt**
  `acc += ∇ log(0,3 + Dichte weit) · COHESION (0,4)`, ausgeblendet ab dem 3- bis 8-Fachen der Durchschnittsdichte
  (sonst fällt der Schwarm ohne „Abstand“ auf einen Punkt zusammen). Regler je 0–100 % (Standard 60/50/50 %).
- **Dazu, damit es wie ein Schwarm wirkt:** Eigenantrieb (jedes Partikel hält sein Schwarm-Tempo = Regler × `CRUISE` 0,5
  Bildhöhen/s, je Partikel 0,75–1,25-fach; wer langsamer ist, beschleunigt mit `THRUST` 4/s, wer schneller ist, gleitet
  aus), zufälliges Umherirren (`WANDER`), **gemeinsames Schlängeln** (`MEANDER`: wanderndes Rauschen dreht Nachbarn in
  dieselbe Richtung → der Schwarm zieht Bögen und teilt sich in Gruppen) und Abdrehen vor dem Bildrand (`TURN_ZONE`
  16 % der Bildhöhe, `TURN`).
- **Kosten sparen:** Ohne Schwarm läuft exakt der alte Weg (R16F-Raster, altes Programm `partGrid`) – keine Mehrkosten.
  Mit Schwarm ersetzt das Schwarm-Raster das Dichte-Raster (`part.gridNow`), und es werden höchstens `SAMPLES` (530.000)
  Partikel hineingezählt: auf Extrem jedes zweite, auf Maximum jedes vierte (die ersten Zeilen der Zustands-Textur =
  feste, durchmischte Auswahl; `part.gridCount`). Für Mittelwerte reicht das, und der Schwarm kostet dadurch auf den
  höchsten Stufen nichts extra. Schwarm-Raster ist RGBA32F, wenn `EXT_float_blend` vorhanden (sonst RGBA16F – beim
  Aufsummieren vieler kleiner Tempos ungenauer); es wird erst beim ersten Einschalten angelegt (`ensureSwarmBuffers`).
- **Mit Kräften kombinierbar:** Die Schwarm-Regeln sind nur weitere Beschleunigungen im selben Schritt – Maus, gesetzte
  Kräfte, Explosionen, Gedränge und Wand wirken unverändert weiter. Der Eigenantrieb zählt relativ zum „Wind“ der
  Kräfte (ein Schwarm im Orbit kreist mit).

### Farbe, Klang, Auto-Play (Schritt 5)
- **Farbe** (`PART_COLORS`, Knöpfe im Abschnitt „Aussehen“, Taste `C`; `PARAMS.partColor.target` = 0/1/2, die Anteile
  `part.colorW` blenden weich über, gerechnet wird im Vertex-Shader `partVertex` nur, was zu sehen ist):
  **Wolken** (bisheriges Aussehen, Standard: `palette(Phase + Zufall · 0,06 + Wolke + Tempo · 0,45)`),
  **Tempo** (`k = 1 − exp(−Tempo · 2,2)`, `palette(Phase + k · 0,8)`, Helligkeit `0,45 + 1,7 · k` – langsam = dunkel),
  **Alter** (`palette(Phase + Alter · 0,7)`, Neugeborene gut doppelt so hell, am Lebensende verglimmt das Partikel).
- **Alter** (`partAge`, `part.age`, R32F, nur gerechnet, solange die Farbe „Alter“ zu sehen ist; `updatePartAge`):
  Alter 0..1 wächst um `dt / Lebensdauer` (Regler 3–40 s, Standard 12 s); bei 1 wird das Partikel an Ort und Stelle
  neu geboren. Sofort jung macht: vom Schwarzen Loch verschluckt (Sprung > 0,2) und die Druckwelle einer Explosion
  (`AGE_BLAST`). **Geburtswellen:** Würde jedes Partikel für sich altern, mischten sich bei Millionen Partikeln alle
  Farben zu grauem Brei. Deshalb legt ein Wolkenmuster (`wave = fract(Zeit + Rauschen der Position)`) fest, wie alt man
  an jeder Stelle sein „sollte“; die Partikel gleichen ihr Alter mit `AGE_SYNC` (0,8/s) daran an
  (`Alter += SYNC · dt · sin(2π · (wave − Alter)) / 2π`). Ergebnis: große Farbflächen, durch die Geburts-Fronten wandern.
  Beim Einschalten und bei neuer Partikelzahl wird das Alter aus dem Muster neu verteilt.
- **Kennzahlen für den Klang** (`partStat`, `readPartStats`): Ein 8×8-Bild mittelt über 4096 Stichproben-Partikel:
  mittleres Tempo, wie viele seit dem letzten Bild verschluckt wurden, Dichte an der Maus-Kraft. Abgeholt wird das
  Ergebnis **ohne die Grafikkarte aufzuhalten** (Zwischenspeicher `PIXEL_PACK_BUFFER` + `fenceSync`, meist zwei Bilder
  später). Läuft nur, wenn der Ton an ist. Klänge: siehe „Ton & Musik“ (`audioBlast`, `audioGather`, `audioSwallow`).
- **Auto-Play** (`partAutoplayStart/Stop`, `partAutoplay`): Die unsichtbare „Maus“ auf der Pinselbahn zieht meist an
  und stößt zwischendurch 4–7 s lang ab (`part.autoPull`; die Einstellung des Nutzers bleibt unberührt). Dazu bis zu
  `AUTO_GHOSTS` (2) **unsichtbare Kräfte** (`ghost: true` in `part.forces`: Orbit, Magnet +/−, Wind – kein Schwarzes
  Loch), die auf eigenen Bahnen wandern und nach 15–30 s durch eine andere ersetzt werden; sie sind nicht zu sehen
  (`uG.w` = 0), nicht zu greifen, zählen nicht in der Infozeile und weichen, wenn der Nutzer selbst 12 Kräfte setzt.
  Alle 7–14 s eine sanfte Explosion (Stärke 45–80 %, mit `audioBurst`). Bei jeder Eingabe blenden die unsichtbaren
  Kräfte aus. Schwarm und Farbe bleiben, wie der Nutzer sie eingestellt hat.
- **Flacker-Reduktion:** Neugeborene leuchten weniger auf (× 0,3), Geburtswellen laufen langsamer, Explosionsklang und
  Auto-Play-Explosionen schwächer; dazu die gemeinsame Helligkeits-Bremse.

### Messwerte (1920×1080; „Bild“ = ganzes Bild inkl. Bloom, CPU + GPU, kleinster von 3 Durchläufen)
| Stufe | Partikel | Bild, ohne Kräfte | … mit Schwarm | Bild, 12 Kräfte + 4 Explosionen | … mit Schwarm | … + Farbe „Alter“ |
|---|---|---|---|---|---|---|
| Niedrig | 36.864 | 0,69 ms | 0,70 ms | 1,28 ms | 1,23 ms | 1,24 ms |
| Mittel | 102.400 | 0,92 ms | 0,85 ms | 1,55 ms | 1,58 ms | – |
| Hoch | 262.144 | 1,67 ms | 1,58 ms | 2,23 ms | 2,38 ms | – |
| Ultra | 524.176 | 2,40 ms | 2,49 ms | 3,08 ms | 3,41 ms | 3,43 ms |
| Extrem | 1.048.576 | 4,02 ms | 3,74 ms | 4,95 ms | 4,93 ms | 5,10 ms |
| Maximum | 2.096.704 | 7,11 ms | 6,61 ms | 8,53 ms | 8,18 ms | 8,31 ms |
- **Schwarm, GPU-Zeit des Rechenschritts** (Raster + `partStep`, ohne Kräfte) ohne → mit Schwarm: Niedrig 0,07 → 0,11 ms,
  Mittel 0,12 → ≈ 0,2 ms, Hoch 0,28 → 0,49 ms, Ultra 0,58 → 0,88 ms, Extrem 1,11 → 1,23 ms, Maximum 2,02 → 2,00 ms.
  Der Schwarm kostet also höchstens 0,3 ms pro Bild; auf Extrem/Maximum gleicht das sparsamere Raster die Mehrarbeit aus.
  Ohne Schwarm sind die Kosten wie vor Schritt 4 (Vergleich direkt hintereinander: 0,67/0,93/1,62/2,35/3,99/7,06 ms).
  Erste Fassung (ein gemeinsames RGBA32F-Raster für alles, jedes Partikel gezählt) kostete auch ohne Schwarm
  0,5–1,1 ms mehr auf Extrem/Maximum → deshalb zwei getrennte Raster.
- **Farbe:** Wolken/Tempo/Alter kosten gleich viel (Maximum 6,91/6,91/7,26 ms); der Alters-Schritt allein
  0,005/0,03/0,06/0,12/0,23/0,46 ms (Niedrig … Maximum). Kennzahlen für den Klang: nicht messbar (60 FPS auf allen
  Stufen, Bildkosten mit und ohne Ton gleich).
- Alle Stufen 60 FPS, GL-Fehler 0, keine ungültigen Partikel (NaN/außerhalb), keine ungültigen Alterswerte. Geprüft
  außerdem: 72 Kombinationen aus Regler-Extremen des Schwarms × Bildrate (30/60/144/240 FPS) × Stufe, Fenstergröße
  ändern mit Schwarm, Auto-Play 90 s auf drei Stufen (7–8 Explosionen, unsichtbare Kräfte wechseln, danach alle weg),
  je 21 Moduswechsel mit Schwarm bzw. Farbe „Alter“.
- Flacker-Reduktion bei Explosion: größter Helligkeitssprung pro Bild 0,49 → 0,043, Anteil Bildpunkte mit Sprung
  > 10 %: 10,4 % → 0 % (Farbe „Wolken“); bei Farbe „Alter“ 5,2 % → 0 %.
- Fluid unverändert: alte und neue Fassung liefern dieselben drei Prüfsummen (`3ff93dc5-b33e3505`, `28e31dc5-e9c55505`,
  `ee1e9dc5-123c5505`; welche wie oft kommt, streut von Lauf zu Lauf).
- Ton (Analyser am Ausgang, Musik aus): Stille 0,003, Explosion Spitze 0,27, Sammel-Töne Spitze 0,06–0,08.

### Grenzen
- Maximum mit vielen Kräften (8,2 ms) liegt über dem 144-Hz-Budget (6,9 ms) → die Auto-Qualität geht dort auf Extrem.
  FPS wurden nur in der 60-Hz-Vorschau gemessen, nicht am 144-Hz-Monitor.
- **Klang nicht angehört** – nur gemessen, dass er entsteht und wie laut er ist. Ob „Sammeln“ und „Verschlucken“
  angenehm klingen oder nerven, kann nur ein Mensch beurteilen (Stellschrauben: Lautstärken und Mindestabstände in
  `audioGather`/`audioSwallow`).
- Schwarm: Partikel sehen keine einzelnen Nachbarn, nur Mittelwerte ihrer Umgebung. Dadurch wirkt der Schwarm eher wie
  fließende Bänder und Wolken als wie einzelne Vögel; feine Abstände zwischen einzelnen Partikeln gibt es nicht.
  Mit Kräften sammelt sich meist der ganze Schwarm an einer Kraft. Standardmäßig ist der Schwarm aus.
- Farbe „Alter“: Das Alter gleicht sich an ein Wolkenmuster an – Farbflecken einer Explosion halten deshalb nur einige
  Sekunden. Im Schwarm (alles bewegt sich) sind die Farbunterschiede geringer als im ruhigen Bild.
- Nach starken Kräften/Explosionen bleiben leere Stellen im Bild lange leer (die Strömung verteilt nicht neu) →
  Leertaste „Neu verteilen“.
- In einem fast quadratischen Fenster reicht die Anziehung über fast das ganze Bild.
- Das Gedränge ist grob (Rasterfeld ≈ 1/128 Bildhöhe): Partikel stoßen sich nicht einzeln ab, sehr feine Strukturen
  bleiben möglich.

### Stabilität – worauf achten
- Ohne Gegenkraft fällt das System in einen Punkt oder eine Linie zusammen (Bremsung + Anziehung = alles kommt zur
  Ruhe am selben Ort). Dagegen helfen drei Dinge zusammen: Kern pro Partikel, Drehung (Swirl) und das Gedränge. Bei
  neuen Kräften prüfen, ob sie nicht wieder einen Sammelpunkt erzeugen.
- Strömung nie als Beschleunigung einbauen (siehe unten), Rand-Kräfte weich halten.
- `partBlast`, Kräfte und Maus nutzen dieselben Einheiten; Tempo wird auf `MAX_SPEED` begrenzt – das verhindert, dass
  starke Kräfte/Explosionen Partikel durch die Wand oder ins Unendliche schießen.
- Explosionen erst nach dem Rechenschritt altern lassen (`updateBlasts` nach `swap`), sonst fehlt der erste Stoß.
- Schwarm: „Zusammenhalt“ braucht eine Grenze (hier: ab 3- bis 8-facher Dichte aus) – ohne sie und ohne „Abstand“ ballte
  sich alles auf das 100-Fache der Durchschnittsdichte. Neue anziehende Regeln immer mit Abstand = 0 testen.
- Raster-Textur: additiv gezeichnet wird in `gridV` (32 Bit braucht `EXT_float_blend`); `uGridNorm` muss zur Zahl der
  wirklich gezählten Partikel passen (`part.gridCount`), sonst stimmen Gedränge und Schwarm-Stärken nicht mehr.
- `PIXEL_PACK_BUFFER` nach jedem Gebrauch wieder lösen (`bindBuffer(…, null)`), sonst schlagen alle anderen
  `readPixels`-Aufrufe fehl.
- Alter nach `fract()` auf < 1 begrenzen (`fract` kann bei winzigen negativen Zahlen genau 1,0 liefern).

### Ausprobiert und verworfen
- **Strömung als Kraft aufs Tempo:** Partikel sammelten sich durch ihre Trägheit in dünnen Fäden und an den Wänden →
  jetzt reines Mitschieben ohne Trägheit, wirbelfreies Feld.
- **Magnet ohne Kern/Drehung:** alles kollabierte zu einem grellen Punkt. **Mit mehreren Kräften** kollabierte es trotz
  Kern wieder → Gedränge eingeführt.
- **Abstoßen ohne Grenze:** fegte das ganze Bild leer, Partikel klebten an den Wänden → begrenzte Blase und weiche Wand.
- **`sin`-Hash:** sichtbare Gittermuster → PCG-Hash. **Punkt nur am neuen Ort:** Spuren wie Perlenketten →
  Bewegungsunschärfe.
- **Helligkeit:** zuerst zu dunkel im Ruhezustand bzw. weiß ausgebrannte Kerne → `BRIGHT` 0,5, farbtreue
  Tonwert-Kompression, Grundhelligkeit 0,75.
- **Schwarm, weite Umgebung mit 16 Feldern, ohne Schlängeln:** der ganze Schwarm wurde eine einzige Masse, die an den
  Wänden entlang kreist → 32 Felder (`WIDE_LEVEL` 1) und gemeinsames Schlängeln; `COHESION` 0,5 ergab einen einzigen
  Klumpen, 0,25 nur flächige Schleier → 0,4.
- **Ein Raster für alles (RGBA32F, alle Partikel):** teurer auch bei ausgeschaltetem Schwarm → getrennte Raster.
- **Farbe „Alter“ mit schwacher Angleichung (`AGE_SYNC` 0,25):** fein gestreifte, blasse Mischfarben → 0,8.
  Farbwechsel als ein Regler 0…2 (Wolken → Alter lief sichtbar über „Tempo“) → drei eigene Anteile (`part.colorW`).
- **Verschluck-Ton bei jeder Messung (bis 9/s):** Dauerregen → höchstens ~4/s, zufällige Abstände.

### Testen
- Lokaler Server (`python -m http.server`, Name `satisim` = Port 8765 bzw. `satisim-b` = Port 8791 in
  `.claude/launch.json`),
  Seite mit `?v=N` neu laden (Cache). Hilfen in `.claude/` (nicht im Repo): `p-harness.js` (`__p.cost(n)` = ms pro Bild
  inkl. GPU-Wartezeit, `__p.stats()` = ungültige Partikel), `p-setup.js` (Auto-Play/Auto-Qualität aus, Partikel-Modus,
  `__crop` für Ausschnitt in echter Pixelgröße, `__sweep` führt die Maus, `__errors`), `run-p1.js` (alle Stufen: Bildkosten,
  GPU-Zeit per Timer-Query, FPS, GL-Fehler, 21 Moduswechsel, Fluid-Prüfsumme; `window.__pre` für Vorbereitung wie
  Kräfte setzen). Ergebnis in `window.__res`. Für Schritt 4/5: `s4-tools.js` (`__s.stats()` = Kennzahlen des Schwarms:
  Ordnung, Dichte-Kontrast, Anteil am Rand; `__s.run(n)`, `__s.set({…})`), `run-p4.js` (Schwarm an/aus auf allen Stufen,
  Regler-Extreme, `window.__opt = { forces: true, quick: true }`), `run-p5.js` (Farben, Alter, Auto-Play, alles zusammen),
  `run-ab.js` (Fluid-Prüfsumme 12-mal), `patchlib.py` (Änderungen an `index.html` per Python, erhält die Zeilenenden).
- Ton prüfen: echter Klick in die Vorschau (sonst läuft der AudioContext nicht), dann Analyser an `audio.master`.
  Direkt nach einem langen JavaScript-Aufruf zeigt ein Bildschirmfoto manchmal noch das alte Bild → 1–2 s warten.
- Ist die Vorschau verdeckt, ist `requestAnimationFrame` gedrosselt → FPS dann nicht messbar, stattdessen `__p.cost`.
- Fluid unverändert: `.claude/ab.js` mit alter Fassung (`.claude/old.html`, `.claude/pre4.html`) vergleichen – die
  Prüfsumme streut zwischen drei Werten; verglichen wird, ob alte und neue Fassung dieselben Werte liefern.
- Bedienung zusätzlich mit echten Maus-/Tasten-Eingaben im Browser geprüft (Tab, R, Leertaste, 1–5, Ziehen, Mausrad,
  Rechtsklick, Klick, `S`, `C`, Knöpfe „Tempo“/„Alter“ im Panel). Verkleinerte Bildschirmfotos zeigen Partikel nur als Nebel → `__crop` benutzen.
## Flüssigkeits-Modus (Partikel) – Schritte 1–3 von 6 fertig
- **Ausbauplan:** 1 Technik wählen und beweisen ✅ · 2 Physik-Grundsystem ✅ · 3 Darstellung über das Look-System ✅ ·
  4 Interaktion (Maus schiebt/zieht, Klick = Spritzer/Tropfen, Hahn, Leeren, Eimer kippen, Hindernisse) ⬜ ·
  5 Presets (Wasser, Öl, Honig, Gel, Quecksilber) ⬜ · 6 Ton, Auto-Play, Flacker-Reduktion, Panel-Feinschliff ⬜.
  Commits: `70b49c0` (1), `d2dd832` (2), `1eca9d5` (3).
- Code: Abschnitt `// ---------- Flüssigkeits-Modus (Partikel) ----------` in `index.html` (vor
  `// ----- Moduswechsel -----`), Konstanten in `LIQUID`, Zustand in `liq`, Modus-Objekt `id: 'liquid'`. Die Shader
  werden erst beim ersten Wechsel in den Modus übersetzt (`liqCompile`, ≈ 0,3 s).

### Technik
- **Nachbarsuche:** WebGL2 hat keine Compute-Shader. Lösung: ein feines Raster (`liq.grid`, RGBA32F), Feldgröße =
  Reichweite / 3 (kleiner als ein Partikel). Jedes Partikel wird als 1 Punkt in sein Feld gezeichnet und schreibt seine
  Daten hinein (`liqGrid`: Ort + Tempo bzw. Ort + Druck + Dichte) → höchstens ein Partikel pro Feld. Nachbarn = die
  7 × 7 Felder drumherum (49 Abfragen, keine Nachbar-Listen). Landen zwei Partikel im selben Feld, ist eines für die
  anderen unsichtbar (es selbst sieht alle). Gegenmittel: die Zeichen-Reihenfolge wechselt je Teilschritt (`uFlip`), und
  wer sein Feld teilt, rückt vom anderen ab (`RESCUE`). Gemessen: im normalen Betrieb 0–0,5 % unsichtbar.
  Geprüft gegen eine „jeder gegen jeden“-Rechnung im JavaScript: Dichte stimmt exakt (Abweichung 0).
- **Physik: Position Based Fluids (PBF)**, je Teilschritt 2 Raster-Füllungen + 2 Durchgänge über alle Partikel:
  1. `liqLambda`: Vorhersage (Schwerkraft, Tempo, Bremsung), Dichte messen (Gewicht `(1−q²)³`), daraus „Druck“
     `λ = −Überdichte · Steifigkeit · ρ0² / Σ|Gradient|²` (nur Überdichte zählt – locker gepackt ist erlaubt), nebenbei
     Tempo-Ausgleich mit den Nachbarn (Viskosität, XSPH). Ergebnis in `liq.pred` (xy = Tempo-Ausgleich, z = Druck,
     w = Dichte/Soll-Dichte).
  2. `liqPush`: wegschieben `Δp = −(h/ρ0) Σ (λi + λj − Nahbereichs-Zuschlag) · Gradient`, Zusammenhalt, neuer Ort,
     Tempo = (neuer − alter Ort) / Zeit + Tempo-Ausgleich, Abprallen am Rand.
- **Wände:** Nahe am Bildrand zählen die Spiegelbilder der Nachbarn (und das eigene) mit → Dichte stimmt auch am Rand,
  die Wand drückt weich zurück. Schnelle Partikel prallen mit 20 % ab (`BOUNCE`), langsame bleiben liegen.
- **Feste Teilschritte:** Schrittdauer `liq.H = Partikelabstand / STEP_RATE` (4,5) – hängt nur von der Partikelgröße
  ab, nicht von der Bildrate. Ein Bild rechnet so viele ganze Schritte, wie in seine Zeit passen (`liq.acc` hebt den
  Rest auf; gezeichnet wird um diesen Rest vorausgerechnet, `uAhead`). Höchstens 64 Schritte pro Bild.
  **Warum so viele Schritte:** Druck breitet sich pro Schritt nur etwa einen Partikelabstand weit aus
  („Schallgeschwindigkeit“ ≈ 0,9 · Abstand · Schritte/s). Mit 4,5/Abstand trägt sich ein volles Becken selbst: unten nur
  5 % dichter als oben – auf jeder Stufe gleich (gemessen 1,051–1,052). Mehr Partikel = kleinere Partikel = mehr
  Schritte: Kosten wachsen mit Partikelzahl^1,5.
- **Normierung:** Alle Partikel zusammen füllen immer `FILL_MAX` (50 %) des Bildes (`d = √(0,5 · Seitenverhältnis /
  Anzahl / Dichte-Regler)`), gerechnet wird in Bildhöhen und Sekunden. Viskosität, Zusammenhalt und Schrittdauer werden
  auf die Partikelgröße umgerechnet. Geprüft (Dammbruch auf Niedrig/Hoch/Maximum): Schwerpunkt und mittleres Tempo
  nach 1 s, 2,5 s, 5 s, 10 s praktisch gleich (z. B. Schwerpunkt 0,468/0,468/0,468, Tempo 0,74/0,73/0,72).
- **Vorrat:** Die Zustands-Textur bietet Platz für `lside²` Partikel; im Bild sind die ersten `liq.count` (beim
  Einfüllen 60 %). Gerechnet werden nur die Zeilen mit Partikeln (`liqPass`). Der Rest ist für den Hahn in Schritt 4.
- **Regler** (Panel-Abschnitt „Flüssigkeit (Partikel)“): **Schwerkraft** 0–200 % (100 % = 4 Bildhöhen/s²),
  **Fallrichtung** (wie im Fluid-Modus), **Viskosität** (Tempo-Ausgleich bis 0,004 Bildhöhen²/s + Bremsung bis 5/s –
  die Bremsung entspricht Reibung an einer dünnen Glasscheibe und macht „Honig“ erst möglich), **Zusammenhalt**
  (Oberflächenspannung), **Steifigkeit** (Anteil des Dichte-Fehlers pro Schritt: 0,2 … 0,45), **Dichte** 70–140 %
  (ändert die Partikelgröße: dichter = die Flüssigkeit nimmt weniger Platz ein).
- **Zusammenhalt = „Haut“:** Nur Partikel an der Oberfläche (Dichte unter dem Soll) ziehen einander an, beidseitig
  gleich stark (Produkt der beiden Oberflächen-Anteile). Stärke ∝ 1/Reichweite², damit gleich große Tropfen auf jeder
  Stufe gleich gut halten. Geprüft: ein Rechteck aus Flüssigkeit zieht sich in Schwerelosigkeit in 2 s zu einem Kreis
  genau der richtigen Größe zusammen (Rundheit 0,93–0,99 auf Niedrig/Hoch/Maximum); ohne Zusammenhalt verfliegt es.
- **Stufenwechsel** übernimmt die Flüssigkeit (`liqResize`: mehr Partikel = Kopien mit kleinem Versatz, weniger =
  Auswahl). Fenstergröße: Orte sind als 0..1 gespeichert, die Flüssigkeit wird mitgestreckt; Partikelgröße,
  Schrittdauer und Raster passen sich an.

### Darstellung (Schritt 3)
- `liqUpdateFields()` macht aus den Partikeln die Bilder, die die Looks lesen: Jedes Partikel wird als weicher Fleck
  (Radius 2 Partikelabstände, `(1−r²)²`) additiv gezeichnet → **Dichte-Feld** im Format der Farb-Textur (Rot = Menge,
  Grün/Blau = Menge · cos/sin der Palettenposition), am Bildrand ausgeglichen (`liqField`: dort fehlt sonst die Hälfte
  der Nachbarn). Dazu die **mittlere Strömung** (halbe Auflösung, in den Einheiten des Fluid-Modus: Bezugs-Rasterfelder
  pro Sekunde) und deren Drehung (derselbe `curl`-Shader). Damit laufen alle 12 Looks, Oberflächen-Baustein, Schaum und
  Bloom unverändert. Auflösung = Bildschirm × `pscale` der Stufe.
- **Farbmenge:** im Inneren `BODY` (0,7). **Druck wird sichtbar:** pro 1 % Verdichtung 6 % mehr Menge (`PRESSURE`) –
  die Flüssigkeit wird nach unten „tiefer“ (Wasser dunkler, Regenbogen/Marmor in Schichten, Aufprall leuchtet auf).
  Ohne das wäre sie für die Looks eine völlig gleichmäßige Fläche.
- **Palettenposition je Partikel:** aus seiner Nummer (`TINT_SPAN` 0,6 der Palette, beim Einfüllen von unten nach oben)
  plus wandernde Verschiebung – die Farbschichten vermischen sich beim Schwappen.
- **Look „Partikel“** (`only: 'liquid'`, `sprites: true`): `liqDrawSprites` zeichnet jedes Partikel als kleine Kugel;
  Look-Regler **Farbe nach** (Tempo/Dichte) und **Partikelgröße**.
- Jeder Modus merkt sich seinen Look (Flüssigkeit startet mit „Wasser“).

### Messwerte (1920×1080, Dammbruch in Bewegung; GPU-Zeit für 1/60 s; „Bild“ = ganzes Bild mit Look „Wasser“ und Bloom)
| Stufe | Platz | im Bild | Schritte/s | Such-Raster | Rechnen | Felder | Bild |
|---|---|---|---|---|---|---|---|
| Niedrig | 6.400 | 3.840 | 382 | 210×118 | 0,5 ms | 0,2 ms | 1,3–1,8 ms |
| Mittel | 16.384 | 9.830 | 611 | 336×189 | 1,3 ms | 0,3 ms | 2,4 ms |
| Hoch | 25.600 | 15.360 | 764 | 420×236 | 2,5 ms | 0,6 ms | 4,1 ms |
| Ultra | 43.264 | 25.958 | 993 | 547×307 | 4,5 ms | 0,6 ms | 6,5 ms |
| Extrem | 65.536 | 39.322 | 1.222 | 673×378 | 8,1 ms | 0,7 ms | 10,2 ms |
| Maximum | 73.984 | 44.390 | 1.298 | 715×402 | 10,6 ms | 0,85 ms | 12,4 ms |
- Darstellung allein: Oberflächen-Baustein 0,04–0,14 ms, Schaum 0,03–0,22 ms, Look „Wasser“ ≈ 0,26 ms, Partikel-Bild
  0,02–0,11 ms. Die Physik ist der teure Teil.
- **Wie viele Partikel bei 60 FPS:** etwa 45.000–50.000 im Bild (Prototyp: 50.176 → 11,6 ms; 65.536 → 18,6 ms = zu viel;
  102.400 → 43,5 ms). 13 Looks × 6 Stufen: alle 60 FPS, GL-Fehler 0 (mit 49.766 Partikeln fielen Marmorpapier/Galaxie
  auf 51–54 FPS → Stufe Maximum deshalb 272² statt 288²). FPS nur in der 60-Hz-Vorschau gemessen.
- Extremfälle (alle ohne ungültige Werte, nichts verlässt das Bild): alle Partikel in einer Ecke (25-fache Dichte) und
  alle exakt auf einem Punkt → entfaltet sich in ≈ 2 s zu einem normalen Becken; 5 s Zeitschritt auf einmal (64
  Schritte, 14 ms); Fenster hoch/sehr breit/sehr schmal/klein; Stufenwechsel mitten im Schwappen; 40 s Dauerlauf mit
  springenden Reglern; alle Regler-Anschläge einzeln und in den schlimmsten Kombinationen.
- Ruhe: Becken nach dem Einschwingen mittleres Tempo 0,003–0,007 Bildhöhen/s (nicht sichtbar).
- Fluid unverändert: Prüfsummen wie vorher, Bilder von 10 Looks bitgenau gleich; 33 Moduswechsel ohne GL-Fehler.

### Grenzen
- **Partikelzahl:** Die Kosten wachsen mit Partikelzahl^1,5 (mehr Partikel brauchen kürzere Schritte). Mehr als
  ≈ 50.000 im Bild gehen bei 60 FPS nicht; bei 144 Hz dürfte die Auto-Qualität auf „Extrem“ oder „Ultra“ gehen.
- **Leicht zusammendrückbar:** unten im Becken 5 % dichter (bei Schwerkraft 200 % oder Steifigkeit 0 % bis 23–34 %).
  Harte Aufschläge federn kurz nach. Ein Verfahren mit echtem Druck-Löser auf einem groben Raster (wie FLIP) könnte das
  beheben und mehr Partikel erlauben – größerer Umbau, bisher nicht gemacht.
- **Sehr schmale Fenster** kosten mehr (kleinere Partikel → bis 1.900 Schritte/s gemessen bei 2:7).
- **Viskosität:** echter Honig ist nicht erreichbar (der Tempo-Ausgleich reicht nur einen Nachbarn weit pro Schritt);
  die zusätzliche Bremsung lässt die Flüssigkeit aber zäh kriechen.
- **Ohne Zusammenhalt** (0 %) verfliegt die Flüssigkeit in Schwerelosigkeit wie Gas.
- **Farben mischen sich nicht zurück:** Jedes Partikel behält seine Palettenposition; nach langem Rühren wird aus den
  Schichten ein feines Gesprenkel.
- Looks, die die Farbmenge als Höhe lesen, zeigen im Inneren nur den Druck-Verlauf – die Strömung im Inneren ist dort
  kaum zu sehen (anders als im Fluid-Modus mit seinen Schlieren).
- Noch keine Interaktion (Schritt 4), kein eigener Ton, kein Auto-Play-Inhalt (Schritt 6) – im Auto-Play läuft der
  Modus einfach weiter.

### Stabilität – worauf achten
- **`MAX_FIX` nicht entfernen:** Bei 400–1.300 Schritten pro Sekunde macht jeder kleine Schubs ein großes Tempo
  (Tempo = Weg / Schrittdauer). Ohne die Grenze fürs Korrektur-Tempo (0,05 Bildhöhen/s je Schritt, zusätzlich zum
  eigenen Tempo) heizt sich die Flüssigkeit beim Aufprall auf und „kocht“ dauerhaft wie Gas.
- **Steifigkeit höchstens ≈ 0,45:** Die Korrekturen benachbarter Partikel überlagern sich (Jacobi-Verfahren); ab
  ≈ 0,6 zittert alles, in stark zusammengedrückter Flüssigkeit (> 15 %) schon ab 0,45–0,5.
- **Zu wenige Schritte = das Becken sackt zusammen und zittert am Boden** (bei 8 statt 13 Schritten pro Bild: unten
  20 % dichter und dort Zittern). Deshalb `STEP_RATE` nicht senken, ohne nachzumessen.
- **Zusammenfallen verhindern:** Im Raster ist nur ein Partikel pro Feld sichtbar – stark zusammengepresste
  Flüssigkeit „merkt“ ihre Dichte nicht mehr und fällt weiter zusammen. Dagegen: `RESCUE` (Abrücken im selben Feld),
  wechselnde Zeichen-Reihenfolge, Zusammenhalt nur an der Oberfläche. Ab Dichte 1,5 (`CRUSH`) wird nur noch
  weggerückt, ohne Tempo zu gewinnen – ein Klumpen entfaltet sich, statt zu explodieren.
- **Paar-Kräfte immer beidseitig gleich** (sonst bleibt der Impuls nicht erhalten → die Oberfläche wird unruhig).
- Mindestabstand zum Rand je Partikel leicht verschieden (`JITTER`), sonst lägen in einer Ecke alle exakt aufeinander
  und sähen einander als „ich selbst“ (Abstand < 10⁻⁶ gilt als ich selbst).
- `near`, `far`, `half` nicht als Namen in Shadern benutzen.

### Ausprobiert und verworfen
- **Wenige Schritte mit vielen Durchgängen / weiche Nachgiebigkeit:** Becken unten 20–40 % dichter oder Zittern → viele
  kurze Schritte mit je einem Durchgang.
- **Druck von Schritt zu Schritt aufheben („Warmstart“):** rechnerisch instabil ab einem Anteil von 0,5 → nicht gebaut.
- **Zusammenhalt als Anziehung zwischen allen Nachbarn:** im Inneren entsteht ein starres Gitter – die Flüssigkeit wird
  zäh wie Gel, umso mehr, je kleiner die Partikel (Dammbruch auf „Maximum“ nach 2,5 s fast stehend). **Nur für
  Oberflächen-Partikel, aber einseitig:** Oberfläche wird unruhig und bucklig → beidseitig gleiche „Haut“.
- **Schlieren (schwankende Farbmenge je Partikel):** werden beim Schwappen zu feinen Fäden und dann zu Körnung →
  Metallic/Wasser/Glas voller kleiner Runzeln und Glanzpunkte → stattdessen den Druck sichtbar machen.
- **Farbmenge 1,2 im Inneren:** Feuer weiß überstrahlt, Metallic eine weiße Fläche, sobald eine Lichtfläche der
  Umgebung vorbeidreht → 0,7.

### Testen
- Hilfen in `.claude/` (nicht im Repo): `l-tools.js` (lädt `__t`/`__p` mit; `__l.stats()` = ungültige Werte, Tempo,
  Schwerpunkt, Dichte-Verteilung; `__l.hidden()` = Anteil unsichtbarer Partikel; `__l.verify()` = Dichte gegen
  JavaScript-Vergleichsrechnung; `__l.run(n)`, `__l.set({…})`, `__l.reset()`, `__block(x, y, breite, packung, anzahl)`,
  `__pool()`, `__bins()` = Tempo/Dichte in 8 Höhen-Schichten, `__scan({…})`, `__trace([…])`), `run-l3.js` (13 Looks ×
  6 Stufen, Kosten, Moduswechsel; Ergebnis in `window.__res`), `ab2.js` (Fluid-Bilder alt/neu), alte Fassungen
  `pre-liq.html`, `pre-l3.html`.
- Der Abschnitt des Modus liegt zum Bearbeiten als `.claude/liquid.js` vor (Panel: `liquid-panel.html`);
  `python .claude/splice.py` setzt beides in `index.html` ein. **Immer dort ändern, nicht direkt in `index.html`** –
  sonst überschreibt der nächste Lauf die Änderung.
- Dammbruch = `liq.fresh = true` (neu einfüllen). In Bewegung messen, nicht im Ruhezustand.
