# Handout - STAC Tooling

STAC Tooling (bspw. STAC Index selber, STAC Browser, pystac, pystac-client, stac-js, ol-stac, …)

--> Vorstellung gängiger Tools mit besonderem Fokus auf Tools, die für diesen Kurs relevant sein könnten

#### bearbeitet von:

* Lenja Fipper, @Lenja-fpr
* Jonas Klaer, @BrokeJ
* Georgios Voulgaris, @georgevoulg

## Was ist STAC überhaupt?​
STAC (SpatioTemporal Asset Catalog) ist ein Standardformat zur Beschreibung und Organisation von Erdbeobachtungsdaten wie Satellitenbildern, Drohnenaufnahmen oder Klimamodellen. Es legt fest, wie Metadaten – etwa zu Ort, Zeit, Sensor oder Auflösung – einheitlich strukturiert werden. Dadurch können Daten aus verschiedenen Quellen einfacher gefunden, durchsucht und kombiniert werden. Kurz gesagt: STAC sorgt dafür, dass Geodaten weltweit standardisiert, auffindbar und interoperabel bereitgestellt werden.

## Warum STAC Tooling wichtig ist

* **Einheitlicher Zugang** zu Geodaten durch offenen Standard
* **Effiziente Verwaltung** und Validierung von Metadaten
* **Interoperabilität** zwischen Plattformen und Programmiersprachen
* **Skalierbare APIs** und Automatisierung durch Tools wie stac-fastapi und PgSTAC
* **Grundlage** für Erweiterungen wie die Collection Search im Kursprojekt

## Wichtige Tools

