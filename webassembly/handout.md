[@Benno01], [@Denkorsch]

# **WebAssembly**


---


## **Idee**

WebAssembly (kurz: **Wasm**) ist ein kompaktes Programmformat, das moderne Browser direkt ausführen können. Damit lassen sich Anwendungen, die ursprünglich in Sprachen wie C, C++ oder Rust geschrieben wurden, im Browser nutzen. Ziel ist es, rechenintensive Aufgaben schnell und zuverlässig im Web auszuführen, ohne die Sicherheitsprinzipien des Webs zu verletzen.

Im Browser läuft WebAssembly in einem sicheren, abgeschotteten Bereich. Der Code hat keinen direkten Zugriff auf die Webseite oder Web-APIs. Wenn eine Interaktion mit der Seite nötig ist, stellt JavaScript die Verbindung zwischen WebAssembly und der Anwendung her.

WebAssembly ergänzt JavaScript und ersetzt es nicht. JavaScript bleibt wichtig für die Benutzeroberfläche und die allgemeine Anwendungslogik. WebAssembly kommt dort zum Einsatz, wo viel Rechenleistung oder eine besonders effiziente Ausführung benötigt wird.


---


## **Zielsetzung** 

Die Hauptziele von WebAssembly lassen sich wie folgt zusammenfassen:

- **Effizienz:** Rechenintensive Aufgaben (z. B. Bildverarbeitung oder Simulationen) laufen im Browser nahe an nativer Geschwindigkeit. Das eignet sich für leistungskritische Module. Übergänge zwischen JavaScript und WebAssembly sowie Datenkopien können die Performance mindern.
- **Portabilität:** Ein WebAssembly-Modul verhält sich über verschiedene Plattformen hinweg konsistent, sowohl im Browser als auch auf Servern und am Netzwerkrand (Edge).
- **Sicherheit:** Striktes Sandboxing und Validierung des Binärcodes verhindern unkontrollierten Zugriff auf Host-Ressourcen.
- **Wiederverwendbarkeit:** Etablierte Bibliotheken aus C/C++/Rust lassen sich ohne komplette Neuimplementierung in Webanwendungen nutzen.
- **Erweiterbarkeit (WASI):** Über Schnittstellen wie das WebAssembly System Interface (WASI) können WebAssembly-Module außerhalb des Browsers in Cloud- oder Edge-Umgebungen betrieben werden (im Browser nicht verfügbar).

Damit adressiert WebAssembly zentrale Herausforderungen moderner Softwareentwicklung: heterogene Plattformlandschaften, steigende Anforderungen an Performance und Sicherheit sowie der Bedarf an portablen, wiederverwendbaren Komponenten.


---


## **Typische Anwendungsfälle**

WebAssembly wird in modernen Web- und Cloud-Architekturen zunehmend eingesetzt. Es eignet sich für eine leistungsfähige, sichere und portable Ausführung komplexer Anwendungen. Die folgende Kategorisierung fasst wichtige Einsatzfelder zusammen:

| Anwendungsfall | Beschreibung |
| :--- | :--- |
| **Datenintensive Anwendungen** | Verarbeitung großer Datenmengen (z. B. Geodatenanalyse, wissenschaftliche Simulationen) direkt auf dem Client. |
| **Portierung bestehender Software** | Wiederverwendung von in C/C++ oder Rust geschriebenen Modulen in Webumgebungen, ohne diese neu implementieren zu müssen. So lassen sich etablierte und optimierte Codebasen weiterverwenden. |
| **Interaktive Visualisierungen** | Rendering von 3D-Grafiken und komplexen visuellen Elementen oder Karten mit hoher Bildrate und geringer Latenz. |
| **Clientseitige Berechnungen** | Verlagerung von Rechenlogik vom Server auf den Browser zur Reduzierung von Latenz und Serverlast durch Auslagerung. |
| **Sichere Plugin-Systeme** | Ausführung von Fremdcode in isolierten WebAssembly-Sandboxes, etwa für benutzerdefinierte Analysen oder Erweiterungen. Das strikte Speichermodell unterstützt die Sicherheit. |

Zudem ist festzuhalten, dass WebAssembly nicht nur eine Performance-Optimierung darstellt, sondern eine architektonische Option zur Gestaltung verteilter, portabler und sicherer Softwaresysteme bietet.


---


## **Relevante Bibliotheken und Tools**

Die folgenden Bibliotheken und Tools bilden die technische Grundlage für den Einsatz von WebAssembly im Kontext geospatialer Webanwendungen. Sie ermöglichen die effiziente Portierung, Ausführung und Integration von Geodatenverarbeitung und STAC-bezogenen Funktionen direkt im Browser.

