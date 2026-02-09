# Handout: Server- und API-Technologien

**Justin Krumböhmer, Simon Imfeld**  
*Simonlmf, jkrumboe*

**Geosoftware II**  
**WiSe 2025/26**  
Dozent*innen: Dr. Christian Knoth

ifgi  
Institut für Geoinformatik  
Universität Münster

---

## 1. Server- & API-Technologien: Der Überblick

### Der Server (Das Backend)

* **Definition:** Software/Hardware, die Dienste und Ressourcen für Clients (Browser, Apps) bereitstellt.  
* **Kernfunktion:** Führt die Geschäftslogik aus (z. B. Logins, Datenberechnungen, Verarbeitung).  
* **Datenaustausch:** Ruft Daten aus Datenbanken ab und formatiert sie für die Übertragung.  
* **Standardformat:** Daten werden im Web meist als JSON (JavaScript Object Notation) übertragen.  

### Die API (Application Programming Interface)

* **Rolle:** Definiert den Kommunikationsvertrag (Schnittstelle) zwischen Client und Server.  
* **Abstraktion:** Verbirgt die Komplexität des Backends vor dem Client.  
* **Ziel:** Ermöglicht es verschiedenen Clients (Webseite, Mobil-App), dieselbe Datenbasis zu nutzen.  
* **Protokoll:** Web-APIs basieren in der Regel auf dem HTTP-Protokoll.  

---

## 2. Gängige Web-Frameworks

* **Frameworks:** Liefern die Grundstruktur für Webserver und übernehmen Aufgaben wie Routing und Anfrage-Verarbeitung.  
* **Routing:** Ordnet eine URL dem zuständigen Code zu (z. B. `/users/123` wird der Nutzer-Funktion zugeordnet).  
* **Middleware:** Funktions-Schicht im Anfrage-Antwort-Zyklus, die Anfragen loggen, authentifizieren oder anreichern kann.  
* **Beispiele:**  
    * **Node.js / Express:** Minimalistisches Framework, das komplett auf Middleware-Ketten basiert; ideal für schlanke REST-APIs.  
    * **Django (Python):** High-Level-Framework für schnelle Entwicklung, mit integrierten Sicherheits- und Admin-Funktionen.  
    * **Spring Boot (Java):** Erstellt eigenständige, produktions-fertige Anwendungen mit minimaler Konfiguration.  

---

## 3. Konzepte von REST (Representational State Transfer)

* **Definition:** Ein Regelwerk (Architecture Style) für die Gestaltung skalierbarer und wartbarer Webservices.  

### Die Vier Schlüsselprinzipien

**1. Ressourcenorientierung:**  
* Alle Entitäten sind Ressourcen (z. B. `/users`).  
* Ressourcen werden über eindeutige URIs (Adressen) identifiziert.  
* Wichtig: URIs sind Nomen (im Plural).  

**2. Zustandslosigkeit (Statelessness):**  
* Der Server speichert keine Session-Infos zwischen Anfragen.  
* Jede Anfrage muss alle benötigten Informationen selbst mitliefern.  
* Vorteil: Hochskalierbar und ausfallsicher.  

**3. Einheitliche Schnittstelle:**  
Die Interaktion nutzt stets die Standard-HTTP-Methoden.  

**4. Cache-Fähigkeit:**  
Antworten können bei Bedarf zwischengespeichert werden, um die Performance zu steigern.  

---

## 4. Best Practices für API-Design

### URIs & Namenskonventionen

* **Klarheit:** Verwenden Sie hierarchische Pfade und definieren Sie Ressourcen als Nomen (z. B. `/users/123/orders/456`).  
* **Konsistenz:** Konsequente Kleinschreibung.  

### HTTP-Methoden

* **Korrekte Nutzung:** Setzen Sie GET, POST, PUT, DELETE richtig ein.  
* **Idempotenz:** Achten Sie darauf, dass manche Methoden (z. B. GET, PUT, DELETE) idempotent (wiederholbare Aufrufe mit gleichem Ergebnis) und sicher sind.  

### Statuscodes

* **Rückmeldung:** Bieten Sie eindeutige Rückmeldungen für klar definierte Ergebnisse.  
    * `200 OK`: Erfolg  
    * `201 Created`: Ressource erfolgreich erstellt  
    * `404 Not Found`: Ressource nicht gefunden  
    * `500 Internal Server Error`: Server-Fehler  

### Versionierung

* **Methode:** Versionsnummern in der URL (`/api/v1/`) oder im Header verwenden.  
* **Ziel:** Bestehende Clients weiter unterstützen, auch wenn die API geändert wird.  

### Sicherheit

* **Zweck:** Authentifizierung (Wer bin ich?) und Autorisierung (Was darf ich?).  
* **Verfahren:** Nutzung tokenbasierter Verfahren wie OAuth 2.0 / JWT (JSON Web Token), um den Zugriff zu ermöglichen, ohne Passwörter offenzulegen.  
