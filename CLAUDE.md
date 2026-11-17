# Satisim – Fluid-, Partikel- & Mandelbrot-Simulationsspiel

## Ziel des Projekts
Ein interaktives Simulations-Spiel (später Desktop-App), in dem man mit Werten, Szenarien, Farben und
Geschwindigkeiten spielen kann. Fünf Modi in einer App per Moduswechsel: **Fluid**, **Mandelbrot**, **Partikel**, **Flüssigkeit (Partikel)**, **3D-Fraktal-Flug**.
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
- Mehrere Modi in einer App: **Fluid**, **Mandelbrot**, **Partikel**, **Flüssigkeit (Partikel)** und
  **3D-Fraktal-Flug** (Abschnitte „Modi“, „Partikel-Modus“, „Flüssigkeits-Modus (Partikel)“ und „3D-Fraktal-Flug“ unten).
  Alle fünf sind fertig ausgebaut.
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

**Flüssigkeit (Partikel):** ✅ Maus schiebt oder zieht die Flüssigkeit, ✅ Tropfen und Spritzer bei Klick, ✅ Strahl und Hahn,
✅ Eimer kippen, ✅ Hindernisse, ✅ Presets (Wasser, Öl, Honig, Gel, Quecksilber), ✅ eigener Klang, ✅ Auto-Play.
⬜ zwei Flüssigkeiten gleichzeitig, ✅ Szenarien speichern (Regler, Look, Hahn – ohne Hindernisse).

**3D-Fraktal-Flug:** ✅ selbst durch Mandelbulb, Mandelbox, Menger-Schwamm, Sierpinski-Pyramide, 3D-Julia fliegen,
✅ Faltungs-Baukasten für eigene Körper (mit Zufalls-Knopf), ✅ Kamera merken, ✅ Kameraflug als Bildschirmschoner,
✅ eigener Klang. ⬜ Zwei-Finger-/Gamepad-Bedienung, ⬜ wandernde Farben, ⬜ Sonnenstand als Regler.

**Mandelbrot:** ✅ Zoom per Scrollen/Ziehen mit Trägheit, ✅ Julia-Sets live mit Mausposition, ✅ animierte Farbpaletten,
✅ automatische Zoom-Fahrt zu schönen Stellen, ✅ tiefer Zoom bis 10³⁰-fach (Bezugsbahn statt Float32-Grenze).
⬜ Zwei-Finger-Zoom auf Touch-Geräten, ⬜ weitere Farbgebungen, ⬜ tiefe Mini-Mandelbrote als Ziel der Zoom-Fahrt.

**Modusübergreifend:** ✅ Paletten-Presets (Neon, Sunset, Ozean, Lava …) mit sanftem Überblenden. ✅ Presets/Szenarien
speichern und als Textcode teilen. ✅ Idle-Modus/Screensaver (Auto-Play). ✅ Screenshot- und Hintergrundbild-Export
(bis 4K), ⬜ Video-Export. ⬜ Optional kleine
Sammelziele („entdecke 10 Muster“). ✅ Moduswechsel Fluid/Mandelbrot/Partikel/Flüssigkeit/3D-Flug, ⬜ Desktop-App (Tauri oder Electron).

**Satisfying-Faktoren:** ✅ Audio-Feedback per Web Audio API (selbst synthetisiert, Pentatonik, Lautstärke/Tonhöhe abhängig
von Geschwindigkeit, ✅ im Mandelbrot-Modus von der Zoomtiefe, ✅ im Partikel-Modus von Tempo und Dichte der Partikel). ✅ Lofi-Musik (generativ: Akkorde,
Vinyl-Knistern, sanfte Drums, reagiert auf Interaktion). ✅ Wenig UI: minimalistisches, ausblendbares Panel (⬜ Radialmenü).
✅ Bloom/Glow, dunkler Hintergrund, kontrastreiche Paletten. ✅ Option „Flackern reduzieren“.

**Looks:** ✅ Palette, Regenbogen, Geschwindigkeit, Wirbel, Feuer / Glut, Metallic, Glas / Kristall, Wasser,
Seifenblase / Ölfilm, Tinte & Aquarell, Marmorpapier (Ebru), Galaxie / Nebel / Aurora.

## Aktueller Stand
- Alles in **einer Datei**: `index.html` (HTML, CSS, JavaScript, GLSL-Shader). Öffnen per Doppelklick im Browser.
- **3D-Fraktal-Flug** (Abschnitt ganz unten, **alle 6 Schritte fertig**): Man fliegt selbst durch 3D-Fraktale
  (Mandelbulb, Mandelbox, Menger-Schwamm, Sierpinski-Pyramide, 3D-Julia, Faltungs-Baukasten mit Zufalls-Knopf),
  gerechnet per Raymarching. Beim Fliegen regelt sich die Auflösung nach der Rechenzeit (60 FPS), im Stillstand wird
  das Bild scharf nachgerechnet und geglättet. Regler für Form, Flug, Licht und Farbe, vier Kamera-Plätze, eigener
  Klang, Kameraflug als Auto-Play (gleitet dicht über die Oberfläche, wechselt alle 20 s die Stelle).
- **Fünf Modi in einer App:** Fluid, Mandelbrot, Partikel, Flüssigkeit (Partikel) und 3D-Fraktal-Flug. Umschalten mit `Tab`
  (Umschalt + `Tab` = zurück) oder im Panel-Abschnitt „Modus“, mit weicher Überblendung (0,8 s). Panel, Paletten,
  Bloom, Flacker-Reduktion, Qualität, FPS, Ton und Auto-Play gibt es nur einmal – sie gelten für alle Modi (Abschnitt
  „Modi“ unten). Ein Modus, der nicht zu sehen ist, kostet nichts und behält seinen Zustand.
- **Flüssigkeits-Modus (Partikel)** (Abschnitt unten, **alle 6 Schritte fertig**): bis 43.264 einzelne Partikel im
  Bild, die sich wie Wasser verhalten (fallen, schwappen, spritzen, Tropfen halten zusammen). Nachbarsuche über ein
  feines Raster auf der GPU, Physik nach „Position Based Fluids“. Die Maus schiebt oder zieht die Flüssigkeit, Klick =
  Tropfen + Spritzer, Maustaste halten = Strahl, Hahn füllt nach, Leeren, Eimer kippen, Hindernisse (Stift und
  Radierer des Fluid-Modus), Presets Wasser/Öl/Honig/Gel/Quecksilber, eigener Klang, Auto-Play, Flacker-Reduktion
  bei Spritzern. Dargestellt über die vorhandenen Looks (Start: „Wasser“) plus Look „Partikel“.
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
  Auto ab), `A` = Auto-Play (im 3D-Flug `P`, weil `A` dort fliegt), `M` = stumm, `I` = Bild speichern.
- Bedienung 3D-Fraktal-Flug: Klick = Maus fangen (bewegen = umsehen, `Esc` = frei) oder mit gedrückter Maustaste
  ziehen, `W` `A` `S` `D` = fliegen, Leertaste / `C` = hoch / runter, Umschalt = schneller, `B` = bremsen,
  Mausrad = Flug-Tempo, `Y` / `X` = rollen, `G` = Horizont gerade, Pfeiltasten = umsehen, `R` = zurück zum Start,
  `1`–`6` = Fraktal wählen, `N` = Zufalls-Form (Baukasten), `K` = Kamera merken, `7`–`0` = gemerkte Kamera
  anspringen, `P` = Auto-Play.
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
- Bedienung Flüssigkeit (Partikel): Maus bewegen = die Hand schiebt die Flüssigkeit (`R` = Schieben ↔ Ziehen),
  Mausrad = Reichweite, Klick = Tropfen + Spritzer, Maustaste halten = Strahl aus der Maus, `T` = Hahn an der Maus
  auf/zu, Leertaste = leeren, `N` = neu füllen, `G` = Eimer kippen (Fallrichtung 90° weiter, Umschalt + `G` = zurück),
  `P` = nächstes Preset, `W` = Hindernis-Stift an/aus, `E` = Radierer an/aus, `X` = alle Hindernisse löschen, rechte
  Maustaste ziehen = Hindernis (mit Umschalt-Taste = radieren), `1`–`9`/`0` = Look wählen, `←`/`→` = Look weiterschalten.
- **Szenarien und Bild-Export** (Abschnitt „Szenarien und Bild-Export“ unten, gilt für alle Modi): Panel-Abschnitt
  „Szenarien“ (mitgelieferte Start-Szenarien je Modus, eigene speichern/laden/löschen, als Textcode kopieren und
  einfügen) und „Bild speichern“ (PNG in Fenstergröße, doppelt, Bildschirm-, 4K- oder Handy-Hintergrundbild; Taste `I`).
- Noch nicht umgesetzt: Video-Export, Desktop-App, Hindernisse im Szenario.
- Testen: Die Seite läuft per Doppelklick. Zum automatischen Prüfen (FPS, GPU-Zeit per `EXT_disjoint_timer_query_webgl2`,
  alle Stufen × alle Looks) wurde sie über einen kleinen lokalen Server geladen (`python -m http.server`). Innerhalb
  eines Seitenaufrufs ist die Simulation bei gleichem Ablauf bitgenau wiederholbar (Prüfsumme der Farb-Textur) – gut für
  Vorher/Nachher-Vergleiche. Zwischen zwei Seitenaufrufen traten zwei verschiedene Prüfsummen auf (Ursache ungeklärt);
  alte und neue Version lieferten aber beide genau dieselben zwei Werte. Der Umbau auf mehrere Modi und der
  Mandelbrot-Modus wurden so geprüft: Fluid-Prüfsumme und fertige Bilder von 7 Looks bitgenau wie vorher.
  Die GPU-Zeitmessung schwankt auf dem Testrechner stark (gleiche Stelle 4–14 ms je nach Durchlauf) – verlässlich
  sind nur direkte Vergleiche hintereinander mit vielen Wiederholungen.
  Konsole: Im Partikel- und im Flüssigkeits-Modus meldete der Browser bei laufendem Ton in jedem zweiten Bild eine
  Leistungs-Warnung („READ-usage buffer was written, then fenced …“) – behoben, indem der Zwischenspeicher für die
  Kennzahlen vor jeder Abfrage neu angelegt wird (`bufferData`). Beim Testen auch Warnungen ansehen, nicht nur Fehler.

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
- **Flüssigkeits-Modus (Partikel):** Rühren = `audioPaint` (nur wo die Hand nass ist), dazu `audioLiqBloop`
  (Plätschern), `audioLiqImpact` (Aufprall), `audioLiqFill` (Tonfolge beim Nachfüllen: je voller, desto höher),
  `audioLiqSplash` (Spritz-Rauschen beim Klick), `audioLiqDrain` (Leeren). Die Zahlen dafür liefert `liqStat`
  (Abschnitt „Flüssigkeits-Modus“, „Klang, Auto-Play, Flacker-Reduktion“).
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
- Flüssigkeits-Modus (Partikel): Spritzer schwächer, Aufprall leuchtet weniger auf, einzeln fliegende Tropfen blasser
  (Messwerte im Abschnitt „Flüssigkeits-Modus“).
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
- Zeichnen: `obstacleStroke(x, y, set, radius)` (Shader `obstacleBrush`) zieht eine dicke Linie vom letzten Punkt; Breite = Pinsel-Ring,
  mindestens 2 % der Bildhöhe (dünnere Wände wären auf niedriger Stufe undicht). `set` = Hindernis-Bild (Standard: das
  des Fluid-Modus; der Flüssigkeits-Modus übergibt sein eigenes `liq.obstacles` und eine feste Breite), ebenso bei
  `wipeObstacles(set)` und `drawObstacles(target, set)`. `clearObstacles()` leert alles und
  schaltet zurück auf die unveränderte Simulation. Anzeige: `drawObstacles(target)` (Shader `obstacleDraw`) legt die
  Hindernisse nach dem Look über das Bild – dunkle Fläche mit hellem Rand, dunkler als die Bloom-Schwelle; sieht in jedem
  Look gleich aus (Looks bleiben unverändert).
- **Bedienung:** Panel-Abschnitt „Hindernisse“ (gehört zum Fluid- und zum Flüssigkeits-Modus, `data-mode="fluid liquid"`;
  jeder der beiden Modi hat eigene Hindernisse, die Werkzeug-Wahl gilt für beide; der erste Knopf heißt im
  Flüssigkeits-Modus „Hand“) mit Werkzeugen **Farbe / Hindernis / Radierer** (`setTool`) und Knopf
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
  Auto-Qualität schaltet dann nicht hoch), `label` (kurzer Name für den Modus-Knopf), `looks` (Look-Stand, falls
  der Modus die Looks benutzt – siehe „Look-System“) und `autoplayKey` (Taste für Auto-Play, falls der Modus `A`
  selbst braucht – der 3D-Flug nimmt `P`).
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
  `readPixels`-Aufrufe fehl. Vor jeder Abfrage neu anlegen (`bufferData`), sonst füllt eine Leistungs-Warnung des
  Browsers die Konsole.
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
## Flüssigkeits-Modus (Partikel) – alle 6 Schritte fertig
- **Ausbauplan:** 1 Technik wählen und beweisen ✅ · 2 Physik-Grundsystem ✅ · 3 Darstellung über das Look-System ✅ ·
  4 Interaktion (Hand der Maus, Tropfen/Spritzer, Strahl, Hahn, Leeren, Eimer kippen, Hindernisse) ✅ ·
  5 Presets (Wasser, Öl, Honig, Gel, Quecksilber) und ruhigeres Verhalten ✅ · 6 Ton, Auto-Play, Flacker-Reduktion,
  Panel ✅. Commits: `70b49c0` (1), `d2dd832` (2), `1eca9d5` (3), `ab31328` (4), `fa8c42f` (5), `4e5137d` (6),
  danach eine kleine Korrektur am Strahl (gleiche Füllzeit auf jeder Stufe).
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
  1. `liqLambda`: Vorhersage (Schwerkraft, Hand, Spritzer, Tempo, Bremsung), Dichte messen (Gewicht `(1−q²)³`), daraus
     „Druck“ `λ = −Überdichte · Steifigkeit · ρ0² / Σ|Gradient|²` (nur Überdichte zählt – locker gepackt ist erlaubt),
     nebenbei Tempo-Ausgleich mit den Nachbarn (Viskosität, XSPH). Ergebnis in `liq.pred` (xy = Tempo-Ausgleich,
     z = Druck, w = Dichte/Soll-Dichte).
  2. `liqPush`: wegschieben `Δp = −(h/ρ0) Σ (λi + λj − Nahbereichs-Zuschlag) · Gradient`, Zusammenhalt, neuer Ort,
     Tempo = (neuer − alter Ort) / Zeit + Tempo-Ausgleich, Abprallen am Rand.
- **Wände:** Nahe am Bildrand zählen die Spiegelbilder der Nachbarn (und das eigene) mit → Dichte stimmt auch am Rand,
  die Wand drückt weich zurück. Schnelle Partikel prallen mit 20 % ab (`BOUNCE`), langsame bleiben liegen.
- **Feste Teilschritte:** Schrittdauer `liq.H = Partikelabstand / STEP_RATE` (4,5) – hängt nur von der Partikelgröße
  ab, nicht von der Bildrate. Ein Bild rechnet so viele ganze Schritte, wie in seine Zeit passen (`liq.acc` hebt den
  Rest auf; gezeichnet wird um diesen Rest vorausgerechnet, `uAhead`). Höchstens 64 Schritte pro Bild.
  **Warum so viele Schritte:** Druck breitet sich pro Schritt nur etwa einen Partikelabstand weit aus
  („Schallgeschwindigkeit“ ≈ 0,9 · Abstand · Schritte/s). Mit 4,5/Abstand trägt sich ein volles Becken selbst: unten nur
  5 % dichter als oben – auf jeder Stufe gleich. Mehr Partikel = kleinere Partikel = mehr Schritte: Kosten wachsen mit
  Partikelzahl^1,5.
