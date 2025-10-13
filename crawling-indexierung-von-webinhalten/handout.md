# Crawling und Indexierung von Webinhalten
Dieses Handout erklärt grundlegende Konzepte des Web-Crawlings und der Indexierung, Vergleich von Strategien, typische Herausforderungen und praxisnahe Tools.

## Lernziele <!-- Wollen wir sowas machen? -->

## Crawling vs. Indexierung?
Stellt dir das Web wie eine riesige Bibliothek ohne Ordnung und Struktur da: unzählige „Bücher“ (Webseiten), ständig neue Regale, dauernd Umbauten. Crawling ist das systematische „Durch-die-Regale-Gehen“. Ein Crawler startet mit ein paar bekannten Adressen (Seeds), lädt die Seite, liest Titel und Text, sammelt weitere Links wie Hinweise auf weitere Regale und packt die neue Adressen auf eine Warteliste. Dabei verhält er sich höflich indem er die robots.txt (Hausordnung der Website) respektiert. Das Ergebnis des Crawlings ist kein fertiges Suchsystem, sondern ein stetig wachsender Stapel von Dokumenten plus Metadaten (URL, Zeitpunkt, Sprache, evtl. letzte Änderung).

Indexierung baut daraus das eigentliche Suchsystem. Texte werden aufgeräumt (Boilerplate weg, Haupttext behalten), in Wörter zerlegt und in einen Index eingetragen: Für jedes Wort wird gespeichert, in welchen Dokumenten es vorkommt. So lässt sich später eine Suchanfrage sofort auf passende Dokumente abbilden. Zusätzlich merkt sich das System Kontext wie Titel, Datum oder ein kurzer Auszug, um Ergebnisse sinnvoll zu sortieren und anzuzeigen. Die einzelnen Wörter bekommen dann Gewichtung. Häufige Füllwörter zählen weniger, seltene, thematisch treffende Begriffe mehr. Aktualität oder Vorkommen im Titel, anstatt im Text, können das Ranking weiter verbessern. Weil sich das Web ständig ändert, wird der Index inkrementell aktualisiert: neue Seiten kommen dazu, geänderte werden ersetzt, veraltete seltener besucht.

Wofür braucht man das? Von großen Web-Suchmaschinen über Nachrichtenseiten bis zu Intranet-Suchen in Unternehmen — überall, wo viele Dokumente schnell und zuverlässig auffindbar sein sollen. Kurz: **Crawling sammelt, Indexierung ordnet**. Zusammen verwandeln sie die chaotische Bibliothek „Web“ in ein effizientes Nachschlagewerk.

## Grundprinzipien von Crawlern
Ein Web-Crawler (auch Spider oder Bot genannt) ist ein Programm, das systematisch Webseiten besucht, um deren Inhalte zu sammeln und zu indizieren. Er startet mit einer Liste von Start-URLs (Seed-URLs), lädt eine Seite herunter, extrahiert den Text und alle darin enthaltenen Links und fügt diese neuen Links der Warteschlange (Frontier) hinzu. \
Anschließend wird die nächste URL aus der Frontier abgearbeitet. Dieser Prozess setzt sich fort, bis alle relevanten Seiten erfasst sind oder eine Abbruchbedingung erreicht wird. \
\
Die Frontier ist die zentrale Warteschlange eines Crawlers. Sie enthält URLs mit Metadaten (Depth, Host, Priorität, Timestamps) und steuert Reihenfolge und Tempo des Crawls. Übliche Queue‑Typen sind FIFO für breite Coverage, LIFO für tiefe Traversals und Priority‑Queues für scorebasierte Reihenfolgen. Prioritäten ergeben sich aus Tiefe, Linkkontext, Änderungsfrequenz oder Geschäftsregeln.

### Ablauf eines Crawlers
1. **Start mit Seed‑URLs** \
    - Starte mit einer oder mehreren Anfangs‑URLs. Diese Seeds geben die Ausgangspunkte für den Crawl vor.
2. **URL aus der Frontier auswählen und auf Höflichkeit prüfen** \
    - Die nächste URL wird aus der Frontier entnommen. Vor dem Fetch prüft der Crawler robots.txt, Host‑Limits und Rate‑Limits.
