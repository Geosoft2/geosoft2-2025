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
Es gibt die Möglichkeit, den STAC Browser mit anderen Diensten zu verknüpfen. Die Erweiterung durch Extentions wird ebenfalls unterstützt. Der Browser kann auch in Verbindung mit APIs verwendet werden, der Fokus der Entwicklung liegt allerdings nicht auf dieser Nutzung. Auch Dockerisierung wird unterstützt.

TODO: Private query parameters???

TODO: Additional metadata filds ???: Zum rendern der Daten wird die Libary stac-filds genutzt, die verschiedene Regeln zum Anzeigen verschiedener stac-extentions enthält. TODO: ??? 

TODO:https://github.com/radiantearth/stac-browser?tab=readme-ov-file#customize-through-root-catalog einbauen?

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

### OL-STAC

## Quellen
https://github.com/radiantearth/stac-browser?tab=readme-ov-file#stac-browser
https://radiantearth.github.io/stac-browser/#/?.language=de
https://marbleclimate.com/tutorials/users/catalog/gui-search.html

## Links zur Recherche:

### STAC generell
https://thejeshgn.com/2024/05/08/exploring-stac-datasets-with-browser/

### Tools generell
https://stacindex.org/

### Browser
amax.openstreetmap.fr/api/users/8684d422-df83-42a4-85ca-acc5be7bc357/catalog/?.language=de
https://apps.thejeshgn.com/stac-browser/#/external/panor

### STAC-js

### OL-STAC
