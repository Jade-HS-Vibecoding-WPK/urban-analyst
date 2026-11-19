# PLAN – QUAVA (früher URBAN ANALYST)

## Die Idee in einem Satz
QUAVA lädt für einen frei gewählten Stadtausschnitt in Deutschland automatisch Geodaten aus OpenStreetMap, sortiert sie in thematische Analyse-Layer (Gebäude, Grün, Wasser, Verkehr) und exportiert sie als Plan, den man in Illustrator oder CAD weiterbearbeiten kann.

## Für wen?
Für Architektur- und Stadtplanungsstudierende, die eine städtebauliche Bestandsanalyse machen
(Schwarzplan, Freiraum, Erschließung, Nutzung). Statt 2 Stunden in QGIS mit QuickOSM: 2 Minuten im Browser.

## Ein typischer Ablauf
1. App öffnen → Karte von Berlin (dunkel).
2. Ort suchen (z. B. „Kreuzberg“) oder ein Rechteck auf der Karte zeichnen.
3. „Analyse starten“ → Gebäude, Straßen, Grün und Wasser erscheinen als eigene Layer.
4. Layer ein-/ausschalten, Farben anpassen, Legende ansehen.
5. Export als SVG/PDF (Illustrator) oder DXF (CAD).

---

## MoSCoW – was muss am Freitag laufen?

### MUST (läuft am Freitag, sonst ist das Projekt nicht fertig)
- [x] **M1 Karte**: große interaktive Karte im Dark Mode, Start in Berlin, Zoom & Verschieben
- [x] **M2 Layout**: Oberfläche wie Aino – linke Leiste (Gebiet, Analyse), Karte in der Mitte, rechte Leiste (Layer, Legende)
- [x] **M3 Ortssuche**: Stadt/Bezirk/Adresse in Deutschland suchen und hinzoomen
- [x] **M4 Gebiet wählen**: Rechteck auf der Karte zeichnen = Untersuchungsgebiet (Fläche in ha/km² anzeigen)
- [x] **M5 Gebäude laden**: Gebäude im Gebiet aus OpenStreetMap laden und als Layer zeigen (Schwarzplan)
- [x] **M6 Weitere Layer**: Straßen (nach Hierarchie), Grünflächen (nach Typ), Wasser, Bahn
- [x] **M7 Layer-Panel + Legende**: jeder Layer ein/aus, Farbe pro Klasse änderbar, Legende
- [x] **M8 Export Illustrator**: SVG mit getrennten Ebenen, im Maßstab (z. B. 1:10.000), mit Legende, Nordpfeil, Maßstabsbalken, OSM-Quellenangabe; PDF über den Druckdialog
- [x] **M9 Export CAD**: DXF in Metern, ein CAD-Layer pro Klasse
- [ ] **M10 Veröffentlichen**: Projekt auf GitHub (Kurs-Organisation), GitHub Pages als Website, README

### SHOULD (wäre gut)
- [x] S1 Gebäudenutzung (Wohnen, Gewerbe, Industrie, Öffentlich …) – fehlende Angaben als „unbekannt“ markieren
- [x] S2 Gebäudehöhen – Herkunft kennzeichnen: OSM-Angabe / geschätzt aus Geschossen / unbekannt
- [x] S3 Statistik: Flächenanteile im Gebiet (Überbauungsgrad, Grünanteil, Straßenlänge)
- [x] S4 Klick auf Element → Infos (Name, Nutzung, Höhe, OSM-Link)
- [x] S5 Polygon statt nur Rechteck zeichnen; Bezirk/Ortsteil aus der Suche direkt als Gebiet übernehmen
- [x] S6 Flächennutzung (Wohnbau-, Gewerbe-, Industrie-, Militärflächen)

### COULD (wenn Zeit bleibt)
- [x] C1 ÖPNV-Haltestellen mit Einzugsradien (300 / 600 m)
- [x] C2 Bäume, Bezirks- und Ortsteilgrenzen
- [x] C3 Analyseauftrag als Text („Erstelle Pläne für Nutzung und Grün“) – erst Schlagworte, später KI
- [x] C4 GeoJSON-Export für QGIS, Projekt speichern/öffnen
- [x] C5 3D-Ansicht der Gebäudehöhen
- [ ] C6 Bebauungstypen (Blockrand, Zeile, Solitär)

### WON'T (diese Woche nicht – bewusst später)
- Lärm, Hitze, Starkregen, Hochwasser, Einkommen (brauchen andere Datenquellen, z. B. Umweltatlas Berlin)
- QGIS-Projektdatei (.qgz), GeoPackage
- Eigener Server / Datenbank

---

## Etappen (an die Kurstage gekoppelt)

| Tag | Etappe | Features | Fertig, wenn … |
|---|---|---|---|
| **Mo 16.11.** | Idee & Plan + Praxistest | PLAN.md, CLAUDE.md, Test Version 1 | Testliste durchgegangen, Bugs notiert |
| **Di 17.11.** | Bugs & Aussehen | Bugs beheben, Design an Aino/Diagnose-Pläne angleichen | Alles aus der Testliste läuft |
| **Mi 18.11.** | Daten | Pläne wie meine Diagnose-Pläne (Beschriftung, Symbole, Schraffuren), evtl. C6 | Export sieht aus wie ein fertiger Analyseplan |
| **Do 19.11.** | Fertig & veröffentlichen | M8, M9, M10 | SVG öffnet sich in Illustrator mit Ebenen, DXF im CAD, Website-Link läuft. **12 Uhr Freeze**, dann Poster |
| **Fr 20.11.** | Polieren & präsentieren | README, Poster, Bugs | Abgabe 16 Uhr |

**Rhythmus pro Feature:** neue Sitzung (`/clear`) → ein Feature bauen → testen → Commit → Stand hier in PLAN.md eintragen.

---

## Stand
- **16.11. vormittags:** Erster Entwurf (Version 1) gebaut. Er steckt komplett in `index.html`.
  Abgehakt [x] = im Entwurf vorhanden und mit Testdaten geprüft, **aber noch nicht mit echten OSM-Daten getestet**.
- **16.11. mittags:** Entscheidung: Wir bauen am ersten Entwurf weiter (statt neu anzufangen).
- **16.11. nachmittags – Version 2:**
  - Hintergrundkarte = echte **OpenStreetMap-Karte** (wie osm.org), zusätzlich OSM dunkel, basemap.de (amtlich), Luftbild, minimal hell/dunkel.
    Google Maps darf man ohne Google-Vertrag und -Schlüssel nicht einbinden, deshalb ist es nicht dabei.
  - **Layer teilen wie in QGIS**: Jeder Layer hat „Aufteilen nach“ (Gebäudetyp detailliert, Nutzung, Höhe, Geschosse, Einheitlich oder jedes OSM-Attribut).
    Klassen lassen sich einzeln ein- und ausblenden, umbenennen, umfärben, zusammenführen und entfernen. Layer duplizieren.
  - **Bausteine** laden jetzt nur Rohdaten (Gebäude, Straßen, Bahn, Grün, Wasser, Flächennutzung, ÖPNV, Bäume, Grenzen) statt fertiger Analysen.
  - **Detail-Abfrage wie QuickOSM**: Schlüssel/Wert-Zeilen mit UND/ODER, Vorschläge, „Vorherige Abfragen“.
  - **Großes Auftragsfeld** (⤢), erkennt auch Kirchen, Hotels, Schulen, Kitas, Ärzte, Supermärkte, Spielplätze …
  - **Ansichten speichern** und per Klick wieder aufrufen. Modus **„Aktuelle Kartenansicht“** lädt nur, was gerade zu sehen ist.
  - Ausgeblendete Klassen werden nicht exportiert.
  - ÖPNV-Einzugsradien gibt es jetzt per Knopf am Haltestellen-Layer.
  - Getestet: 16 Kerntests + Oberflächentest mit Testdaten.