3. **Seite abrufen (HTTP‑Request)** \
    - Der Crawler lädt die Ressource per HTTP(S). Dabei werden Statuscodes, Header (z. B. Last‑Modified, ETag) und mögliche Weiterleitungen beachtet.
4. **Seite parsen** \
    - Der heruntergeladene Inhalt wird geparst. Bei Bedarf wird JavaScript gerendert (Headless‑Browser) oder API‑Endpunkte genutzt, um dynamisch nachgeladene Inhalte zu erfassen.
5. **Text indizieren und Links extrahieren** \
    - Relevanter Text und Metadaten werden gespeichert oder an die Indexierung weitergegeben. Links, Media‑Referenzen und strukturierte Metadaten werden identifiziert und annotiert.
6. **Neue Links normalisieren, deduplizieren und zur Frontier hinzufügen** \
    - Gefundene URLs werden normalisiert, auf Duplikate geprüft und gegebenenfalls priorisiert in die Frontier eingefügt. Fehlerhafte oder blockierte Links werden entsprechend behandelt.

Der Prozess ist iterativ. Nach Schritt 6 beginnt der Crawler wieder bei Schritt 2 mit der nächsten URL aus der Frontier und läuft so lange, bis Abbruchbedingungen erreicht sind (Frontier leer, Budget/Limit erreicht, zeitliche Begrenzung oder manuelle Unterbrechung).

### Modulare Architektur eines Crawlers
Ein Crawler ist üblicherweise in klar abgegrenzte Komponenten organisiert. Das vereinfacht Wartung, Skalierung und Austausch einzelner Teile. Wichtige Module sind:
- URL‑Frontier: Warteschlange mit Metadaten wie Tiefe, Priorität und Host. Zuständig für Scheduling und Persistenz.
- DNS/HTTP‑Fetch‑Modul: Führt DNS‑Auflösung, Verbindungsaufbau und HTTP(S)‑Requests aus. Handhabt Timeouts, Redirects und Header‑Parsing.
- Parser: Extrahiert HTML‑Inhalte, Links, Metadaten und strukturierte Daten. Kann optional JavaScript‑Rendering anstoßen.
- Duplikaterkennung: Prüft Inhalte und URLs auf Duplikate mit Techniken wie URL‑Canonicalization, Content‑Hashes oder Bloom‑Filtern.
- Indexierer / Speicher: Speichert Rohdaten, extrahierten Text, Metadaten und Media‑Referenzen in der Datenbank oder an einen Suchindex wie Elasticsearch.
- Scheduler / Politess‑Layer: Setzt Crawl‑Delays, Host‑Limits und Token‑Bucket‑Regeln durch.
- Monitoring & Logging: Metriken für Fetch‑Rate, Fehler, Latenzen und Ressourcenverbrauch sowie Alerting.
- Optional: Proxy‑/IP‑Management, Captcha‑Solver, Post‑Processing (OCR, Transkription).

### Fehlertoleranz und Schutzmechanismen
Ein produktiver Crawler muss robust gegen Netzwerk‑ und Inhaltsfehler sein und sich gegen Fallen im Web schützen.
- Fehlerbehandlung: Timeouts, HTTP‑Fehlercodes und Verbindungsabbrüche mit Backoff und Retry‑Limits behandeln.
- Validierung: Ungültige oder schadhafte URLs erkennen und filtern. URL‑Normalisierung und Blacklists einsetzen.
- Spider‑Trap‑Detektion: Endlose Seitenfolgen erkennen durch Muster wie sich wiederholende URL‑Parameter, Kalenderpaginierung oder rekursive Redirects. Maßnahmen sind Max‑Depth, Max‑Pages‑per‑Host, Erkennung zyklischer URL‑Sequenzen und Heuristiken für „sich wiederholende Pfade“.
- Ressourcenschutz: Limits für parallele Verbindungen pro Host, Bandbreitenbegrenzung und Timeout‑Richtlinien.
- Datenschutz und Legalität: robots.txt respektieren, rechtliche Prüfungen durchführen, personenbezogene Daten erkennen und behandeln.
- Observability: Fehlerquoten, langsame Hosts und ungewöhnliche Redirect‑Muster kontinuierlich überwachen und Alerts einrichten.

