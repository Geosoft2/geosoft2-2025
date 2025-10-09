# STAC – SpatioTemporal Asset Catalog

## Überblick

STAC (SpatioTemporal Asset Catalog) ist ein offener Standard zur Beschreibung, Katalogisierung und Suche von georäumlichen Daten mit Raum- und Zeitbezug, wie z. B. Satellitenbildern, Drohnendaten oder Fernerkundungsprodukten.

### Zielsetzung

- Einheitliche Metadatenstruktur für georäumliche Assets
- Interoperabilität zwischen Datenanbietern, Clouds und Tools
- Ermöglicht effizientes Durchsuchen und Abrufen großer Datensätze
- Unterstützt sowohl statische Kataloge als auch dynamische STAC-APIs

STAC stellt sicher, dass raum-zeitliche Assets leicht auffindbar, zugänglich und wiederverwendbar sind – unabhängig vom Speicherort.

---

## STAC-Komponenten

| Komponente   | Beschreibung |
|--------------|-------------|
| `Catalog`    | Ein Container für STAC-Collections oder weitere Kataloge |
| `Collection` | Eine strukturierte Gruppe von STAC-Items mit gemeinsamen Metadaten (z. B. Sensor, Datentyp, zeitlicher Umfang) |
| `Item`       | Eine konkrete Beobachtung oder Szene mit Raum- und Zeitbezug sowie verlinkten Assets |
| `Asset`      | Ein einzelnes Datenprodukt (z. B. GeoTIFF, JPEG, JSON), das mit einem Item verknüpft ist |

### Zusatzkomponenten

- `Link`: Verbindungen zwischen STAC-Objekten
- `Extensions`: Modular erweiterbare Spezifikationen für spezielle Metadaten (z. B. EO, Raster, Projection)

---

## STAC-Hierarchie

```text
Catalog
├── Collection: sentinel-2-l2a
│   ├── Item: S2A_20250815T103031_L2A_34UFS
│   │   ├── Asset: B02.tif
│   │   ├── Asset: B04.tif
│   │   └── Asset: thumbnail.jpg
```

---

## Beispiel

---

## STAC-Erweiterungen (Extensions)

### Zweck:



---

## Vorteile von STAC

JSON-basiert, leichtgewichtig und einfach zu verarbeiten

Flexibel einsetzbar (Dateisysteme, APIs, Cloud-native)

Unterstützt moderne Formate wie Cloud-Optimized GeoTIFF (COG)

Erweiterbar über standardisierte Extensions

Offener Standard mit breiter Community und Tool-Unterstützung

---

## Tools & Ressourcen

STAC Spezifikation: https://github.com/radiantearth/stac-spec

Copernicus STAC API: https://stac.dataspace.copernicus.eu

STAC Browser (GUI): https://github.com/radiantearth/stac-browser

Python-Bibliothek: https://pystac.readthedocs.io

QGIS STAC Plugin: https://stac-utils.github.io/qgis-stac-plugin/