- **Normierung:** Alle Partikel zusammen (samt Vorrat) füllen immer `FILL_MAX` (50 %) des Bildes (`d = √(0,5 ·
  Seitenverhältnis / Anzahl / Dichte-Regler)`), gerechnet wird in Bildhöhen und Sekunden. Viskosität, Zusammenhalt und
  Schrittdauer werden auf die Partikelgröße umgerechnet. Geprüft (Dammbruch je Preset auf allen 6 Stufen): mittleres
  Tempo und Schwerpunkt nach 1 s praktisch gleich (Wasser: Tempo 0,75–0,78, Schwerpunkt 0,473–0,475; Honig 0,197–0,199).
- **Vorrat:** Die Zustands-Textur bietet Platz für `lside²` Partikel; im Bild sind die ersten `liq.count` (beim
  Einfüllen 60 % = 30 % der Bildfläche). Gerechnet werden nur die Zeilen mit Partikeln (`liqPass`). Den Rest holen
  Tropfen, Strahl und Hahn ins Bild (`liqSpawn`); ist er aufgebraucht, ist das Becken „voll“ (50 % der Bildfläche).
- **Regler** (Panel-Abschnitt „Eigenschaften“): **Schwerkraft** 0–200 % (100 % = 4 Bildhöhen/s²),
  **Fallrichtung** (wie im Fluid-Modus), **Viskosität** (Tempo-Ausgleich bis 0,004 Bildhöhen²/s + Bremsung bis 5/s –
  die Bremsung entspricht Reibung an einer dünnen Glasscheibe und macht „Honig“ erst möglich), **Zusammenhalt**
  (Oberflächenspannung), **Steifigkeit** (Anteil des Dichte-Fehlers pro Schritt: 0,2 … 0,45), **Dichte** 70–140 %
  (ändert die Partikelgröße: dichter = die Flüssigkeit nimmt weniger Platz ein).
- **Zusammenhalt = „Haut“:** Nur Partikel an der Oberfläche (Dichte unter dem Soll) ziehen einander an, beidseitig
  gleich stark (Produkt der beiden Oberflächen-Anteile). Stärke ∝ 1/Reichweite², damit gleich große Tropfen auf jeder
  Stufe gleich gut halten. Der Regler wirkt nicht gleichmäßig (`liqCohesion()`: `c · (0,3 + 0,7·c²) · COHESION` (150) –
  30 % ≈ 16, 100 % = 150). Seit Schritt 5:
  - **Die Haut endet nicht an Wänden und Hindernissen:** Auch die Spiegelbilder hinter der Wand ziehen mit (die Wand
    wird „benetzt“); an Hindernissen wird jeder Nachbar an der (als eben angenommenen) Oberfläche gespiegelt
    (`cling`). Ausnahme: die Wand, die gerade „oben“ ist, und waagrechte Unterseiten von Hindernissen
    (`1 − smoothstep(0,8; 0,97; …)`) – sonst blieben Tropfen an der Decke kleben.
  - **Die Haut wird gedämpft** (`SKIN_VISC` 0,003, wächst quadratisch mit dem Zusammenhalt): Partikel an der
    Oberfläche gleichen ihr Tempo zusätzlich aneinander an. Ohne das „kocht“ die Oberfläche bei starkem Zusammenhalt.
- **Stufenwechsel** übernimmt die Flüssigkeit (`liqResize`: mehr Partikel = Kopien mit kleinem Versatz, weniger =
  Auswahl). Fenstergröße: Orte sind als 0..1 gespeichert, die Flüssigkeit wird mitgestreckt; Partikelgröße,
  Schrittdauer, Raster und das Hindernis-Bild passen sich an.

### Darstellung (Schritt 3)
- `liqUpdateFields()` macht aus den Partikeln die Bilder, die die Looks lesen: Jedes Partikel wird als weicher Fleck
  (Radius 2 Partikelabstände, `(1−r²)²`) additiv gezeichnet → **Dichte-Feld** im Format der Farb-Textur (Rot = Menge,
  Grün/Blau = Menge · cos/sin der Palettenposition), am Bildrand und an Hindernissen ausgeglichen (`liqField`: dort
  fehlt sonst die Hälfte der Nachbarn). Dazu die **mittlere Strömung** (halbe Auflösung, in den Einheiten des
  Fluid-Modus: Bezugs-Rasterfelder pro Sekunde) und deren Drehung (derselbe `curl`-Shader). Damit laufen alle 12 Looks,
  Oberflächen-Baustein, Schaum und Bloom unverändert. Auflösung = Bildschirm × `pscale` der Stufe.
- **Farbmenge:** im Inneren `BODY` (0,7). **Druck wird sichtbar:** pro 1 % Verdichtung 6 % mehr Menge (`PRESSURE`) –
  die Flüssigkeit wird nach unten „tiefer“ (Wasser dunkler, Regenbogen/Marmor in Schichten, Aufprall leuchtet auf).
  Ohne das wäre sie für die Looks eine völlig gleichmäßige Fläche.
- **Palettenposition je Partikel:** aus seiner Nummer, über alle Partikel samt Vorrat (`TINT_SPAN` 1,0 → beim
  Einfüllen 0,6 der Palette von unten nach oben; was aus dem Hahn kommt, hat eine andere Farbe) plus wandernde
  Verschiebung – die Farbschichten vermischen sich beim Schwappen.
- **Look „Partikel“** (`only: 'liquid'`, `sprites: true`): `liqDrawSprites` zeichnet jedes Partikel als kleine Kugel;
  Look-Regler **Farbe nach** (Tempo/Dichte) und **Partikelgröße**.
- Jeder Modus merkt sich seinen Look (Flüssigkeit startet mit „Wasser“). Hindernisse liegen wie im Fluid-Modus über
  dem fertigen Bild (`drawObstacles(target, liq.obstacles)`). Beim Leeren blendet die Flüssigkeit aus (`liqFade`).

### Interaktion (Schritt 4)
- **Bedienung:** Maus bewegen = die **Hand** schiebt die Flüssigkeit weg (oder zieht sie an: Taste `R` bzw. Knöpfe
  Schieben/Ziehen) und nimmt sie in ihrer Bewegung mit · Mausrad = Reichweite der Hand · **Klick** = ein Tropfen neuer
  Flüssigkeit an der Maus + ein Spritzer in der vorhandenen · **Maustaste halten** (ab 0,2 s) = Strahl aus der Maus ·
  `T` = **Hahn** an der Maus auf/zu (Schalter im Panel: an der letzten Stelle, anfangs oben in der Mitte) ·
  **Leertaste** = leeren · `N` = neu füllen (Block links, der zusammensackt) · `G` = **Eimer kippen** (Fallrichtung 90°
  weiter, mit Umschalt zurück; auch Knopf und Regler) · `W` Hindernis-Stift, `E` Radierer, `X` alle Hindernisse
  löschen, rechte Maustaste ziehen = Hindernis (mit Umschalt = radieren) · `P` = nächstes Preset · `1`–`0`, `←` `→` = Look.
- **Hand** (`liq.hand`, `liqUpdateHand`): folgt der Maus weich (`HAND_FOLLOW` 30/s), blendet ein/aus (`HAND_LEVEL`),
  ihr Tempo ist auf `HAND_SPEED` (3 Bildhöhen/s) begrenzt. In `predict()` (also in allen drei Rechen-Shadern gleich)
  als Beschleunigung: `±r/R · 3,5 · Stärke · (1−q²)²` (in der Mitte null, am stärksten auf halbem Radius; Stärke =
  Regler Maus-Kraft × `HAND` 24) plus **Mitnehmen** `(Hand-Tempo − Tempo) · CARRY (14/s) · (1−q²)²`. Der Cursor-Ring
  zeigt die Reichweite (gestrichelt = zieht an). **Beim Klick und solange die Taste gehalten wird, lässt die Hand los**
  (`liq.handPause`, bis der Tropfen aus ihrer Reichweite gefallen ist) – sonst schöbe sie den eigenen Tropfen weg.
- **Neue Partikel** (`liqSpawn(n, o)`, Shader `liqSpawn`): holt die nächsten n aus dem Vorrat (`liq.count` wächst) und
  schreibt Ort + Tempo. Form 0 = **Tropfen** (`liqDrop`: runde Scheibe im Sonnenblumen-Muster, Radius `DROP` 0,035 ·
  √Regler), Form 1 = **Strahl** (`liqJet`: Reihen quer zur Fallrichtung; immer wenn der Strahl 0,9 Partikelabstände
  weiter ist, entsteht die nächste Reihe – so ist er bei jeder Bildrate gleich dicht; Tempo `JET_SPEED` 1,4, Breite
  `JET_WIDTH` 0,03 · Regler Strahl). Die Breite geht nur in ganzen Partikeln auf; damit trotzdem auf jeder Stufe
  gleich viel pro Sekunde kommt, strömt ein zu schmal geratener Strahl etwas schneller (Faktor 0,75–1,5). Gemessen:
  Der Hahn füllt den Vorrat auf allen 6 Stufen in 15,1–15,2 s (Strahl 30 %: 25 s, 150 %: 5 s).
- **Spritzer** (`liqSplash`, höchstens 2 gleichzeitig, `uKick[2]`): `KICK_TIME` (0,05 s) lang eine Beschleunigung vom
  Klick weg und nach oben (zusammen `KICK` 2,2 Bildhöhen/s bei 100 %), Radius `KICK_RANGE` 0,11. Endet er mitten in
  einem Bild, wird er entsprechend schwächer gerechnet → bei jeder Bildrate gleich stark. Er trifft nur Partikel, die
  vor dem Klick schon da waren (`uKickN`) – der neue Tropfen fällt einfach.
- **Leeren** (`liqDrain`): 0,6 s ausblenden, dann `liq.count = 0` (alles ist wieder Vorrat; Hindernisse bleiben).
- **Eimer kippen** (`liqTilt`): setzt nur den Zielwert des Reglers Fallrichtung (wird weich nachgezogen); beim
  Überschreiten von ±180° springt die Zahl, nicht die Flüssigkeit.
- **Hindernisse:** eigenes Bild `liq.obstacles` (R8, so fein wie im Fluid-Modus), aber **Stift, Radierer, Werkzeug-
  Auswahl und Anzeige sind die des Fluid-Modus** (`obstacleStroke(x, y, set, radius)`, `wipeObstacles(set)`,
  `drawObstacles(target, set)`, `tool`, `obstaclePen`, `setTool`; der Panel-Abschnitt „Hindernisse“ gehört zu beiden
  Modi, `data-mode="fluid liquid"`). Stiftbreite fest (`WALL_PEN` 0,028 Bildhöhen halbe Breite).
  Aus dem Bild wird ein **Abstandsfeld** (`liqBuildSdf`, nur wenn sich Hindernisse ändern, „Jump Flooding“:
  `liqSeed` merkt je Kanten-Bildpunkt die genaue Stelle der Kante → `liqJump` in Sprüngen … 8, 4, 2, 1, 1 →
  `liqDist` Abstand, im Hindernis negativ → `liqNormal` Richtung): `liq.sdf` (RGBA16F: x = Abstand in Bildhöhen,
  yz = Richtung vom Hindernis weg). Die Partikel lesen es mit **einer** Abfrage (`obstacle(p, n)`):
  `inside()` schiebt sie auf kürzestem Weg hinaus; in `liqLambda` zählt ein Hindernis wie dicht gepackte Flüssigkeit
  hinter seiner Oberfläche (`ρ += ρ0 · 0,5 · (1 − s/h)^2,8` – der Anteil der Gewichtsfunktion hinter einer geraden
  Wand), in `liqPush` schiebt es entsprechend zurück. Gemessen: kein Partikel im Hindernis, Dichte am Hindernis wie
  im Inneren (1,00–1,02), kein Zittern.
- **Stufen:** `QUALITY[].lside` = 80/128/160/184/196/208 → Platz für 6.400/16.384/25.600/33.856/38.416/43.264
  Partikel (vorher 208/256/272 für Ultra/Extrem/Maximum). Grund: Mit dem Hahn kann das Becken ganz voll werden, und
  65.536 Partikel im Bild liefen nur mit 27 FPS. Jetzt hält auch ein volles Becken 60 FPS auf jeder Stufe.

### Presets und Gefühl (Schritt 5)
- **Presets** (`LIQ_PRESETS`, `setLiqPreset`, Knöpfe im Abschnitt „Eigenschaften“, Taste `P`): setzen **nur
  Zielwerte der Regler**; `easeParams` blendet weich über (auch die Dichte = Partikelgröße). Verstellt man einen
  Regler, zeigt das Panel „Eigene Mischung“ (`liqShowPreset`). Schalter **„Passenden Look mitwählen“** (an): das
  Preset wählt zusätzlich einen Look (und ggf. den Metall-Typ).

| Preset | Viskosität | Zusammenhalt | Steifigkeit | Dichte | Look | Charakter (gemessen, Stufe Hoch) |
|---|---|---|---|---|---|---|
| Wasser (= Standard) | 12 % | 30 % | 85 % | 100 % | Wasser | Dammbruch nach 1 s: Tempo 0,75, spritzt bis zur Decke; schwappt lange nach |
| Öl | 50 % | 20 % | 85 % | 92 % | Seifenblase / Ölfilm | Tempo 0,54, kaum Spritzer, nach 5 s ruhig |
| Honig | 100 % | 50 % | 85 % | 110 % | Metallic (Gold) | Tempo 0,20, kriecht; Pfütze bleibt 0,8 breit und 0,026 hoch |
| Gel | 65 % | 90 % | 25 % | 100 % | Glas / Kristall | Tempo 0,39, federt; Pfütze 0,58 × 0,035 |
| Quecksilber | 5 % | 100 % | 100 % | 135 % | Metallic (Chrom) | Tempo 0,69, dicke Tropfen; Pfütze 0,64 × 0,033 (Wasser: 1,7 × 0,014) |

- **Geprüft:** 5 Presets × 6 Stufen (Pfütze, Dammbruch, 15 s Ruhe, wildes Spiel mit Hand/Klicks/Hahn, danach Ruhe),
  Wechsel aller Presets alle 1,5 s mitten in der Bewegung auf allen Stufen, alle 16 Ecken von
  Viskosität/Zusammenhalt/Steifigkeit/Dichte × 6 Stufen: nirgends ungültige Werte, nichts verlässt das Bild.
  In Ruhe höchstens 9 von bis zu 26.000 Partikeln schneller als 0,15 Bildhöhen/s.
- **Ruhigeres Verhalten:** Vor Schritt 5 brodelten dort, wo die Oberfläche auf eine Wand trifft, dauerhaft Partikel
  (Quecksilber-Werte: 49–59 Partikel mit 0,2–0,7 Bildhöhen/s, Wasser 2–3). Ursache: Der Haut fehlten hinter der Wand
  die Nachbarn, sie zog sich ständig von der Wand weg. Mit Spiegelbildern und Dämpfung der Haut: 0 an den Wänden
  bei allen Presets; an Hindernissen Quecksilber 59 → 0, Wasser 18 → 0–16 (je nach Lauf, höchstens 0,21
  Bildhöhen/s). An der Decke bleibt nichts hängen.

### Klang, Auto-Play, Flacker-Reduktion (Schritt 6)
- **Kennzahlen** (`liqStat`, `readLiqStats`, Shader `liqStat`): 8×8-Bild, 2048 Stichproben-Partikel: mittleres Tempo,
  Anteil einzeln fliegender Tropfen (Dichte < 0,6), Anteil stark zusammengedrückter Partikel (Dichte > 1,09 =
  Aufprall), dazu „wie nass ist die Hand“ (64 Stellen im Umkreis der Hand im Such-Raster). Abgeholt ohne die
  Grafikkarte aufzuhalten (wie `partStat`), nur wenn der Ton läuft. Gemessene Größen: Ruhe Tempo 0,02–0,08; Rühren
  0,2–0,5 / Tropfen-Anteil 0,02; Dammbruch 0,77 / 0,03 / Aufprall 0,03; Hahn 0,15–0,2.