### Crawling‑Strategien und Tiefenbegrenzung
Wichtige Grundstrategien sind Breitensuche und Tiefensuche. Beide haben Vor‑ und Nachteile und benötigen Schutzvorkehrungen.
- Breitensuche (BFS): Arbeitet Ebene für Ebene. Vorteil ist frühe Coverage und gute Coverage nahe den Seeds. Gut für frische Indizierung. Nachteil ist hoher Speicherbedarf für die Frontier.
- Tiefensuche (DFS): Taucht tief in einer Seitenstruktur ein. Vorteil ist vollständige Traversierung einzelner Pfade. Nachteil ist Risiko, in tiefe oder endlose Strukturen zu geraten.
- Priority‑ oder Focused‑Crawling: URLs nach Score, Thema oder Geschäftsregeln priorisieren. Gut bei thematisch eingeschränkten Projekten.
- Revisit‑Strategien: Seiten mit hoher Änderungsrate öfter recrawlen. Zeitbasiertes Scheduling bietet mehr Effizienz als einheitliche Intervalle.
Schutz gegen Endlosschleifen und Over‑Crawling
- Max‑Depth: Eine feste maximale Tiefe definiert, wie „weit“ vom Seed aus gecrawlt wird.
- Max‑Pages‑per‑Host: Begrenzt die Zahl der Seiten, die pro Host besucht werden.
- Muster‑Blacklist: URLs mit typischen Fallen (z. B. session‑IDs, sort/dir‑Parameter, sehr tiefe Paginierung) filtern.
- Seen‑Set und Duplikatprüfung: Verhindert wiederholtes Besuchen derselben oder sehr ähnlicher URLs.
- Adaptive Regeln: Bei vielen 4xx/5xx‑Fehlern oder hohen Redirect‑Raten Host temporär niedriger priorisieren oder sperren.

## Indexierung
Indexierung verwandelt die beim Crawling gesammelten Rohdokumente in eine strukturierte, durchsuchbare Repräsentation. Während Crawling dokumentorientiert ist (Seite → Dokument), ist Indexierung term- bzw. feld-orientiert: Ziel ist, Anfragen (z. B. Stichwörter, Phrasen oder Filter) sehr schnell auf die relevanten Dokumente abzubilden.

### Schritte der Indexierung
Die Indexierung lässt sich in wenige, leicht verständliche Schritte zusammenfassen. Wichtig zu beachten ist, dass diese Liste nicht vollständig ist.

1\. Aufnahme & Text‑Extraktion
- Rohdokumente (vom Crawler, Feed oder API) werden eingesammelt. Aus HTML/PDF/Feeds wird der lesbare Text und die wichtigsten Metadaten (Titel, URL, Datum, Sprache) extrahiert.

2\. Reinigung & Kerntext
- Boilerplate (Navigation, Footer, Werbung) wird entfernt, so dass hauptsächlich der eigentliche Inhalt indexiert wird. Ziel: Rauschen reduzieren, relevante Informationen behalten.

3\. Tokenisierung & Normalisierung
- Zerlegung in Tokens (Wörter, Zahlen, URLs) und Vereinheitlichung (Kleinschreibung, einfache Unicode‑Normalisierung).
- Stopword-Filter: Entfernt sehr häufige, wenig aussagekräftige Wörter wie „und“, „der“, „aber“, um das Rauschen im Index zu reduzieren.
- Stemming: Führt Wörter auf ihre Grundform zurück (z. B. „läuft“, „laufen“ → „lauf“), damit verschiedene Wortformen gemeinsam gefunden werden.
- Kurzes Beispiel: \
"René läuft einen Marathon"  → ["rene", "lauf", "marathon"] \
"Der Lauf endet, aber sie laufen weiter." → ["lauf", "endet", "sie", "lauf", "weiter"]

4\. Feld‑Mapping & Signale
- Wichtiges Mapping in Felder (title, body, url, tags). Zusätzliche Signale (z. B. ob der Term im Titel vorkommt) werden als Gewicht oder Filter gespeichert.