- **16.11. Praxistest:** Echte OSM-Daten laden in Berlin-Mitte (1.902 Gebäude, 6.348 Wege). Die OSM-Standardkarte wird bei lokal geöffneter Datei blockiert („Access blocked“).
- **16.11. Version 3:**
  - Auftragsfeld steht fest unten, nur Bausteine und Verlauf scrollen.
  - Detail-Abfrage öffnet sich über **+** neben „Auftrag in eigenen Worten“ als Fenster über der Karte.
  - Layer und Untergruppen werden per **Maus gezogen** (⋮⋮), statt mit Pfeilen. Reihenfolge gilt auch für Karte und SVG-Export.
  - **Papierkorb** bei Layern und Untergruppen, mit „Rückgängig“ im Verlauf.
  - **Laden abbrechen** über einen Knopf in der Ladeanzeige.
  - OSM-Karten (blockiert) entfernt. Neu: „Karte farbig“ (CARTO Voyager). Standard: „Karte dunkel“.
- **16.11. Version 3.1:** basemap.de funktioniert (getestet). Laden ist jetzt **Baustein für Baustein**: Jeder fertige Layer erscheint sofort.
  Schlägt einer fehl, laufen die anderen weiter (automatisch 1 neuer Versuch). Am Ende gibt es „↻ Fehlgeschlagene erneut laden“.
  Projektordner ist mit Claude verbunden: Updates landen direkt in `Desktop\urban-analyst`.
- **16.11. Version 3.2:** „Gebiet“ und „Bausteine“ lassen sich einklappen (wird gemerkt, eingeklappt steht eine Kurzinfo daneben).
  Bausteine haben **Gruppen-Tabs**: Grundauswahl · Gebäude · Verkehr · Grün & Freiraum · Wasser · Nutzung & Einrichtungen (insgesamt 60 Bausteine,
  z. B. nur Kirchen, nur Hauptverkehrsstraßen, nur Parks, Schulen & Kitas, Gastronomie). Teilmengen nutzen die schon geladenen Daten: kein Doppel-Download.

- **16.11. Version 3.5:** Ausführliche **Ladeanzeige**: welcher Baustein (Schritt x von y), Quelle (OpenStreetMap · Overpass-API · welcher Server),
  was gerade passiert (Server sucht / empfange X MB / wandle Objekte um / zeichne Layer), Laufzeit, Fortschrittsbalken, Serverwechsel bei Überlastung.

## Tagesabschluss Mo 16.11.
- Aktuelle Version: **3.5** (`index.html`), Sicherung: `versionen/urban-analyst-v3.5_2026-11-16.html`.
- Getestet mit echten OSM-Daten in Berlin-Mitte: Laden, Kartenwechsel, Ladeanzeige, Abbrechen.
- Noch **nicht** mit echten Daten getestet: Export SVG → Illustrator, DXF → CAD, PDF.

## Di 17.11. – Planänderung
Export-Test verschoben. Heute zuerst die **Daten** verbessern, Schritt für Schritt (vorher immer fragen).
Bewusst so lassen: Gebäude dürfen über das Gebiet hinausragen; bei mehreren Gebäude-Layern ist nur einer sichtbar (Rest per Layer-Panel umschalten).

- [x] **1. Auftragsfeld versteht Wörter genau** (Version 3.6, getestet und ok):
  Erst genaue Wörter erkennen und ganz aus dem Satz streichen, dann allgemeine Wörter.
  „Straßenbahn“ → nur Straßenbahn · „Parkplätze“ → nur Parkplätze (keine Parks) · „Parks“ → nur Parks ·
  „Autobahn“ → Hauptverkehrsstraßen · „Hochschule“ ≠ Schule · Flughafen/Baumarkt/Gründerzeit lösen nichts Falsches mehr aus.
  „Wohngebäude nach Höhe“ → nur Wohngebäude, aufgeteilt nach Höhe. 54 Beispielsätze geprüft.
  Sicherung vorher: `versionen/urban-analyst-v3.5_vor-auftragsfeld_2026-11-17.html`
- [x] **2. Achsen** (Version 3.7, getestet und ok): Bisherige Darstellung bleibt unverändert. Zusätzliche Aufteilung im Layer-Panel:
  „Hierarchie – Achsen“ (Straßen), „Bahnart – Achsen“ (Bahn), „Gewässertyp – Achsen“ (nur Wasser-Linien; Flächen bleiben).
  Gleiche Untergruppen und Farben, Linien immer 1,5 px, im SVG 0,15 mm. Baumreihen unverändert.
  Sicherung vorher: `versionen/urban-analyst-v3.6_vor-achsen_2026-11-17.html`
- [x] **2b. Fahrbahnbreiten** (Versionen 3.8–3.11, getestet und ok) – Möglichkeit A (OSM, überall in Deutschland), nur Fahrbahnen (wo Fahrzeuge fahren):
  Breite aus OSM (`width:carriageway` / `width`), sonst geschätzt aus Fahrspuren × Spurbreite (3,5 / 3,25 / 3,0 / 2,75 m),
  sonst geschätzte Standardbreite (Haupt 7 m · 2. Haupt 6,5 · Sammel 6 · Neben 5,5 · Zufahrt 3,5; Einbahn schmaler). Unplausible Werte (< 2 m, > 50 m) werden ignoriert.
  Herkunft sichtbar: Tab „Element“, Tab „Statistik“ (Datenlage in %), SVG-Planlayout. Fuß-, Rad-, Wirtschaftswege bleiben dünne Achsen.
  Drei Varianten unter „Aufteilen nach“:
  - „Fahrbahnen – Flächen (weiche Übergänge)“: Flächen, Trichter zur schmaleren Anschlussbreite (6–25 m), keine überstehenden Kreise, freie Enden gerade, Deckkraft 100 %
  - „Fahrbahnen – dicke Linien (runde Enden)“: alte Darstellung
  - „Fahrbahnen – nur Außenlinien“: nur Fahrbahnränder (1,5 px / SVG 0,15 mm), Einmündungen offen; an Zufahrten (Servicestraßen) läuft der Rand durch
  SVG: Flächen bzw. Linien im Maßstab. DXF: Mittellinie mit Polylinienbreite (ohne Trichter, noch nicht im CAD geprüft).
  Auftragsfeld: „Fahrbahnen“, „Straßenbreiten“, „Fahrbahnbreite“; Baustein „Fahrbahnen (echte Breite, Flächen)“ im Tab Verkehr.
  Sicherungen: `versionen/urban-analyst-v3.7_vor-fahrbahnbreiten…` bis `…v3.10_vor-zufahrten-schliessen…`
- [x] **3. Neue Höhenklassen** (Version 3.12, getestet und ok): bis 7 m · 7–13 · 13–20 · 20–25 · 25–30 · über 30 m · unbekannt.
  Grenzwert gehört zur unteren Klasse. Farben hell (sand) → dunkel (rotbraun), unbekannt grau.
  Sicherung vorher: `versionen/urban-analyst-v3.11_vor-hoehenklassen_2026-11-17.html`
- [x] **4. Gebäudenutzung aus Nutzungs-Punkten** (Versionen 3.13–3.14, getestet und ok):
  Beim Laden von Gebäuden werden im Hintergrund Flächennutzung + alle Nutzungs-Punkte (Läden, Gastronomie, Büros, Praxen, Kitas, Schulen,
  Behörden, Kultur, Sport, Hotels, Handwerk, Leerstand) geladen. Punkte werden NICHT gezeichnet, nur dem Gebäude zugeordnet, in dem sie liegen.
  - „Nutzung (Gruppen)“ neu: Wohnen mit Gewerbe/Gastronomie im EG · Wohnen mit Büro/Praxis · Büro & Verwaltung · Mischnutzung (sonstige)
  - Wohnen in den Obergeschossen wird angenommen bei: Gebäude ohne Typ, ≥ 3 Geschosse, in Wohnbaufläche, Nutzungen nur unten (sichtbar markiert)
  - Neue Aufteilung „Erdgeschossnutzung“ (inkl. Leerstand, Mehrere Nutzungen); Baustein im Tab Gebäude; Auftrag „Erdgeschossnutzung“, „Mischnutzung“
  - „Gebäudetyp“: Gebäude ohne Typ heißen z. B. „Wohn- und Geschäftshaus“, „Gastronomie“, „Praxen / Gesundheit“ (abgeleitet)
  - Eigene klare Gebäudeangabe (Kirche, Schule …) hat Vorrang. Tab „Element“: Liste der Nutzungen im Gebäude. Tab „Statistik“: Datenlage Nutzung in %.
  - Ladeanzeige zeigt nur die gewählten Bausteine; Hilfsdaten laden unsichtbar als Teil von „Gebäude“ mit (Hinweis, falls nicht erreichbar).
  Sicherungen: `versionen/urban-analyst-v3.12_vor-nutzung-aus-punkten…`, `…v3.13_vor-ladeanzeige…`, Stand danach: `…v3.14_2026-11-17.html`