- **Klänge** (siehe auch „Ton & Musik“): **Rühren** – bewegt sich die nasse Hand, erklingen die gezupften Töne von
  `audioPaint` (schneller = höher und lauter); **Plätschern** (`audioLiqBloop`: kurzer Ton, dessen Höhe ansteigt;
  Rate `min(10; 70 · Tropfen-Anteil + 8 · Bewegung²)` pro Sekunde, unregelmäßig); **Aufprall** (`audioLiqImpact`:
  dumpfer Schlag + Rauschen, wenn der Aufprall-Anteil sprunghaft um > 0,012 steigt, höchstens alle 0,4 s);
  **Nachfüllen** (`audioLiqFill`: etwa 3 Töne pro Sekunde, solange Hahn/Strahl laufen – je voller das Becken, desto
  höher); **Klick** = `audioClick` + Spritz-Rauschen (`audioLiqSplash`); **Leeren** = Wischen + drei absteigende
  „Gluck“-Töne (`audioLiqDrain`). Das mittlere Tempo hebt `audio.energy` (bis 0,75) → die Musik öffnet sich.
  Gemessen (Analyser am Ausgang, Musik aus): Ruhe 0,000; schnelles Rühren Spitze 0,22 / RMS 0,049, langsames
  0,13 / 0,021; Hahn 0,06; Klick 0,24–0,28; Leeren 0,08; Dammbruch 0,06–0,39 (je nachdem, ob der erste Schlag in die
  Messung fällt); Klänge aus 0,004. **Nicht geprüft: wie es klingt.**
- **Auto-Play** (`liqAutoplayStart/Stop`, `liqAutoplay`): unsichtbare Hand auf der Pinselbahn im unteren Bildteil
  (meist schiebt sie, alle 14–24 s zieht sie 5–9 s lang; `liq.autoPush`), der **Eimer schaukelt** (`liq.autoTilt`,
  bis `AUTO_TILT` 18°, zwei überlagerte langsame Schwingungen – zusätzlich zur Fallrichtung des Nutzers), ein
  **unsichtbarer Hahn** oben füllt in Schüben nach (5–9 s auf, 5–10 s zu), alle 4–9 s fällt ein **Tropfen**. Ist das
  Becken voll: `AUTO_PAUSE` (18 s) stehen lassen, leeren, dann von vorn (mal mit einem Schwall, mal aus dem leeren
  Becken). Regler, Preset, Look und der eigene Hahn des Nutzers bleiben unberührt; nach dem Ende klingen Hand und
  Schaukeln weich aus. Geprüft (150 s im Zeitraffer auf Niedrig/Hoch/Maximum): 2× gefüllt und geleert, Neigung bis
  18°, Hand wechselt 11–12× zwischen Schieben und Ziehen, keine ungültigen Werte, danach Neigung 0, Hahn aus,
  Einstellungen unverändert.
- **Flacker-Reduktion:** Spritzer × 0,6 (Stärke), Aufprall leuchtet weniger auf (`PRESSURE` × 0,4), einzeln
  fliegende Tropfen sind bis 60 % blasser (`uSprayDim`), Auto-Play 40 % langsamer und mit kleineren Tropfen, Klänge
  leiser; dazu die gemeinsame Helligkeits-Bremse. Gemessen (fester Ablauf: drei Klick-Spritzer + großer Tropfen):

| Look | größter Helligkeitssprung pro Bild | Anteil Bildpunkte mit Sprung > 10 % | mittlere Änderung pro Bild |
|---|---|---|---|
| Wasser | 0,99 → 0,04 | 4,3 % → 0 % | 0,0113 → 0,0038 |
| Palette | 0,68 → 0,05 | 2,2 % → 0 % | 0,0064 → 0,0031 |
| Metallic | 1,00 → 0,04 | 8,7 % → 0 % | 0,0167 → 0,0027 |

- **Panel:** drei Abschnitte – „Flüssigkeit (Partikel)“ (Schieben/Ziehen, Maus-Kraft, Reichweite, Spritzer,
  Tropfen, Schalter Hahn, Strahl, Füllstand, Leeren / Neu füllen), „Eigenschaften“ (Presets, Schalter „Passenden Look
  mitwählen“, Schwerkraft, Fallrichtung, Eimer kippen, Viskosität, Zusammenhalt, Steifigkeit, Dichte), „Hindernisse“
  (gemeinsam mit dem Fluid-Modus). Zeichen für den Hahn: `#liqTap` (kleines Röhrchen, zeigt in Fallrichtung).

### Messwerte (1920×1080; „Bild“ = ganzes Bild mit Look „Wasser“ und Bloom, CPU + GPU; „Rechnen“ = GPU-Zeit für 1/60 s)
| Stufe | Platz | beim Einfüllen | Schritte/s | Such-Raster | Rechnen (Dammbruch) | Bild (Dammbruch) | Rechnen (voll) | Bild (voll, Hindernisse, Hand) |
|---|---|---|---|---|---|---|---|---|
| Niedrig | 6.400 | 3.840 | 382 | 210×118 | 0,6 ms | 1,6 ms | 0,65 ms | 1,8 ms |
| Mittel | 16.384 | 9.830 | 611 | 336×189 | 1,4 ms | 2,6 ms | 2,3 ms | 4,2 ms |
| Hoch | 25.600 | 15.360 | 764 | 420×236 | 2,6 ms | 4,4 ms | 4,2 ms | 6,9 ms |
| Ultra | 33.856 | 20.314 | 878 | 484×272 | 3,5 ms | 5,4 ms | 5,9 ms | 8,9 ms |
| Extrem | 38.416 | 23.050 | 936 | 515×290 | 4,3 ms | 6,3 ms | 7,5 ms | 10,6 ms |
| Maximum | 43.264 | 25.958 | 993 | 547×307 | 5,1 ms | 7,3 ms | 9,4 ms | 12,4 ms |
- Darstellung allein: Felder 0,16–0,65 ms, Oberflächen-Baustein 0,04–0,13 ms, Schaum 0,03–0,21 ms, Look „Wasser“
  ≈ 0,26 ms, Partikel-Bild 0,02–0,09 ms. Die Physik ist der teure Teil. Hand, Spritzer, Hindernisse und Ton kosten
  nicht messbar extra (Rechnen vor/nach Schritt 4: 2,81 → 2,82 ms auf „Hoch“).
- 13 Looks × 6 Stufen: alle 60 FPS, GL-Fehler 0; 33 Moduswechsel fehlerfrei; alle Stufen mit vollem Becken, Hahn,
  Hindernissen, Hand, Klicks und Kippen 60 FPS. FPS nur in der 60-Hz-Vorschau gemessen.
- Extremfälle (alle ohne ungültige Werte, nichts verlässt das Bild, kein Partikel im Hindernis): Fenster 600×900 und
  zurück mit Hindernissen und laufendem Hahn; Stufenwechsel mitten im Spiel; schwerelos mit Hahn; fünfmal kippen
  hin und zurück; Hindernis mitten durch die ruhende Flüssigkeit gezogen; großes gefülltes Hindernis über der
  Flüssigkeit; Maus-Kraft 300 % mit Reichweite 40 % und wildem Rühren; dazu die Fälle aus Schritt 2 (alle Partikel in
  einer Ecke/auf einem Punkt, 5 s Zeitschritt, Dauerlauf mit springenden Reglern).
- Ruhe: Becken nach dem Einschwingen mittleres Tempo 0,0001–0,03 Bildhöhen/s je nach Preset (nicht sichtbar).
- Fluid unverändert: dieselben drei Prüfsummen wie vorher (`3ff93dc5-b33e3505`, `28e31dc5-e9c55505`,
  `ee1e9dc5-123c5505`; einmal trat in einem Lauf ein vierter Wert auf – die Prüfsumme streut, siehe „Testen“ oben);
  Hindernisse im Fluid-Modus funktionieren nach dem Umbau von `obstacleStroke` weiter.

### Grenzen
- **Partikelzahl:** Die Kosten wachsen mit Partikelzahl^1,5 (mehr Partikel brauchen kürzere Schritte). Mehr als
  ≈ 45.000 im Bild gehen bei 60 FPS nicht – deshalb fasst „Maximum“ 43.264 (volles Becken 12,4 ms). Bei 144 Hz
  (Budget 6,9 ms) dürfte die Auto-Qualität auf „Hoch“ gehen, mit vollem Becken eher „Mittel“.
- **Leicht zusammendrückbar:** unten im Becken 5 % dichter (bei Schwerkraft 200 % oder Steifigkeit 0 % bis 23–34 %).
  Harte Aufschläge federn kurz nach. Ein Verfahren mit echtem Druck-Löser auf einem groben Raster (wie FLIP) könnte das
  beheben und mehr Partikel erlauben – größerer Umbau, bisher nicht gemacht.
- **Sehr schmale Fenster** kosten mehr (kleinere Partikel → mehr Schritte pro Sekunde).
- **Viskosität:** echter Honig ist nicht erreichbar (der Tempo-Ausgleich reicht nur einen Nachbarn weit pro Schritt);
  die zusätzliche Bremsung lässt die Flüssigkeit zäh kriechen – sie bremst aber auch den freien Fall (Honig fällt
  höchstens mit ≈ 0,8 Bildhöhen/s).
- **Quecksilber perlt nur ansatzweise:** Eine kleine Pfütze bleibt 0,64 breit und 0,033 hoch (Wasser: 1,7 × 0,014),
  zieht sich aber nicht zu einer runden Perle zusammen. Mehr als `COHESION` 150 wurde mit der Dämpfung nicht
  ausprobiert (ohne Dämpfung kochte die Oberfläche schon bei 150). Auf „Niedrig“ ist der Zusammenhalt schwächer
  (Pfütze 0,90 breit).
- **Benetzung:** Wände und Hindernisse werden immer benetzt (Randwinkel ≈ 90°) – ein Tropfen auf dem Boden wird zur
  Halbkugel, nicht zur Perle. An Hindernissen bleibt bei dünnflüssigen Einstellungen etwas Unruhe (Wasser: bis
  zu 16 Partikel mit bis zu 0,21 Bildhöhen/s), vor allem an runden Enden und an Unterseiten, die die Oberfläche
  durchstoßen – die Spiegelung nimmt dort eine ebene Oberfläche an. Mehr Dämpfung der Haut würde das beheben,
  nimmt dem Wasser aber die Spritzer (Tropfen-Anteil beim Dammbruch 0,022 → 0,004) und wurde deshalb verworfen.
- **Ohne Zusammenhalt** (0 %) verfliegt die Flüssigkeit in Schwerelosigkeit wie Gas.
- **Stillstehende Hand:** Beim Schieben hält sie nur eine Mulde frei (kleiner als der Cursor-Ring), der Druck der
  Flüssigkeit hält dagegen. Ein Klick mitten in die Flüssigkeit setzt den Tropfen in die vorhandene hinein (sie rückt
  zur Seite).
- **Farben mischen sich nicht zurück:** Jedes Partikel behält seine Palettenposition; nach langem Rühren wird aus den
  Schichten ein feines Gesprenkel.
- Looks, die die Farbmenge als Höhe lesen, zeigen im Inneren nur den Druck-Verlauf – die Strömung im Inneren ist dort
  kaum zu sehen (anders als im Fluid-Modus mit seinen Schlieren). „Metallic“ ist in Ruhe eine fast gleichmäßige Fläche.
- **Auto-Play leert das Becken** des Nutzers (so wie es im Fluid-Modus über das Bild malt). Hindernisse bleiben.
- **Kein Zwei-Finger-Bedienen** auf Touch-Geräten (ein Finger = Hand, Tippen = Tropfen; Hindernisse nur über die
  Werkzeug-Knöpfe).
- **Klang nicht angehört** – nur gemessen. Stellschrauben: Lautstärken in `audioLiqBloop`/`audioLiqImpact`/
  `audioLiqFill`, Rate und Schwellen in `updateLiqSound`.

### Stabilität – worauf achten
- **`MAX_FIX` nicht entfernen:** Bei 400–1.000 Schritten pro Sekunde macht jeder kleine Schubs ein großes Tempo
  (Tempo = Weg / Schrittdauer). Ohne die Grenze fürs Korrektur-Tempo (0,05 Bildhöhen/s je Schritt, zusätzlich zum
  eigenen Tempo) heizt sich die Flüssigkeit beim Aufprall auf und „kocht“ dauerhaft wie Gas. Dieselbe Grenze sorgt
  dafür, dass Partikel, die aus einem frisch gezeichneten Hindernis geschoben werden, dabei kein Tempo gewinnen.
- **Steifigkeit höchstens ≈ 0,45:** Die Korrekturen benachbarter Partikel überlagern sich (Jacobi-Verfahren); ab
  ≈ 0,6 zittert alles, in stark zusammengedrückter Flüssigkeit (> 15 %) schon ab 0,45–0,5.
- **Zu wenige Schritte = das Becken sackt zusammen und zittert am Boden.** Deshalb `STEP_RATE` nicht senken, ohne
  nachzumessen.
- **Zusammenfallen verhindern:** Im Raster ist nur ein Partikel pro Feld sichtbar – stark zusammengepresste
  Flüssigkeit „merkt“ ihre Dichte nicht mehr und fällt weiter zusammen. Dagegen: `RESCUE` (Abrücken im selben Feld),
  wechselnde Zeichen-Reihenfolge, Zusammenhalt nur an der Oberfläche. Ab Dichte 1,5 (`CRUSH`) wird nur noch
  weggerückt, ohne Tempo zu gewinnen – ein Klumpen entfaltet sich, statt zu explodieren (das fängt auch Tropfen auf,
  die mitten in die Flüssigkeit gesetzt werden).
- **Paar-Kräfte immer beidseitig gleich** (sonst bleibt der Impuls nicht erhalten → die Oberfläche wird unruhig).
- **Zusammenhalt braucht Gegenstücke hinter jeder Wand** (Spiegelbilder, `cling` an Hindernissen) **und die
  Dämpfung der Haut** (`SKIN_VISC`) – fehlt eins von beiden, brodelt es an der Wand bzw. kocht die Oberfläche.
  Neue Ränder (z. B. bewegte Hindernisse) brauchen dasselbe.
- **Kräfte von außen nur in `predict()`** (Hand, Spritzer, Schwerkraft): Die Funktion wird von `liqGrid`,
  `liqLambda` und `liqPush` gleich benutzt – nur so stimmt die Vorhersage überall überein. Radius der Hand nie 0
  (Division), unbenutzte Spritzer weit weg legen (`[−10, −10, 1, 0]`).
- **Neue Partikel nie exakt aufeinander** (kleiner Zufall in `liqSpawn`; Abstand < 10⁻⁶ gilt als „ich selbst“).
  Mindestabstand zum Rand je Partikel leicht verschieden (`JITTER`).
- **Abstandsfeld:** Abstand und Richtung getrennt speichern (nicht den Vektor zur Kante – der wird zwischen zwei
  Hindernissen beim Filtern null und täuscht eine Oberfläche vor). Die Kanten-Stellen brauchen 32 Bit (RG32F).
- **Kennzahlen:** Zwischenspeicher (`PIXEL_PACK_BUFFER`) vor jeder Abfrage neu anlegen (`bufferData`), sonst meldet
  der Browser bei jeder Abfrage eine Leistungs-Warnung; nach Gebrauch wieder lösen. In einem einzelnen
  JavaScript-Aufruf wird eine Abfrage nie fertig (erst im nächsten Bild) – zum Testen das 8×8-Bild direkt lesen.
- `near`, `far`, `half` nicht als Namen in Shadern benutzen.

### Ausprobiert und verworfen
- **Wenige Schritte mit vielen Durchgängen / weiche Nachgiebigkeit:** Becken unten 20–40 % dichter oder Zittern → viele
  kurze Schritte mit je einem Durchgang.
- **Druck von Schritt zu Schritt aufheben („Warmstart“):** rechnerisch instabil ab einem Anteil von 0,5 → nicht gebaut.
- **Zusammenhalt als Anziehung zwischen allen Nachbarn:** im Inneren entsteht ein starres Gitter – die Flüssigkeit wird
  zäh wie Gel. **Nur für Oberflächen-Partikel, aber einseitig:** Oberfläche wird unruhig und bucklig → beidseitig
  gleiche „Haut“.