| Kategorie | Name | Beschreibung |
| :--- | :--- | :--- |
| **Wasm Geospatial Core** | [**GEOS-WASM**](https://chrispahm.github.io/geos-wasm) | WebAssembly-Build der C++-Geospatial-Bibliothek GEOS. Ermöglicht Low-Level-Geometrieoperationen mit nahezu nativer Performance. Essenziell für die effiziente Verarbeitung der STAC-Item-Geometrien. |
| **Build- & Toolchains** | [**wasm-pack**](https://github.com/rustwasm/wasm-pack) | Toolchain für die Kompilierung von Rust-Code nach WebAssembly und die Generierung der JavaScript-Schnittstellen. |
| **Build- & Toolchains** | [**Emscripten**](https://emscripten.org)| Standard-Toolchain zur Kompilierung von C/C++-Code nach WebAssembly. Essenziell für die Portierung etablierter C-Bibliotheken. |
| **Wasm STAC Utility** | [**stac-rs**](https://github.com/stac-utils/stac-rs) | Rust-Implementierung der STAC-Spezifikation, die nach WebAssembly kompiliert werden kann und clientseitig im Browser einsetzbar ist. Ermöglicht das effiziente Parsen, Validieren und Erstellen von STAC-Metadaten auf dem Client, wodurch serverseitige STAC-Verarbeitung und zusätzliche API-Latenzen entfallen. |
| **Wasm Datenbank/Index** | [**SQL.js**](https://sql.js.org) | Ermöglicht die Bereitstellung einer vollständigen SQL-Datenbank zur Speicherung und schnellen Abfrage von Metadaten-Caches direkt im Browser. Relevant für die komplexe Suche in STAC-Katalogen. |


---


## **Konkrete Applikationsbeispiele**

Die breite Akzeptanz von WebAssembly in der Industrie dient als Beleg für seine Leistungsfähigkeit. Große Technologieunternehmen nutzen WebAssembly, um Desktop-Anwendungen ins Web zu portieren:

| Anwendung | Beschreibung | Relevanz |
| :--- | :--- | :--- |
| **Google Earth Web** | Führt rechenintensive 3D-Geometrie- und Terrainberechnungen im Browser mithilfe von WebAssembly (kompiliert aus C++) aus. In Kombination mit WebGL ermöglicht dies ein flüssiges, interaktives 3D-Erlebnis globaler Geodaten  [(vgl. Mears, 2019)](https://web.dev/case-studies/earth-webassembly?hl=de). | Beispiel für 3D-Visualisierung und Geodatenverarbeitung mit nativer Performance im Web. |
| **Figma** | Kollaborative Design-Plattform, die WebAssembly nutzt, um komplexe Vektor- und Pixeldaten effizient im Browser zu verarbeiten. Dadurch wird flüssiges, latenzarmes Arbeiten an großen Designprojekten ermöglicht [(vgl. Wallace, 2017)](https://www.figma.com/blog/webassembly-cut-figmas-load-time-by-3x/). | Beispiel für leistungsfähige Client-seitige Anwendungen mit rechenintensiver Logik. |
| **AutoCAD Web** | Führt den ursprünglich in C++ implementierten CAD-Kern mithilfe von WebAssembly direkt im Browser aus. So wird präzises 2D/3D-Rendering ohne lokale Installation möglich [(vgl. O’Brien, 2018)](https://www.autodesk.com/blogs/autocad/autocad-web-app-google-io-2018/). | Demonstriert die Portierung komplexer Desktop-Software in leistungsfähige, webbasierte Umgebungen. |


---


## **WebAssembly vs JavaScript**

Obwohl beide Technologien zentral für das moderne Web sind und häufig zusammenarbeiten, erfüllen sie unterschiedliche Rollen:

- JavaScript eignet sich hervorragend für die allgemeine Webentwicklung und insbesondere für interaktive Aufgaben wie die DOM-Manipulation.

- Für einfache Aufgaben, etwa die Weiterleitung von URLs, ist JavaScript einfacher und bequemer zu verwenden.

- WebAssembly kommt überall dort zum Einsatz, wo JavaScript an Leistungsgrenzen stößt, zum Beispiel bei rechenintensiven Aufgaben wie der 
clientseitigen Bildkompression.

- Während JavaScript eine Programmiersprache ist, dient WebAssembly als Kompilierungsziel für andere Sprachen.

- Auch im Bereich des Edge Computings dominiert JavaScript (z.B. für Routing oder Request-Handling) bei Anbietern wie Cloudflare Workers [(vgl. Cloudflare Inc., o.J.)](https://developers.cloudflare.com/workers/runtime-apis/webassembly/) oder Deno Deploy [(vgl. Deno Land Inc., o.J.)](https://docs.deno.com/runtime/reference/wasm/). WebAssembly gewinnt dort jedoch zunehmend an Bedeutung, um rechenintensive Module performant auszuführen, die mit reinem JavaScript zu langsam wären.

Zusammengefasst besteht keine Konkurrenz zwischen JavaScript und WebAssembly. Beide ergänzen sich. WebAssembly profitiert von der Interoperabilität mit JavaScript, da so eine optimale Einbindung in den Browser möglich ist.


---


## **Fazit**

WebAssembly ist mehr als eine Performance-Optimierung, es ist eine architektonische Schlüsseltechnologie, die Softwarearchitekturen nachhaltig verändert.

Für die Geosoftware-Entwicklung und insbesondere STAC-basierte Anwendungen bietet WebAssembly entscheidende Vorteile: nahezu native Performance für rechenintensive GIS-Operationen, Entlastung der Server durch clientseitige Berechnungen, Wiederverwendung bestehender Bibliotheken und plattformübergreifende Portabilität.

WebAssembly ersetzt JavaScript nicht, sondern ergänzt es. Die Kombination beider Technologien ermöglicht leistungsfähige, skalierbare und sichere Webarchitekturen für moderne Geodatenanwendungen.


---


# **Quellen**

- Haas, A. et al. (2017): Bringing the Web up to Speed with WebAssembly. https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf (Zuletzt aufgerufen am 14.10.2025).

- Fraunhofer IESE (o. J.): WebAssembly: Grundlagen von Wasm. https://www.iese.fraunhofer.de/blog/webassembly-grundlagen-von-wasm/ (Zuletzt aufgerufen am 14.10.2025).

- developer.mozilla.org (o. J.): WebAssembly. MDN Web Docs. https://developer.mozilla.org/en-US/docs/WebAssembly (Zuletzt aufgerufen am 14.10.2025).

- Rossberg, A. (2025): WebAssembly Specification Release 3.0. (Wurde als lokale Datei übermittelt, kann aber über die Community Group bezogen werden). https://webassembly.org/ (Zuletzt aufgerufen am 14.10.2025).

- Schmid, F. et al. (2020): Unleashing the Power of WebAssembly. https://www.software-lab.org/publications/usenixSec2020-WebAssembly.pdf (Zuletzt aufgerufen am 14.10.2025).

- webassembly.org (o. J.): WebAssembly Homepage. https://webassembly.org/ (Zuletzt aufgerufen am 14.10.2025).

- Healey, A. (2020). WebAssembly Search Tools for Static Sites. https://healeycodes.com/webassembly-search-tools-for-static-websites (Zuletzt aufgerufen am 14.10.2025).

- Chrispahm. (2024). GEOS-WASM. GitHub Page. https://chrispahm.github.io/geos-wasm/ (Zuletzt aufgerufen am 14.10.2025).

- The Rust and WebAssembly Working Group (o. J.): wasm-pack. GitHub Repository. https://github.com/rustwasm/wasm-pack (Zuletzt aufgerufen am 05.02.2026).

- Emscripten Contributors (o. J.): Emscripten: A complete WebAssembly & asm.js toolchain. https://emscripten.org/ (Zuletzt aufgerufen am 05.02.2026).

- stac-utils (o. J.): stac-rs: Rust implementation of the SpatioTemporal Asset Catalog (STAC) specification. GitHub Repository. https://github.com/stac-utils/stac-rs (Zuletzt aufgerufen am 05.02.2026).

- SQL.js Community (o. J.): SQL.js: SQLite compiled to WebAssembly. https://sql.js.org/ (Zuletzt aufgerufen am 05.02.2026).

- De Melo, L. (2024). Real-Time Geospatial Intelligence: Leveraging Rust WebAssembly and Predictive AI for Browser-Based Spatial Queries. https://medium.com/@LeonardoDeMeloWeb/real-time-geospatial-intelligence-leveraging-rust-webassembly-and-predictive-a608ca5ed7c2 (Zuletzt aufgerufen am 14.10.2025).

- Mears, J. (2019): Google Earth on WebAssembly. https://web.dev/case-studies/earth-webassembly?hl=de (Zuletzt aufgerufen am 05.02.2026).

- Wallace, E. (2017): WebAssembly cut Figma's load time by 3x. https://www.figma.com/blog/webassembly-cut-figmas-load-time-by-3x/ (Zuletzt aufgerufen am 05.02.2026).

- O'Brien, M. (2018): The AutoCAD Web App: Google I/O 2018. https://www.autodesk.com/blogs/autocad/autocad-web-app-google-io-2018/ (Zuletzt aufgerufen am 05.02.2026).

- Cloudflare Inc. (o. J.): WebAssembly (Wasm) in Workers. Cloudflare Developers Docs. https://developers.cloudflare.com/workers/runtime-apis/webassembly/ (Zuletzt aufgerufen am 05.02.2026).

- Deno Land Inc. (o. J.): WebAssembly in Deno. Deno Docs. https://docs.deno.com/runtime/reference/wasm/ (Zuletzt aufgerufen am 05.02.2026).