- [x] **5. Amtliche Gebäudehöhen Berlin** (Version 3.15, getestet und ok): automatisch, ohne Knopf. Liegt das Gebiet in Berlin, holt die App beim
  Laden der Gebäude unsichtbar die Höhen + Geschosszahlen vom Geoportal Berlin (WFS `ua_gebaeudehoehen`, Umweltatlas, aus LoD2/Laserscan).
  Amtliche Umrisse werden nicht gezeichnet; jedes OSM-Gebäude bekommt die größte Höhe der amtlichen Teile an seiner Stelle.
  Reihenfolge Höhe: amtlich gemessen > OSM height > Geschosse × 3 m (auch amtliche Geschosse) > unbekannt. Quelle in Element, Statistik, SVG.
  Geprüft: NRW-Dienst blockiert Browser-Abfragen, Brandenburg nur komplexes INSPIRE-Format → außerhalb Berlins wie bisher.
  Sicherung vorher: `versionen/urban-analyst-v3.14_vor-berlin-hoehen…`, Stand danach: `…v3.15_2026-11-17.html`
- [ ] Danach: Export testen (SVG/DXF/PDF)

- [x] **6. Berliner Baumkataster** (Version 3.16, getestet und ok): Baustein „Bäume & Baumkronen“. In Berlin werden unsichtbar alle Straßen- und
  Anlagenbäume (Geoportal Berlin, WFS `baumbestand`) geladen. Kronen als Kreis in echter Größe (Kataster `kronedurch`, sonst OSM `diameter_crown`),
  ohne Angabe Punkt. OSM-Bäume ≤ 3 m neben Katasterbaum werden weggelassen. Klassen: Laub/Nadel/unbekannt/Baumreihe; Attribute Gattung, Art, Höhe, Pflanzjahr.
  Element-Steckbrief, Kronenfläche in Statistik, Quelle im SVG. Sicherung vorher: `versionen/urban-analyst-v3.15_vor-baumkataster…`
- [x] **6b. Vorrang Baumkataster in Berlin** (Versionen 3.17–3.18): Ist das Kataster geladen, werden ALLE OSM-Bäume und -Baumreihen ignoriert.
  Außerhalb Berlins bzw. wenn das Kataster nicht erreichbar ist: OSM-Bäume. (Test durch Nutzerin steht noch aus.)
- Wilhelmshaven (17.11.): kein öffentliches Baumkataster gefunden; Kataster-WFS Niedersachsen ohne Geschosse/Höhen;
  gemessene LoD1/LoD2 nur als Download (opengeodata.lgln.niedersachsen.de) → **Umweg A**: Download einmalig, als Datendatei mitliefern.
- [x] **7. Amtliche Gebäudehöhen Niedersachsen** (Version 3.19, in Wilhelmshaven getestet und ok): automatisch für ganz Niedersachsen.
  STAC-Suche `lod.stac.lgln.niedersachsen.de` (Collection lod2) → 1×1-km-Kacheln als SHP-ZIP (~1 MB, MultiPatch, UTM32) → `measHeight`
  (höchster Punkt über Boden, Laserscan). Max. 25 Kacheln. Quelle „amtlich Niedersachsen (gemessen, LoD2)“, im SVG „© LGLN … (CC BY 4.0)“.
  Behobene Fehler beim Bau: Exponent-Zahlen („1.489e+01“), MultiPatch-Format. Sicherung vorher: `…v3.18_vor-niedersachsen-hoehen…`
- [x] **8. Amtliche Gebäudefunktion** (Version 3.20, eingebaut, **Test durch Nutzerin steht noch aus**): Berlin (Geoportal `funktion`) und
  Niedersachsen (LGLN LoD2 `function`) liefern die ALKIS-Gebäudefunktion mit den Höhen mit. Codeliste AdV (BuildingFunctionTypeAdV, 287 Einträge)
  in der App. Nutzung: OSM eindeutig > amtliche Funktion > Nutzungs-Punkte > Flächennutzung. Gebäudetyp „… (amtlich)“ statt „ohne Typangabe“.
  9998 „Nach Quellenlage nicht zu spezifizieren“ bleibt unbekannt. Element-Hinweis + Statistik-Anteil. Sicherung vorher: `…v3.19_vor-gebaeudefunktion…`
- Recherche archiMap (17.11.): nutzt Overture Maps (eigener Server), ALKIS-WFS fast aller Länder, LoD2, Baumkataster, Meta-Kronenhöhen, Sentinel-2.
  Test aus dem Browser: alle 12 Länderdienste erreichbar; Geschosszahl gut lesbar in Brandenburg, Sachsen-Anhalt (GML); BW nur Gebäudefunktion.

## Mi 18.11.
- [x] **Test Punkt 8 + 6b** (durch Nutzerin): amtliche Gebäudefunktion und „Berlin nur Katasterbäume“ funktionieren.
- [x] **9. Geschosszahl geschätzt aus Höhe** (Version 3.21, getestet und ok): LGLN Niedersachsen liefert **keine** Geschosszahl
  (geprüft: weder Shape-ZIP noch CityGML, nur Höhen, Firsthöhe, Traufhöhe, Dachform). Neu: App liest zusätzlich die **Traufhöhe** (`Traufhoehe`).
  Reihenfolge Geschosse: OSM `building:levels` > amtlich Berlin > **geschätzt aus amtlicher Traufhöhe ÷ 3 m** > **geschätzt aus Gebäudehöhe ÷ 3 m** > unbekannt
  (abgerundet, mindestens 1). Beispiele: Traufe 4,4 m → 1, 9,6 m → 3, 17,9 m → 5. Gilt überall (auch Berlin ohne Geschosse, OSM-Höhe).
  Sichtbar als „geschätzt“: Layer „Geschosszahl“, Tab „Element“ (mit Traufhöhe), Tab „Statistik“ („Datenlage Geschosse“), SVG-Hinweiszeile + LGLN-Quelle.
  Behoben: Geschosse außerhalb Berlins hießen fälschlich „amtlich Berlin“. Regel „Wohnen in OG ab 3 Geschossen“ nutzt auch geschätzte Geschosse.
  Grenze: Altbauten (Geschosse 3,5–4 m) evtl. ein Geschoss zu hoch geschätzt.
  Sicherung vorher: `versionen/urban-analyst-v3.20_vor-geschosse-schaetzen_2026-11-18.html`, Stand danach: `…v3.21_2026-11-18.html`
- [ ] ~~**10. Schneller laden**~~ (Version 3.22, **verworfen**): Bausteine gleichzeitig laden (OSM max. 2 Abfragen), LGLN-Kacheln 4 gleichzeitig,
  Hauptserver nach 25 s ohne Antwort wechseln, danach sofort wieder bevorzugen. In der Simulation schneller, bei der Nutzerin **kein spürbarer Unterschied**
  → auf 3.21 zurückgesetzt. Datei bleibt zum Nachsehen: `versionen/urban-analyst-v3.22_2026-11-18.html`.
  Ursache für „keine Besserung“ nicht geklärt (evtl. nur ein Baustein geladen oder die Wartezeit liegt beim Server selbst).
  Falls später nochmal: eher „Downloads im Browser merken“ (gleiches Gebiet lädt sofort, wichtig für die Präsentation).

