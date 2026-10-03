# Fluid-Simulation (Satisim)

## Ziel des Projekts
Eine kleine, eigenständige Web-App, die eine interaktive Flüssigkeits-Simulation mit WebGL im Browser zeigt.
Wenn man mit der Maus (oder dem Finger) über das Fenster fährt, wird bunte Farbe in die Flüssigkeit gemalt,
die sich mit der Strömung bewegt und verwirbelt.

## Rahmenbedingungen
- Alles steckt in **einer einzigen Datei**: `index.html` (HTML, CSS, JavaScript und GLSL-Shader).
- **Kein Framework**, keine Build-Tools, keine externen Abhängigkeiten – die Datei lässt sich per Doppelklick im Browser öffnen.
- Benötigt einen Browser mit WebGL2 und der Erweiterung `EXT_color_buffer_float` (aktuelle Versionen von Chrome, Edge, Firefox, Safari).

## Aufbau (kurz)
- Simulation nach dem „Stable Fluids“-Verfahren auf der GPU: Advektion, Wirbelverstärkung (Vorticity Confinement),
  Druck-Lösung (Jacobi-Iteration) und Gradienten-Subtraktion.
- Parameter zum Anpassen (Verblassen, Wirbelstärke, Pinselgröße …) stehen im `CONFIG`-Objekt oben im Skript.
- Bedienung: Maus bewegen = malen, Klicken = Farbklecks, Leertaste = alles leeren.
