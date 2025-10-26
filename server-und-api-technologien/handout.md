[Handout.pdf](https://github.com/user-attachments/files/22913171/Handout.pdf)
# [cite_start]Handout: Server- und API-Technologien [cite: 286]

[cite_start]**Justin Krumböhmer, Simon Imfeld** [cite: 287]
[cite_start]*Simonlmf, jkrumboe* [cite: 288]

[cite_start]**Geosoftware II** [cite: 289]
[cite_start]**WiSe 2025/26** [cite: 290]
[cite_start]Dozent*innen: Dr. Christian Knoth [cite: 291]

[cite_start]ifgi [cite: 292]
[cite_start]Institut für Geoinformatik [cite: 293]
[cite_start]Universität Münster [cite: 293]

---

## [cite_start]1. Server- & API-Technologien: Der Überblick [cite: 294]

### [cite_start]Der Server (Das Backend) [cite: 295]

* [cite_start]**Definition:** Software/Hardware, die Dienste und Ressourcen für Clients (Browser, Apps) bereitstellt. [cite: 296, 297]
* [cite_start]**Kernfunktion:** Führt die Geschäftslogik aus (z. B. Logins, Datenberechnungen, Verarbeitung). [cite: 298]
* [cite_start]**Datenaustausch:** Ruft Daten aus Datenbanken ab und formatiert sie für die Übertragung. [cite: 299, 300]
* [cite_start]**Standardformat:** Daten werden im Web meist als JSON (JavaScript Object Notation) übertragen. [cite: 301]

### [cite_start]Die API (Application Programming Interface) [cite: 302]

* [cite_start]**Rolle:** Definiert den Kommunikationsvertrag (Schnittstelle) zwischen Client und Server. [cite: 303]
* [cite_start]**Abstraktion:** Verbirgt die Komplexität des Backends vor dem Client. [cite: 304]
* [cite_start]**Ziel:** Ermöglicht es verschiedenen Clients (Webseite, Mobil-App), dieselbe Datenbasis zu nutzen. [cite: 305]
* [cite_start]**Protokoll:** Web-APIs basieren in der Regel auf dem HTTP-Protokoll. [cite: 306]

---

## [cite_start]2. Gängige Web-Frameworks [cite: 307]

* [cite_start]**Frameworks:** Liefern die Grundstruktur für Webserver und übernehmen Aufgaben wie Routing und Anfrage-Verarbeitung. [cite: 308, 309]
* [cite_start]**Routing:** Ordnet eine URL dem zuständigen Code zu (z.B. /users/123 wird der Nutzer-Funktion zugeordnet). [cite: 310]
* [cite_start]**Middleware:** Funktions-Schicht im Anfrage-Antwort-Zyklus, die Anfragen loggen, authentifizieren oder anreichern kann. [cite: 311]
* [cite_start]**Beispiele:** [cite: 312]
    * [cite_start]**Node.js / Express:** Minimalistisches Framework, das komplett auf Middleware-Ketten basiert; ideal für schlanke REST-APIS. [cite: 313]
    * [cite_start]**Django (Python):** High-Level-Framework für schnelle Entwicklung, mit integrierten Sicherheits- und Admin-Funktionen. [cite: 314]
    * [cite_start]**Spring Boot (Java):** Erstellt eigenständige, produktions-fertige Anwendungen mit minimaler Konfiguration. [cite: 315]

---

## [cite_start]3. Konzepte von REST (Representational State Transfer) [cite: 316]

* [cite_start]**Definition:** Ein Regelwerk (Architecture Style) für die Gestaltung skalierbarer und wartbarer Webservices. [cite: 317]

### [cite_start]Die Vier Schlüsselprinzipien [cite: 318]

**1. [cite_start]Ressourcenorientierung:** [cite: 319]
* [cite_start]Alle Entitäten sind Ressourcen (z. B. /users). [cite: 320]
* [cite_start]Ressourcen werden über eindeutige URIS (Adressen) identifiziert. [cite: 321]
* [cite_start]Wichtig: URIs sind Nomen (im Plural). [cite: 322]

**2. [cite_start]Zustandslosigkeit (Statelessness):** [cite: 323]
* [cite_start]Der Server speichert keine Session-Infos zwischen Anfragen. [cite: 324]
* [cite_start]Jede Anfrage muss alle benötigten Informationen selbst mitliefern. [cite: 324]
* [cite_start]Vorteil: Hochskalierbar und ausfallsicher. [cite: 324]

**3. [cite_start]Einheitliche Schnittstelle:** Die Interaktion nutzt stets die Standard-HTTP-Methoden. [cite: 325]

**4. [cite_start]Cache-Fähigkeit:** Antworten können bei Bedarf zwischengespeichert werden, um die Performance zu steigern. [cite: 326]

---

## [cite_start]4. Best Practices für API-Design [cite: 327]

### [cite_start]URIs & Namenskonventionen [cite: 328]

* [cite_start]**Klarheit:** Verwenden Sie hierarchische Pfade und definieren Sie Ressourcen als Nomen (z. B. /users/123/orders/456). [cite: 329]
* [cite_start]**Konsistenz:** Konsequente Kleinschreibung. [cite: 330]

### [cite_start]HTTP-Methoden [cite: 331]

* [cite_start]**Korrekte Nutzung:** Setzen Sie GET, POST, PUT, DELETE richtig ein. [cite: 332]
* [cite_start]**Idempotenz:** Achten Sie darauf, dass manche Methoden (z.B. GET, PUT, DELETE) idempotent (wiederholbare Aufrufe mit gleichem Ergebnis) und sicher sind. [cite: 333]

### [cite_start]Statuscodes [cite: 334]

* [cite_start]**Rückmeldung:** Bieten Sie eindeutige Rückmeldungen für klar definierte Ergebnisse. [cite: 335]
    * [cite_start]`200 OK`: Erfolg [cite: 336]
    * [cite_start]`201 Created`: Ressource erfolgreich erstellt [cite: 338]
    * [cite_start]`404 Not Found`: Ressource nicht gefunden [cite: 340]
    * [cite_start]`500 Internal Server Error`: Server-Fehler [cite: 342]

### [cite_start]Versionierung [cite: 343]

* [cite_start]**Methode:** Versionsnummern in der URL (/api/v1/) oder im Header verwenden. [cite: 344]
* [cite_start]**Ziel:** Bestehende Clients weiter unterstützen, auch wenn die API geändert wird. [cite: 345]

### [cite_start]Sicherheit [cite: 346]

* [cite_start]**Zweck:** Authentifizierung (Wer bin ich?) und Autorisierung (Was darf ich?). [cite: 347]
* [cite_start]**Verfahren:** Nutzung tokenbasierter Verfahren wie OAuth 2.0/JWT (JSON Web Token), um den Zugriff zu ermöglichen, ohne Passwörter offenzulegen. [cite: 348]