- **Entscheidung 10:15:** Erst neue Analyse-Themen (Nutzerin), Export-Test danach. Nur **Berlin + Niedersachsen**. Jedes Thema = eigener Baustein
  im neuen Tab **„Analyse & Umwelt“**. Reihenfolge: 1. Sonnenbahn + Schatten · 2. Flurstücke · 3. Bevölkerung · 4. Hochwasser · 5. Verkehrslärm ·
  danach weitere archiMap-Themen (Höhenlinien/Hangneigung, Starkregen, Klima/Hitze …, vorher Datenquellen prüfen). Lärm/Hochwasser damit nicht mehr WON'T.
- **Geprüfte Datenquellen (18.11., aus dem Browser abrufbar):**
  - Flurstücke Berlin: WFS `gdi.berlin.de/services/wfs/alkis_flurstuecke` (JSON) · Niedersachsen: LGLN `opendata.lgln.niedersachsen.de/doorman/noauth/alkis_wfs_einfach`, `ave:Flurstueck` (GML, mit Lage + tats. Nutzung)
  - Bevölkerung Berlin: WFS `ua_einwohnerdichte_2025` (Einwohner/ha je Block, Altersgruppen) · Niedersachsen: Zensus 2022 WMS `www.wms.nrw.de/wms/zensusatlas`, Layer `bevoelkerung_100m` (GetFeatureInfo je 100-m-Zelle)
  - Hochwasser beide: BfG `geoportal.bafg.de/arcgis3/rest/services/nHWGK_HWRK/…` (RWMe/RWlo/CWlo, Flächen mit Wassertiefen-Klasse `T_class`), Nds. zusätzlich NLWKN `umweltkarten-niedersachsen.de/arcgis/rest/services/HWSchutz_wms`
  - Lärm Berlin: WFS `ua_stratlaerm_2022` (Fassadenpegel je Punkt, LDEN/LN, Straße/Schiene/Flug/Gesamt) · Niedersachsen: UBA `datahub.uba.de/server/rest/services/VeLa/LK` (Isophonen) – **sehr langsam/unzuverlässig** (> 40 s)
- [x] **11. Sonnenbahn + Schattenwurf** (Version 3.23, getestet und ok): neuer Tab „Analyse & Umwelt“. Sonnenstand nach SunCalc-Formeln (geprüft: Berlin 21.6. mittags 61°).
  Sonnenbahn-Diagramm über dem Gebiet (21.6./21.3./21.12./gewähltes Datum, Stundenpunkte, N/O/S/W, Sonnenstand zu den Uhrzeiten). Schatten je Gebäude als Block
  mit größter Höhe auf ebenem Boden, je Uhrzeit eine Untergruppe; Gebäude ohne Höhe werfen keinen Schatten (gezählt). Amtliche Höhen laden mit. SVG (Füllregel nonzero) + DXF (Text).
  Sicherung vorher: `versionen/urban-analyst-v3.21_vor-sonne-schatten_2026-11-18.html`. (Nummer 3.22 = verworfenes „schneller laden“.)
- [x] **11b. Bedienung Sonne** (Version 3.24, getestet und ok): Uhrzeiten als Buttons (× entfernen, + hinzufügen), Tage 21.3./21.6./21.12. in einer Reihe,
  Erklär-Kästen als aufklappbares **„Für Nerds“** (Layer + Statistik; Tab „Element“ bleibt offen). Sonnenbahn auf der Karte: Mittelpunkt ziehen = verschieben,
  Uhrzeit-Punkte entlang der Bahn ziehen (5-min-Schritte), Regler „Größe“. Schatten: nur Flächen (Variante „mit Umrisslinien“ unter Aufteilen nach), Live-Regler (eigene Uhrzeit, lila).
  Sicherung vorher: `…v3.23_vor-sonne-bedienung_2026-11-18.html`
- [x] **11c. Schatten als saubere Fläche** (Version 3.25, getestet und ok, aber Live-Regler/Ein-Aus sehr langsam): Karte zeichnet alle Schattenteile in ein gemeinsames Bild (Canvas, 0,4 m/Pixel)
  → keine Linien, keine dunkleren Überlappungen; unsichtbare Fläche zum Anklicken. Beim Laden nur Live-Schatten (12:00) an, feste Uhrzeiten ausgeblendet; Live liegt oben.
  Sicherung vorher: `…v3.24_vor-schatten-flaeche_2026-11-18.html`

- [x] **11d. Tempo Schatten** (Version 3.26, getestet und ok – „perfekt“): Live-Regler zeichnet nur den Live-Schatten neu (feste Uhrzeiten als fertiges Bild),
  beim Ziehen gröber (1,25 m/Pixel, max. 1024), beim Loslassen scharf (0,5 m/Pixel, max. 2048). Umrisse als ein Text an die Zeichenfläche (34 ms statt 2,5 s).
  Klickflächen erst beim Loslassen aktualisiert, Ein/Aus ohne Neusortieren. Gemessen (2.500 Gebäude): Live-Schritt 10,4 s → 0,12 s, Uhrzeit ein/aus 9 s → 0,23 s.
  Sicherung vorher: `…v3.25_vor-schatten-tempo_2026-11-18.html`

- [x] **12. Flurstücke** (Version 3.27, getestet und ok – „alles super“): Baustein „Flurstücke (Kataster)“ im Tab „Analyse & Umwelt“, Auftragsfeld: Flurstück/Kataster/Grundstück/Parzelle.
  Berlin: Geoportal WFS `alkis_flurstuecke` (JSON) · **ganz Niedersachsen**: LGLN `alkis_wfs_einfach`, `ave:Flurstueck` (GML, seitenweise je 2.000).
  Mit echten Daten geprüft: Wilhelmshaven 468, Hannover 654, Göttingen 1.012, Osnabrück 814, Lüneburg 914 Flurstücke (je ca. 0,6 s), Berlin-Kreuzberg 352 (0,2 s).
  Aufteilen: Grenzen (Flurkarte, Standard, nur Linien) · Flächengröße (bis 300 / 1.000 / 5.000 / darüber) · tatsächliche Nutzung (nur Nds., Farben wie Diagnose-Pläne).
  Element: Flurstück (Zähler/Nenner), Flur, Gemarkung, amtliche Fläche, Lage, Nutzung mit m². Statistik: Anzahl + mittlere Größe. SVG-Quelle: Geoportal Berlin bzw. © LGLN (CC BY 4.0).
  Außerhalb Berlin/Nds. (auch Hamburg/Bremen) klare Meldung. Außerdem: **Schatten starten mit 50 % Deckkraft**. Sicherung vorher: `…v3.26_vor-flurstuecke_2026-11-18.html`

- [ ] **12b. Aufteilen-Liste** (Version 3.28, eingebaut, **Test steht aus**): „Einheitlich (eine Farbe)“ heißt jetzt **„Monochrom“** und steht in jeder Liste oben.
  **Alle Bausteine starten einfarbig** (Ausnahmen: Schattenwurf startet mit Live-Uhrzeit; Sonnenbahn und Bezirke haben kein Monochrom). Teilmengen (z. B. Wohngebäude) bleiben gefiltert.
  Auftragsfeld: ohne genannte Aufteilung einfarbig, mit („Gebäude nach Höhe“) wie gewünscht. Attribute mit lesbaren Namen ohne „Attribut:“ und ohne Anzahl (z. B. „Gemarkung“, „Dachform“).
  „Tatsächliche Nutzung (nur Niedersachsen)“ → „Tatsächliche Nutzung“. **Alter Fehler behoben:** Teilmengen-Baustein zusammen mit anderen gewählt → „Ausgewählte laden“ brach ab.
  Sicherung vorher: `…v3.27_vor-aufteilen-namen_2026-11-18.html`

