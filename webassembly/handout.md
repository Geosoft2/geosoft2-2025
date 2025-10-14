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

# **Quellen**

- Haas, A. et al. (2017): Bringing the Web up to Speed with WebAssembly. https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf (Zuletzt aufgerufen am 14.10.2025).

- Fraunhofer IESE (o. J.): WebAssembly: Grundlagen von Wasm. https://www.iese.fraunhofer.de/blog/webassembly-grundlagen-von-wasm/ (Zuletzt aufgerufen am 14.10.2025).

- developer.mozilla.org (o. J.): WebAssembly. MDN Web Docs. https://developer.mozilla.org/en-US/docs/WebAssembly (Zuletzt aufgerufen am 14.10.2025).

- Rossberg, A. (2025): WebAssembly Specification Release 3.0. (Wurde als lokale Datei übermittelt, kann aber über die Community Group bezogen werden). https://webassembly.org/ (Zuletzt aufgerufen am 14.10.2025).

- Schmid, F. et al. (2020): Unleashing the Power of WebAssembly. https://www.software-lab.org/publications/usenixSec2020-WebAssembly.pdf (Zuletzt aufgerufen am 14.10.2025).

- webassembly.org (o. J.): WebAssembly Homepage. https://webassembly.org/ (Zuletzt aufgerufen am 14.10.2025).