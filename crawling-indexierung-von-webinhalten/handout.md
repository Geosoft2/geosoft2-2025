# Crawling und Indexierung von Webinhalten
## Crawling und Indexierung - Wofür?
Stellt dir das Web wie eine riesige Bibliothek ohne Ordnung und Struktur da: unzählige „Bücher“ (Webseiten), ständig neue Regale, dauernd Umbauten. Crawling ist das systematische „Durch-die-Regale-Gehen“. Ein Crawler startet mit ein paar bekannten Adressen (Seeds), lädt die Seite, liest Titel und Text, sammelt weitere Links wie Hinweise auf weitere Regale und packt die neue Adressen auf eine Warteliste. Dabei verhält er sich höflich indem er die robots.txt (Hausordnung der Website) respektiert. Das Ergebnis des Crawlings ist kein fertiges Suchsystem, sondern ein stetig wachsender Stapel von Dokumenten plus Metadaten (URL, Zeitpunkt, Sprache, evtl. letzte Änderung).

Indexierung baut daraus das eigentliche Suchsystem. Texte werden aufgeräumt (Boilerplate weg, Haupttext behalten), in Wörter zerlegt und in einen Index eingetragen: Für jedes Wort wird gespeichert, in welchen Dokumenten es vorkommt. So lässt sich später eine Suchanfrage sofort auf passende Dokumente abbilden. Zusätzlich merkt sich das System Kontext wie Titel, Datum oder ein kurzer Auszug, um Ergebnisse sinnvoll zu sortieren und anzuzeigen. Die einzelnen Wörter bekommen dann Gewichtung. Häufige Füllwörter zählen weniger, seltene, thematisch treffende Begriffe mehr. Aktualität oder Vorkommen im Titel, anstatt im Text, können das Ranking weiter verbessern. Weil sich das Web ständig ändert, wird der Index inkrementell aktualisiert: neue Seiten kommen dazu, geänderte werden ersetzt, veraltete seltener besucht.

Wofür braucht man das? Von großen Web-Suchmaschinen über Nachrichtenseiten bis zu Intranet-Suchen in Unternehmen — überall, wo viele Dokumente schnell und zuverlässig auffindbar sein sollen. Kurz: **Crawling sammelt, Indexierung ordnet**. Zusammen verwandeln sie die chaotische Bibliothek „Web“ in ein effizientes Nachschlagewerk.

## Grundprinzipien von Crawlern
Ein Web-Crawler (auch Spider oder Bot genannt) ist ein Programm, das systematisch Webseiten besucht, um deren Inhalte zu sammeln und zu indizieren. Er startet mit einer Liste von Start-URLs (Seed-URLs), lädt eine Seite herunter, extrahiert den Text und alle darin enthaltenen Links und fügt diese neuen Links der Warteschlange (Frontier) hinzu. \
Anschließend wird die nächste URL aus der Frontier abgearbeitet. Dieser Prozess setzt sich fort, bis alle relevanten Seiten erfasst sind oder eine Abbruchbedingung erreicht wird.

Ablauf eines Crawlers: Start mit Seed-URLs → Seite abrufen (HTTP-Request) → Seite parsen → Text indizieren und Links extrahieren → neue Links zur Frontier hinzufügen

Modulare Architektur: Typische Komponenten sind eine URL-Frontier (Warteschlange), ein DNS/HTTP-Fetch-Modul, ein Parser (für HTML/Links), eine Duplikaterkennung und ein Indexierer.

Robustheit: Der Crawler muss fehlertolerant sein (z.B. gegen Abbruch durch ungültige URLs) und „Spider-Traps“ (seitenweise Endlosschleifen) erkennen und umgehen.
## Strategien zur Indexierung
 TODO
## Herausforderungen
### Skalierung
 Das Web wächst ständig. Historisch mussten Suchmaschinen bereits in den 1990er Jahren ununterbrochen zusätzliche Hardware für Crawling und Indexierung bereitstellen, da sich die Zahl der Seiten alle paar Monate verdoppelte. Moderne Crawler setzen auf verteilte Architekturen (z.B. Apache Nutch auf Hadoop) und parallele Prozesse, um Milliarden von Seiten zu verarbeiten.

### robots.txt und Politeness
 Website-Betreiber können Crawler über die robots.txt-Datei steuern, indem sie angeben, welche URLs gecrawlt werden dürfen. Diese Datei dient vor allem dazu, Crawling-Traffic zu lenken und Serverüberlastung zu vermeiden. Crawler sollten die robots.txt-Regeln beachten und vorsichtig crawlen: etwa nie mehr als eine Verbindung gleichzeitig zu einem Host öffnen und zwischen den. Solche Politeness-Strategien verhindern, dass Server durch das Crawling überlastet oder blockiert werden.

### Dynamische Inhalte
 Viele moderne Webseiten laden Inhalte erst zur Laufzeit per JavaScript/AJAX nach. Traditionelle Crawler, die nur statisches HTML laden, überspringen diese Daten oft. Um dynamische Seiten vollständig zu erfassen, werden Techniken wie Headless-Browser (z.B. Puppeteer, Playwright oder Selenium) eingesetzt, die JavaScript ausführen und die Seite „vollständig“ rendern. Dadurch können auch Inhalte erfasst werden, die sonst übersehen würden.

### Rate Limits
 Sowohl Crawler als auch Server setzen oft Crawling-Ratenbegrenzungen. Crawler implementieren daher Verzögerungen oder lesen in der robots.txt einen Crawl-Delay aus. Beispielsweise kann ein Crawler nach jeder Anfrage automatisch 200ms warten. Crawler4j z.B. nutzt seit Version 1.3 standardmäßig 200 ms Pause zwischen Anfragen. Wer zu schnell crawlt, riskiert, vom Server geblockt zu werden oder als Bot markiert zu werden.

### Pay-per-Crawl
Kommerzielle Anbieter ermöglichen Crawling „on demand“, bezahlt pro Crawl oder Datenvolumen.
- Vorteile: Skalierbarkeit, geringere Wartung, robots.txt-Handling.
- Nachteile: Kosten, eingeschränkte Kontrolle über Crawling-Strategie.
- Beispiele: Zyte, Apify, SerpApi, Bright Data.

### AI Crawler
Cloudflare hat ein Feature namens Pay per Crawl eingeführt, Teil ihres AI Crawl Control-Produktes.
Dabei Publisher können einen Preis pro erfolgreichem Crawl festlegen oder auch ggf. ablehnen. 

#### Vorteile
- Monetarisierungsmöglichkeit für Content Owner  
- Mehr Kontrolle 0über Zugriff durch AI-Crawler  
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
- Scrapy (Python): Weit verbreitetes Open-Source-Framework für Web-Crawling und -Scraping. Es ist schnell, flexibel und wird von einer großen Community gepflegt.
- Crawler4j (Java): Einfacher Java-Crawler mit moderner API. Open Source, Multi-Thread-fähig und schnell einsetzbar.
- Apache Nutch: Hochskalierbarer Java-Crawler auf Hadoop-Basis. Extrem anpassbar und für große Crawling-Jobs optimiert.
- Heritrix: Vom Internet Archive entwickelter - Open-Source-Web-Crawler für Archivierungszwecke. Sehr skalierbar und erweiterbar („web-scale, archival-quality crawler“)
- StormCrawler: Java-Framework für verteiltes Crawling mit Apache Storm. Skalierbar, echtzeit-fähig und modular für eigene Crawling-Pipelines
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