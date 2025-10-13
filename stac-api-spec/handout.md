# STAC API Spezifikation
### Unterschiede zur STAC-Spezifikation · Architektur & Endpunkte (ohne Erweiterungen) · Typische Anwendungsfälle

---

## 1. Einleitung

Die **SpatioTemporal Asset Catalog (STAC)** Spezifikation ist ein offener Standard zur Beschreibung, Strukturierung und Verlinkung von Geodaten (z.B. Erdbeobachtungsdaten).
Sie definiert, **wie Datensätze beschrieben** (Catalogs, Collections, Items) und **über standardisierte Schnittstellen zugänglich gemacht** werden.

Während die **STAC Spezifikation** das Datenmodell und statische JSON-Strukturen beschreibt, erweitert die **STAC API Spezifikation** dieses Konzept um **dynamische, maschinenlesbare Endpunkte**, über die Daten gesucht und gefiltert werden können.

---

## 2. Unterschiede zwischen STAC Spezifikation und STAC API Spezifikation

| Aspekt | STAC (statisch) | STAC API (dynamisch) |
|--------|------------------|----------------------|
| **Datenmodell** | JSON-Dateien (Catalog, Collection, Item) mit Hyperlinks | Gleiche Datenstruktur, aber per HTTP-Endpunkte zugänglich |
| **Zugriff** | Statischer Webserver oder Cloud Storage (z. B. GitHub Pages, S3) | RESTful Webservice mit GET/POST Requests |
| **Navigation** | Manuelles Browsen über Links | Programmatische Suche und Filterung (Raum, Zeit, Metadaten) |
| **Interaktivität** | Keine – Inhalte sind fix | Dynamisch – Abfragen, Paging, Filter, Sortierung möglich |
| **Hosting-Aufwand** | Minimal (Dateien veröffentlichen) | Höher – API-Server notwendig |
| **Typische Nutzung** | Dokumentation, Open Data Portale, Referenzkataloge | Datenzugriff für Clients, Analyseplattformen, Visualisierungstools |

> **Kurz gesagt:**  
> Die STAC API ist die *programmierbare* Erweiterung der statischen STAC-Kataloge – beide nutzen dasselbe Datenmodell, unterscheiden sich aber in der Art des Zugriffs.

---