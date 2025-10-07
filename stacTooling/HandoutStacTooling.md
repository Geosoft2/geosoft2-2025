# Handout - Stac Tooling
STAC Tooling (bspw. STAC Index selber, STAC Browser, pystac, pystac-client, stac-js, ol-stac, …)

--> Vorstellung gängiger Tools mit besonderem Fokus auf Tools, die für diesen Kurs relevant seien könnten

## bearbeitet von:
Lenja Fipper, @Lenja-fpr

...

...

## Wichtige Tools
- [STAC Browser](#stac-browser)
- [STAC-js](#stac-js)
- [OL-STAC](#ol-stac)

### STAC Browser
Der STAC Browser ist ein Tool, um statische STAC-Datenbanken zu durchsuchen. Dabei werden die Daten möglichst benutzerfreundlich dargestellt. Der Browser wurde als Single-Page-Anwendung entwickelt, um Nutzung und Weiterentwicklung zu vereinfachen.

Es gibt die Möglichkeit, den STAC Browser mit anderen Diensten zu verknüpfen. Die Nutzung von Extentions sowie Dockerisierung wird ebenfalls unterstützt. Der Browser kann auch in Verbindung mit APIs verwendet werden, der Fokus der Entwicklung liegt allerdings nicht auf dieser Nutzung. 

Der STAC Browser kann über npm installiert und in eigene Webprojekte eingebunden werden. Dabei werden einige Elemente des Browsers automatisch erstellt, beispielsweise der Titel, der STAC Browser kann für das aber auch angepasst werden.
Es werden beispielsweise neun verschiedene Sprachen unterstützt, unter anderem Deutsch. Auch verschiedene Basemaps können zur Anzeige der Daten gerendert werden. Weitere Änderungen können im Ordner src/theme der Browserdateien angepasst werden. (TODO: weitere änderungen oder generell???)

Mehr Informationen zur Installation und Nutzung: https://github.com/radiantearth/stac-browser?tab=readme-ov-file#get-started

#### Beispiel:
https://radiantearth.github.io/stac-browser/#/?.language=de
TODO: Was ist das für ein Beispiel? von wem wird das betrieben?

Hier kann nach STAC Katalogen gesucht werden und dann innerhalb der Kataloge nach Geodaten gesucht werden

TODO: https://apps.thejeshgn.com/stac-browser/#/external/panor als zweites Beispiel?

TODO: WIe nutzt man einen Browser? 
amax.openstreetmap.fr/api/users/8684d422-df83-42a4-85ca-acc5be7bc357/catalog/?.language=de

### STAC-js
STAC-js ist eine Libary für JS, die Funktionen und Klassen enthält, die die Interaktion mit STAC-Daten oder schreibgeschützten STAC-Objekten vereinfachen. STAC-js kann im Browser und in NodeJS genutzt werden. Die Funktionen sind allerdings nicht direkt auf Dateien oder Dateisysteme anwendbar. So kann STAC-js nicht zum Erstellen oder Updaten eines Katalogs genutzt werden. 

Es können einzelne Funktionen oder Klassen importiert werden.
```js
import getObjectType from 'stac-js'
import {STACObject} from 'stac-js'
```

#### Beispiel: STACObject
- Basisklasse für STAC-Objekte
- In der [Dokumentation](https://stac-js.moregeo.it/latest/#stacobject): "Don't instantiate this class!":
  - nicht dazu gedacht STAC-Objekte zu erstellen
  - dazu gedacht mit STAC-Objekten zu interagieren
- Enthält beispielsweise:
  ```js
  isAsset() //Ist das Objekt ein Asset?
  // ...
  getObjectType() //Um was für ein STAC-Objekt handelt es sich?

  getMetadata(field) //Gibt die Metadaten zurück

  getCenter() //gibt das Zentrum eines STAC-Objekts zurück

  toJSON() //gibt ein JSON-Objekt zurück, das exportiert werden kann
  ```

### OL-STAC

## Quellen
- https://github.com/radiantearth/stac-browser?tab=readme-ov-file#stac-browser
- https://radiantearth.github.io/stac-browser/#/?.language=de
- https://marbleclimate.com/tutorials/users/catalog/gui-search.html

- https://github.com/moregeo-it/stac-js
- https://stac-js.moregeo.it/latest/

## Links zur Recherche:

### STAC generell
https://thejeshgn.com/2024/05/08/exploring-stac-datasets-with-browser/
https://www.gdi.nrw/system/files/media/document/file/20231017_5_geoit_rt_einfuehrung-in-stac-und-stac-api-de_mohr.pdf

### Tools generell
https://stacindex.org/
https://www.youtube.com/watch?v=16wryujzqd8

### Browser
amax.openstreetmap.fr/api/users/8684d422-df83-42a4-85ca-acc5be7bc357/catalog/?.language=de
https://apps.thejeshgn.com/stac-browser/#/external/panor
https://www.youtube.com/watch?v=16wryujzqd8 12:10

### STAC-js
https://www.youtube.com/watch?v=16wryujzqd8 4:06

### OL-STAC
