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
  erst beim Anzeigen wird eingefärbt – durch den aktiven **Look** (siehe unten). Dadurch blendet ein Palettenwechsel
  das ganze Bild sanft um.
- Looks (Farbdarstellungen): **Palette**, **Regenbogen**, **Geschwindigkeit**, **Wirbel**, **Feuer / Glut** – wählbar im
  Panel-Abschnitt „Look“ oder mit `1`–`9` (Details im Abschnitt „Look-System“ unten).
- **Bloom (Glow)** als Nachbearbeitungs-Schritt nach dem Look – funktioniert mit allen Looks (Details im Abschnitt
  „Bloom“ unten). Panel-Abschnitt „Bloom“: Schalter „Glow“, Regler Bloom-Intensität/-Schwelle/-Weichheit.
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
- Bedienung: Maus bewegen = malen, Klick = Farbklecks, Leertaste = leeren, `H` = Panel, `F` = FPS, `Q` = eine Qualitätsstufe höher (schaltet Auto ab), `A` = Auto-Play, `1`–`9` = Look wählen.
- Noch nicht umgesetzt: Schwerkraft, Hindernisse, Flacker-Reduktion, Audio, weitere Modi, weitere Looks (siehe unten).

## Bloom (Nachbearbeitung / Post-Processing)
- Reihenfolge pro Frame: Simulation (`step`) → Look → **Bloom** → Bildschirm. Der Bloom verändert die Simulation nicht und
  arbeitet nur mit dem fertigen Bild des Looks, daher funktioniert er automatisch mit allen (auch zukünftigen) Looks.
- Ablauf (`render()` / `applyBloom()`): Look zeichnet in die Szenen-Textur `scene` (volle Auflösung) statt direkt auf den
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
  (`index.html`): `{ name, usesPalette?, params?, smoothCurl?, glsl }`. `glsl` enthält genau eine Funktion
  `vec3 look(LookInput L)` (darf eigene Hilfsfunktionen davor definieren).
- `LookInput`: `L.uv` (Bildposition 0..1), `L.density` (Farbmenge), `L.t` (Palettenposition 0..1), `L.dye` (Rohdaten).
  Gemeinsame Hilfen im `lookHeader`: `palette(t)`, `hsv2rgb(hsv)`, `brightness(density)`, `dyeColor(L)` (eingemalte
  Farbe wie im Look „Palette“), `uTime`, `speedAt(uv)` (Tempo), `curlAt(uv)` (rohe Drehung, ±),
  `curlSmoothAt(uv)` (geglättete Drehung). `lookMain` liest die Farb-Textur und ruft `look()` auf.
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
- Auswahl: Abschnitt „Look“ im Panel (Knöpfe werden automatisch aus `LOOKS` erzeugt) und Zifferntasten `1`–`9`.
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
- Geplant (nacheinander einbauen): Metallic, Glas/Kristall, Wasser, Seifenblase/Ölfilm, Tinte & Aquarell,
  Marmorpapier (Ebru), Galaxie/Nebel/Aurora.
  Hinweis: Mehr als 9 Looks → Tasten reichen nur bis 9, die Knöpfe im Panel funktionieren für alle.
