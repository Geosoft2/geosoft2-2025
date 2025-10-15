[@Benno01], [@Denkorsch]

# **WebAssembly**

---

## **Idee und Zielsetzung**

### **Idee**

WebAssembly ist ein kompaktes Programmformat, das moderne Browser direkt ausführen können. Damit lassen sich Anwendungen, die ursprünglich in Sprachen wie C, C++ oder Rust geschrieben wurden, im Browser nutzen. Ziel ist es, rechenintensive Aufgaben schnell und zuverlässig im Web auszuführen, ohne die Sicherheitsprinzipien des Webs zu verletzen.

Im Browser läuft WebAssembly in einem sicheren, abgeschotteten Bereich. Der Code hat keinen direkten Zugriff auf die Webseite oder Web-APIs. Wenn eine Interaktion mit der Seite nötig ist, stellt JavaScript die Verbindung zwischen WebAssembly und der Anwendung her.

WebAssembly ergänzt JavaScript und ersetzt es nicht. JavaScript bleibt wichtig für die Benutzeroberfläche und die allgemeine Anwendungslogik. WebAssembly kommt dort zum Einsatz, wo viel Rechenleistung oder eine besonders effiziente Ausführung benötigt wird.

---

### **Zielsetzung** 

Die Hauptziele von WebAssembly lassen sich wie folgt zusammenfassen:

- **Effizienz:** Rechenintensive Aufgaben (z.B. Bildverarbeitung oder Simulationen) laufen im Browser nahe an nativer Geschwindigkeit. Das eignet sich für leistungskritische Module. Übergänge zwischen JavaScript und WebAssembly sowie Datenkopien können die Performance mindern.
- **Portabilität:** Ein WebAssembly-Modul verhält sich über verschiedene Plattformen hinweg konsistent, sowohl im Browser als auch auf Servern und am Netzwerkrand (Edge).
- **Sicherheit:** Striktes Sandboxing und Validierung des Binärcodes verhindern unkontrollierten Zugriff auf Host-Ressourcen.
- **Wiederverwendbarkeit:** Etablierte Bibliotheken aus C/C++/Rust lassen sich ohne komplette Neuimplementierung in Webanwendungen nutzen.
- **Erweiterbarkeit (WASI):** Über Schnittstellen wie das WebAssembly System Interface (WASI) können WebAssembly-Module außerhalb des Browsers in Cloud- oder Edge-Umgebungen betrieben werden (im Browser nicht verfügbar).

Damit adressiert WebAssembly zentrale Herausforderungen moderner Softwareentwicklung: heterogene Plattformlandschaften, steigende Anforderungen an Performance und Sicherheit sowie der Bedarf an portablen, wiederverwendbaren Komponenten.

## **Typische Anwendungsfälle**

WebAssembly wird in modernen Web- und Cloud-Architekturen zunehmend eingesetzt. Es eignet sich für eine leistungsfähige, sichere und portable Ausführung komplexer Anwendungen. Die folgende Kategorisierung fasst wichtige Einsatzfelder zusammen:

### Wichtige Einsatzfelder

| Feld | Beschreibung & Vorteile |
| :--- | :--- |
| **Datenintensive Anwendungen** | Verarbeitung großer Datenmengen (z.B. Geodatenanalyse, wissenschaftliche Simulationen) direkt auf dem Client. |
| **Portierung bestehender Software** | Wiederverwendung von in C/C++ oder Rust geschriebenen Modulen in Webumgebungen, ohne diese neu implementieren zu müssen. So lassen sich etablierte und optimierte Codebasen weiterverwenden. |
| **Interaktive Visualisierungen** | Rendering von 3D-Grafiken und komplexen visuellen Elementen oder Karten mit hoher Bildrate und geringer Latenz. |
| **Clientseitige Berechnungen** | Verlagerung von Rechenlogik vom Server auf den Browser zur Reduzierung von Latenz und Serverlast durch Auslagerung. |
| **Sichere Plugin-Systeme** | Ausführung von Fremdcode in isolierten WebAssembly-Sandboxes, etwa für benutzerdefinierte Analysen oder Erweiterungen. Das strikte Speichermodell unterstützt die Sicherheit. |

Zudem ist festzuhalten, dass WebAssembly nicht nur eine Performance-Optimierung darstellt, sondern eine architektonische Option zur Gestaltung verteilter, portabler und sicherer Softwaresysteme bietet.

## Relevante Bibliotheken und Tools