5\. Indexaufbau (invertierter Index)
- Terme werden in einem invertierten Index abgelegt: Term → Liste von Dokument‑IDs (und optional Positionen oder Frequenzen). Zusätzlich werden sogenannte Vorwärtsdaten (auch „gespeicherte Felder“ oder „Forward Index“) abgelegt: Das sind ausgewählte Originalinhalte eines Dokuments (z. B. Titel, URL, Auszüge), die nicht nur für die Suche, sondern auch für die Anzeige von Suchergebnissen (z. B. Snippets/Vorschautexte) benötigt werden.
- Kleines Beispiel (Positions‑frei): \
D1: "Katzen und Hunde" → katze:[D1], und:[D1], hund:[D1] \
D2: "Katzen laufen" → katze:[D1,D2], lauf:[D2]

6\. Commit, Sichtbarkeit & Updates
- Der Index wird in schnappschussartigen Commits sichtbar gemacht, er kann also für eine Suchmaschine verwendet werden. Änderungen sind entweder sofort (NRT) oder periodisch (Batch) verfügbar; Updates werden meist als "Löschen + Neuindexieren" gehandhabt.

7\. Monitoring & Qualität
- Laufende Tests (Suche‑Antworten, Latenz, Indexgröße) sowie einfache Metriken (Dokumentanzahl, Indexgröße, Fehler) überwachen die Qualität.

### Wichtige Datenstrukturen und Konzepte

Beim Aufbau einer Suchmaschine oder eines Suchsystems spielen bestimmte Datenstrukturen eine zentrale Rolle. Sie sorgen dafür, dass Suchanfragen schnell und effizient beantwortet werden können. Hier die wichtigsten Konzepte, einfach erklärt:

- Invertierter Index (Inverted Index):  
    Stell dir vor, du hast viele Dokumente (z. B. Webseiten) und möchtest wissen, in welchen Dokumenten ein bestimmtes Wort vorkommt. Der invertierte Index ist wie ein großes Inhaltsverzeichnis: Für jedes Wort (Term) wird eine Liste gespeichert, in der steht, in welchen Dokumenten dieses Wort vorkommt. Diese Liste nennt man „Posting-Liste“. Oft werden zusätzlich die Positionen des Wortes im Dokument und wie oft es vorkommt (Term-Frequenz) gespeichert.  
    Beispiel:  
    - „Hund“ → kommt vor in Dokument 1, 3 und 7  
    - „Katze“ → kommt vor in Dokument 2 und 3  
    So kann das System blitzschnell alle Dokumente finden, die ein bestimmtes Wort enthalten.

- Vorwärtsindex (Forward Index):  
    Während der invertierte Index von Wort zu Dokument zeigt, geht der Vorwärtsindex den umgekehrten Weg: Er speichert für jedes Dokument, welche Wörter darin vorkommen. Das ist praktisch, wenn man z. B. für ein bestimmtes Dokument schnell alle enthaltenen Begriffe oder Metadaten (wie Titel, URL) nachschlagen möchte. Außerdem wird der Vorwärtsindex oft genutzt, um Suchergebnisse anzuzeigen (z. B. einen Textausschnitt/Snippet zu erzeugen) oder um die Relevanz eines Dokuments für eine Suchanfrage zu berechnen.

- Positionsindex (Positional Index):  
    Manchmal reicht es nicht zu wissen, ob ein Wort im Dokument vorkommt – man möchte auch wissen, an welcher Stelle. Der Positionsindex speichert deshalb zusätzlich die genaue Position jedes Wortes im Text. Das ist wichtig für Suchanfragen nach ganzen Phrasen („große Katze“) oder wenn Wörter in einem bestimmten Abstand zueinander stehen sollen.  
    Beispiel:  
    - Dokument 1: „Die große Katze schläft.“  
    - Für das Wort „Katze“ wird gespeichert: kommt in Dokument 1 an Position 3 vor.

Zusammengefasst:  
- Der invertierte Index macht die Suche nach Wörtern schnell.  
- Der Vorwärtsindex hilft, Dokumente und deren Inhalte effizient zu verwalten.  
- Der Positionsindex ermöglicht präzise Suchen nach Phrasen oder Wortabständen.

### Trade-Offs bei der Indexierung

Im Folgenden eine strukturierte Gegenüberstellung gängiger Indexierungsstrategien. Zu jeder Strategie kurz: Beschreibung, typische Vor-/Nachteile und typische Einsatzfälle.