- **Haut ohne Spiegelbilder an der Wand:** dauerhaftes Brodeln am Rand der Oberfläche (siehe oben). **Spiegelbilder
  auch an der Decke:** Spritzer blieben oben kleben → dort ausgenommen. **Ausnahme schon ab 45° Neigung:** an schrägen
  Unterseiten brodelte es wieder → nur fast waagrechte Unterseiten ausnehmen (von schrägen rutschen Tropfen ab).
- **Stärkerer Zusammenhalt ohne Dämpfung** (`COHESION` 150–600): Oberfläche kocht (500–2.100 schnelle Partikel).
  **Dämpfung 0,0006:** reicht nicht (109) → 0,003.
- **Spritzer trifft auch den neuen Tropfen:** der Tropfen flog nach oben weg → `uKickN`. **Hand bleibt beim Klick
  aktiv:** sie schob den Tropfen auseinander → lässt kurz los.
- **Klick-Verhalten je nach Ort (im Wasser = Spritzer, in der Luft = Tropfen):** hätte gebraucht, dass man weiß, ob
  die Maus im Wasser ist – beim Schieben ist dort aber gerade eine Mulde. Jetzt immer beides.
- **Hand-Stärke 14:** nur ein winziges Loch unter der Maus → 24. **Strahl-Tempo 0,9:** zerfiel sofort in Tropfen → 1,4.
- **Platz für 65.536/73.984 Partikel (Extrem/Maximum):** volles Becken nur 27 FPS → kleinere Stufen.
- **Schlieren (schwankende Farbmenge je Partikel):** werden beim Schwappen zu Körnung → stattdessen den Druck sichtbar
  machen. **Farbmenge 1,2 im Inneren:** Feuer/Metallic überstrahlt → 0,7.
- **Auto-Play mit dauernd laufendem Hahn:** alle 30 s geleert, zu hektisch → Schübe und 18 s Pause.
- **Strahlbreite 0,05 ohne Ausgleich:** Becken in 8–10 s voll und je Stufe verschieden schnell → schmaler, und das
  Tempo gleicht die Rundung auf ganze Partikel aus.

### Warum „Position Based Fluids“ statt klassischem SPH
- Klassisches SPH (Druck als Kraft, Kräfte aufsummieren) wurde **nicht gebaut und nicht gemessen**. Gewählt wurde von
  Anfang an PBF, das dieselbe Nachbarsuche und dieselben Gewichtsfunktionen benutzt (also „verwandtes Verfahren“), aber
  Positionen direkt verschiebt statt Kräfte aufzusummieren. Begründung (Annahme, nicht im Vergleich geprüft): Bei
  SPH muss der Druck sehr steif sein, damit Wasser nicht wie Gummi federt, und steife Kräfte explodieren bei zu großen
  Schritten; PBF bleibt auch bei extrem zusammengepressten Partikeln beschränkt (gemessen: alle Partikel auf einem
  Punkt → entfaltet sich ohne ungültige Werte). Der Preis: PBF ist leicht zusammendrückbar und braucht viele
  Teilschritte (siehe „Grenzen“).

### Aufbau (Code in `index.html`, Abschnitt „Flüssigkeits-Modus (Partikel)“; Entwurf in `.claude/liquid.js`)
- **Texturen/Puffer** (alle in `liq`):
  - `state` – Doppelpuffer RGBA32F, NEAREST, `lside × lside`: xy = Ort (0..1 im Bild), zw = Tempo (Bildhöhen/s).
    Partikel-Nummer k = x + y · side; die ersten `liq.count` sind im Bild, der Rest ist Vorrat.
  - `pred` – RGBA32F, gleiche Größe: xy = Tempo-Ausgleich (Viskosität), z = Druck λ, w = Dichte / Soll-Dichte.
    Wird auch von der Darstellung und den Kennzahlen gelesen.
  - `grid` – Such-Raster RGBA32F, angelegt für den kleinsten Partikelabstand (Dichte-Regler 140 %); benutzt wird der
    Teil `liq.gw × liq.gh` (Feldgröße ≈ Reichweite / 3). Leere Felder: x = −1.
  - `obstacles` (R8, Doppelpuffer) → `seeds` (RG32F, Doppelpuffer) → `dist` (R32F) → `sdf` (RGBA16F, weich gefiltert):
    Hindernis-Bild und Abstandsfeld, alle in der Auflösung `resolution(CONFIG.OBSTACLE_RES)`.
  - `field` (roh), `dye` (fertig) – Dichte-Feld RGBA16F, Bildschirm × `pscale`; `flowSum`/`flow`/`curl` in halber
    Auflösung; `sprites` nur für den Look „Partikel“. Angelegt in `ensureLiqFields()`.
  - `liqStat.target` (8×8, RGBA32F) + `liqStat.buffer`: Kennzahlen für den Ton.
- **Shader-Programme** (übersetzt in `liqCompile()`): `liqInit`, `liqResize`, `liqSpawn` (neue Partikel),
  `liqSeed`/`liqJump`/`liqDist`/`liqNormal` (Abstandsfeld), `liqGrid`, `liqLambda`, `liqPush`, `liqSplat`, `liqField`,
  `liqFlow`, `liqSprites`, `liqStat`. Gemeinsamer GLSL-Teil `liqCommonGLSL`: `obstacle(p, n)`, `inside`, `predict`
  (Schwerkraft, Hand `uHand`/`uHandVel`, Spritzer `uKick`/`uKickN`/`uUp`), `cellOf`. Für die Drehung `curl`, für
  Hindernisse `obstacleBrush`/`obstacleDraw` des Fluid-Modus.
- **Funktionen:** `ensureLiqBuffers()` (Puffer, Partikelgröße, Schrittdauer, Raster, Hindernis-Bild; ruft bei Bedarf
  `liqBuildSdf()` und `liqFill()`), `liqSpawn`, `liqUniforms`, `liqPass`, `liqFillGrid`, `liqMeasure` + `liqResolve`
  (= ein Teilschritt), `liqCohesion`, `liqSimulate(steps)` (Regler → Shader-Größen, Spritzer, Abstandsfeld binden),
  `liqUpdateHand`, `updateLiquid(dt)` (Hand, Leeren, Hahn/Strahl, Ton, Panel-Anzeigen, Teilschritte, Cursor),
  `liqUpdateFields`, `liqDrawSprites`, `drawLiquid`; Bedienung: `liqMouse`, `liqDown`, `liqSplash`, `liqDrop`,
  `liqJet`, `liqClick`, `liqWallStroke`, `liqClearObstacles`, `liqPointerMove/Down/Up`, `liqWheel`, `setLiqPush`,
  `setLiqTap`, `liqShowTap`, `liqShowInfo`, `liqDrain`, `liqRefill`, `liqTilt`, `liqKey`; Ton: `readLiqStats`,
  `audioAt`, `audioLiqBloop/Impact/Fill/Splash/Drain`, `updateLiqSound`; Auto-Play: `liqAutoplayStart/Stop`,
  `liqAutoplay`; Presets: `LIQ_PRESETS`, `setLiqPreset`, `liqShowPreset`, `setLiqPresetLook`.

### Standardwerte der Regler (`PARAMS`, Doppelklick = Standard)
| Regler | Schlüssel | Bereich | Standard | wirkt als |
|---|---|---|---|---|
| Maus-Kraft | `liqForce` | 0–300 % | 100 % | × `HAND` 24 Bildhöhen/s² (schieben/ziehen), Mitnehmen bis `CARRY` 14/s |
| Reichweite | `liqRange` | 4–40 % | 12 % | Radius der Hand (Anteil der Bildhöhe); auch per Mausrad |
| Spritzer (Klick) | `liqSplash` | 0–250 % | 100 % | × `KICK` 2,2 Bildhöhen/s im Zentrum |
| Tropfen (Klick) | `liqDrop` | 0–300 % | 100 % | Fläche des Tropfens (Radius `DROP` 0,035 · √Wert); 0 = keiner |
| Strahl | `liqJet` | 30–150 % | 50 % | Breite × `JET_WIDTH` 0,03 (Hahn und gedrückte Maustaste); 50 % füllt den Vorrat in 15 s |
| Schwerkraft | `liqGravity` | 0–200 % | 100 % | × `GRAVITY` 4 Bildhöhen/s² |
| Fallrichtung | `liqGravityDir` | −180…180° | 0 (unten) | wie im Fluid-Modus; abgeblendet bei Schwerkraft 0; Taste `G` dreht 90° weiter |
| Viskosität | `liqViscosity` | 0–100 % | 12 % | quadratisch: Tempo-Ausgleich `v² · 0,004` Bildhöhen²/s (pro Schritt höchstens 60 %) + Bremsung `v² · 5`/s |
| Zusammenhalt | `liqCohesion` | 0–100 % | 30 % | `c · (0,3 + 0,7·c²) · 150` · (0,0127 / Reichweite)²; nur an der Oberfläche; dazu Dämpfung der Haut |
| Steifigkeit | `liqStiff` | 0–100 % | 85 % | Korrektur-Anteil 0,2 + 0,25 · Wert (Standard ≈ 0,41) |
| Dichte | `liqDensity` | 70–140 % | 100 % | Partikelabstand / √Wert |
| Look-Regler „Farbe nach“ | `dotColor` | Tempo/Dichte | Tempo | nur Look „Partikel“ |
| Look-Regler „Partikelgröße“ | `dotSize` | 0,5–2× | 1× | nur Look „Partikel“ |
- Feste Konstanten in `LIQUID` (Kommentare im Code): `FILL_MAX` 0,5, `START` 0,6, `REACH` 2,15, `STEP_RATE` 4,5,
  `MAX_RATE` 2400, `MAX_STEPS` 64, `MAX_SPEED` 4, `STIFF_MIN/MAX` 0,2/0,45, `SPREAD` 0,012, `MAX_PUSH` 0,2,
  `MAX_FIX` 0,05, `CRUSH` 1,5, `COHESION` 150, `SKIN_VISC` 0,003, `RESCUE` 0,08, `BOUNCE` 0,2 ab 0,3 Bildhöhen/s,
  `JITTER` 0,5, `SPLAT` 2, `BODY` 0,7, `PRESSURE` 6 (höchstens 25 % Verdichtung), `TINT_SPAN` 1,0, `HAND` 24,
  `CARRY` 14, `HAND_FOLLOW` 30, `HAND_SPEED` 3, `KICK` 2,2, `KICK_TIME` 0,05, `KICK_RANGE` 0,11, `DROP` 0,035,
  `JET_SPEED` 1,4, `JET_WIDTH` 0,03, `HOLD` 0,2, `DRAIN` 0,6, `WALL_PEN` 0,028, `AUTO_TILT` 18, `AUTO_PAUSE` 18.
- Hinweis: Ob sich die Presets und die Hand gut anfühlen, hat noch kein Mensch beurteilt – alle Werte sind nach
  Messwerten und Bildschirmfotos eingestellt.

### Offene Ideen
- Presets/Szenarien speichern (Hindernisse + Reglerstellung), eigene Flüssigkeits-Farben je Preset.
- Zwei Flüssigkeiten gleichzeitig (z. B. Öl auf Wasser) – bräuchte eine Eigenschaft je Partikel.
- Echte Perlen für Quecksilber (einstellbare Benetzung der Wände) – bisher an der Stabilität gescheitert.
- Zwei-Finger-Bedienung auf Touch-Geräten.

### Testen
- Hilfen in `.claude/` (nicht im Repo): `l-tools.js` (lädt `__t`/`__p` mit; `__l.stats()` = ungültige Werte, Tempo,
  Schwerpunkt, Dichte-Verteilung; `__l.hidden()`, `__l.verify()`, `__l.run(n)`, `__l.set({…})`, `__l.reset()`,
  `__block(x, y, breite, packung, anzahl)`, `__pool()`, `__bins()`, `__scan({…})`, `__trace([…])`),
  `l4-tools.js` (`__h.wall([[x, y], …], radieren)`, `__h.obst()` = Partikel im Hindernis und Dichte/Tempo am
  Hindernis, `__h.move(n, bild → [x, y])` = Hand führen, `__h.s()`, `__h.clear()`), `l5-tools.js` (`__cand`,
  `__fastObs()` = wie viele Partikel sind unruhig und wo, `__shape()`, `__puddle()`, `__preset(werte)`),
  `run-l3.js` (13 Looks × 6 Stufen, Kosten, Moduswechsel), `run-l4.js` (Interaktion auf allen Stufen, volles Becken,
  Kosten, FPS), `run-l5.js` (Presets × Stufen, Preset-Wechsel, Regler-Anschläge; ≈ 6 min),
  `run-l6.js` (Auto-Play im Zeitraffer, Flacker-Messung), `l6-audio.js` (Lautstärken am Ausgang; vorher echter Klick),
  `run-ab.js` (Fluid-Prüfsumme). Ergebnisse jeweils in `window.__res` bzw. `__aud`/`__ab`. Alte Fassungen:
  `pre-liq.html`, `pre-l3.html`, `pre-l4.html`, `pre-l6.html`.
- Der Abschnitt des Modus liegt zum Bearbeiten als `.claude/liquid.js` vor (Panel samt Abschnitt „Hindernisse“:
  `liquid-panel.html`); `python .claude/splice.py` setzt beides in `index.html` ein. **Immer dort ändern, nicht direkt
  in `index.html`** – sonst überschreibt der nächste Lauf die Änderung. Änderungen außerhalb des Abschnitts
  (`PARAMS`, `QUALITY`, CSS, Hindernis-Funktionen) stehen direkt in `index.html` (Patch-Skripte `patch-l4.py` …).
- Dammbruch = `liq.fresh = true` (neu einfüllen). In Bewegung messen, nicht im Ruhezustand.
- Echte Maus-Eingaben in der Vorschau: `hover` an mehreren Stellen bewegt die Hand, `left_click` setzt Tropfen,
  `left_click_drag` mit Werkzeug „Hindernis“ zeichnet. Bildschirmfotos entstehen sehr schnell nach der Eingabe –
  ein Tropfen hängt darauf scheinbar noch in der Luft.

## Szenarien und Bild-Export (für alle Modi)
- Code: Abschnitt `// ---------- Szenarien und Bild-Export ----------` in `index.html` (direkt vor
  `// ---------- Hauptschleife ----------`), Panel-Abschnitte „Szenarien“ und „Bild speichern“ (zwischen „Bloom“ und
  „Ton“, in jedem Modus zu sehen). Bearbeitet wird in `.claude/share.js` und `.claude/share-panel.html`, eingesetzt mit
  `python .claude/splice-share.py` – **nicht direkt in `index.html` ändern**. Änderungen außerhalb (CSS, Tasten,
  Hauptschleife, `resizeCanvas`, Bloom, Mandelbrot, Partikel): `patch-share5.py`, `patch-share5b.py`, `patch-share5c.py`.

### Szenarien
- Ein **Szenario** = `{ v: 1, m: Modus-Kennung, n: Name, p: Palette, r: { Regler: Wert }, s: Zustand des Modus }`.
  Gespeichert werden nur Regler, die vom Standardwert abweichen. **Nicht** gespeichert: der Inhalt der Simulation
  (gemalte Farbe, einzelne Partikel, Hindernisse) und alles, was Geschmack des Nutzers ist (Lautstärke, Qualität,
  Flacker-Reduktion, im 3D-Flug Tempo/Trägheit/Maus-Empfindlichkeit).
