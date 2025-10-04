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
Der Browser kann in Verbindung mit APIs verwendet werden, der Fokus der Entwicklung liegt allerdings nicht auf dieser Nutzung.

TODO: Private query parameters???

TODO: Additional metadata filds ???: Zum rendern der Daten wird die Libary stac-filds genutzt, die verschiedene Regeln zum Anzeigen verschiedener stac-extentions enthält. TODO: ??? 

Der STAC Browser kann über npm installiert und in eigene Webprojekte eingebunden werden. Der Browser kann für das jeweilige Projekt angepasst werden.
Es werden beispielsweise neun verschiedene Sprachen unterstützt, unter anderem Deutsch. Auch verschiedene Basemaps können gerendert werden. Es gibt zudem die Möglichkeit, den STAC Browser mit anderen Diensten zu verknüpfen. Weitere Änderungen können im Ordner src/theme der Browserdateien angepasst werden. (TODO: weitere änderungen oder generell???)

Auch Dockerisierung wird unterstützt.

Mehr Informationen zur Installation und Nutzung: https://github.com/radiantearth/stac-browser?tab=readme-ov-file#get-started
### STAC-js

### OL-STAC

## Quellen

## Links zur Recherche:
### Tools generell
https://stacindex.org/

### Browser
https://github.com/radiantearth/stac-browser?tab=readme-ov-file#stac-browser
https://github.com/radiantearth/stac-browser/blob/main/docs/actions.md
https://radiantearth.github.io/stac-browser/#/?.language=de
https://thejeshgn.com/2024/05/08/exploring-stac-datasets-with-browser/
https://apps.thejeshgn.com/stac-browser/#/external/panoramax.openstreetmap.fr/api/users/8684d422-df83-42a4-85ca-acc5be7bc357/catalog/?.language=de
https://marbleclimate.com/tutorials/users/catalog/gui-search.html

### STAC-js

### OL-STAC