A) Batch-Indexierung (periodisch)
- Kurzbeschreibung: Dokumente werden gesammelt und in großen Batches (z. B. nächtliche Jobs) indexiert. Das Ergebnis sind große, optimierte Segmente, die seltener gemerged werden.
- Vorteile: Sehr hoher Durchsatz beim Schreiben, sehr gute Kompression und niedrige Merge-Kosten pro Dokument.
- Nachteile: Hohe Freshness‑Latenz (neue Inhalte sind erst nach dem Batch sichtbar).
- Typische Einsatzfälle: Archive, wissenschaftliche Repositorien, Websites mit geringer Änderungsrate.
- Trade‑off: Maximale Schreibeffizienz vs. Aktualität der Sucheergebnisse.

B) Inkrementelle / Near-Real-Time (NRT) Indexierung
- Kurzbeschreibung: Kleine Blöcke oder einzelne Dokumente werden fortlaufend indexiert; Änderungen sind in Sekunden bis Minuten verfügbar.
- Vorteile: Geringe Latenz, geeignet für News, Feeds oder interaktive Anwendungen.
- Nachteile: Höherer Overhead (viele kleine Segmente), häufigere Merges, evtl. schlechtere Kompressionsraten.
- Typische Einsatzfälle: Nachrichtenportale, E‑Commerce (Produktänderungen), Publish/Subscribe-Systeme.
- Trade‑off: Freshness auf Kosten von Schreib‑/Merge‑Kosten und möglicher Fragmentierung des Indexes.

C) Streaming- / Event-getriebene Indexierung
- Kurzbeschreibung: Änderungen werden als Events (z. B. Kafka) gestreamt und von Indexer‑Services in Pipelines verarbeitet.
- Vorteile: Sehr skalierbar, natürliche Integration in verteilte Architekturen, gute Eignung für Microservices.
- Nachteile: Komplexere Fehlerbehandlung (genau‑einmal‑Semantik), Latenz kann variieren, zusätzliche Infrastruktur nötig.
- Typische Einsatzfälle: Große verteilte Systeme, Multi‑tenant‑Plattformen, Event‑sourcing‑Architekturen.
- Trade‑off: Operationaler Aufwand und Komplexität vs. Skalierbarkeit und Flexibilität.

D) Nearline / Hybrid-Strategien
- Kurzbeschreibung: Hybridansatz: kritische Felder (Titel, Headline, Metadaten) werden NRT indexiert, der Volltext periodisch in Batches optimiert.
- Vorteile: Kompromiss zwischen Freshness und Effizienz; häufig gute Nutzererfahrung bei moderatem Betriebsoverhead.
- Nachteile: Mehr Komplexität im Pipeline‑Management (zwei Wege pflegen).
- Typische Einsatzfälle: News‑Aggregatoren, große Websites mit wechselnder Priorität von Inhalten.
- Trade‑off: Implementationskomplexität gegen bessere Balance von Frische und Kompressions-/Mergeeffizienz.

E) Feld- und gewichtete Indexierung
- Kurzbeschreibung: Indexierung nach Feldern (title, body, url, anchor_text, tags) mit feldspezifischen Boosts/Weighting.
- Vorteile: Feingranulare Relevanzsteuerung, ermöglicht facettierte Suche und bessere Ranking‑Signale.
- Nachteile: Größerer Index und komplexere Query‑Scoring‑Logik.
- Typische Einsatzfälle: Enterprise‑Search, E‑Commerce, fachliche Suchen mit Metadaten.
- Trade‑off: Genauigkeit/Ranking‑Feinheit vs. Indexgröße und Query‑Komplexität.

F) Positions- und Phrase-Indexierung
- Kurzbeschreibung: Speicherung von Term‑Positionen innerhalb von Dokumenten (positional index) für Phrasen‑ und Proximity‑Queries.
- Vorteile: Ermöglicht exakte Phrasen‑ und Abstandsabfragen, steigert Relevanzpräzision.
- Nachteile: Deutlich größerer Speicherbedarf und zusätzliche Verarbeitung beim Indexieren.
- Typische Einsatzfälle: Juristische Texte, wissenschaftliche Suche, Anwendungen mit hohem Bedarf an exakten Phrasen.
- Trade‑off: Präzision bei der Suche vs. zusätzlicher Speicher‑ und CPU‑Aufwand.