- Was ein Modus beiträgt, steht in **`SCENE_MODES`** (ein Eintrag je Modus-Kennung – die Modi selbst bleiben
  unverändert): `params(state)` (Namen der Regler), `save()` (kleiner Zustand), `load(state, apply)`
  (`apply(instant)` stellt die Regler um; der Modus ruft es auf, wann es passt).
  - `fluid`: Fluid-Regler + alle Look-Regler; Zustand: Look.
  - `mandel`: Fraktal-Regler; Zustand: Julia ja/nein, Bildmitte (BigInt als Dezimaltext), Zoom, Julia-Form. Beim
    Laden fliegt die Ansicht dorthin (`fracFlyTo`); eine Julia-Form wird festgehalten (`frac.frozen`).
  - `particles`: alle `part…`/`swarm…`-Regler; Zustand: Anziehen/Abstoßen, gesetzte Kräfte (Typ, Ort, Stärke,
    Reichweite, Richtung). Beim Laden wird die Liste der Kräfte **ersetzt** (`part.forces = []`, siehe Fallstricke).
  - `liquid`: alle `liq…`-Regler + Look-Regler; Zustand: Look, Schieben/Ziehen, Hahn (an, Ort).
  - `flight`: Regler des gewählten Fraktals + `FLY_SHARED` + Licht/Farbe/Blickwinkel; Zustand: Fraktal, Ort und
    Drehung der Kamera, Baukasten-Startwert. Geladen wird per `flyGo` mit `apply` (Blende, Umstellen im Dunkeln).
  - Bloom-Regler (`SCENE_BLOOM`) und die Palette gehören zu jedem Szenario.
- `sceneCapture(name)` → Szenario des aktiven Modus, `sceneApply(sc)` → anwenden (wechselt bei Bedarf den Modus).
  **Fremde Werte werden entschärft:** Regler nur im Bereich ihres Panel-Reglers (`sceneRange`), Zahlen müssen endlich
  sein, Kamera innerhalb der Welt, höchstens 12 Kräfte, BigInt nur aus Ziffern (≤ 90 Stellen), unbekannte Regler und
  alles außer den genannten Feldern wird ignoriert.
- **Textcode:** `SATISIM1.` + Base64 (URL-sicher) des JSON-Texts (`sceneEncode`/`sceneDecode`). Länge: Fluid ≈ 160,
  Flüssigkeit ≈ 220, Partikel ≈ 240, 3D-Flug ≈ 300, Mandelbrot ≈ 500 Zeichen (die Koordinaten haben 60 Stellen).
  „Code kopieren“ legt ihn in die Zwischenablage (klappt das nicht, steht er markiert im Textfeld), „Code einfügen“
  öffnet ein Textfeld + „Diesen Code laden“. Der Code darf in anderem Text stecken (er wird herausgesucht).
- **Eigene Szenarien:** im Browser gespeichert (`localStorage`, Schlüssel `satisim.scenes`, Hilfen
  `loadStore`/`saveStore` aus dem Flug-Abschnitt). Das Panel zeigt die des aktiven Modus; gleicher Name im selben
  Modus überschreibt; ✕ löscht. Ohne Namen heißt es „Modus N“.
- **Start-Szenarien** (`SCENE_STARTS`, je Modus): Fluid 4 (Lavalampe, Tintenwirbel, Chrom-Schlieren, Polarlicht),
  Mandelbrot 4 (Glühende Ränder, drei Julia-Formen), Partikel 4 (Galaxie, Fischschwarm, Windkanal, Zwei Sonnen),
  Flüssigkeit 4 (Quecksilber-Brunnen, Honigtopf, Schwerelos, Bunte Perlen), 3D-Flug 10 (Korallenfels, Leuchtende Hänge,
  Kugelgarten, Ringebene, Würfelschacht, Im Schwamm, Pyramidental, Seidenstrudel, Kreisel, Tempelstadt – Kameras dicht
  über der Oberfläche, gefunden mit `flyFindSpot` und von Hand aus Kontaktbögen ausgesucht).
- In Textfeldern (`isTyping`) lösen Buchstaben keine Tastenkürzel aus (gemeinsame Tasten-Behandlung und Flug-Tasten).

### Bild-Export
- **Bedienung:** Knöpfe im Abschnitt „Bild speichern“ (`SHOT_KINDS`): Bildschirmfoto (Fenstergröße), Doppelte Größe,
  Hintergrundbild (Größe dieses Bildschirms), Hintergrund 4K (3840×2160), Handy-Hintergrund (1440×3120). Taste **`I`**
  wiederholt die zuletzt gewählte Größe. Ergebnis: PNG-Datei im Download-Ordner
  (`Satisim-<Modus>-<Breite>x<Höhe>-<Datum>-<Uhrzeit>.png`).
- **Ablauf** (`shotStart` → `shotFrame` in jedem Bild → `shotGrab` → `shotDeliver` → `shotEnd`): `shot` (früh
  deklariert, direkt nach `qualityLevel`) hält den Zustand. Erst warten, bis Übergänge fertig sind (Moduswechsel,
  Look-Wechsel, `mode.shotBusy()`; höchstens 20 s). Dann `shot.active = true`: `resizeCanvas()` stellt die
  Zeichenfläche auf `shot.size`, und **solange der Export läuft, wird in `frame()` nur noch `render(0)` aufgerufen**
  (kein `update`, kein `easeParams`, kein Auto-Play, kein `initFramebuffers`) – die Simulation steht exakt still.
  Ist das Bild fertig (`mode.shotReady()`, sonst nach 2 Bildern), wird es **im selben Augenblick** von der
  Zeichenfläche in ein 2D-Canvas kopiert (`drawImage`; später hat der Browser den Inhalt schon freigegeben), auf die
  Ziel-Größe zugeschnitten und als PNG übergeben. Abbruch nach 180 s.
- **Zwei Arten von Modi:** `freeAspect: true` (Mandelbrot, 3D-Flug) rechnen genau in der Ziel-Größe neu – wirklich
  schärfer. Die Simulations-Modi (Fluid, Partikel, Flüssigkeit) müssen das Seitenverhältnis des Fensters behalten:
  gerechnet wird in einem **ganzen Vielfachen der Fenstergröße** (dann bleiben alle Simulations-Puffer exakt, wie sie
  sind), daraus wird die Bildmitte im Ziel-Seitenverhältnis ausgeschnitten und verkleinert. Dort werden Look,
  Oberflächen-Baustein, Dichte-Feld (Flüssigkeit) und Glow in der hohen Auflösung gerechnet; die Simulationsdaten
  selbst (Farb-Textur, Spuren-Bild der Partikel) werden nur vergrößert.
- **Grenzen:** höchstens `SHOT.PIXELS` 16,6 Mio. Bildpunkte und 8192 je Seite (größere Ziele werden verkleinert).
- **Anpassungen an gemeinsamen Teilen** (alle mit `shot && shot.active`): Bloom-Kette beginnt um den Vergrößerungs-
  Faktor kleiner (`grow` in `ensureBloomBuffers` – der Glow ist im Verhältnis so breit wie am Bildschirm); die
  Flacker-Bremse ruht (sie vergleicht mit dem Bild davor); Mandelbrot rechnet mindestens 1 Fraktal-Bildpunkt pro
  Bildpunkt (höchstens 20 Mio.); Partikel zeigen die Zeichen der gesetzten Kräfte nicht; der 3D-Flug rechnet mit der
  höchsten Stufe (`flyQuality()`: 320 Schritte, 16-fache Kantenglättung), Standbild bis `SHOT.PIXELS`, dreifaches
  Zeit-Budget pro Bild, ohne Überblenden.
- **Gemessen** (1920×1080-Fenster, RTX 3050 Laptop; Zeit vom Klick bis zur fertigen Datei): Fluid/Partikel/
  Flüssigkeit/Mandelbrot 0,1–0,4 s für 3840×2160; 3D-Flug 0,5–1,1 s (Übersicht bzw. Nahaufnahme, 16-fach geglättet).
  Dateien 2–13 MB. Danach haben Zeichenfläche und alle Puffer wieder ihre alte Größe; die Farb-Textur des
  Fluid-Modus ist während des Exports bitgenau unverändert (Prüfsumme). Alle Modi danach 60 FPS, GL-Fehler 0.

### Fallstricke
- **`shot` muss vor dem ersten `resizeCanvas()` deklariert sein** (steht deshalb oben bei `qualityLevel`, nicht im
  Abschnitt selbst).
- **Liste der Partikel-Kräfte nie länger als `MAX_FORCES`:** Beim Laden eines Szenarios die alte Liste leeren, nicht
  nur „ausblenden“ – sonst schreibt `updateForces` über das Ende der Uniform-Felder hinaus (so passiert: RangeError).
- **Mitten in einem Übergang exportieren ergibt ein dunkles oder halb verwandeltes Bild** (so passiert bei der
  Verwandlung Julia → Mandelbrot) → `shotBusy()` im Modus angeben. Ein neuer Modus mit eigenen Blenden braucht das auch.
- Nur das, was in die WebGL-Zeichenfläche gezeichnet wird, landet im Bild (Hindernisse ja; Cursor, Hahn-Zeichen und
  Panel nicht).
- Ein neuer Regler, der zu einem Szenario gehören soll, braucht einen Panel-Regler (`bindSlider`) – sonst kennt
  `sceneRange` seinen Bereich nicht und er wird beim Laden übergangen (Ausnahmen stehen dort: `bloomOn`, `swarm`,
  `partColor`).
- Ein neuer Modus braucht einen Eintrag in `SCENE_MODES` (sonst stürzt `sceneCapture` ab) und, falls gewünscht, in
  `SCENE_STARTS`.

### Grenzen und Offenes
- **Nicht geprüft:** das echte Herunterladen der Datei und das echte Kopieren in die Zwischenablage (im Test wurde
  die fertige PNG-Datei abgefangen und nachgemessen: Größe, Helligkeit, Kontrast; der Code-Text wurde hin und zurück
  geprüft). Beides sind Standard-Funktionen des Browsers, aber ein Mensch sollte es einmal ausprobieren. Über
  `file://` (Doppelklick) erlauben manche Browser das Kopieren nicht – dann steht der Code markiert im Textfeld.
- Hindernisse (Fluid, Flüssigkeit) und der Inhalt der Simulation gehören nicht zum Szenario.
- Partikel-Modus: Das exportierte Bild ist ein vergrößertes Spuren-Bild – größer, aber nicht feiner aufgelöst.
- Kein Video-Export. Kein Bild größer als 16,6 Mio. Bildpunkte (Kacheln wären möglich: `uOffset` im Flug-Shader ist
  dafür vorbereitet, wird aber nicht benutzt).

### Testen
- `.claude/run-s5.js` (vorher `test-harness.js` und `p-harness.js` laden): `window.__opt = { parts: ['shots',
  'scenes', 'codes'], kinds: [0, 1, 3, 4], modes: […], level }` → `window.__res`. Bilder werden dabei **nicht**
  heruntergeladen (`shotDeliver` ist ersetzt). Dauert mit allem ≈ 1,5 min → nach dem Start mit `wait` warten.
- `.claude/s-tools.js`: `__s5.sheet(szenarien, spalten, bilder)` lädt Szenarien nacheinander und zeigt sie als
  Kontaktbogen in EINEM Bildschirmfoto (läuft > 45 s → im Hintergrund starten, dann warten).

## 3D-Fraktal-Flug (alle 6 Schritte fertig)
- **Ausbauplan:** 1 Kern (Raymarching, Distanzschätzer Mandelbulb, Licht, Farben, einfache Flugsteuerung) ✅ ·
  2 Leistung und Genauigkeit (Auflösung regelt sich beim Fliegen, im Stillstand verfeinern, Kamera kann nicht in die
  Oberfläche, Grenze der 32-Bit-Zahlen, Extremfälle) ✅ · 3 weitere Fraktale (Mandelbox, Menger-Schwamm,
  Sierpinski-Pyramide, 3D-Julia) und Faltungs-Baukasten ✅ · 4 Bedienung (Mausrad = Tempo, Rollen, Bremsen, Regler je
  Fraktal, Zufalls-Knopf, Kamera merken) ✅ · 5 Szenarien, Textcode, Bild-Export – als gemeinsamer Teil für ALLE Modi
  (eigener Abschnitt „Szenarien und Bild-Export“ direkt vor diesem) ✅ · 6 eigener Klang, Kameraflug als Auto-Play /
  Bildschirmschoner, Flacker-Reduktion, Panel ✅.
- **Stand:** fertig. Was ein Mensch noch beurteilen muss und was offen ist, steht unter „Grenzen und Offenes“.
- Code: Abschnitt `// ---------- 3D-Fraktal-Flug ----------` in `index.html` (direkt vor `// ----- Moduswechsel -----`),
  Konstanten in `FLY`, Aufwand je Qualitätsstufe in `FLY_LEVELS`, Fraktale in `FLY_KINDS`, Zustand in `fly`,
  Modus-Objekt `id: 'flight'`. Commits: `82b4833` (Schritt 1), `2c47ead` (Schritt 2), `ca15f07` (Schritt 3),
  `a24097a` (Schritt 4), `1f32dfd` (Schritt 5), Schritt 6 direkt danach.

### Technik (Schritt 1: Kern)
- **Raymarching:** Für jeden Bildpunkt läuft ein Strahl von der Kamera los. An jeder Stelle sagt der
  **Distanzschätzer** (GLSL-Funktion `de(p)`), wie weit es mindestens bis zur Oberfläche ist – um diese Strecke
  springt der Strahl weiter. Treffer, sobald der Abstand kleiner ist als `FLY.HIT` (0,75) Bildpunkte (die Schwelle
  wächst mit der Entfernung mit: `gEps = max(t · uPix, uEpsMin)`).
- **Distanzschätzer Mandelbulb** (`FLY_KINDS[0].glsl`, ausführlich im Code kommentiert): z → z^n + c in
  Kugelkoordinaten (Abstand hoch n, beide Winkel mal n; Pol-Achse = y). Mitgerechnet wird `dz` (wie stark winzige
  Unterschiede wachsen: `dz ← n · r^(n−1) · dz + 1`). Abstand ≈ `0,5 · ln(r) · r / dz`, abgebrochen erst bei r > 16.
  Potenz als Regler (2–16, Standard 8, `PARAMS.flyPower`).
- **Detailgrad nach Entfernung:** Die Formel bricht ab, sobald ihre Details feiner als ein Bildpunkt wären
  (`dz · gEps > uLod`, `FLY.LOD` = 2). Ferne Stellen brauchen so nur 4–5 Durchgänge. Für Normalen und Ritzen wird
  danach mit **fester** Durchgangszahl gerechnet (`gIter = gUsed`, `gEps = 0`) – sonst rauschen die Normalen.
- **Gemeinsame Struktur für alle Fraktale:** Shader = `flyHead` + `kind.glsl` (nur `de()`) + `flyMain` (Strahlen, Licht,
  Schatten, Nebel, Farben). `de()` liest `gIter`/`gEps` und schreibt `gUsed`/`gTrap`. Neues Fraktal = Eintrag in
  `FLY_KINDS` (`id`, `name`, `home`, `params`, `bound()`, `uniforms(u)`, `glsl`; optional `fudge`, `relax`, `lod`).
- **Licht:** Normale aus vier Messpunkten (Tetraeder, `gradient`), Sonne mit weichem Schatten (`shadow`: zweiter
  Strahl, Halbschatten aus `10 · d / t`), Himmelslicht und etwas Gegenlicht mal Verschattung in Ritzen (`occlusion`:
  bis 5 Messpunkte über der Oberfläche), Stirnlampe an der Kamera (`uHead`: 0,5 nah an der Oberfläche, 0,2 in der
  Übersicht; reicht 14 Kamera-Abstände weit), Glanzlicht. Alle Licht-Maße hängen an `uPixRef` (Bildpunkt eines
  1080-Zeilen-Bilds), nicht an der gerade benutzten Auflösung – deshalb sehen Flug-Bild und Standbild gleich aus.
- **Farben per Orbit-Trap:** `gTrap` = wie nah z den Achsen-Ebenen und dem Mittelpunkt kam; Palettenstelle =
  `uColorShift + uColorScale · (1,5 · √trap.w + 0,6 · trap.x + 0,35 · trap.z)`, Helligkeits-Maserung aus `trap.y`.
- **Farben werden als Anteile gespeichert:** Der Strahlen-Shader schreibt nicht Rot/Grün/Blau, sondern die Anteile
  der fünf Palettenfarben plus Weiß in zwei Texturen (RGBA16F, `flyTarget` = Ziel mit zwei Texturen).
  `addColor(t, menge)` rechnet wie `palette(t)`. Der billige Shader `flyResolve` setzt die aktuelle Palette ein
  (`uPalette`). Folge: Palettenwechsel braucht keine neue Strahlen-Rechnung; Mitteln mehrerer Bilder bleibt exakt.
