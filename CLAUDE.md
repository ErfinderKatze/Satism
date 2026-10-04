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
- Mit EINEM Modus (Fluid) anfangen, später Partikel und Mandelbrot ergänzen.
- Jede Eingabe muss innerhalb eines Frames sichtbar werden. Bewegungen und Parameteränderungen immer weich
  interpolieren (Easing, Trägheit).
- FPS-Zähler und einstellbare Qualitätsstufe (Auflösung, Partikelzahl) für schwächere Geräte.
- Option, schnelles Blinken/Flackern zu reduzieren.
- Git: Commits mit Autor `ErfinderJojo <erfinder-jojo@posteo.de>` (lokal im Repo konfiguriert).

## Ideensammlung (für später – nicht alles auf einmal!)
**Fluid:** Farbe mit der Maus malen, die verwirbelt (Stable Fluids nach Jos Stam). Regler für Viskosität,
Wirbelstärke, Schwerkraft, Verblassen. Hindernisse zeichnen, um die die Flüssigkeit herumfließt.

**Partikel:** Anziehung/Abstoßung durch die Maus. Kräfte wie schwarze Löcher, Magnete, Wind, Orbits.
Schwarmverhalten, Trails und Glow. Explosionen bei Klick.

**Mandelbrot:** Endloser Zoom per Scrollen/Ziehen, Julia-Sets live mit Mausposition, animierte Farbpaletten,
automatische Zoom-Fahrt zu schönen Stellen. (Float32 pixelt ab ca. 1e5–1e6-fach – für tiefen Zoom später Tricks nötig.)

**Modusübergreifend:** Paletten-Presets (Neon, Sunset, Ozean, Lava …) mit sanftem Überblenden. Presets/Szenarien
speichern und teilen. Idle-Modus/Screensaver. Screenshot-, Wallpaper- und Video-Export. Optional kleine Sammelziele
(„entdecke 10 Muster“).

**Satisfying-Faktoren:** Audio-Feedback per Web Audio API (selbst synthetisiert, Pentatonik, Lautstärke/Tonhöhe abhängig
von Geschwindigkeit, Zoomtiefe, Partikelzahl). Lofi-Musik (lizenzfrei oder generativ: Akkorde, Vinyl-Knistern, sanfte
Drums, reagiert auf Interaktion). Wenig UI: minimalistisches, ausblendbares Panel oder Radialmenü. Bloom/Glow,
dunkler Hintergrund, kontrastreiche Paletten.

## Aktueller Stand
- Alles in **einer Datei**: `index.html` (HTML, CSS, JavaScript, GLSL-Shader). Öffnen per Doppelklick im Browser.
- Fluid-Modus nach Stable Fluids auf der GPU (WebGL2 + `EXT_color_buffer_float`): Vorticity Confinement (Wirbel),
  Viskosität (Jacobi-Diffusion), Druck-Lösung (Jacobi), Gradienten-Subtraktion, Advektion.
- Farbe wird als „Dichte + Position auf der Palette“ gespeichert (R = Dichte, G/B = Dichte·cos/sin des Palettenwinkels);
  erst beim Anzeigen wird über die aktive Palette eingefärbt. Dadurch blendet ein Palettenwechsel das ganze Bild sanft um.
- Ausblendbares Einstellungs-Panel (Zahnrad oben rechts bzw. Taste `H`): Regler für Pinselgröße (30–300 %, wirkt nur auf
  das eigene Malen, nicht auf Auto-Play; Pinsel-Ring zeigt die echte Größe, beim Ziehen Vorschau-Ring in der Bildmitte),
  Viskosität, Wirbelstärke, Verblassen
  (Doppelklick = Standardwert); Paletten Neon, Sunset, Ozean, Lava. Reglerwerte und Paletten werden weich interpoliert,
  die Akzentfarben der Oberfläche folgen der aktiven Palette.
- Qualität als Regler mit 6 Stufen: Niedrig/Mittel/Hoch/Ultra/**Extrem**/**Maximum** (Extrem/Maximum = Supersampling der
  Farbe bis 1,5×/2× Bildschirmauflösung, Strömungsraster bis 512, bis 70 Druck-Iterationen). Schalter „Automatisch anpassen“:
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
  sofort, Schalter „Bei Inaktivität starten“ im Panel.
- Bedienung: Maus bewegen = malen, Klick = Farbklecks, Leertaste = leeren, `H` = Panel, `F` = FPS, `Q` = eine Qualitätsstufe höher (schaltet Auto ab), `A` = Auto-Play.
- Noch nicht umgesetzt: Schwerkraft, Hindernisse, Flacker-Reduktion, Audio, weitere Modi.
