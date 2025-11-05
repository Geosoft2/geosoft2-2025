# Datenbanken
von Lenn Kruck ([@Escombra](https://github.com/Escombra)) und Kian Jay Lenert ([@kjlenert](https://github.com/kjlenert))


# Grundtypen von Datenbanken

## Relationale Datenbanken
- bestehen aus Tabellen, die Relationen genannt werden
- Spalten: Attribute
    - Typen (numerisch, Zeichenketten, date/timestamp, benutzerdefiniert)
    - Wertebereich (Domain)
- Zeilen: Tupel/Datensatz
- Schlüssel: Attribut (oder Kombination von Attributen), das den Datensatz eindeutig identifiziert; normalerweise ein extra zu diesem Zweck erstelltes Attribut 
    - als Primärschlüssel oder Fremdschlüssel (referentielle Integrität wahren)
- Intension: Relationenschemata
    - eindeutiger Name innerhalb der DB
    - Liste von Attributen mit Wertebereichen
    - Grad: Anzahl von Attributen, die die Relation bilden
- relationales Datenbankschema:
    - Menge von Relationenschemata
    - Integritätsbedingungen (integrity constraints)
- Extension: konkrete Relation / Datenbankzustand
- Operationen basieren auf relationaler Algebra
- am weitesten verbreitete Art von Datenbank
- ### Vorteile:
    - einfach, aber leistungsstark
    - Beziehungen zwischen Daten gut abbildbar
    - Konsistenz der Daten wird aufrechterhalten
    - ACID-Konform: Atomarität, Konsistenz, Isolation, Dauerhaftigkeit
- ### Nachteile:
    - keine rekursiven Abfragen möglich
    - aufwendiger Objektzugriff über joins bei komplexen Objekten
    - künstliche Schlüssel müssen zusätzlich gespeichert werden
    - externe Programmierschnittstelle notwendig
    - Verhalten von Objekten kann nicht beschrieben werden

## noSQL-Datenbanken
- „not only SQL“
- Daten in Datenstruktur (bspw. JSON) gespeichert
- unstrukturierte Speicherung
- kein Schema → schnell skalierbar
- verteilte Datenbank
- nicht unbedingt ACID-konform
- verschiedene Arten: Schlüsselwert, Dokument, Graph (siehe unten), in-memory, wide-column, ...
- ### Vorteile:
    - kann gut viele Schreib- und Leseanfragen verarbeiten
    - kann mit großen und unstrukturierten Datenmengen umgehen
    - zuverlässige Verfügbarkeit der Daten (durch Replikation auf verschiedenen Servern)
    - hohe Geschwindigkeit
    - Skalierbarkeit (horizontal und vertikal)
    - Datenerfassung muss in kein Schema passen
- ### Nachteile:
    - nicht standardisiert (verschiedene Abfragesprachen, ACID-Konformität)

## Graphdatenbanken
- eine Art von noSQL-Datenbank
- Daten werden als Knoten (nodes) mit Attributen gespeichert, Beziehungen als Kanten (edges)
- Abfragesprachen: bspw. Cypher, SPARQL
- ### Vorteile:
    - ideal für stark vernetzte Informationen (effiziente Modellierung und Abfrage) 
    - Ergebnisse in Echtzeit
    - flexibel
- ### Nachteile:
    - schlecht skalierbar   

(sonstige Vor- und Nachteile: siehe noSQL-Datenbanken)



# PostgreSQL
PostgreSQL ist ein objekt-relationales Open-Source-Datenbanksystem, das den SQL-Standard vollständig unterstützt.
- Unterstützt komplexe Datentypen und Transaktionen
- Erweiterbarkeit:
    - Eigene Datentypen, Operatoren, Funktionen
    - Module: Postgis, pgRouting, hstore, timescaldedb
- ACID-konform (Atomicity, Consistency, Isolation, Durability)

## Installation
Beispielhafte Installation unter Ubuntu:   
`sudo apt install postgresql` 

# PostGIS
PostGIS erweitert PostgreSQL um die Fähigkeit, räumliche Daten zu speichern, zu analysieren und abzufragen.
Beispiele für Geodatentypen: GEOMETRY (Punkt, Linie, Polygon), GEOGRAPHY  (geografische Koordinaten, z.B. WGS84).
Wichtige Funktionen:
- ST_Distance(geom1, geom2) - Berechnet die Distanz
- ST_Intersects(a, b) - Prüft, ob sich Geometrien schneiden
- ST_Buffer(geom, dist) - Erzeugt Pufferzonen
- ST_Contains(a,b) – Prüft, ob Geometrie A – B enthält
- ST_Within(a,b) – Prüft, ob A innerhalb von B liegt
- ST_Area(a) - Berechnet Fläche von A

## Anwendung
- Integration mit QGIS oder GeoServer
- WebGIS-Anwendungen mit Leaflet, OpenLayers oder GeoDjango
- Speicherung und Analyse von z.B. Straßen-, Gebäude- oder Klimadaten

## Installation
Beispielhafte Installation unter Ubuntu:   
`sudo apt install postgis` 

Datenbank mit PostGIS anlegen:  
`CREATE DATABASE geodaten;
\c geodaten
CREATE EXTENSION postgis;`  

Beispielanwendung: Gebe alle Gebäude im Umkreis von 500m eines Punktes aus  
`SELECT name
FROM buildings
WHERE ST_DWithin(geom, ST_Point(7.6, 51.9)::geography, 500);`

# Quellen:
- Vorlesung Datenbanken WiSe 2024/25 Prof. Dr. Xiaoyi Jiang
- https://de.wikipedia.org/wiki/Relationale_Datenbank
- https://www.oracle.com/de/database/what-is-a-relational-database/
- https://de.wikipedia.org/wiki/Graphdatenbank
- https://de.wikipedia.org/wiki/NoSQL
- https://www.ibm.com/de-de/think/topics/nosql-databases
- https://www.oracle.com/de/database/nosql/what-is-nosql/
- https://www.astera.com/de/knowledge-center/sql-vs-nosql/
- https://postgis.net/
- https://www.postgresql.org/