- [x] **12c. Attribut-Namen zurück** (Version 3.29, getestet und ok – „perfekt“): Lesbare Attribut-Namen **nur bei Flurstücken**; alle anderen Bausteine wieder „Attribut: … (Anzahl×)“.
  „Monochrom“ oben + Start einfarbig bleiben. Hinweis: Attribut „Nutzung“ gibt es nur bei Flurstücken in Niedersachsen (Berlin liefert keine Nutzung). Sicherung vorher: `…v3.28_vor-attribut-zurueck_2026-11-18.html`

- [x] **13. Bevölkerung** (Version 3.30, getestet und ok – „perfekt“; Berlin wegen Geoportal-Störung noch nachtesten): Baustein „Bevölkerung (Einwohnerdichte)“, Auftragsfeld: Bevölkerung/Einwohner/Bewohner/Zensus.
  **Berlin:** Umweltatlas WFS `ua_einwohnerdichte_2025` (je Block: Einwohner, EW/ha, unter 18, ab 65, Blocktyp). **Sonst (ganz Niedersachsen, auch HH/HB):** Zensus 2022
  WMS `www.wms.nrw.de/wms/zensusatlas` (`bevoelkerung_100m`, ab 4 km² bzw. > 600 Zellen `bevoelkerung_1km`), GetFeatureInfo je Gitterzelle (EPSG:3035, 6 gleichzeitig).
  Umrechnung LAEA (EPSG:3035) nach EPSG-Formeln, geprüft am EPSG-Beispiel (cm-genau). Echte Daten: Hannover-Mitte 1 km² = 4.648 EW (2,3 s), Wilhelmshaven 1 km² = 4.017 EW (1,9 s).
  Aufteilen: Einwohnerdichte (bis 50 / 100 / 200 / 400 / darüber EW/ha) · Anteil ab 65 Jahre (Berlin). Statistik: Einwohner im Gebiet + Ø Dichte; „Für Nerds“: Hinweis Zensus-Geheimhaltung.
  SVG-Quelle: Zensus 2022 © Statistische Ämter (dl-de/by-2-0) bzw. AfS Berlin-Brandenburg. **18.11. ab ca. 13:55: gdi.berlin.de nicht erreichbar** (Server-Störung, betrifft alle Berliner Daten) → Berlin noch nicht mit echten Daten getestet.
  Sicherung vorher: `…v3.29_vor-bevoelkerung_2026-11-18.html`

- [x] **14. Hochwasser** (Version 3.31/3.32, getestet und ok – „perfekt“): zwei Bausteine in „Analyse & Umwelt“, Auftragsfeld: Hochwasser/Überflutung/Flut/HQ100 bzw. Überschwemmungsgebiet.
  **„Hochwasser (Wassertiefen)“:** amtliche Gefahrenkarten der Länder über den BfG-Dienst `geoportal.bafg.de/arcgis3/rest/services/nHWGK_HWRK/{RW|CW}{Hi|Me|lo}/MapServer/{Layer}` (GeoJSON, `T_class`).
  Layer: Berlin RW 2 · Niedersachsen RW 8 + Küste CWlo 4 (Küste nur Extremereignis) · Bremen RW 5/4/4 + CWlo 3 · Hamburg RW 7/6/6 + CW 1/1/2 (nur wenn das Gebiet dort liegt).
  Alle 3 Szenarien werden gleichzeitig geladen; Start: nur HQ100 an (gibt es kein HQ100, z. B. WHV-Küste: extrem + Hinweis). Knöpfe „häufig · HQ100 · extrem“ im Layer.
  Flächen auf Gebiet + 50 m zugeschnitten. Aufteilen: Monochrom · Wassertiefe (Farben wie amtlich) · Szenario · Schutz durch Deiche (überflutet / geschützt / nachrichtlich).
  Statistik: „% des Gebiets überflutet bei …“; „Für Nerds“: Erklärung Szenarien, Starkregen nicht enthalten. SVG/DXF: Quelle BfG. Teilausfall: ⚠-Hinweis, welche Karte fehlt.
  Echte Daten: Hannover-Leine 1 km² ≈ 5–10 s (HQ100 73 ha) · Wilhelmshaven 2 s (extrem, Küste) · Berlin-Spandau 3,5 s.
  **„Überschwemmungsgebiete (amtlich)“:** NLWKN `umweltkarten-niedersachsen.de/.../HWSchutz_wms/MapServer/39,40,41,42` (vorläufig gesichert · festgesetzt · Bremen · Risikogebiete § 78b WHG), 0,6 s.
  Berlin: noch nicht (klare Meldung; Geoportal Berlin war gestört). Außerdem: „In OSM ansehen“ nur noch bei echten OSM-Objekten. Sicherung vorher: `…v3.30_vor-hochwasser_2026-11-18.html`

- [x] **14b. Baustein „Überschwemmungsgebiete“ gelöscht** (Version 3.32, getestet und ok): komplett aus Katalog und Code entfernt. Das Wort „Überschwemmung“ im Auftragsfeld lädt jetzt „Hochwasser“.
  Hochwasser (Wassertiefen) bleibt unverändert. Sicherung vorher: `…v3.31_vor-uesg-loeschen_2026-11-18.html`

- [x] **15. Verkehrslärm (Straße)** (Version 3.33, getestet und ok – „alles perfekt“): Baustein in „Analyse & Umwelt“, Auftragsfeld: Lärm/Verkehrslärm/Straßenlärm/dB/Lden/Lnight.
  Quelle: Umweltbundesamt, Lärmkartierung 2022 (EU-Umgebungslärmrichtlinie), `datahub.uba.de/server/rest/services/INSPIRE/end_2022_mroad/MapServer/1` (Lden) und `/2` (Lnight), Feld `category` (z. B. Lden6569).
  Bundesweit, also Berlin + ganz Niedersachsen. Nur Hauptverkehrsstraßen > 3 Mio. Kfz/Jahr + Straßen in Ballungsräumen; unter 55 dB(A) ganztags / 50 nachts nicht kartiert (steht in „Für Nerds“).
  Knöpfe „Ganztags (Lden) · Nacht (Lnight)“ im Layer, Start: ganztags + Monochrom. Aufteilen: Lärmpegel (55–59 … ab 75 dB(A), Farben wie UBA). Flächen auf Gebiet + 50 m zugeschnitten.
  Statistik: Anteil des Gebiets ab 55/65/70 dB(A) ganztags bzw. 50/55/60 nachts. SVG/DXF: Quelle UBA. Echte Daten Hannover-Mitte: Lden 2,3 s, Lnight 1,3 s; Klassen überlappen nicht (geprüft).
  Bahn- und Fluglärm: noch nicht (UBA-Dienst VeLa/LK heute > 40 s). Sicherung vorher: `…v3.32_vor-laerm_2026-11-18.html`