- **Glow/Nebel:** Glühen um die Umrisse (Strahlen, die knapp verfehlen: `exp(−Winkel / 0,012)`), Glühen in Ritzen
  (`0,5 · (1 − ao)³`, heller als Weiß → gemeinsamer Bloom). Nebel `1 − exp(−Weg / uFogDist)` mit
  `uFogDist = FLY.FOG (40) · fly.scale` (Sichtweite = 40 Kamera-Abstände); er liegt **nur innerhalb der Hüllkugel**:
  von außen (Übersicht) bleibt der Hintergrund dunkel, tief im Fraktal verschwindet die Ferne in einem leicht
  leuchtenden, palettengetönten Dunst.
- **Hüllkugel:** Strahlen beginnen am Eintritt in die Kugel `kind.bound() · 1,12` und enden am Austritt bzw. nach
  `7 · uFogDist` im Nebel; Strahlen daran vorbei kosten keinen Schritt.
- **Messfühler** (`flyProbe`, `uTask = 1`): derselbe Shader rechnet für 1 Bildpunkt Abstand und Richtung zur Oberfläche
  an der Kamera; abgeholt ohne die Grafikkarte aufzuhalten (PBO + `fenceSync`, wie `readPartStats`), nach einem Sprung
  einmal direkt (`flyProbe(true)`). `flyClear()` = letzte Messung minus seither geflogene Strecke (sicherer Wert).
- **Flug:** Kamera = Ort + Quaternion (frei drehbar). Maus-Blick: Klick fängt die Maus (Pointer Lock), sonst Ziehen;
  Pfeiltasten drehen auch. `W A S D`, Leertaste/`C` hoch/runter, Umschalt = 3× Tempo. Tempo in „Abständen zur
  Oberfläche pro Sekunde“ (`FLY.SPEED` 0,9) mit Trägheit (`ACCEL` 5/s, Ausrollen `GLIDE` 2,2/s).
- **Sprung** (`flyGo(o)`, Taste `R` = Start): Bild blendet 0,5 s ab und auf, in der Mitte wird die Kamera versetzt
  (Einzelheiten unter „Bedienung (Schritt 4)“).
- **Auto-Play:** Kameraflug (siehe „Klang, Kameraflug, Flacker-Reduktion (Schritt 6)“). Taste **`P`** statt `A`
  (Modus-Eigenschaft `autoplayKey`; `A` fliegt nach links).
- **Shader wird erst beim ersten Besuch übersetzt**, im Hintergrund (`KHR_parallel_shader_compile`), ≈ 0,5–1 s;
  solange bleibt das Bild schwarz und die Info-Zeile meldet es.

### Leistung und Genauigkeit (Schritt 2)
- **Zwei Betriebsarten** (`drawFlight`): `flyImageKey()` fasst alles, wovon das Strahlen-Bild abhängt, in einen Text
  (Kamera, Maßstab, gerundete Regler, Stufe; **nicht** die Palette). Ändert er sich → **Bewegung**, sonst
  **Stillstand**. Damit das Bild wirklich zur Ruhe kommt, werden Rest-Tempo (< 0,004), Rest-Drehung (< 2 · 10⁻⁵) und
  der Maßstab `fly.scale` (auf 0,4 % genau) „eingerastet“.
- **Bewegung = verkleinertes Bild, das sich selbst regelt:** Gerechnet wird in die linke untere Ecke von `fly.g`
  (Größe = Bildschirm × `FLY_LEVELS[].move`), und zwar `fly.dyn` (0,35 … 1) davon; `flyShow` zeigt den Teil
  vergrößert an. `fly.dyn` folgt der **gemessenen Rechenzeit der Grafikkarte** (`EXT_disjoint_timer_query_webgl2`,
  `flyTimeBegin/End/Poll`, Antwort 1–2 Bilder später): Ziel = `FLY.GPU_SHARE` (60 %) der Zeit eines Bildschirm-Bilds
  (`flyBudget()`, bei 60 Hz 10 ms, bei 144 Hz 4,2 ms); neuer Maßstab = alter · √(Ziel / gemessen), 40 % des Wegs pro
  Messung (`flyMeasured`). Ohne die Erweiterung regelt `flyPace` nach den Bildabständen (gröber, geprüft).
- **Stillstand = scharfes Standbild in Streifen:** `flyRefine` rechnet pro Bildschirm-Bild so viele Zeilen von
  `fly.acc` (Bildschirm × `still`), wie ins Zeit-Budget passen (`gl.scissor`; Schätzung aus der zuletzt gemessenen
  Zeit pro Bildpunkt, wächst höchstens 1,6-fach pro Bild). Durchgang 1 füllt das Bild, danach wird weich übergeblendet
  (`FLY.FADE` 0,2 s). Durchgänge 2 … `aa` verschieben die Strahlen um Bruchteile eines Bildpunkts (`flyJitter`,
  Halton-Folge) und werden mit Anteil 1/k eingemischt (`blendColor` + `CONSTANT_ALPHA`) → Mittelwert =
  Kantenglättung. Danach kostet das Bild nichts mehr.
- **Stufen** (`FLY_LEVELS`: move / still / aa / steps / shadow / ao): Niedrig 0,5 / 0,75 / 2 / 100 / 10 / 2 ·
  Mittel 0,7 / 1 / 3 / 120 / 16 / 3 · Hoch 0,85 / 1 / 4 / 150 / 20 / 4 · Ultra 1 / 1 / 8 / 190 / 24 / 5 ·
  Extrem 1 / 1 / 12 / 250 / 32 / 5 · Maximum 1 / 1 / 16 / 320 / 40 / 5. Obergrenzen `MOVE_PIXELS` 4,2 Mio.,
  `STILL_PIXELS` 9 Mio. (Speicher auf 4K-Schirmen).
- **Auto-Qualität:** `idle()` meldet „nicht hochschalten“ im Stillstand und solange `fly.dyn < 0,98` – hochgeschaltet
  wird nur, wenn beim Fliegen wirklich Luft ist. Geprüft: Hoch → Ultra nach 6 s, danach stabil, immer 60 FPS.
- **Schneller gerechnet** (Nahaufnahme, Ultra, 1351×1205: 19 ms → ≈ 10 ms):
  - Potenz genau 8: ohne Winkelfunktionen (Winkel als Zahlenpaar, dreimal verdoppeln; `uPowInt == 8`) → −25 %.
  - Schatten: entlang des Schatten-Strahls gröber (`gEps = max(px, 0,05 · t)`), Mindestschritt `px + 0,25 · t`,
    weniger Schritte → Schatten kosten 3–4 ms statt 7–9 ms.
  - Größere Schritte auf Probe („Über-Relaxation“, `FLY.RELAX` 1,25, mit Rückzieher, wenn sich die leeren Kugeln nicht
    überlappen) → −12 %; Tiefen-Unterschied im Mittel < 0,1 %, an 0,1–0,2 % der Bildpunkte > 2 %.
- **Kamera kann nicht in die Oberfläche:** Der Anteil der Bewegung auf die Oberfläche zu ist auf ¼ des freien
  Abstands pro Bild begrenzt, insgesamt auf die Hälfte (schützt bei riesigen Zeitschritten). Steckt die Kamera doch
  zu dicht davor oder im Inneren (Regler hat die Form verändert), schiebt `updateFlight` sie hinaus: davor entlang
  `fly.grad`, im Inneren (`dist < 2 %` der Untergrenze) vom Mittelpunkt weg; solange dunkelt `fly.dim` das Bild ab.
- **Grenze der 32-Bit-Zahlen:** `flyEpsMin()` = 3 Rundungsschritte (`FLY.EPS_FLOOR` · 1,2 · 10⁻⁷ · größte
  Koordinate) ist die feinste Treffer-Schwelle. `flyFloor()` = Abstand, bei dem ein Bildpunkt (1080 Zeilen) genau so
  groß ist ≈ **0,00037** (≈ 3000-fache Vergrößerung gegenüber dem Start). Näher lässt die Bewegungs-Begrenzung die
  Kamera nicht: sie bremst weich bis zum Stillstand, ein Toast erklärt es. Tangential und rückwärts geht es weiter.
- **Anlauf nach einer Pause:** Nach > 0,7 s Stillstand startet die Bewegung mit 60 % von `fly.dyn` (die Grafikkarte
  taktet sich im Leerlauf herunter: erste Bilder 43 ms statt 8 ms → ohne das 3 Ruckler, mit: keiner).

### Weitere Fraktale und Faltungs-Baukasten (Schritt 3)
- **Sechs Einträge in `FLY_KINDS`** (Knöpfe im Panel-Abschnitt „3D-Fraktal“, Tasten `1`–`6`): Mandelbulb, Mandelbox,
  Menger-Schwamm, Sierpinski-Pyramide, 3D-Julia, Faltungs-Baukasten. Jeder liefert nur `de()`; Strahlen, Licht,
  Schatten, Nebel, Farben, Regelung der Auflösung und Standbild sind für alle derselbe Code (`flyHead`/`flyMain`).
- **Alle Formen sind auf Radius 1,3 … 2,2 umgerechnet** (Faktor im Shader: `uBSize`, `uKSize`) – dadurch gelten
  Flugtempo, Nebel, Welt-Grenze (`FLY.WORLD` 7) und die Grenze der Rechengenauigkeit unverändert für alle.
- **Mandelbox** (`id: 'box'`): Kasten-Faltung (`clamp(z, −1, 1) · 2 − z`), Kugel-Faltung (`k = clamp(1/r², 1, 4)`),
  dann `z · s + c`; `dr ← dr · k · |s| + 1`; Abstand = `|z| / dr`. Regler **Skalierung** −3 … 3,5 (zwischen −1,25 und
  1,25 gibt es kein Fraktal → der Wert bleibt am Rand stehen, `flyBoxScale()`); Größe des Würfels
  `flyBoxHalf(s) = 2 (s + 1) / (s − 1)` bzw. 2 bei negativem s. `fudge` 0,9, `lod` 2.
- **Faltungs-Vorlage `flyKifs(fold)`** für Menger-Schwamm (`fold` 3, s = 3), Sierpinski-Pyramide (`fold` 2, s = 2) und
  Baukasten (`fold` 0 = vom Regler `uFold`): pro Wiederholung 1) Falten (1 Spiegeln, 2 Tetraeder, 3 Menger,
  4 Kasten), optional Kugel-Faltung, 2) Drehen (`uKRot`, Matrix aus `flyRotation(x, y, z)`), 3) Vergrößern um den
  Punkt `uKShift` (`z · s − Verschiebung · (s − 1)`). `dr` = Produkt aller Vergrößerungen; Abstand = Abstand zur
  Grundform (Würfel, Tetraeder, bei „keine Faltung“ Kugel) geteilt durch `dr`. Bei festem `fold` ist es ein
  `#define` – der Übersetzer wirft die anderen Zweige weg. Regler-Werte setzt `flyKifsUniforms`.
- **3D-Julia** (`id: 'julia'`): Quaternionen-Julia z → z² + c, Schnitt mit viertem Teil 0;
  `dz ← 2 · r · dz`, Abstand = `0,5 · ln(r) · r / dz`. Regler **Form A–D** = die vier Teile von c
  (Standard −0,2 / 0,6 / 0,2 / 0,2); Hüllkugel `(1 + √(1 + 4·|c|)) / 2`.
- **Baukasten** (`id: 'kit'`): Regler **Falten** (keine/Spiegeln/Tetraeder/Menger/Kasten, rastet ein), **Skalieren**
  1,3–3,5×, **Verschieben X/Y/Z** 0–2, **Drehen X/Y/Z** ±90°, **Kugel-Faltung** 0–90 %, **Wiederholungen** 3–24.
  **Startwerte** (`FLY_KIT`, Knöpfe; setzen nur Zielwerte → die Form verwandelt sich weich): Wirbel-Würfel
  (Menger, 3×, Drehen Z 25°), Gitterwürfel (Menger, Verschieben 1/1/0,5), Kristall (Tetraeder, Drehen 0/10/5),
  Koralle (Spiegeln, 2×, Drehen 20/0/30), Tempel (Kasten + Kugel-Faltung 50 %, 2,2×), Felsnadel (Spiegeln, 1,8×,
  Verschieben 1/1,2/0,6, Drehen 20/35/10). Wer einen Regler anfasst, hat eine „Eigene Mischung“ (`fly.kit = −1`).
- **Wechsel des Fraktals** (`setFlyKind`): Der Shader wird beim ersten Mal im Hintergrund übersetzt (0,3–1,1 s); so
  lange bleibt das alte Fraktal zu sehen, dann Blende (`flyGo` mit `kind`) an die Start-Kamera des neuen.
  **Geteilte Regler** (`FLY_SHARED`: Drehen X/Y/Z, Wiederholungen): Jedes Fraktal merkt sich seine Werte
  (`flyEnterKind`, `kind.saved`) – ein verdrehter Baukasten verdreht nicht den Menger-Schwamm.
- **Panel:** Abschnitt „3D-Fraktal“ (Fraktal-Knöpfe, Flug-Tempo, Zurück zum Start, Info) und Abschnitt „Form“
  (Zeilen mit `data-kind="bulb"`, `"menger sierp kit"` … – `updateFlyUi` zeigt nur die des gewählten Fraktals;
  welche Regler die Form ändern, steht in `kind.params` und geht in `flyImageKey` ein).
- **Leistung der neuen Formen:** Faltungs-Fraktale haben viele Löcher und Kanten → mehr Schritte pro Strahl. Dagegen:
  `lod: 0,5` (Details nur bis 1 Bildpunkt; Menger 25 → 16 ms), in Bewegung nur `FLY.MOVE_STEPS` (60 %) der Schritte
  (die letzten brauchen wenige Strahlen, kosten aber fast die halbe Zeit), Schatten mit Mindestschritt `px + 0,35 · t`
  und 10–24 Schritten. Den Rest fängt die Regelung der Auflösung ab.
- **Eigene Schätzung der Bildschirmfrequenz** (`flyRefresh`, `fly.hz`): sechstkürzester Bildabstand der letzten 60,
  kann nur steigen. Grund: `autoQ.refresh` (höchste geglättete Bildrate) stieg in den Tests durch zwei direkt
  aufeinanderfolgende Bilder nach Rucklern auf 157 Hz → das Zeit-Budget war 4 statt 10 ms, das Bild unnötig unscharf.

### Bedienung (Schritt 4)
- **Tasten und Maus:** Mausrad = Flug-Tempo (10–400 %, derselbe Wert wie der Regler; `flyWheel`) · `B` halten =
  bremsen (`FLY.BRAKE` 9/s: steht nach ≈ 0,6 s weich) · `Y` / `X` = rollen (Drehung um die Blickachse, läuft weich an
  und aus; im Code `KeyZ`/`KeyX` = Lage der Tasten, auf deutschen Tastaturen steht dort Y) · `G` = Horizont wieder
  gerade (`flyLevel`) · `N` = Zufalls-Form (nur Baukasten) · `K` = Kamera merken · `7` `8` `9` `0` = Kamera-Platz 1–4
  anspringen. Unverändert: Klick/Ziehen = umsehen, `W A S D`, Leertaste/`C`, Umschalt = 3× Tempo, `R` = Start, `1`–`6`.
- **Sprung `flyGo({ pos, look ODER quat, kind, apply })`** (ersetzt `flyJump`/`fly.nextKind`): wartet in `fly.go`, bis
  der Shader des Ziel-Fraktals übersetzt ist, dann Blende (`fly.jump`). In der Mitte der Blende (Bild dunkel):
  Fraktal wechseln (`flyEnterKind`), `apply()` aufrufen (Regler ohne Überblenden umstellen), Kamera setzen, Abstand
  sofort messen. Alles, was die Szene schlagartig ändert, soll diesen Weg nehmen (Zufalls-Form, Kamera-Plätze,
  später Szenarien).