G) Kompressions- und Speicherstrategien
- Kurzbeschreibung: Optimierungen wie Delta‑Codierung, Variable‑Byte, Block‑Kompression, columnar storage für Term‑Statistiken oder segmentbasierte Stores (SSTables).
- Vorteile: Reduzierter Speicherplatz und I/O, oft schnellere Durchsatzraten bei Lesebetrieb.
- Nachteile: Höherer CPU‑Aufwand für Dekompression und komplexere Implementierung.
- Typische Einsatzfälle: Große, read‑heavy Indizes mit begrenztem Speicherbudget.
- Trade‑off: Speicherersparnis vs. CPU‑Kosten und eventuell höhere Latenz pro Query.

Zusammengefasst:
- Freshness vs. Throughput: Batch maximiert Durchsatz; NRT/Streaming maximiert Freshness. Hybridansätze sind in der Praxis oft sinnvoll.
- Genauigkeit vs. Speicher vs. Query‑Latenz: Speichern von zusätzlichen Informationen (Positions- und Phrase-Indizes) und komplexe Gewichtung der Indizes führt zu mehr Speicherbedarf und ist CPU-intensiver. Aggressive Kompression spart Platz, kann aber die CPU‑intensivtät und Query‑Latenz weiter erhöhen.

Zusammenfassung
Indexierung ist mehr als "Wörter speichern": Es ist ein ganzes Ökosystem aus Textaufbereitung, datenstruktureller Gestaltung, Kompressions- und Verteilungsentscheidungen sowie Operationalisierung für Freshness und Skalierung. Die beste Strategie hängt von Anforderungen (Echtzeitbedarf, Speicher, Relevanzqualität) ab; häufig ist ein Hybridansatz (z. B. schneller NRT-Index für Headlines + Batch-Merges für Volltext) der praktischste Kompromiss.


## Herausforderungen
### Skalierung
 Das Web wächst ständig. Historisch mussten Suchmaschinen bereits in den 1990er Jahren ununterbrochen zusätzliche Hardware für Crawling und Indexierung bereitstellen, da sich die Zahl der Seiten alle paar Monate verdoppelte. Moderne Crawler setzen auf verteilte Architekturen (z.B. Apache Nutch auf Hadoop) und parallele Prozesse, um Milliarden von Seiten zu verarbeiten.

### robots.txt und Politeness
 Website-Betreiber können Crawler über die robots.txt-Datei steuern, indem sie angeben, welche URLs gecrawlt werden dürfen. Diese Datei dient vor allem dazu, Crawling-Traffic zu lenken und Serverüberlastung zu vermeiden. Crawler sollten die robots.txt-Regeln beachten und vorsichtig crawlen: etwa nie mehr als eine Verbindung gleichzeitig zu einem Host öffnen und zwischen den Anfragen mehrere Sekunden warten. Solche Politeness-Strategien verhindern, dass Server durch das Crawling überlastet oder blockiert werden.

### Dynamische Inhalte
 Viele moderne Webseiten laden Inhalte erst zur Laufzeit per JavaScript/AJAX nach. Traditionelle Crawler, die nur statisches HTML laden, überspringen diese Daten oft. Um dynamische Seiten vollständig zu erfassen, werden Techniken wie Headless-Browser (z.B. Puppeteer, Playwright oder Selenium) eingesetzt, die JavaScript ausführen und die Seite „vollständig“ rendern. Dadurch können auch Inhalte erfasst werden, die sonst übersehen würden. \
 \
 Multimedia (Bilder, Videos, Audio) ist hier ein separater, aber häufig überlappender Aspekt. Viele Medien werden per JS geladen oder in externen Playern eingebunden, weshalb ein reiner HTML‑Fetch nicht alle Mediendateien entdecken kann. Die reine Erfassung der HTML‑Referenz genügt oft nicht: für Suche/Analyse braucht man Thumbnails, Metadaten, OCR‑Texte oder Transkripte, die man anderweitig extrahieren und verarbeiten muss.

### Rate Limits
 Sowohl Crawler als auch Server setzen oft Crawling-Ratenbegrenzungen. Crawler implementieren daher Verzögerungen oder lesen in der robots.txt einen Crawl-Delay aus. Beispielsweise kann ein Crawler nach jeder Anfrage automatisch 200ms warten. Crawler4j z.B. nutzt seit Version 1.3 standardmäßig 200 ms Pause zwischen Anfragen. Wer zu schnell crawlt, riskiert, vom Server geblockt zu werden oder als Bot markiert zu werden.

