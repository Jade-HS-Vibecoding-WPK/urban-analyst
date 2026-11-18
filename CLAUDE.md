# CLAUDE.md – Projektgedächtnis QUAVA (früher URBAN ANALYST)

## Ziel
Web-App für städtebauliche Bestandsanalyse: Stadtausschnitt wählen → OpenStreetMap-Daten laden →
thematische Analyse-Layer → Export für Illustrator (SVG/PDF) und CAD (DXF).
Was gebaut wird und der aktuelle Stand stehen in **PLAN.md**. Lies PLAN.md zu Beginn jeder Sitzung.

## Über mich
- Ich studiere Architektur und kann nicht programmieren. **Erklär jeden Schritt einfach**, ohne Fachjargon.
- Sag mir nach jedem Feature genau, **wie ich es teste** (was klicke ich, was sollte ich sehen).
- Mein Laptop: Windows, HP, nicht sehr leistungsstark. Ich habe QGIS und Illustrator.
- Kurs: Vibecoding KI-Werkstatt, Jade Hochschule. Abgabe Fr 20.11., 16 Uhr (GitHub + README + Poster).

## Regeln
- **Ein Feature pro Sitzung.** Klein anfangen. Nur das bauen, was in PLAN.md als nächster Schritt steht.
- Nach jedem Feature: mich testen lassen → Commit → Stand in PLAN.md aktualisieren.
- **Nichts vortäuschen:** Keine Knöpfe ohne Funktion, keine Platzhalter, die nur echt aussehen.
- **Keine Daten erfinden:** Fehlt eine Angabe in OSM (z. B. Gebäudehöhe), steht „unbekannt“ da.
  Geschätzte Werte (z. B. Höhe = Geschosse × 3 m) werden sichtbar als „geschätzt“ markiert.
- **Keine API-Keys** im Code, in Chats oder auf GitHub.
- **Quellenangabe:** „© OpenStreetMap-Mitwirkende (ODbL)“ auf der Karte und in jedem Export.
- Arbeite nur in diesem Projektordner.

## Technik (bewusst einfach)
- Nur **HTML, CSS und JavaScript**. Keine Installation, kein Build-Tool, kein Node, kein Python.
- Die App muss **per Doppelklick auf `index.html`** im Browser laufen (Edge/Chrome) und später auf **GitHub Pages**.
  Deshalb: normale `<script src="…">`-Dateien, **keine ES-Module** (`type="module"` geht bei Doppelklick nicht).
- Bibliotheken nur per CDN-Link:
  - Karte: MapLibre GL JS 4.7.1 (`https://unpkg.com/maplibre-gl@4.7.1/dist/maplibre-gl.js` + `.css`)
  - Hintergrundkarte: CARTO Dark Matter `https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json`
    (hell: `positron-gl-style`), kein Schlüssel nötig
- Datenquellen (kostenlos, ohne Key):
  - OSM-Daten: Overpass API `https://overpass-api.de/api/interpreter` (POST, `[out:json]`, `out geom;`),
    Ersatzserver `https://overpass.private.coffee/api/interpreter`
  - Ortssuche: Nominatim `https://nominatim.openstreetmap.org/search?format=jsonv2&countrycodes=de&q=…`
- **Nicht** `tile.openstreetmap.org` als Hintergrund benutzen: wird bei lokal geöffneter Datei blockiert (403 „Access blocked“).
- Eigene Karten-Layer immer **über allen Flächen/Linien** der Hintergrundkarte einfügen (nicht vor dem ersten Beschriftungs-Layer). Kartenwechsel nur mit `setStyle(…, {diff:false})` und eigenem Merkzeichen `styleReady`.
- Pläne in Metern: Projektion UTM Zone 32/33 (ETRS89), Berlin = Zone 33.
- Gebiete am Anfang klein halten (unter ca. 5 km²), damit der Laptop nicht überlastet.

## Projektstruktur
```
urban-analyst/
├─ CLAUDE.md     ← diese Datei (Regeln)
├─ PLAN.md       ← was wir bauen + Stand + Bugs
├─ README.md     ← kommt am Donnerstag
└─ index.html    ← die ganze App in einer Datei (Version 1)
```
Aufbau von `index.html` (von oben nach unten):
1. `<style>` – Aussehen (Farben als CSS-Variablen, Dark/Light)
2. HTML – linke Leiste, Karte, rechte Leiste, Export-Dialog
3. erstes `<script>` – **Kernlogik `UA`**: OSM → GeoJSON, Overpass-Abfragen (`FETCHES`), Klassen & Farben (`CL`),
   Klassifizierung, Statistik, Auftrag verstehen (`parseCommand`), SVG- und DXF-Export, UTM
4. zweites `<script>` – **Oberfläche**: Karte, Zeichnen, Suche, Analyse starten, Layer-Panel, Legende, Statistik, Export
Wir bauen an dieser Datei weiter. Ändere nur die Stellen, die das aktuelle Feature/den aktuellen Bug betreffen.

## Gestaltung
- Vorbild: **Aino Site Analyst**. Modern, minimalistisch, professionell, nicht wie eine GIS-Verwaltungssoftware.
- **Dark Mode** als Standard. Hintergrund fast schwarz (#0f0e13), Panels #17161d, eine Akzentfarbe Violett (#8b5cf6).
- Schrift: Inter. Viel Luft, abgerundete Ecken, dezente Linien.
- Die **Karte ist das Hauptelement**. Ein Hauptbutton pro Bereich.
- Plan-Farben orientieren sich an meinen Diagnose-Plänen: Wohnen gold (#E2B33C), Gewerbe rosa,
  Industrie braun, Grün in mehreren Grüntönen, Wasser hellblau, Straßen hell nach Hierarchie.

## Nächste Sitzung (Prompt zum Kopieren)
> Lies CLAUDE.md und PLAN.md. Heute testen wir den Export (SVG für Illustrator, DXF für CAD, PDF) mit echten Daten.
> Ich beschreibe dir, was beim Öffnen in Illustrator/CAD passiert. Behebe danach einen Fehler nach dem anderen,
> erklär mir jeden Schritt einfach und trage den Stand in PLAN.md ein.