- **Trägheit** (Regler `flyInertia`, 0–100 %, Standard 40 %): Ausroll-Rate = `GLIDE` 6/s · `GLIDE_LONG` 0,08^Regler.
  Gemessen (aus vollem Tempo bis zum Stillstand): 0 % 0,9 s · 40 % 2,5 s · 100 % 11 s · mit Bremse 0,6 s.
- **Neue Regler:** Abschnitt „Flug“ (Flug-Tempo, Trägheit, Maus-Empfindlichkeit `flyLook` 25–300 %, Blickwinkel
  `flyFov` 35–110°, Standard 70° – ersetzt die frühere Konstante `FLY.FOV`; `flyTanHalf()`), Abschnitt „Licht & Farbe“
  (Glühen `flyGlow` 0–1,5, Anzeige 0–300 %; Nebel `flyFog` 0–300 %; Schatten `flyShadow`; Farbdichte `flyColor`
  0,2–4×; Farb-Verschiebung `flyHue` = `uColorShift`, Standard 8 %). Alle stehen in `flyImageKey` (sonst bliebe das
  alte Standbild stehen). Der Blickwinkel verschiebt die Untergrenze des Abstands (35°: 0,0010; 110°: 0,00023).
- **Zufalls-Form** (`flyKitRandom`, Knopf im Abschnitt „Form“): würfelt bis zu 16 Kandidaten in bewährten Bereichen
  (Faltung Spiegeln/Tetraeder/Menger/Kasten mit Gewichten 30/15/30/25 %, Skalierung je Faltung, Verschiebung
  1 / 0,55–1,3 / 0,45–1,3, Drehung je Achse mit 55 % Wahrscheinlichkeit 8–40° (Tetraeder höchstens 12°, Menger 30°),
  Kugel-Faltung beim Kasten zu 85 %, beim Menger-Schwamm nie, 11–17 Wiederholungen; Spiegeln bekommt immer
  mindestens eine Drehung). Von jedem der 16 Kandidaten wird ein Probe-Bild gerechnet (`flyViewRender`/`flyViewRead`: 32×32 Bildpunkte von
  der Start-Kamera, gelesen wird der G-Buffer): `cover` (Anteil getroffener Bildpunkte, gut 0,14–0,68), `edges`
  (Sprünge in der Entfernung, < 0,36 – sonst Staub), `bumps` (Anteil unebener Stellen, > 0,3 – sonst glatter
  Klotz), `light` (mittlere Helligkeit, > 0,2 – sonst dunkles Gestrüpp). Der erste brauchbare gewinnt, sonst der
  beste. Kosten in Echtzeit: 35–70 ms pro Klick (zwei Rückfragen an die Grafikkarte, siehe Fallstricke). Umgestellt wird per `flyGo` mit `apply` (Blende, Start-Kamera), `fly.kit = −2`.
- **Kamera-Plätze** (`fly.cams`, 4 Stück, `flySaveCam(i)`, `flyGoCam(i)`): merken Fraktal, Ort und Drehung
  (Quaternion), **nicht** die Form-Regler (das machen die Szenarien in Schritt 5). Gespeichert im Browser unter
  `satisim.flyCams` (`loadStore`/`saveStore` – stürzen nicht ab, wenn der Browser das Speichern verbietet).
  Knöpfe im Abschnitt „Kamera merken“: belegter Platz = anspringen, leerer Platz oder Umschalt + Klick = merken.
- **Panel:** fünf Abschnitte – „3D-Fraktal“ (Fraktal-Knöpfe, Hinweis, Info-Zeile), „Form“ (Baukasten-Startwerte,
  Zufalls-Knopf, Regler des gewählten Fraktals, Wiederholungen), „Flug“, „Kamera merken“, „Licht & Farbe“.
- **Geprüft** (`run-f4.js`, `run-fq.js`): Mausrad-Grenzen, Rollen und Ausrichten (Kamera steht danach exakt wie
  vorher), Bremse/Trägheit, Kamera-Platz merken → anderes Fraktal → anspringen (Ort und Drehung exakt, auch nach
  Neuladen), 12 Zufalls-Formen ohne ungültige Werte, alle neuen Regler an beiden Anschlägen ohne ungültige Werte;
  echte Eingaben in der Vorschau (Mausrad, `K`, `G`, `7`). In Echtzeit (1523×1205, alle 6 Stufen, Mandelbulb und
  Baukasten, nah an der Oberfläche): 60 FPS, GPU 2,9–10,1 ms, längstes Bild 17–33 ms, keine GL-Fehler.

### Anbindung an Szenarien und Bild-Export, Stellen-Suche (Schritt 5)
- **Szenario des Flugs** (`SCENE_MODES.flight` im gemeinsamen Abschnitt): Fraktal, Kamera (Ort, Quaternion),
  Baukasten-Startwert, dazu die Regler des gewählten Fraktals, `FLY_SHARED`, Licht/Farbe und Blickwinkel. Geladen
  wird über `flyGo({ kind, pos, quat, apply })`. 10 Start-Szenarien in `SCENE_STARTS.flight`.
- **Bild-Export:** `freeAspect: true` (jedes Seitenverhältnis wird direkt gerechnet), `shotBusy()` (wartet auf
  Sprünge), `shotReady()` (alle Durchgänge der Kantenglättung fertig), `shotProgress()`. **`flyQuality()`** ersetzt
  überall `FLY_LEVELS[qualityLevel]`: beim Export gilt die höchste Stufe. Das Standbild darf dann bis `SHOT.PIXELS`
  groß werden, die Streifen sind dreimal so groß, es wird nicht übergeblendet; `flyImageKey` enthält, ob gerade
  exportiert wird.
- **Probe-Bilder** (`flyViewRender(i, pos, quat, scale)` rechnet Kachel i, `flyViewRead(n)` wertet n Kacheln aus):
  bis zu 16 Ansichten zu je 32×32 Bildpunkten liegen nebeneinander in `fly.tiny` und werden **gemeinsam** gelesen.
  Je Kachel `cover`, `edges`, `bumps`, `light` (Erklärung bei „Zufalls-Form“). `flyViewProbe(…)`/`flyKitProbe()` = ein
  einzelnes Probe-Bild (für Tests). Kacheln entstehen über `flyRender(…, { at: [x, y] })` (verschobener Viewport,
  `uOffset` gleicht aus).
- **Stellen-Suche `flyFindSpot(level, tries ≤ 8)`** → `{ pos, quat, dist, light }` oder `null`: sucht eine Kamera im
  Abstand `level` dicht über der Oberfläche, die flach über sie hinwegschaut. 8 Strahlen starten an zufälligen Punkten
  einer Kugel um das Fraktal (Radius `bound · 1,1 + level · 1,5`) und zielen auf zufällige Punkte im Inneren. Das
  Herantasten rechnet **der Shader** für alle zugleich (`uTask = 2`, Funktion `seek()`, Zielbild 8×2 Bildpunkte
  `fly.seekBuf`: Zeile 0 = Richtung von der Oberfläche weg + Strecke, Zeile 1 = wie hell die Stelle in der Sonne
  liegt, mit Schatten) – **eine** Rückfrage genügt. Gewählt wird die am besten beschienene Stelle (plus etwas Zufall).
  Kamera: Blick entlang der Oberfläche, zur Oberfläche geneigt um `0,85 · flyDip + 0,2…0,4` rad (`flyDip(pos, clear)`
  = so weit liegt der Horizont unter der Waagrechten, wenn das Fraktal eine Kugel wäre – aus großer Höhe muss die
  Kamera stärker nach unten schauen, sonst zeigt das Bild fast nur Himmel), „oben“ = von der Oberfläche weg.
  Kosten in Echtzeit: ≈ 17 ms (ein Bildschirm-Bild).

### Klang, Kameraflug, Flacker-Reduktion (Schritt 6)
- **Klang** (`updateFlySound(dt, clear)`, einmal pro Bild aus `updateFlight`; Zustand `fly.snd`):
  - *Fahrtwind:* das gemeinsame Pinsel-Rauschen (`audio.brushLevel = 0,7 · √v`, v = Tempo / 2,2).
  - *Flug-Töne:* ein gezupfter Ton pro `FLY.NOTE_TRAVEL` (0,5) geflogener „Abstände zur Oberfläche“ – bei normalem
    Tempo knapp 2 pro Sekunde, Lautstärke `0,04 + 0,12 · v`. Tonhöhe = Nähe zur Oberfläche: Stufe
    `15 − 0,9 · Tiefe` + vier wechselnde Stufen (kleine Melodie); Tiefe = wie oft sich der Abstand gegenüber der
    Übersicht halbiert hat (0 … ≈ 11). Übersicht hoch, tief im Fraktal tief (wie die Zoomtiefe im Mandelbrot-Modus).
    Stereo: Flug nach rechts klingt rechts.
  - *Tiefen-Ton:* leiser tiefer Ton (eine Oktave unter der Tonleiter, Lautstärke 0,055), wenn der Abstand eine
    Stufe (Faktor 1,41) näher oder ferner wird – höchstens alle 0,8 s.
  - *Grenze erreicht:* `audioFlyLimit` (weicher Ton, 65 Hz). Sprünge: `audioClear`; Kamera merken: `audioTock`;
    Zufalls-Form: `audioClick`; Ankunft an einer Stelle im Kameraflug: `audioBurst`.
  - Das Tempo hebt `audio.energy` (die Musik öffnet sich beim Fliegen). „Flackern reduzieren“: Töne 40 % leiser.
  - Gemessen (Analyser am Ausgang, Musik aus): Ruhe 0,001; Anflug aus der Übersicht Spitze 0,06 / RMS 0,015;
    Seitwärtsflug nah an der Oberfläche 0,03–0,055; Vollgas 0,15–0,18 / RMS 0,04; Kameraflug 0,03 / RMS 0,004;
    Grenz-Ton 0,07; Klänge aus 0,000. In einem Lauf trat einmal eine einzelne Spitze von 0,38 auf (Ursache nicht
    gefunden; beim Nachmessen mit Protokoll aller Töne nicht wieder). **Nicht geprüft: wie es klingt.**
- **Kameraflug** (`flyTourStart`, `flyAutoplay(dt)`, Zustand `fly.tour`; Auto-Play/Bildschirmschoner, Taste `P`,
  Knopf „Kameraflug starten“): fliegt im **gewählten** Fraktal – Form, Regler, Palette-Wahl des Nutzers bleiben
  (die Palette wechselt wie in allen Modi alle 25 s), funktioniert deshalb auch mit eigenen Baukasten-Formen.
  - *Beginn:* 4 s fast still (treibt nur mit Tempo 0,04 vorwärts, `tour.hold`), dann die erste Blende.
  - *Gleiten:* `flyAutoplay` gibt `fly.auto = { dir, speed, quat }` vor, geflogen wird über `updateFlight` (derselbe
    Weg wie von Hand → kann nicht in die Oberfläche). Tempo `FLY.TOUR_SPEED` 0,2 Abstände/s. „Oben“ (`tour.up`) = die
    stark geglättete Richtung von der Oberfläche weg. Flugrichtung = Blickrichtung ohne ihren Anteil zur Oberfläche
    hin, plus leichtes Schlängeln; **Höhe halten:** zu hoch → zur Oberfläche hin (Gewicht 0,35), zu tief → weg (1,2).
    Blick: in Flugrichtung, um `0,85 · flyDip + 0,3` rad zur Oberfläche geneigt; die Kamera führt mit
    `FLY.TOUR_TURN` 0,45/s nach.
  - *Wechsel:* nach 18–26 s `flyGo({ blink: 1,8 s, spot: () => flyFindSpot(level), after })`: Die Stelle wird erst
    gesucht, wenn das Bild dunkel ist. Abstände reihum `FLY.TOUR_LEVELS` 0,035 / 0,09 / 0,16 / 0,055 (× 0,75–1,3).
    Findet die Suche nichts, bleibt die Kamera, wo sie ist.
  - Jede Eingabe beendet ihn (`autoplayStop`: `fly.auto = fly.tour = null`), die Kamera rollt normal aus.
  - Geprüft im Zeitraffer (`run-f6.js`, 90 s je Form, alle 6 Formen): 4 Stellen-Wechsel, keine ungültigen Werte, nie
    im Inneren, Abstand im Mittel das 1,04–1,17-Fache des Soll-Abstands (kleinster 0,88-fach), nie näher als das
    68-Fache der Untergrenze, steht nie still. In Echtzeit (Mandelbulb, Ultra, 75 s): 59,9 FPS, schnellste Drehung
    5°/s; die einzigen langen Bilder sind die Stellen-Wechsel (50–67 ms, genau im dunkelsten Moment der Blende).
- **Flacker-Reduktion:** Blenden bei Sprüngen dauern doppelt so lange (`1 + calm`), der Kameraflug ist 40 %
  langsamer und wechselt seltener, Töne leiser; dazu die gemeinsame Helligkeits-Bremse. Gemessen (Sprung „Zurück zum
  Start“ aus einer Nahaufnahme): größter Sprung der mittleren Helligkeit pro Bild 0,116 → 0,029, größter Anteil der
  Bildpunkte mit Sprung > 10 %: 67 % → 4,6 % (ein einzelnes Bild), mittlere Änderung pro Bild 0,0153 → 0,0080.
- **Panel:** „3D-Fraktal“ (Fraktal-Knöpfe, Hinweis, Info-Zeile, Knopf „Kameraflug starten“), „Form“, „Flug“,
  „Kamera merken“, „Licht & Farbe“; dazu die gemeinsamen Abschnitte (Szenarien, Bild speichern, Palette, Bloom …).
- **Leistung nach Schritt 6** (`run-fq.js`, 1920×1080, nah an der Oberfläche, alle 6 Stufen, Mandelbulb und
  Menger-Schwamm): 60 FPS, GPU 1,6–8,5 ms, längstes Bild 17–20 ms, keine ungültigen Werte, keine GL-Fehler;
  Fluid-Prüfsummen wie vorher (dieselben drei Werte); Konsole ohne Fehler und Warnungen.

### Grenzen und Offenes
- **Ein Mensch muss noch beurteilen:** wie der Flug sich anfühlt (Trägheit, Tempo, Rollen), wie es klingt, ob der
  Kameraflug zu schnell/zu langsam wechselt. Alle Werte sind nach Messwerten und Bildschirmfotos eingestellt.
- **Maus fangen** (Pointer Lock) ließ sich im Test-Browser nicht prüfen; Ziehen mit gedrückter Maustaste ist geprüft.
- **144 Hz:** gemessen wurde nur in der 60-Hz-Vorschau. Die Auflösung beim Fliegen regelt sich nach der Rechenzeit –
  bei 144 Hz wird das Flug-Bild entsprechend kleiner gerechnet (unschärfer), das Standbild bleibt scharf.
- Der Kameraflug bleibt im gewählten Fraktal und nutzt nicht die 10 Start-Szenarien. Bei Formen aus lauter Staub
  („Kristall“) findet die Stellen-Suche wenig Halt – die Kamera gleitet dann durch den Staub.
- Die Stellen-Suche wählt nur nach Sonnenlicht, nicht nach Bildaufbau; bei großem Abstand (0,16) ist oft die halbe
  Bildfläche Himmel.
- Zufalls-Form: der Klick hält das Bild kurz an (35–70 ms), bevor die Blende beginnt.
- Tiefer hineinzoomen als ≈ 3000-fach geht nicht (siehe „Ausprobiert und verworfen“).
- Offen: Zwei-Finger-Bedienung, Gamepad, Farben wandern lassen (bräuchte neue Strahlen-Rechnung pro Bild),
  Sonnenstand als Regler, Kameraflug über mehrere Fraktale/Szenarien.

