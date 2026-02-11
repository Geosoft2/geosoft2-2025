@PerMertesAchter

# STAC API-Erweiterungen

## Übersicht
- **Collection Search & erweiterte Abfragen ohne CQL2**
- **Autor:** Daniel Achter
- **Ziel:** Erweiterte Such-, Filter- und Ausgabeoptionen über STAC API Extensions

## STAC API ist modular
- Zusätzliche Funktionen über **Extensions**
- Modulares Design ermöglicht flexibles Abfragen von Geodaten

## Wichtige Extensions
- **Query:** Filterung nach Metadaten
- **Sort:** Steuerung der Ergebnisreihenfolge
- **Fields:** Auswahl der zurückgegebenen Attribute
- **Collection Search:**
  - Funktion: Suche über Collections statt Items
  - Nutzen: passende Datensätze finden (z.B. bestimmte Sensoren)

## Beispiele Collection Search
- Ergebnis: Liste von Collections, z.B.:
  - `sentinel-1-grd`
  - `sentinel-2-l1c`
- Jede Collection enthält Metadaten über Sensor, Lizenz, räumliche und zeitliche Abdeckung

### Beispiel für Informationen einer einzelnen Collection
```python
GET /collections/sentinel-2-l1c/
```
- Rückgabe: Metadaten zu dieser Collection (ohne Items)

## Abfragemöglichkeiten ohne CQL2
- Nicht alle STAC-Implementierungen unterstützen CQL2 vollständig
- STAC API bietet parameterbasierte Abfragen:
  - Vorteil: sofort nutzbar, weniger komplex, verständlich für schnelle Suchanfragen

### Simple GET Search
- Filter über URL-Parameter
- Beispiel:
```python
query = {
  "bbox": [13, 45, 14, 46],
  "datetime": "2019-12-01T00:00:00Z/2020-01-01T00:00:00Z",
  "collections": ["sentinel-1-grd"],
  "limit": 100
}
url = "https://sh.dataspace.copernicus.eu/api/v1/catalog/1.0.0/search"
response = oauth.get(url, params=query)
```

### Simple POST Search (JSON)
- Filter als JSON über POST-Request
- Beispiel:
```python
data = {
  "bbox": [13, 45, 14, 46],
  "datetime": "2019-12-01T00:00:00Z/2020-01-01T00:00:00Z",
  "collections": ["sentinel-1-grd"],
  "limit": 100
}
url = "https://sh.dataspace.copernicus.eu/api/v1/catalog/1.0.0/search"
response = oauth.post(url, json=data)
```

### Simple POST Search (GeoJSON)
- Filter als GeoJSON über POST-Request
- Beispiel: polygonale Abfrage statt bbox
```python
data = {
    "datetime": "2019-12-10T00:00:00Z/2019-12-11T00:00:00Z",
    "collections": ["sentinel-1-grd"],
    "limit": 5,
    "intersects": {
        "type": "Point",
        "coordinates": [
            13,
            45,
        ],
    },
}
```

## Search with Fields
- `include`: zusätzliche Attribute zum Output hinzufügen
- `exclude`: Standardattribute vom Output entfernen
- Beispiel:
```python
data = {
    "bbox": [13, 45, 14, 46],
    "datetime": "2019-12-10T00:00:00Z/2019-12-11T00:00:00Z",
    "collections": ["sentinel-2-l1c"],
    "limit": 1,
    "fields": {"include": ["properties.gsd"]},
    "fields": {"exclude": ["properties.datetime"]},
}

url = "https://sh.dataspace.copernicus.eu/api/v1/catalog/1.0.0/search"
response = oauth.post(url, json=data)
```

## Sort und Distinct
```python
data = {
  "bbox": [13, 45, 14, 46],
  "datetime": "2019-12-01T00:00:00Z/2020-01-01T00:00:00Z",
  "collections": ["sentinel-1-grd"],
  "limit": 100,
  "sortby": [{"field": "properties.datetime", "direction": "desc"}],
  "distinct": "date"
}
response = oauth.post(url, json=data)
```
- `sortby`: sortiert Ergebnisse, z.B. nach Datum absteigend
- `distinct`: nur ein Item pro Datum zurückgeben


## Quellen
- [Sentinel Hub Catalog Examples](https://docs.sentinel-hub.com/api/latest/api/catalog/examples/) (15.10.2025)
- [Copernicus Data Space API Examples](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Catalog/Examples.html) (15.10.2025)
- [STAC Specification](https://stacspec.org/en/about/stac-spec/) (15.10.2025)
- [STAC API Extensions](https://stac-api-extensions.github.io) (15.10.2025)
- [pystac-client Documentation](https://pystac-client.readthedocs.io/en/v0.2.0) (15.10.2025)