- [ ] **16. Höhenlinien + Hangneigung** (Version 3.34, eingebaut, **Test steht aus**): zwei Bausteine in „Analyse & Umwelt“, Auftragsfeld: Höhenlinien/Gelände/Topografie/DGM bzw. Hangneigung/Neigung/Gefälle/Steigung.
  Quelle: LGLN OpenGeoData DGM1 (Laserscan, 1-m-Raster, ≤ 0,3 m genau). Kachelliste: ArcGIS `services-eu1.arcgis.com/4v3xxN52w88W065F/.../lgln_opengeodata_dgm1/FeatureServer/0` (Feld `dgm1` = URL der COG-Kachel auf `dgm1.s3.eu-de.cloud-object-storage.appdomain.cloud`).
  Kacheln 1 × 1 km, Float32, LZW, 512er Blöcke; die App lädt nur die nötigen Blöcke (HTTP-Range) und entpackt selbst (LZW, Deflate, Prädiktor 2/3 – ohne Bibliothek). Neueste Befliegung je Kachel, bei Lücken ältere dahinter.
  Raster bis ~1,2 Mio. Zellen (größere Gebiete gröber). Höhenlinien: 2-m-Raster leicht geglättet, Marching Squares, Abstand automatisch (0,5/1/2/5 m), Knöpfe „Abstand“ im Layer, jede 5. = Haupthöhenlinie mit Höhenzahl.
  Hangneigung: Horn-Verfahren, 5-m-Zellen, Klassen bis 2 / 6 / 12 / 25 / darüber % (6 % = Rampen DIN 18040), gleiche Nachbarn zu Rechtecken zusammengefasst, ohne Umrisslinien.
  Statistik: Geländehöhe von–bis (m ü. NHN), Höhenunterschied, mittlere Neigung. SVG/DXF: Quelle © LGLN; Höhenzahlen als Text (kein Kreis). Echte Kacheln Hannover/WHV entpackt: Werte plausibel (48–75 m / 1,3–3,8 m).
  Berlin: noch nicht (Geoportal Berlin gestört) – klare Meldung. Außerdem: Legende zeigt bei Höhenlinien Linien statt Punkte. Sicherung vorher: `…v3.33_vor-gelaende_2026-11-18.html`

- [x] **17. UI aufräumen, Schritt 1: kurze Baustein-Namen** (Version 3.35, ok – übernommen): „Analyse & Umwelt“: Sonnenbahn · Schattenwurf · Flurstücke · Bevölkerung · Hochwasser · Verkehrslärm · Höhenlinien · Hangneigung.
  Die alte Erklärung steht als Hinweis beim Darüberfahren (Feld `hint`). Weitere UI-Punkte (Schritt für Schritt, je mit Rückfrage): Layer-Karten (Unterzeile/„Aufteilen nach“), Sortier-Hinweis, leere Untergruppen, „Attribut:“-Einträge bei amtlichen Daten, Statistik-Fußnote. Sicherung vorher: `…v3.34_vor-ui-namen_2026-11-18.html`

- [x] **17b. UI Schritt 2: Layer-Karten** (Version 3.36, ok – nächster Schritt freigegeben): Unterzeile ohne Gruppenname, nur „N Elemente · Aufteilung“, einzeilig (zu lang → „…“, ganzer Text als Hinweis beim Darüberfahren).
  Beschriftungen links („Aufteilen nach“, „Deckkraft“ …) 92 px breit, ohne Umbruch. Sicherung vorher: `…v3.35_vor-layerkarten_2026-11-18.html`

- [ ] **17c. UI Schritt 3: Sortier-Hinweis entfernt** (Version 3.37, Wunsch, **Test steht aus**): Zeile „Mit ⋮⋮ ziehen zum Sortieren · oben liegt oben“ über der Layer-Liste ist weg (Ziehen funktioniert weiter). Sicherung vorher: `…v3.36_vor-hinweis-weg_2026-11-18.html`

- [ ] **18. Paralleles Laden** (Version 3.38, **verworfen** – beim Nutzer lud danach gar nichts mehr; Ursache noch unbekannt, im Test mit nachgebauten Servern lief es. Zurück auf 3.37. Datei bleibt als `versionen/urban-analyst-v3.38_2026-11-18.html`): Alle gewählten Bausteine laden gleichzeitig statt nacheinander. Overpass (OSM) höchstens 2 Abfragen gleichzeitig (Warteschlange, sonst „Server ausgelastet“),
  amtliche Dienste (BfG, UBA, LGLN, Zensus, Geoportal Berlin) ohne Begrenzung. Gebäude/Schatten zeichnen erst, wenn ihre Hilfsdaten (amtliche Höhen, Nutzungs-Punkte, Flächennutzung) da sind; Bäume warten aufs Baumkataster.
  Ladeanzeige: „Lade N Bausteine gleichzeitig“, je Baustein eine Zeile mit Stand + Quelle, Gesamtbalken, „X von N fertig“. Abbrechen bricht alle ab. Test mit künstlich langsamen Servern: 6 Bausteine 11,0 s → 4,7 s.
  Sicherung vorher: `…v3.37_vor-parallel-laden_2026-11-18.html`

- [ ] **19. Start-Aufteilung, deutsche Attribut-Namen, weniger OSM-Ballast** (Version 3.39, Wunsch, **Test steht aus**):
  Start mit der ersten fachlichen Aufteilung statt Monochrom bei: Bezirke, ÖPNV, Bäume, Straßen, Bahn, Wasser, Grün, Flächennutzung, Verkehrslärm, Bevölkerung, Hochwasser, Schatten (Live). Monochrom-Start bleibt bei Gebäuden, Flurstücken, Sonnenbahn, Höhenlinien, Hangneigung, eigenen Abfragen.
  „Attribut: roof:shape (713×)“ → „– Dachform“ bei **allen** Bausteinen (Wörterbuch `ATTR_DE` erweitert + Wort-für-Wort-Übersetzung `TOK_DE`); Element-Tab zeigt deutsche Namen (OSM-Schlüssel als Hinweis beim Darüberfahren), yes/no → ja/nein.
  OSM-Angaben ohne Nutzen werden beim Einlesen verworfen (`DROP_TAGS`: Kontakt, Telefon, Webseiten, Öffnungszeiten, Bezahlarten, Wikidata/Wikipedia, Fotos, Prüfdaten, fremdsprachige Namen, Marken-/Betreiber-IDs …). Download wird dadurch kaum kleiner (Overpass schickt alle Angaben), aber Speicher/Export/Liste schlanker.
  Messung Oldenburg (631 Gebäude): 537 KB gesamt, davon Angaben ~92 KB (Adressen 42, Gebäude 16, Dach 15) – die Ladezeit bestimmt fast nur der Overpass-Server (heute 73 s, überlastet). Sicherung vorher: `…v3.37_vor-aufteilung-namen_2026-11-18.html`

- [x] **20. GitHub** (Mi 18.11., 16:45): ganzes Projekt hochgeladen nach https://github.com/Jade-HS-Vibecoding-WPK/urban-analyst (Branch `main`): `index.html` (3.39), `CLAUDE.md`, `PLAN.md`, `versionen/` (71 Dateien), kurzes `README.md`, `LICENSE` (Apache 2.0, war schon da). Inhalt von `index.html` auf GitHub geprüft (gleich). **GitHub Pages läuft** (18.11., 17:00, vom Nutzer eingeschaltet, Branch `main`, Ordner `/`): https://jade-hs-vibecoding-wpk.github.io/urban-analyst/ – liefert 3.39, Karte und Bausteine geprüft. Adresse steht in der README. Offen: README ausbauen, Poster.

- [ ] **Bekannte Grenze (bewusst so gelassen, 18.11.):** „Wasser & Gewässer“ enthält kein Meer. In OSM gibt es dafür nur die Küstenlinie (`natural=coastline`), keine Meeresfläche; Buchten (`natural=bay`), Watt und Küstenlinie werden ebenfalls nicht geladen. Mögliche Lösung später: Küstenlinie + Buchten/Watt laden, Meeresfläche aus der Küstenlinie berechnen.

- [x] **21. Seitenleisten einklappen** (Version 3.40, ok – „mach weiter“): Knöpfe ‹ / › am linken und rechten Kartenrand (oben unter der Suche) klappen die Leisten ein und wieder aus, die Karte wird größer. Zustand bleibt beim Neuladen erhalten. Sicherung vorher: `…v3.39_vor-seitenleisten_2026-11-18.html`
  Danach (Schritt 2, abgesprochen): Schreibfeld „Auftrag in eigenen Worten“ + Detail-Abfrage (+) komplett entfernen; „Verlauf“ = Liste der Arbeitsschritte mit Rückgängig/Wiederholen (Strg+Z / Strg+Y).

