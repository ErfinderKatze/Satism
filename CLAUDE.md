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
- Looks (Farbdarstellungen): **Palette** (1), **Regenbogen** (2), **Geschwindigkeit** (3), **Wirbel** (4), **Feuer / Glut** (5),
  **Metallic** (6), **Glas / Kristall** (7), **Wasser** (8), **Oberfläche (Test)** (9) – wählbar im Panel-Abschnitt „Look“
  oder mit den Zifferntasten (Details im Abschnitt „Look-System“ unten). Alle 9 Tasten sind damit belegt.
- **Oberflächen-Baustein** (Höhenfeld + Neigung) für Metallic/Glas/Wasser/Ölfilm ist fertig, darauf aufbauend Metallic,
  Glas / Kristall und Wasser.
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
  (`index.html`): `{ name, usesPalette?, params?, smoothCurl?, surface?, surfaceBlur?, foam?, glsl }`. `glsl` enthält genau eine Funktion
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
- **Spiegelnde Oberflächen – gemeinsame Hilfen im `lookHeader`** (von Metallic und Glas genutzt, nicht kopieren):
  `softbox(...)`, `studio(r, soft)` (Studio-Umgebung, dreht mit `uEnvAngle`), `fresnelSchlick(f0, cosT)`,
  `studioSpecular(n, gloss)` (Glanzlicht Lampe oben links).
- **Weiches Rauschen – gemeinsamer Baustein `noiseGLSL`** (im `lookHeader` und im Schaum-Shader eingebunden): `hash(p)`,
  `noise(p)` („Value Noise“, 0..1). Genutzt von Feuer, Wasser und dem Schaum-Puffer.
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
  blendet weich über; Standard Chrom), **Wölbung** (geteilter Regler `bump`, auch im Test-Look), **Glanz** 0–100 %
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
- **Oberfläche (Test)** (Taste `9`): Prüf-Look für den Oberflächen-Baustein. Zeigt die Normale als Farben (Normal-Map-Stil:
  Neigung nach rechts = Rot, nach oben = Grün, flach = Lila-Blau) mit leichter Schattierung durch ein festes Licht;
  Bereiche ohne Farbe schwarz. Vorläufige Regler (`params: ['bump', 'saturation']`, später entfernen oder in Metallic
  übernehmen): **Wölbung** 0–4× (`uBump`, Standard 1×) und **Sättigung** 0,3–6 (k in der Höhenformel, Standard 2).
- Geplant (nacheinander einbauen): Seifenblase/Ölfilm, Tinte & Aquarell, Marmorpapier (Ebru), Galaxie/Nebel/Aurora.
  Achtung: Die Zifferntasten `1`–`9` sind jetzt alle belegt – weitere Looks sind nur noch über die Knöpfe im Panel wählbar
  (oder der Test-Look wird entfernt/ans Ende geschoben).

## Schaum-Puffer (Look „Wasser“, mitgetragen)
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
  1. `surfaceHeight`: Höhe = `1 − exp(−Dichte · Sättigung)` (weich gesättigt), 4 Messpunkte gemittelt. Die Dichte kommt aus
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
  `bindSurface(u, unit)`): `heightAt(uv)` (0..1) und `surfaceNormal(uv, strength)` – zentrale Differenzen zu den
  Nachbarpunkten im Abstand 1,5 × Blur-Schritt (`uSurfaceStep`), seitenverhältnis-korrigiert (`uAspect`),
  `normalize(vec3(−Steigung · strength · 0,12, 1))`. `strength` ist Parameter, damit jeder Look seine eigene Wölbung nutzt.
- Gemessen (674×1322 px, Höhenfeld in voller Auflösung, Stufe Maximum): Baustein ≈ 0,46 ms GPU-Zeit pro Frame, Test-Look
  ≈ 0,1 ms. Grob hochgerechnet ≈ 2 ms bei 2560×1440 auf Ultra+. Wird es zu teuer: Stufe „Hoch“ rechnet das Höhenfeld in
  halber Auflösung (≈ ¼ der Kosten) und sieht durch die Glättung fast gleich aus.
  Hinweis: Mehr als 9 Looks → Tasten reichen nur bis 9, die Knöpfe im Panel funktionieren für alle.
