[@luis-waldi](https://github.com/luis-waldi)  
[@nils-gb156](https://github.com/nils-gb156)  

# OGC Common Query Language 2 (CQL2) (#7)

## 1. Einstieg & Motivation

## 2. Was ist CQL2?

## 3. Syntaxvarianten (Text vs JSON)

### Text-Encoding

- Menschlich lesbare Syntax (ähnelt SQL)
- Kompakt & gut für URL-Parameter geeignet
- Unterstützt logische, räumliche & zeitliche Filter
- Wird von OGC API - Features, Records & STAC unterstützt

### JSON-Encoding

- Maschinenlesbar (JSON-Struktur)
- Ideal für Web-APOs und zur Programmierung
- Besser validierbar & einfacher zu parsen
- Gleiche Logik wie Text-Encoding

## 4. Operatorenüberblick

### Vergleichoperatoren

- `=`, `<>`, `<`, `>`, `BETWEEN`, `LIKE`, `IN`
- Vergleich von Attributen & Werten

### Logische Operatoren

- `AND`, `OR`, `NOT`
- Kombinieren von Bedingungen

### Räumliche Operatoren

- `S_INTERSECTS`, `S_CONTAINS`, `S_CROSSES`, `S_DISJOINT`, `S_EQUALS`, `S_OVERLEAPS`, `S_TOUCHES`, `S_WITHIN`
- Beziehungen zwischen Geometrien

### Zeitliche Operatoren

- `T_BEFORE`, `T_AFTER`, `T_DURING`, `T_EQUALS`, …
- Vergleich zeitlicher Eigenschaften

>Jeder Ausdruck wertet entweder als `true`, `false` oder `null` aus.

## 5. Beispiel-Filter (Text + JSON)

### Beispiel-Daten:

| ID | platform    | cloud_cover (%) | date       | region    | geom |
|----|-------------|-----------------|------------|-----------|------|
| 1  | Sentinel-2A | 8               | 2024-03-15 | Münster   | POLYGON((7.5 51.9, 7.7 51.9, 7.7 52.0, 7.5 52.0, 7.5 51.9)) |
| 2  | Sentinel-2B | 23              | 2024-04-20 | Münster   | POLYGON((7.6 51.8, 7.8 51.8, 7.8 51.9, 7.6 51.9, 7.6 51.8)) |
| 3  | Landsat-8   | 12              | 2023-03-08 | Münster   | POLYGON((7.5 52.0, 7.7 52.0, 7.7 52.2, 7.5 52.2, 7.5 52.0)) |
| 4  | Sentinel-2A | 5               | 2025-03-08 | Münster   | POLYGON((7.4 51.9, 7.6 51.9, 7.6 52.0, 7.4 52.0, 7.4 51.9)) |
| 5  | Landsat-9   | 40              | 2025-04-11 | Paderborn | POLYGON((8.0 51.7, 8.2 51.7, 8.2 51.9, 8.0 51.9, 8.0 51.7)) |

### Beispiele

| Abfrage | Text | JSON |
|---|------|------|
| Landsat-8 Datensätze | `platform = 'Landsat-8'` | <img src="img/example1.png" alt="Beispiel1" height="110"> |
| Weniger als 10% Wolken | `cloudcover < 10` | <img src="img/example2.png" alt="Beispiel2" height="110"> |
| Bilder, die Münster überdecken | `S_INTERSECTS(geom, BBOX(7.5, 51.9, 7.7, 52.0))` | <img src="img/example3.png" alt="Beispiel3" height="160"> |
| Sentinel-Bilder mit wenig Wolken | `cloudcover < 10 AND platform LIKE 'Sentinel%'` | <img src="img/example4.png" alt="Beispiel4" height="250"> |

## 6. Anwendung in STAC & OGC API

## 7. Fazit