- [x] **22. Verlauf mit Rückgängig/Wiederholen, Schreibfeld entfernt** (Version 3.41, ok):
  Entfernt: „Auftrag in eigenen Worten“ (Textfeld, Senden, Vergrößern), Detail-Abfrage (+) mit „Vorherige Abfragen“, im Kern `RULES`/`parseCommand`. Feste Einrichtungs-Bausteine (z. B. Schulen) laden weiter.
  „Verlauf“ listet jeden Schritt (Gebiet, Ort gesucht, Baustein gewählt/abgewählt, Geladen, Sichtbarkeit, Aufteilung, Farbe, Name, Deckkraft, Untergruppe ein/aus/gelöscht, Layer gelöscht/dupliziert, Reihenfolge,
  Element geändert/entfernt, Sonne/Schatten, Szenario/Zeitraum/Abstand, Alles geleert, Projekt geöffnet). Knöpfe ↶ ↷ im Kopf „Verlauf“, Strg+Z / Strg+Y (auch Strg+Umschalt+Z), Klick auf einen Schritt springt dorthin.
  Rückgängig gemachte Schritte grau durchgestrichen; neuer Schritt verwirft sie. Bis 60 Schritte. Technik: Zustand je Schritt (Layer flach kopiert, Klassen/Stile tief), Element-Änderungen ohne Überschreiben.
  Sicherung vorher: `…v3.40_vor-verlauf_2026-11-18.html`

- [x] **22b. Verlauf: Neues oben** (Version 3.42, ok): Schritte und Meldungen (Laden, Hinweise) erscheinen jetzt oben im Verlauf, Älteres rutscht nach unten. Sicherung vorher: `…v3.41_vor-verlauf-oben_2026-11-18.html`

- [x] **22c. Verlauf ohne Bausteinwahl** (Version 3.43, ok): Bausteine an-/abwählen (auch „Standard“, „Auswahl leeren“) erscheint nicht mehr im Verlauf und wird beim Rückgängig nicht verändert. Sicherung vorher: `…v3.42_vor-ohne-bausteinwahl_2026-11-18.html`

- [x] **23. Kreis-Werkzeug, Untergruppen nicht im Verlauf, Hinweis blendet aus** (Version 3.44, ok):
  Neues Werkzeug „◯ Kreis“ ganz links in der Leiste unten: Mittelpunkt klicken, Rand klicken (Vorschau mit Radius und Fläche), Gebiet = Kreis (72 Ecken), Name „Gezeichneter Kreis (r = … m)“.
  Untergruppen ein/aus („alle ein/aus“) erscheinen nicht im Verlauf; Rückgängig ändert ihre Sichtbarkeit nicht. Hinweis „↶ Rückgängig: …“ und kurze Meldungen verschwinden nach 1 s (Ausblenden 0,4 s); Zeichen-Hinweise bleiben stehen.
  Sicherung vorher: `…v3.43_vor-kreis_2026-11-18.html`

- [x] **24. Esc bricht Laden ab, „Auswahl laden“, Fläche beim Zeichnen** (Version 3.45, ok): Esc = „Abbrechen“ in der Ladeanzeige. Knopf heißt „Auswahl laden (N)“, Text „Die wichtigsten Grunddaten“ entfernt.
  Beim Zeichnen steht unten die Fläche in ha und m²: Rechteck mit Seitenlängen, Polygon ab 3 Punkten, Kreis mit Radius. Sicherung vorher: `…v3.44_vor-esc-flaeche_2026-11-18.html`