### Messwerte (1920×1080, 60-Hz-Vorschau, NVIDIA RTX 3050 Laptop; Flug = seitwärts fliegen, Stillstand = danach anhalten)
| Stufe | Flug: Übersicht | im Tal (Abstand 0,1) | nah (0,02) | sehr nah (0,0005) | FPS im Flug | Standbild | scharf nach | fertig geglättet nach |
|---|---|---|---|---|---|---|---|---|
| Niedrig | 960×540 · 1,6 ms | 960×540 · 2,4 ms | 960×540 · 5,2 ms | 960×540 · 5,7 ms | 60 | 1440×810, 2-fach | ≤ 0,03 s | ≤ 0,07 s |
| Mittel | 1344×756 · 2,1 ms | 1344×756 · 5,0 ms | 1344×756 · 5,7 ms | 1317×741 · 9,8 ms | 60–61 | 1920×1080, 3-fach | ≤ 0,03 s | ≤ 0,15 s |
| Hoch | 1632×918 · 2,7 ms | 1632×918 · 6,2 ms | 1632×918 · 9,4 ms | 1290×725 · 9,8 ms | 60 | 1920×1080, 4-fach | ≤ 0,05 s | ≤ 0,17 s |
| Ultra | 1920×1080 · 3,4 ms | 1920×1080 · 9,8 ms | 1656×931 · 10,7 ms | 1225×689 · 10,1 ms | 59–61 | 1920×1080, 8-fach | ≤ 0,05 s | ≤ 0,4 s |
| Extrem | 1920×1080 · 3,4 ms | 1815×1021 · 9,4 ms | 1645×925 · 10,0 ms | 1223×688 · 9,8 ms | 59–60 | 1920×1080, 12-fach | ≤ 0,05 s | ≤ 0,6 s |
| Maximum | 1920×1080 · 3,3 ms | 1920×1080 · 9,7 ms | 1617×910 · 9,5 ms | 1191×670 · 10,0 ms | 60 | 1920×1080, 16-fach | ≤ 0,08 s | ≤ 0,82 s |
- (Zellen „Flug“: gerechnete Auflösung · gemessene GPU-Zeit der Strahlen-Rechnung.) Längstes Bild im Flug 17 ms,
  vereinzelt 33 ms; keine GL-Fehler, keine ungültigen Werte.
- **Fenster 3840×2160:** Flug 55–60 FPS (Flug-Bild höchstens 2733×1537, nah 1603×901, sehr nah 1183×665),
  Standbild 3840×2160 scharf nach 0,03–0,19 s, fertig nach 0,17–3,3 s (Maximum, 16-fach; dabei 13 Bilder mit 34 ms).
- **Ohne Zeitmessung** (Ersatz-Regelung): 58 FPS im Flug (3 von 87 Bildern über 25 ms), Standbild nach 1,2 s.
- **Extremfälle:** mit Vollgas in die Oberfläche (2500 Bilder, auch bei 30 Bildern/s): kleinster Abstand 0,000367 bei
  Untergrenze 0,000370; Zeitschritte von 3 s: kein Durchflug; Kamera im Inneren gestartet: nach 30 Bildern draußen;
  Potenz-Regler in Fahrt bei Kamera dicht an der Oberfläche: 2 Bilder im Inneren, danach frei; an der Untergrenze
  keine ungültigen Werte im Bild.
- 54 Moduswechsel durch alle fünf Modi fehlerfrei; Fluid-Prüfsumme unverändert (`ee1e9dc5-123c5505`, 12 von 12).

### Messwerte Schritt 3 (1920×1080, RTX 3050 Laptop)
| Form | übersetzen | Flug nah an der Oberfläche, Stufe Ultra (in Echtzeit) | GPU-Zeit bei voller Auflösung: fern / nah / an der Grenze |
|---|---|---|---|
| Mandelbulb | 0,5–0,9 s | 59 FPS · 1831×1030 | 1,9 / 12,3 / 20,3 ms |
| Mandelbox | 0,3 s | 60 FPS · 1413×795 | 5,0 / 17,8 / 46,1 ms |
| Menger-Schwamm | 0,5 s | 60 FPS · 1716×965 | 1,3 / 14,9 / 14,5 ms |
| Sierpinski-Pyramide | 0,5 s | 60 FPS · 1661×934 | 2,6 / 23,8 / 31,8 ms |
| 3D-Julia | 0,3 s | 60 FPS · 1920×1080 | 1,6 / 10,5 / 13,0 ms |
| Baukasten: Wirbel-Würfel | 1,1 s (einmal) | 60 FPS · 1787×1005 | 3,1 / 24,9 / 33,6 ms |
| Baukasten: Gitterwürfel | | 60 FPS · 1697×954 | 3,3 / 25,6 / 34,6 ms |
| Baukasten: Kristall | | 60 FPS · 1644×925 | 1,8 / 17,5 / – |
| Baukasten: Koralle | | 59 FPS · 1560×878 | 2,3 / 23,0 / 26,8 ms |
| Baukasten: Tempel | | 59 FPS · 1051×591 | 2,4 / 38,6 / 61,3 ms |
| Baukasten: Felsnadel | | 60 FPS · 1354×762 | 2,7 / 23,5 / 25,4 ms |
- (Mittlere Spalte: Bildrate und die Auflösung, auf die sich das Flug-Bild einregelt; längstes Bild 17 ms, zweimal
  33 ms. Rechte Spalte: Flug-Bild fest auf 1920×1080 – so teuer wäre es ohne Regelung.)
- **Stabilität:** jeder Form-Regler an beiden Anschlägen, einzeln und alle zusammen, beim Baukasten zusätzlich alle
  5 Faltungen × Skalieren 1,3/3,5 × Kugel-Faltung 0/90 % × drei Drehungen: 126 Fälle, **kein ungültiger Wert**,
  kein GL-Fehler, längstes Bild 14 ms (Stufe Mittel). Alle 11 Formen × Stufen Niedrig/Ultra/Maximum: fern, nah,
  Standbild und an der Grenze der Rechengenauigkeit ohne ungültige Werte; die Kamera bleibt überall an der
  Untergrenze stehen (0,00037; Mandelbox 0,00045, weil sie weiter vom Mittelpunkt entfernt ist).
- 54 Moduswechsel (mit jedem der sechs Fraktale) fehlerfrei; Fluid-Prüfsummen wie vorher (dieselben Hauptwerte).

### Fallstricke
- **Direktes Zurücklesen (`readPixels`) kostet im laufenden Betrieb ein ganzes Bildschirm-Bild (≈ 17 ms) pro
  Aufruf** – in Tests innerhalb EINES JavaScript-Aufrufs sieht man das nicht (dort ≈ 1 ms). Erst alles rechnen, dann
  einmal lesen (Probe-Bilder als Kacheln, Stellen-Suche als 8×2-Bild). Was ruckfrei sein muss, liest gar nicht direkt
  (Messfühler: Zwischenspeicher + `fenceSync`).
- **Im Sprung-Objekt heißt das Merkfeld „Kamera ist versetzt“ `done`** – eine Option gleichen Namens in `flyGo`
  verhindert den Sprung (so passiert; der Rückruf heißt deshalb `after`).
- Test-Falle: Läuft der Kameraflug und ein Test rechnet Bilder mit `__p.one`/`__f.still()`, fliegt die Kamera mit dem
  zuletzt gesetzten `fly.auto` ungesteuert weiter (leere Bilder im Kontaktbogen) → vorher `fly.auto = null;
  fly.vel = [0, 0, 0]`.
- `near`, `far`, `half` nicht als Namen im Shader. `atan(x, z + 1e-20)` und `max(r, 1e-20)`: ohne das gibt es auf der
  Pol-Achse ungültige Werte. Die Ausgabe wird mit `max(min(…))` begrenzt – ein einziger ungültiger Bildpunkt würde
  sich im Bloom über das Bild ausbreiten.
- **Alles, was das Strahlen-Bild verändert, muss in `flyImageKey()` stehen** (Form-Regler: in `kind.params` eintragen;
  andere: direkt dort) – sonst bleibt das alte Standbild stehen. Was sich dauernd ändert, darf dort nicht hinein (sonst wird nie verfeinert);
  solche Werte runden oder einrasten lassen.
- Neue Puffer sind leer → `ensureFlyBuffers` löscht `imageKey`, damit sofort neu gerechnet wird.
- **Hüllkugel muss stimmen:** Ist `bound()` bzw. die Größe in `flyKifsUniforms` zu klein, wird die Form kugelförmig
  abgeschnitten (so beim ersten „Tempel“: Die Kasten-Faltung klappt auch weit entfernte Punkte zurück, die Form
  reicht bis `|Verschiebung| · (s + 1) / (s − 1)`, mit Kugel-Faltung noch geteilt durch deren Radius).
- Faltungs-Fraktale: Die Orbit-Trap darf nicht auf den Falt-Ebenen liegen (dort ist der Abstand fast immer 0 →
  alles eine Farbe); deshalb Nähe zu drei verschobenen Ebenen (`abs(q − (0,3; 0,45; 0,6))`).
- Beim Detailgrad der Mandelbox gilt das Gegenteil der anderen: Hört die Formel zu früh auf, unterschätzt sie den
  Abstand und die Strahlen brauchen MEHR Schritte (`lod` 0,5: 30 ms, 2: 19 ms).
- Der Baukasten-Startwert „Kristall“ ist Staub (lauter kleine, getrennte Teile) – man fliegt hindurch statt daran
  hängen zu bleiben. Kein Fehler.
- `autoQ.refresh` (gemeinsame Auto-Qualität) kann nach Rucklern zu hoch geschätzt werden (siehe oben); das betrifft
  alle Modi und wurde nicht angefasst.
- Der Messfühler und die Zeitmessung werden innerhalb EINES JavaScript-Aufrufs nie fertig → in Tests
  `flyProbe(true)` benutzen (`__f.fly` macht das) und zum Messen `__f.fix(maßstab)` (hält die Auflösung fest).
- Es kann immer nur EINE Zeitmessung laufen: `flyTimeBegin` prüft das (`gl.getQuery(…, CURRENT_QUERY)`), sonst
  stören sich App und Test-Messung (`__t.gpu`).
- Helligkeit: Flächen dürfen nicht durchgehend über der Bloom-Schwelle (0,4) liegen, sonst legt sich ein rosa
  Schleier über alles.
- Rand des Bildes wirkt bei 70° Blickwinkel gestreckt (normale Perspektive, kein Fehler).
- **Maus fangen konnte in der Vorschau nicht geprüft werden** (der Test-Browser erlaubt es nicht); Ziehen ist geprüft.
- Ist die Vorschau verdeckt (`document.hidden`), läuft `requestAnimationFrame` mit 1 Bild/s → FPS-Tests hängen.
  Dann Bilder direkt rechnen (`__p.one`, `__f.move`, `__f.still`).

### Ausprobiert und verworfen
- **Stellen-Suche mit Probe-Bild je Versuch** (schönstes Bild gewinnt): 18 Rückfragen an die Grafikkarte = 0,3 s
  Stillstand bei jedem Stellen-Wechsel → Auswahl nach Sonnenlicht direkt im Such-Shader (eine Rückfrage).
- **Feste Blickneigung im Kameraflug (17–30°):** aus größerer Höhe zeigte das Bild zu drei Vierteln leeren Himmel →
  Neigung nach Flughöhe (`flyDip`). **Abstand 0,22 als „weite“ Etappe:** trotzdem viel Himmel → 0,16.
- **Tiefen-Ton alle 0,3 s mit langem Ausklang:** beim schnellen Anflug überlagerten sich viele tiefe Töne (Spitze
  0,77 am Ausgang) → höchstens alle 0,8 s, kürzer, leiser.
- **Kameraflug als Rundflug um das Fraktal** (Schritt 1–5, `orbit` je Fraktal): zeigte immer nur die Übersicht.
- **Stellen-Suche mit dem Messfühler in einer JavaScript-Schleife** (bis 70 Einzelmessungen pro Versuch, jede mit
  direktem Zurücklesen): 0,6 s pro Suche – das Bild blieb sichtbar stehen → Herantasten im Shader (11 ms).
- **Zufalls-Form ohne Prüfung der Unebenheit** (nur Füllgrad und Kanten): etwa jede dritte Form war ein glatter
  Quader (Spiegeln ohne Drehung), ein gestreifter Block (Kasten ohne Kugel-Faltung) oder dunkles Gestrüpp
  (Menger mit Kugel-Faltung) → Regeln dafür und die Messwerte `bumps`/`light`.
- **Baukasten-Startwerte mit starker Drehung bei Tetraeder-Faltung** (0/12/24°, Seeigel 30/10/45°): zerfallen zu
  winzigem Staub → kleinere Drehungen bzw. Spiegel- und Menger-Faltung.
- **3D-Julia als Julia-Fassung der Mandelbulb** (z^n + c): nicht gebaut; die klassische Quaternionen-Julia ist glatt
  und sieht ganz anders aus als die übrigen Formen (mehr Abwechslung).
- **Schneller Weg für jede ganze Potenz als Schleife** (Winkel-Paar per „schnellem Potenzieren“): langsamer als die
  Winkelfunktionen (23–30 ms statt 19–20 ms) → nur Potenz 8 fest ausgeschrieben.
- **Erste Licht-Fassung** (Sonne 1,25, Ritzen-Glühen 1,6, Umriss-Glühen 0,035 breit): alles rosa überstrahlt, Glühen
  als Scheibe mit hartem Rand an der Hüllkugel.
- **Feinste Schwelle 16 Rundungsschritte:** nahe Flächen werden glatt wie Plastik; **1 Rundungsschritt:** Streifen,
  Details gehen verloren → 3.
- **Nebel überall (auch außerhalb der Hüllkugel) und fast schwarz:** tiefe Ansichten waren düster und flach.
- **Tief hineinzoomen wie im Mandelbrot-Modus (Bezugsbahn):** nicht gebaut. Für Faltungs-Fraktale ginge es exakt
  (Abstand zur Bahn der Kamera pro Faltung mitführen), für die Mandelbulb gibt es keine einfache auslöschungsfreie
  Formel – der Aufwand stand in keinem Verhältnis. Stattdessen sanfte Grenze bei ≈ 3000-facher Vergrößerung.

### Testen
- `.claude/flight.js` (Code-Abschnitt) und `.claude/flight-panel.html` (Panel) bearbeiten, dann
  `python .claude/splice-fly.py` – **nicht direkt in `index.html` ändern**, der nächste Lauf überschreibt es.
  Änderungen außerhalb des Abschnitts (CSS, `PARAMS`, Tasten) per Patch-Skript (`patch-f1.py`, Muster `patchlib.py`).
  Diesen Abschnitt von CLAUDE.md: `.claude/md-fly.md` ändern, dann `python .claude/md-fly.py`.
- `.claude/f-tools.js` laden → `__f.ready()` (wartet auf den Shader), `__f.view(ort, blickpunkt)`,
  `__f.fly(['KeyW'], bilder)`, `__f.fix(maßstab)`, `__f.move()` (ein Flug-Bild), `__f.still()` (Standbild zu Ende),
  `__f.stats('g' | 'acc')` (ungültige Werte), `__f.cost(n)`, `__f.gpu(n)`.
  `__f.kind('menger')` (Fraktal sofort wechseln und auf den Shader warten),
  `__f.sheet([async () => …, …], spalten)` (Kontaktbogen: mehrere Ansichten als Kacheln in EINEM Bildschirmfoto –
  spart viele Einzelbilder; `__f.sheet()` entfernt ihn wieder).
  `run-f2.js` (Stufen: Flug und Stillstand in Echtzeit; Extremfälle; Ersatz-Regelung → `window.__res`,
  `window.__opt = { parts, levels }`), `run-f3.js` (jede Form: Kosten, Regler-Anschläge, Echtzeit-Bildrate;
  `parts: ['cost', 'extremes', 'fps']`), `run-f1b.js` (Moduswechsel und Tasten in Echtzeit → `window.__res2`),
  `run-f4.js` (Bedienung aus Schritt 4), `run-s5.js` (Szenarien und Bild-Export, alle Modi), `run-f6.js` (Kameraflug
  im Zeitraffer auf allen Formen, Flacker-Messung; `window.__opt = { kinds, seconds, parts: ['tour', 'flicker'] }`;
  dauert ≈ 2 min → starten, dann mit `wait` warten), `run-fq.js` (Kurztest in Echtzeit auf allen Stufen: FPS, GPU-Zeit,
  Standbild, ungültige Werte; `window.__opt = { kinds, levels }` – nach jeder Änderung laufen lassen).
  Alte Fassung zum Vergleich: `.claude/pre-fly.html`.
