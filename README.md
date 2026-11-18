# URBAN ANALYST

Städtebauliche Standortanalyse im Browser – Uni-Projekt (Jade Hochschule, WPK Vibecoding).

Gebiet wählen, Bausteine laden (Gebäude, Straßen, Grün, Wasser, ÖPNV, Bäume, Flächennutzung, Sonnenbahn, Schatten, Flurstücke, Bevölkerung, Hochwasser, Verkehrslärm, Höhenlinien, Hangneigung) und als **SVG, PDF oder DXF** exportieren.

## Starten

`index.html` herunterladen und per Doppelklick im Browser öffnen. Keine Installation, keine Anmeldung, keine API-Keys.

## Daten

- © OpenStreetMap-Mitwirkende (ODbL) – über die Overpass-API
- Berlin: Geoportal Berlin (Umweltatlas, ALKIS, Baumkataster, Gebäudehöhen)
- Niedersachsen: LGLN OpenGeoData (LoD2-Gebäude, ALKIS-Flurstücke, DGM1), CC BY 4.0
- Zensus 2022 (Statistische Ämter des Bundes und der Länder), Hochwassergefahrenkarten der Länder (BfG), Lärmkartierung 2022 (Umweltbundesamt)

Fehlende Werte erscheinen als „unbekannt“, geschätzte Werte sind als „geschätzt“ gekennzeichnet.

## Ordner

- `index.html` – die App (HTML/CSS/JS, MapLibre, turf, JSZip per CDN)
- `CLAUDE.md` – Regeln und Technik
- `PLAN.md` – Plan, Stand, getestete Schritte
- `versionen/` – Sicherungen aller Zwischenstände