- [x] **25. Lila Trennlinien links** (Version 3.46, ok): Trennstreifen unter „Neues Projekt“, „Gebiet“ und „Bausteine“ jetzt 2 px im Akzent-Lila (#8b5cf6). Sicherung vorher: `…v3.45_vor-trennlinien_2026-11-18.html`

- [x] **26. Neues Logo, Projektzeile oben** (Version 3.47, ok): Logo „UA“-Kachel ersetzt durch das Nutzer-Logo (lila Zeichen, als Bild in der Datei eingebettet, 96 px, auch als Tab-Symbol).
  Projektname (zum Ändern anklicken), Speichern ⤓, Öffnen ⤒ und Hell/Dunkel ◐ stehen jetzt in der obersten Zeile statt „URBAN ANALYST / Städtebauliche Analyse“; eigene Projektzeile entfällt. Sicherung vorher: `…v3.46_vor-logo_2026-11-18.html`

- [x] **26b. Logo getauscht („Logo_besser“, gestapelte lila Flächen)** (Version 3.48, ok): weißer Hintergrund entfernt (transparent), Querformat 28 px hoch, auch als Tab-Symbol. Sicherung vorher: `…v3.47_vor-logo2_2026-11-18.html`

- [x] **25b. Trennlinien dezenter** (Version 3.49, ok): lila Trennstreifen links zu 70 % durchsichtig (Lila mit 30 % Deckkraft), 14 px Abstand zu beiden Rändern, abgerundete Enden. Sicherung vorher: `…v3.48_vor-trennlinien-dezent_2026-11-18.html`

- [x] **27. Intro beim Öffnen** (Version 3.50, ok): Vollbild in #0f0e13 (Hintergrund der App), Logo „QUAVA“ mit Schrift (weißer Rand entfernt, 900 px, eingebettet) blendet in 0,6 s ein, steht 1 s, dann blenden Hintergrund und Logo zusammen in 0,6 s aus; Klick überspringt. Läuft bei jedem Öffnen/Neuladen.
  Hinweis: App heißt im Tab/Export weiterhin „URBAN ANALYST“ – ggf. mit Nutzer klären (QUAVA?). Sicherung vorher: `…v3.49_vor-intro_2026-11-18.html`

- [x] **28. Name „QUAVA“ überall** (Version 3.51, ok – „passt alles“): Browser-Tab, Logo-Hinweis, SVG/PDF-Fußzeile („erstellt mit QUAVA“), DXF-Kopf, GeoJSON-LIESMICH, Projektdatei (`app: 'QUAVA'`, Endung `.quava.json`; alte URBAN-ANALYST-Projektdateien öffnen weiter), README, CLAUDE.md, PLAN.md.
  Unverändert (technisch nötig): Ordner `urban-analyst`, GitHub-Repository `urban-analyst`, Dateinamen der Sicherungen. Sicherungen vorher: `…v3.50_vor-name-quava_2026-11-18.html`, `CLAUDE_vor-name-quava…`, `README_vor-name-quava…`

- [x] **29. GitHub aktualisiert** (Mi 18.11., 20:05): Stand 3.51 (QUAVA) mit README, CLAUDE.md, PLAN.md und allen neuen Sicherungen hochgeladen; GitHub Pages liefert 3.51 (Intro, Logo, Name geprüft).

- [ ] **30. Schneller laden + Niedersachsen-Cache** (Version 3.52, nur im Branch `schneller-laden`, **Test steht aus**; `main` bleibt unverändert der Stand 3.51 (QUAVA), darum keine Sicherung in `versionen/`).
  Grund (gemessen 18.11.): Fast die ganze Ladezeit war Warten beim Overpass-Server, 30–55 s **je Abfrage**, oft „Server voll“. Deshalb halfen 3.22/3.38 nicht. Der Branch ändert:
  - **Niedersachsen-Cache** (neu): fertige OSM-Daten für 10 Städte (8 Großstädte + Wilhelmshaven, Delmenhorst, je 3 km Rand) und seit 19.11. auch für das Umland von Oldenburg (alle Gemeinden über 5.000 Einwohner bis ca. 90 km, z. B. Rastede, Bad Zwischenahn, Brake, Varel, Cloppenburg, Leer, Emden), wöchentlich neu, Repo `niedersachsen-cache` (GitHub Pages).
    Die App fragt dort zuerst. Gebiet nicht drin, Cache nicht erreichbar oder „Frisch vom Server laden“ → wie bisher Overpass. Je Baustein steht „Quelle: Niedersachsen-Cache (OpenStreetMap, Stand …)“.
    Ergebnis gleich wie Overpass, nur das technische OSM-Merkmal `created_by` (Name des Editors) fehlt. Daten bis ca. 8 Tage alt.
  - **Zwischenspeicher im Browser:** gleiches Gebiet lädt beim 2. Mal in unter 1 s (bis 7 Tage, mit Hinweis und Knopf „↻ Frisch vom Server laden“).
  - **OSM-Sammelabfrage:** alle OSM-Bausteine in 1 Overpass-Abfrage statt 7. **Serverwahl:** bei „Server voll“ kurz warten und neu fragen statt zu Ersatzservern, die nicht antworten.
  - **Amtliche Daten:** LGLN-Höhen 4 Kacheln gleichzeitig und Rechnen im Hintergrund (Oberfläche friert nicht ein), Geländemodell weniger Anfragen, Flurstücke weniger Daten, Zeitlimits statt endlos warten.
  - **Korrekturen:** Traufhöhe Niedersachsen jetzt über Boden statt über Meeresspiegel (war in Wilhelmshaven ca. 1,5 m, in Hannover ca. 55 m zu hoch → zu viele Geschosse geschätzt). Zensus: fehlende Gitterzellen werden mit ⚠ angezeigt.
  Gemessen (1 km², Grundauswahl): Wilhelmshaven 1,2–2,0 s mit Cache (3.39: 5–13 min, nur Sammelabfrage: 44–55 s), Hannover-Mitte 1,4–2,4 s, Berlin weiter über Overpass (44–49 s).
  **Testen:** 1. `index.html` doppelklicken, „Wilhelmshaven“ suchen, Rechteck (ca. 1 km²) zeichnen, Grundauswahl → „Auswahl laden“ → nach wenigen Sekunden fertig, bei jedem Baustein „Quelle: Niedersachsen-Cache (OpenStreetMap, Stand …)“.
  2. Noch einmal „Auswahl laden“ → unter 1 s, „aus dem Zwischenspeicher“. 3. „↻ Frisch vom Server laden“ → lädt über Overpass (ca. 1 Minute, Cache-Hinweis weg).
  4. „Hannover“ suchen, Rechteck in der Mitte, „Gebäude“ laden, beim Layer „Aufteilen nach“ → „Geschosszahl“: Farben gemischt (1–2, 3–4, 5–6, 7+); Gebäude anklicken → Tab „Element“: Traufhöhe ca. 5–25 m, nicht 60–80 m.
  5. Berlin-Mitte laden → wie bisher über Overpass, ohne Cache-Hinweis.

### Stand Mi 18.11., 20:05 (Pause) – hier weitermachen
- Aktuelle Version: **3.51** (`index.html`, QUAVA), Sicherung: `versionen/urban-analyst-v3.51_2026-11-18.html`. GitHub + Pages auf demselben Stand (https://jade-hs-vibecoding-wpk.github.io/urban-analyst/).
- **Branch `schneller-laden`** (von der Kursleitung, 18./19.11.): Version **3.52** = Punkt 30 (schneller laden + Niedersachsen-Cache), **Test steht aus**. `main` = 3.51 unverändert – ob gemergt wird, entscheidest du.
- Noch nicht vom Nutzer mit echten Daten bestätigt: 3.34 Höhenlinien/Hangneigung (Gelände) – beim nächsten Mal kurz prüfen.
- **Nächste Schritte (vor Freeze Do 19.11., 12 Uhr):** 1. **Export-Test** SVG/PDF (Illustrator) und DXF (CAD-Programm erfragen) mit echten Daten. 2. DXF-Layernamen ≤ 31 Zeichen.
  3. Starkregen besprechen (BKG-Hinweiskarte nur als Bild → Flächen zurückrechnen). Klima/Hitze eher weglassen.
- Bis Abgabe Fr 20.11., 16 Uhr: README ausbauen (Funktionen, Screenshots, Quellen), Poster.
- Bekannte Grenzen: kein Meer (nur Küstenlinie in OSM), Berlin-Dienste (gdi.berlin.de) waren am 18.11. gestört → Berlin bei Bevölkerung/Gelände nachtesten; paralleles Laden verworfen (3.38).

### Stand Di 17.11., 15:10 (Pause) – (erledigt, siehe Mi 18.11.)
- Aktuelle Version: **3.20** (`index.html`), Sicherung: `versionen/urban-analyst-v3.20_2026-11-17.html`
- **Zuerst testen:** Punkt 8 (amtliche Gebäudefunktion) in Wilhelmshaven und Berlin: „Gebäudetypen“ laden → kaum noch „ohne Typangabe“?
  Element-Tab „Amtliche Gebäudefunktion“, Statistik „Datenlage Nutzung“. Außerdem 6b (Berlin nur Katasterbäume) noch nicht bestätigt.
- **Gefundener Fehler (noch nicht behoben):** DXF-Layernamen können länger als 31 Zeichen werden (z. B. `Strassen_Wege_Nebenstrasse_Wohnstrasse`).
  DXF R12 erlaubt max. 31 Zeichen → sinnvoll kürzen + bei Gleichheit nummerieren. Vor dem Export-Test beheben.
- Danach: **Export-Test** (MUST M8/M9) mit echten Daten: SVG → Illustrator (Ebenen? Maßstab?), PDF, DXF. Frage: welches CAD-Programm?
- Später möglich: Geschosszahlen aus Kataster Brandenburg / Sachsen-Anhalt (GML), weitere Baumkataster.
- Freeze: Do 19.11., 12 Uhr. Danach M10: GitHub, GitHub Pages, README.

## Testliste Version 1
1. `index.html` doppelklicken → dunkle Berlin-Karte erscheint?
2. Suche „Kreuzberg“ → „Als Untersuchungsgebiet“ → violette Umrandung + Fläche links?
3. „Analyse starten“ (Standard) → nach ca. 1 Minute Layer rechts?
4. Layer ein/aus, Farbe ändern, Legende, Statistik ansehen
5. Auf ein Gebäude klicken → Infos im Tab „Element“?
6. Export SVG → in Illustrator öffnen → Ebenen vorhanden? Maßstab stimmt?
7. Export DXF → im CAD öffnen; Export PDF (Druckdialog)
8. Auftrag schreiben: „Gebäudenutzung und Höhen“ → neue Layer?

## Bugs
- [x] **Auftragsfeld verwechselt Wörter** (17.11.): „Straßenbahn“ lud alle Straßen, „Parkplatz“ alle Grünflächen, „Autobahn“ alle Gleise. Grund: Suche nach Wortteilen. Lösung: genaue Wörter zuerst erkennen und streichen.
- [x] **Kartenwechsel lässt alle Layer verschwinden** (16.11.): MapLibre feuert bei `setStyle` mit „diff“ kein `style.load`, und beim Ereignis meldet `isStyleLoaded()` noch „false“.
  Lösung: `setStyle(…, {diff:false})` + eigenes Merkzeichen `styleReady`. Mit echter MapLibre geprüft (4 Kartenwechsel, Layer bleiben).
- [x] **Objekte unsichtbar nach Wechsel auf „Karte hell/farbig“ und beim nahen Heranzoomen** (16.11.): Eigentliche Ursache gefunden mit der echten App im Testbrowser:
  Die Daten-Layer wurden vor dem *ersten* Beschriftungs-Layer eingefügt. Bei CARTO hell/farbig liegt der ganz unten (Position 13 von 106),
  dadurch lagen Gebäudeflächen, Straßen und Landnutzung der Hintergrundkarte ÜBER unseren Daten. Beim Heranzoomen kommen weitere
  Hintergrund-Flächen dazu, darum „verschwanden“ Objekte. Die 3D-Ansicht wird immer obenauf gezeichnet, deshalb half der Umweg.
  Lösung: Daten-Layer über alle Flächen/Linien der Hintergrundkarte setzen (nur Beschriftungen bleiben oben). Mit echten Daten (3.936 Gebäude) geprüft.

## Offene Fragen / Entscheidungen
- Projektname auf GitHub: `urban-analyst`
- KI für Textaufträge (C3): erst Schlagworte. Eine echte KI nur ohne API-Key im Code (Keys gehören nie auf GitHub).
