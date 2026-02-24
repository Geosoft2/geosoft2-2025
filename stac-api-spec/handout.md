# STAC API Spezifikation
### Unterschiede zur STAC-Spezifikation · Architektur & Endpunkte (ohne Erweiterungen) · Typische Anwendungsfälle
**Kurs:** Geosoftware II, Wintersemester 2025/2026  
**Bearbeitet von:** Cedric Gräber[@cgraeber](https://github.com/graeberc), Maximilian Oliver Holtkamp[@MaxiKamp](https://github.com/MaxiKamp)

---

## 1. Einleitung

Die **SpatioTemporal Asset Catalog (STAC)** Spezifikation ist ein offener Standard zur Beschreibung, Strukturierung und Verlinkung von Geodaten (z.B. Erdbeobachtungsdaten).
Sie definiert, **wie Datensätze beschrieben** (Catalogs, Collections, Items) und **über standardisierte Schnittstellen zugänglich gemacht** werden.

Während die **STAC Spezifikation** das Datenmodell und statische JSON-Strukturen beschreibt, erweitert die **STAC API Spezifikation** dieses Konzept um **dynamische, maschinenlesbare Endpunkte**, über die Daten gesucht und gefiltert werden können.

---

## 2. Unterschiede zwischen STAC Spezifikation und STAC API Spezifikation

| Aspekt | STAC (statisch) | STAC API (dynamisch) |
|--------|------------------|----------------------|
| **Datenmodell** | JSON-Dateien (Catalog, Collection, Item) mit Hyperlinks | Fokus auf Collections und Items über HTTP-Endpunkte; ItemCollections als paginierte Ergebnislisten |
| **Zugriff** | Statischer Webserver oder Cloud Storage (z. B. GitHub Pages, S3) | RESTful Webservice mit GET/POST Requests |
| **Navigation** | Manuelles Browsen über Links | Programmatische Suche und Filterung (Raum, Zeit, Metadaten) |
| **Interaktivität** | Keine – Inhalte sind fix | Dynamisch – Abfragen, Paging, Filter, Sortierung möglich |
| **Hosting-Aufwand** | Minimal (Dateien veröffentlichen) | Höher – API-Server notwendig |
| **Typische Nutzung** | Dokumentation, Open Data Portale, Referenzkataloge | Performante Suche, Filterung und automatisierter Zugriff auf große oder häufig aktualisierte Datenbestände |

> **Kurz gesagt:**  
> Die STAC API erweitert statische STAC-Kataloge um standardisierte Web-Service-Endpunkte, die von Software automatisiert abgefragt werden können (z.B. über HTTP-Requests mit Raum- und Zeitfiltern).

---

## 3. Architektur der STAC API (ohne Erweiterungen)

Die **STAC API Core Spezification** baut auf HTTP und JSON auf und ist modular strukturiert.
Sie definiert den Kern (Core), auf den Erweiterungen aufsetzen können (z.B. Filter, Sortierung, Query).

### Komponenten der Architektur

- **Landing Page (`/`)**
 Einstiegspunkt der API mit Links zu den wichtigsten Ressourcen.

- **Collections (`/collections`, `/collections/{collectionId}`)**
 Beschreiben Datensammlungen (z.B. Sentinel-2, Landsat-8).
 Enthalten Metadaten wie räumliche/zeitliche Abdeckung, Lizenz, Assets.

- **Items (`/collections/{collectionId}/items`, `/collections/{collectionId}/items/{itemId}`)**
 Repräsentieren einzelne Beobachtungen oder Dateien innerhalb einer Collection.

- **Search (`/search`)**
 Zentrales Feature zur Abfrage von Items anhand von Filtern:
 ```bash
  /search
 {
    "collections": ["sentinel-2-l2a"],
    "bbox": [7.0, 50.0, 8.0, 51.0],
    "datetime": "2025-01-01/2025-01-31"
 }
```
---

## 4. Endpunkte der STAC API (ohne Erweiterungen)

| Endpoint | Methode | Beschreibung |
|----------|---------|--------------|
|`/`| GET | Landing Page mit Links zu den wichtigsten Ressourcen|
|`/conformance`|GET|Zeigt unterstützte STAC- und OGC-Standards an |
|`/collections`|GET| Listet alle verfügbaren Collections auf |
|`/collections/{collectionId}`| GET | Details zu einer Collection |
|`/collections/{collectionId}/items`|GET |Liste der Items einer Collection|
|`/collections/{collectionId}/items/{itemId}`| GET | Einzelnes Item |
| `/search`| GET/POST | Suche nach Items über Filter (Raum, Zeit, etc.) |

Diese Endpunkte entsprechen der **STAC API Core Specification**, ohne zusätzliche Erweiterungen wie *Filter*, *Query* oder *Transaction*.

---

## 5. Typische Anwendungsfälle

### STAC API (dynamisch)
- **Interaktive Datensuche:** Clients (z.B. QGIS, Python-Skripte, Jupyter Notebooks) können Datensätze nach Raum, Zeit oder Attributen abfragen.
- **Automatisierte Workflows:** Verarbeitungspipelines können API-Aufrufe automatisch durchführen (z.B. tägliche Datenupdates).  
- **Integration:** REST/JSON-Schnittstellen lassen sich leicht in Web- oder Desktop-Anwendungen integrieren.

### STAC (statisch)
- **Dokumentation & Open Data-Kataloge:** Leichtgewichtige Veröffentlichung kleiner oder fixer Datensammlungen, z.B. Forschungsprojekte.  
- **Offline-Nutzung:** STAC-Dateien (JSON) können ohne Serverinfrastruktur genutzt werden.

### Vergleich

| Szenario | STAC (statisch) | STAC API (dynamisch) |
|----------|-----------------|----------------------|
| Kleine fixe Datensätze | Ideal | Overkill|
| Große, häufig aktualisierte Datensätze | Möglich, aber schwer effizient zu durchsuchen | Optimal |
| Nutzerfreundliche Suche | Manuell | Automatisiert |
| Integration in Clients | Möglich, aber ohne standardisierte Suchschnittstelle | Einfach durch standardisierte API-Endpunkte |

---

## 6. Bedeutung für das Geosoftware-II-Projekt

Der **STAC Index** dient als *Meta-Katalog* über viele bestehende STAC-APIs und statische STAC Kataloge.
Im Rahmen des Projekts soll dieser Index um eine **Collection Search** erweitert werden - das heißt, Benutzer sollen nicht nur einzelne Items finden, sonder gezielt nach *Collections* über mehrere APIs hinweg suchen können.

Das Verständnis der **STAC API Architektur und ihrer Endpunkte** ist dafür essenziell:
- um zu ermitteln, **welche Collections eine API bereitstellt** (`/collections`)
- um die **Struktur und Verlinkung von STAC-Ressourcen** zu verstehen
- um optional über Item-Suchen (`/search`) zusätzliche Hinweise auf relevante Collections zu gewinnen
- und um darauf aufbauend eine API-übergreifende Collection-Suche zu implementieren
--- 

## 7. Quellen & weiterführende Literatur

- [STAC Spezifikation – stacspec.org](https://stacspec.org)  
- [STAC API Core Spezifikation (GitHub)](https://github.com/radiantearth/stac-api-spec) 
- [Radiant Earth Blog – Static vs. Dynamic STAC](https://medium.com/radiant-earth-insights)