* [STAC Index](#stac-index)
* [STAC Browser](#stac-browser)
* [PySTAC & PySTAC-Client (Python)](#pystac--pystac-client-python)
* [STAC-js](#stac-js)
* [OL-STAC](#ol-stac)

---

## STAC Index

Der **STAC Index** ist eine zentrale Plattform, die alle bekannten STAC-APIs, Catalogs und Tools weltweit zusammenfasst.
Er dient als **Such- und Vergleichsportal**, mit dem Nutzer gezielt nach Datensätzen, Regionen oder API-Typen filtern können.
Entwickelt und gepflegt wird der Index von der **STAC-Community**, insbesondere der **Radiant Earth Foundation**.
Er ist ein wichtiger **Orientierungspunkt** für Entwickler, um verfügbare Datenquellen und unterstützte STAC-Funktionen zu entdecken.
Im Rahmen des **Kursprojekts** wird der STAC Index um eine **Collection Search-Funktion** erweitert, sodass künftig auch ganze Collections durchsucht werden können.

### Beispiel

* **Website:** [https://stacindex.org/](https://stacindex.org/)
* **Suche:** z. B. nach „Sentinel-2“ oder „Planetary Computer“ → zeigt verfügbare STAC-APIs und deren Metadaten
* Ergebnisse enthalten API-Typ, Lizenz, Kontakt und direkte Links zur STAC-API
* Informationen können anschließend mit Tools wie **PySTAC-Client** oder **ol-STAC** weiterverarbeitet werden

---

## STAC Browser

Der STAC Browser ist ein Tool, um statische STAC-Datenbanken zu durchsuchen. Dabei werden die Daten möglichst benutzerfreundlich dargestellt. Der Browser wurde als Single-Page-Anwendung entwickelt, um Nutzung und Weiterentwicklung zu vereinfachen.

Es gibt die Möglichkeit, den STAC Browser mit anderen Diensten zu verknüpfen. Die Nutzung von Extentions sowie Dockerisierung wird ebenfalls unterstützt. Der Browser kann auch in Verbindung mit APIs verwendet werden, der Fokus der Entwicklung liegt allerdings nicht auf dieser Nutzung.

Der STAC Browser kann über npm installiert und in eigene Webprojekte eingebunden werden. Dabei werden einige Elemente des Browsers automatisch erstellt, beispielsweise der Titel, der STAC Browser kann für das jeweilige Projekt aber auch angepasst werden.
Es werden beispielsweise neun verschiedene Sprachen unterstützt, unter anderem Deutsch. Auch verschiedene Basemaps können zur Anzeige der Daten gerendert werden.

Mehr Informationen zur Installation und Nutzung: [https://github.com/radiantearth/stac-browser?tab=readme-ov-file#get-started](https://github.com/radiantearth/stac-browser?tab=readme-ov-file#get-started)

### Beispiel:

* Link: [https://radiantearth.github.io/stac-browser/#/?.language=de](https://radiantearth.github.io/stac-browser/#/?.language=de)
* offizieller STAC Browser der Radiant Earth Foundation
* Hier kann gezielt nach STAC Katalogen oder STAC APIs gesucht werden, es sind auch Beispielkataloge angezeigt, die ausgewählt werden können.
* Innerhalb der Kataloge kann durch Filter und Schlüsselwörter nach Geodaten gesucht werden.

---

## PySTAC & PySTAC-Client (Python)

**PySTAC** ist eine Python-Bibliothek zum **Erstellen, Lesen und Validieren** von STAC Catalogs, Collections und Items.
**PySTAC-Client** erweitert diese Funktionen und ermöglicht die **Abfrage von STAC-APIs** über das STAC Search-Interface.

### Wichtige Funktionen

* Unterstützung für **CQL2-Filter**, räumliche und zeitliche Suchanfragen
* Einfache Integration in **Jupyter Notebooks** und Python-Workflows
* Ideal für **Analyse, Tests und Entwicklung** eigener STAC-Erweiterungen
* Ermöglicht das **Erstellen lokaler Catalogs** und deren Veröffentlichung über APIs

### Beispiel

```python
from pystac_client import Client

# Verbindung zu einer STAC-API (z. B. Microsoft Planetary Computer)
api = Client.open("https://planetarycomputer.microsoft.com/api/stac/v1")

# Suche nach Sentinel-2 Items in einer Bounding Box
search = api.search(collections=["sentinel-2-l2a"], bbox=[6.5, 51.8, 7.8, 52.2])
items = list(search.get_items())
print(f"{len(items)} Items gefunden")
```

---

## STAC-js

STAC-js ist eine Libary für JS, die Funktionen und Klassen enthält, die die Interaktion mit STAC-Daten oder schreibgeschützten STAC-Objekten vereinfachen. STAC-js kann im Browser und in NodeJS genutzt werden. Die Funktionen sind allerdings nicht direkt auf Dateien oder Dateisysteme anwendbar. So kann STAC-js nicht zum Erstellen oder Updaten eines Katalogs genutzt werden. STAC-js ist eine Basis für weitere Packages.

Es können einzelne Funktionen oder Klassen importiert werden.

```js
import getObjectType from 'stac-js'
import {STACObject} from 'stac-js'
```

### Beispiel: STACObject

* Basisklasse für STAC-Objekte
* In der [Dokumentation](https://stac-js.moregeo.it/latest/#stacobject): "Don't instantiate this class!":

  * nicht dazu gedacht STAC-Objekte zu erstellen
  * dazu gedacht mit STAC-Objekten zu interagieren
* Enthält beispielsweise:

  ```js
  isAsset() //Ist das Objekt ein Asset?
  getObjectType() //Um was für ein STAC-Objekt handelt es sich?
  getMetadata(field) //Gibt die Metadaten zurück
  getCenter() //gibt das Zentrum eines STAC-Objekts zurück
  toJSON() //gibt ein JSON-Objekt zurück, das exportiert werden kann
  ```

---

## OL-STAC

OL-STAC ermöglicht es, STAC-Daten in einer STAC LayerGroup in OpenLayers anzuzeigen. Geladen werden können Geometries, GeoTIFF-Dateien, web map layers und andere Geodaten.

### Einbinden von OL-STAC in ein Projekt

zunächst muss OL-STAC über npm installiert werden.

Einbinden in den Code:

```js
//STACLayer importieren
import STACLayer from 'ol-stac'

//neuen STAC-Layer mit Geodaten erstellen
const stac = new STAC({
  url: //Daten als URL
  //ODER
  data: //Daten als inline JSON data
})

//Layer in eine Karte "map" laden
map.addLayer(stac)
```

### Beispiel

* Link: [https://openlayers.org/en/latest/examples/stac-item.html](https://openlayers.org/en/latest/examples/stac-item.html)
* Beispielmap, die eine Basemap und Sentinel 2 Daten enthält
* Beispiele für eine index.html-Datei, eine main.js-Datei und eine package.json-Datei

#### -> für Leaflet gibt es die Libary stac-layer

---



---

## Fazit

* **STAC** schafft einen gemeinsamen Standard für Geodaten.
* **STAC-Tools** machen diesen Standard praktisch nutzbar – z. B.:

  * STAC Browser (Visuelle Darstellung)
  * PySTAC (Code-Verarbeitung in Python)
  * OL-STAC (Webkarten in OpenLayers)
* Sie erleichtern den Datenaustausch und die Zusammenarbeit zwischen Anbietern und Nutzern.
* Das Projekt zeigt, wie STAC Tooling Geodaten **auffindbar, durchsuchbar und wiederverwendbar** macht.

---

## Quellen

* Mohr, M. (2023): *The STAC JavaScript Ecosystem + CNG Excursion.* [https://www.youtube.com/watch?v=16wryujzqd8](https://www.youtube.com/watch?v=16wryujzqd8) (zuletzt aufgerufen am 10.10.2025)
* Mohr, M., Fitzsimmons, S. et al. (o.J.): *stac-browser.* [https://github.com/radiantearth/stac-browser?tab=readme-ov-file#stac-browser](https://github.com/radiantearth/stac-browser?tab=readme-ov-file#stac-browser) (zuletzt aufgerufen am 10.10.2025)
* Radiant Earth Foundation (o.J.): *STAC Browser.* [https://radiantearth.github.io/stac-browser/#/?.language=de](https://radiantearth.github.io/stac-browser/#/?.language=de) (zuletzt aufgerufen am 10.10.2025)
* Marble Community (o.J.): *STAC Browser.* [https://marbleclimate.com/tutorials/users/catalog/gui-search.html](https://marbleclimate.com/tutorials/users/catalog/gui-search.html) (zuletzt aufgerufen am 10.10.2025)
* Mohr, M. et al. (o.J.): *stac-js.* [https://github.com/moregeo-it/stac-js](https://github.com/moregeo-it/stac-js) (zuletzt aufgerufen am 10.10.2025)
* Mohr, M. (o.J.): *stac-js 0.1.9.* [https://stac-js.moregeo.it/latest/](https://stac-js.moregeo.it/latest/) (zuletzt aufgerufen am 10.10.2025)
* Mohr, M., Pirelli, L. et al. (o.J.): *ol-stac.* [https://github.com/moregeo-it/ol-stac](https://github.com/moregeo-it/ol-stac) (zuletzt aufgerufen am 10.10.2025)
* OpenLayers (o.J.): *stac support.* [https://openlayers.org/en/latest/examples/stac-item.html](https://openlayers.org/en/latest/examples/stac-item.html) (zuletzt aufgerufen am 10.10.2025)
* Mohr, M. (o.J.): *OL STAC. Quick Start.* [https://ol-stac.moregeo.it/doc/quickstart.html](https://ol-stac.moregeo.it/doc/quickstart.html) (zuletzt aufgerufen am 10.10.2025)
* Mohr, M. (2024): *ol-stac: STAC and OpenLayers combined.* [https://av.tib.eu/media/68503](https://av.tib.eu/media/68503) (zuletzt aufgerufen am 10.10.2025)
* Azavea, Radiant Earth Foundation (o.J.): *PySTAC.* [https://github.com/stac-utils/pystac](https://github.com/stac-utils/pystac) (zuletzt aufgerufen am 13.10.2025)
* Azavea, Radiant Earth Foundation (o.J.): *pystac-client.* [https://github.com/stac-utils/pystac-client](https://github.com/stac-utils/pystac-client) (zuletzt aufgerufen am 13.10.2025)
* Azavea, Radiant Earth Foundation (o.J.): *PySTAC Documentation.* [https://pystac.readthedocs.io/en/stable/](https://pystac.readthedocs.io/en/stable/) (zuletzt aufgerufen am 13.10.2025)
* Azavea, Radiant Earth Foundation (o.J.): *pystac-client Documentation.* [https://pystac-client.readthedocs.io/en/stable/](https://pystac-client.readthedocs.io/en/stable/) (zuletzt aufgerufen am 13.10.2025)
* Radiant Earth Foundation (o.J.): *STAC Index.* [https://stacindex.org/](https://stacindex.org/) (zuletzt aufgerufen am 13.10.2025)
* Radiant Earth Foundation (o.J.): *stacindex-website (GitHub Repository).* [https://github.com/radiantearth/stacindex-website](https://github.com/radiantearth/stacindex-website) (zuletzt aufgerufen am 13.10.2025)
* Mohr, M. (2023): *The STAC Ecosystem and Community Overview.* [https://stacspec.org/en](https://stacspec.org/en) (zuletzt aufgerufen am 13.10.2025)