| Kategorie | Name | Beschreibung |
| :--- | :--- | :--- |
| **Wasm Geospatial Core** | **GEOS-WASM** | WebAssembly-Build der C++ Geospatial Library GEOS. Ermöglicht Low-Level-Geometrieoperationen mit Near-Native-Performance. Essenziell für die effiziente Verarbeitung der STAC Item-Geometrien. |
| **Wasm Geospatial Tools** | **wasm-pack** | Die zentrale Toolchain für die Kompilierung von Rust-Code nach WebAssembly und die Generierung der JavaScript-Schnittstellen. |
| **Wasm Geospatial Tools** | **Emscripten** | Standard-Toolchain zur Kompilierung von C/C++-Code nach Wasm. Essentiell für die Portierung etablierter C-Bibliotheken. |
| **STAC Utility (Backend)** | **PySTAC**, **stac-fastapi** | Frameworks zur Erstellung, Validierung und Bereitstellung von STAC Katalogen. Liefern die optimierte Datengrundlage für die clientseitige Wasm-optimierte Suche. |

---

## 4. Fazit

### Fazit

WebAssembly ist eine architektonische Schlüsseltechnologie für die moderne Geosoftware-Entwicklung, insbesondere im Umgang mit STAC.

1.  **Performance:** Wasm schließt die Performancelücke von JavaScript, indem es GIS-typische, rechenintensive Operationen im Browser mit Near-Native-Performance ermöglicht.
2.  **Skalierbarkeit & Kosteneffizienz:** Durch die Auslagerung der Rechenlast auf den Client entlastet Wasm die STAC API Server. Dies ist entscheidend für die Skalierbarkeit im Umgang mit großen STAC-Katalogen.
3.  **Wiederverwendung:** Wasm ermöglicht es, etablierte, hochoptimierte GIS-Bibliotheken direkt im Web wiederzuverwenden.



---




# **Quellen**

- Haas, A. et al. (2017): Bringing the Web up to Speed with WebAssembly. https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf (Zuletzt aufgerufen am 14.10.2025).

- Fraunhofer IESE (o. J.): WebAssembly: Grundlagen von Wasm. https://www.iese.fraunhofer.de/blog/webassembly-grundlagen-von-wasm/ (Zuletzt aufgerufen am 14.10.2025).

- developer.mozilla.org (o. J.): WebAssembly. MDN Web Docs. https://developer.mozilla.org/en-US/docs/WebAssembly (Zuletzt aufgerufen am 14.10.2025).

- Rossberg, A. (2025): WebAssembly Specification Release 3.0. (Wurde als lokale Datei übermittelt, kann aber über die Community Group bezogen werden). https://webassembly.org/ (Zuletzt aufgerufen am 14.10.2025).

- Schmid, F. et al. (2020): Unleashing the Power of WebAssembly. https://www.software-lab.org/publications/usenixSec2020-WebAssembly.pdf (Zuletzt aufgerufen am 14.10.2025).

- webassembly.org (o. J.): WebAssembly Homepage. https://webassembly.org/ (Zuletzt aufgerufen am 14.10.2025).

- Healey, A. (2020). WebAssembly Search Tools for Static Sites. [healeycodes.com.](https://healeycodes.com/webassembly-search-tools-for-static-websites) (Zuletzt aufgerufen am 14.10.2025).

- Chrispahm. (2024). GEOS-WASM. GitHub Page. https://chrispahm.github.io/geos-wasm/ (Zuletzt aufgerufen am 14.10.2025).

- De Melo, L. (2024). Real-Time Geospatial Intelligence: Leveraging Rust WebAssembly and Predictive AI for Browser-Based Spatial Queries. [Medium.](https://medium.com/@LeonardoDeMeloWeb/real-time-geospatial-intelligence-leveraging-rust-webassembly-and-predictive-ai-for-browser-based-a608ca5ed7c2) (Zuletzt aufgerufen am 14.10.2025).

- STAC Specification. (2024). Create a STAC Catalog with a Collection Using PySTAC. [stacspec.org.](https://stacspec.org/en) (Zuletzt aufgerufen am 14.10.2025).

- Sparkgeo. (2024). Introducing stac-fastapi-indexed: Low Overhead STAC Metadata Support. [Sparkgeo Blog.](https://sparkgeo.com/blog/introducing-stac-fastapi-indexed-low-overhead-stac-metadata-support/) (Zuletzt aufgerufen am 14.10.2025).