### Pay-per-Crawl
Pay‑per‑Crawl‑Angebote sind kommerzielle Dienste, die Crawling und Datenerfassung „on demand“ bereitstellen. Bezahlt wird nach einzelnen Crawls, nach übertragenem Datenvolumen oder nach API‑Aufrufen. Solche Anbieter übernehmen Infrastruktur, Proxy‑Management, Skalierung und oft auch Anti‑Bot‑Mechanismen, sodass du dich hauptsächlich auf Daten‑Extraktion und Nachverarbeitung konzentrieren kannst.

- Vorteile: Skalierbarkeit, geringere Wartung, robots.txt-Handling
- Nachteile: Kosten, eingeschränkte Kontrolle über Crawling-Strategie
- Beispiele: Zyte, Apify, SerpApi, Bright Data

### AI Crawler 
AI‑Crawler sind automatisierte Programme (Bots), die gezielt Webinhalte sammeln, um sie z. B. für Training, Feeds oder Antwortgenerierung in KI‑Systemen zu verwenden. Sie unterscheiden sich von klassischen Suchmaschinen‑Crawlern oft durch deutlich höhere Abrufraten, andere Nutzungszwecke (z. B. Training großer Modelle) und teils abweichende Identifikations‑/Authentifizierungsformen. \
\
Cloudflare nutzt das Prinzip des Pay per Crawl, als Teil ihres AI Crawl Control-Produktes.
Dabei können Publisher einen Preis pro erfolgreichem Crawl festlegen oder auch ggf. ablehnen.

#### Vorteile
- Monetarisierungsmöglichkeit für Content Owner  
- Mehr Kontrolle über den Zugriff durch AI-Crawler  
- Transparenz durch HTTP Status Codes und Preisauszeichnung  

#### Herausforderungen
- Preisfestlegung vs. Wert der Inhalte  
- Technische Identifikation legitimer AI-Crawler vs. Bot-Maskierung  
- Akzeptanz durch AI Betreiber  
- Teilweise rechtliche und lizenzrechtliche Unsicherheiten  

#### Status & Einsatz
- Aktuell private Beta, eingeschränkter Zugang  
- Mindestpreis: $0,01 pro erfolgreichem Crawl 

## Mögliche Frameworks/Tools
Web‑Crawler‑ und Scraping‑Tools helfen dabei, große Mengen von Webseiten automatisiert zu durchsuchen, Inhalte zu extrahieren und ggf. in eine durchsuch- bzw. analysierbare Form zu bringen (z. B. strukturierte Datensätze oder Volltext‑Indizes). Man wählt ein Tool nach Programmiersprache, Skalierbarkeit und Bedarf an JavaScript‑Rendering.
- Scrapy (Python): Weit verbreitetes Open-Source-Framework für Web-Crawling und -Scraping. Es ist schnell, flexibel und wird von einer großen Community gepflegt.
- Headless-Browser/Browser-Automatisierung: Tools wie Puppeteer oder Selenium dienen zum Crawlen von JS-lastigen Seiten, indem sie einen echten Browser simulieren. Sie werden häufig zusammen mit klassischen Crawlern eingesetzt, um dynamische Inhalte zu erfassen.
- Volltext-Engine (Indexierung): Für den Suchindex können auch spezialisierte Lösungen wie Elasticsearch oder Apache Solr genutzt werden. Diese bieten verteilte, hochperformante Indizes für Volltextsuche (oft in Kombination mit einem Crawler-Framework).
## Quellen
1. https://www.cloudflare.com/learning/bots/what-is-a-web-crawler/
2. https://nlp.stanford.edu/IR-book/pdf/19web.pdf
3. https://nlp.stanford.edu/IR-book/pdf/20crawl.pdf
5. https://smudge.ai/blog/ratelimit-algorithms
6. https://blog.cloudflare.com/introducing-pay-per-crawl/
7. https://developers.google.com/search/docs/crawling-indexing/robots/intro
8. https://www.promptcloud.com/blog/crawling-techniques-for-javascript-heavy-websites/
9. https://www.akamai.com/glossary/what-is-a-web-crawler
10. https://youtu.be/xqvnBxu7960?si=1jldEja7fqudwv1I