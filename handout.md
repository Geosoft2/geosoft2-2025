# Container/Docker
---
[@SonkeHoffmann](https://github.com/SonkeHoffmann), [@Luisa-SP](https://github.com/Luisa-Sp)

## Was ist Containerisierung?

**Definition:**  
Containerisierung ist eine Methode, um Softwareanwendungen samt ihren Abhängigkeiten (Bibliotheken, Laufzeitumgebung, Konfigurationen) in isolierten, leichtgewichtigen Umgebungen – den Containern – auszuführen.

**Wichtig, weil:**

- **Portabilität:** Container laufen überall gleich – ob auf dem Laptop, Server oder in der Cloud.  
- **Konsistenz:** „It works on my machine“ gehört der Vergangenheit an – Container garantieren identische Umgebungen.  
- **Effizienz:** Container teilen sich den Kernel des Host-Systems, was sie ressourcenschonender als virtuelle Maschinen macht.  
- **Skalierbarkeit & Agilität:** Ideal für Microservices – Anwendungen können leicht skaliert, aktualisiert oder ausgetauscht werden.  
- **Isolation & Sicherheit:** Container sind voneinander getrennt; Fehler oder Abstürze in einem Container beeinflussen andere nicht.

---

## Docker

### Grundlagen von Docker

Docker ist die bekannteste Plattform zur Containerisierung.  
Sie bietet Werkzeuge, um Container zu erstellen, zu verteilen und auszuführen.

**Zentrale Konzepte:**

| Begriff | Erklärung |
|----------|------------|
| **Docker Image** | Eine Vorlage (Snapshot) mit allem, was eine Anwendung braucht – Code, Laufzeit, Bibliotheken. |
| **Docker Container** | Eine laufende Instanz eines Images. |
| **Dockerfile** | Eine Textdatei mit Anweisungen, wie ein Image gebaut wird. |
| **Docker Hub** | Eine öffentliche Registry, in der Images gespeichert und geteilt werden. |
| **Docker Engine** | Die Laufzeitumgebung, die Container startet und verwaltet. |

**Beispiel:**
```bash
# Image bauen
docker build -t myapp .

# Container starten
docker run -p 8080:80 myapp

```

### Typische Anwendungsfälle für Docker

**Entwicklung & Test (Development & Testing)**

Einheitliche Entwicklungsumgebung
Entwickler arbeiten oft mit unterschiedlichen Betriebssystemen und Toolchains.
→ Docker schafft identische Umgebungen für alle.

```bash
docker run -it -v $(pwd):/app python:3.11 bash

#Schnelle lokale Tests

docker run --rm -d -p 5432:5432 postgres:latest
```

**Continuous Integration (CI)**

Container werden in CI/CD-Pipelines (z. B. GitLab CI, GitHub Actions, Jenkins) genutzt.
→ Saubere, reproduzierbare Build-Umgebungen.

**Vorteile:**
- Keine Abhängigkeiten zwischen Builds
- Leichtgewichtiges Spin-up / Tear-down
- Standardisierte Toolchains

```bash
docker build -t myapp:v1 .
docker push myrepo/myapp:v1
docker run myrepo/myapp:v1
```
### Microservices-Architekturen

Jede Komponente läuft in ihrem eigenen Container (z. B. Webserver, Datenbank, Auth-Service, Cache).

**Vorteile:**
- Kapselung & Isolation
- Unabhängige Skalierung & Updates
- Einfache Rollbacks (versionierte Images)
- Orchestrierung mit Docker Compose, Kubernetes etc.

### Container-Orchestrierung
Docker ist Basis für Kubernetes, OpenShift, Docker Swarm, AWS ECS u. a.

**Vorteile:**
- Automatische Skalierung
- Self-healing
- Load Balancing
- Rolling Updates
- Images als „Portable Binaries“

### Images als „Portable Binaries“
Docker-Images enthalten alles, was eine App braucht.
→ Eine Art „Software-Container“ wie ein ZIP-Archiv mit garantierter Laufzeitumgebung.

```bash
docker run nginx
```

### Alte Anwendungen modernisieren

```bash
FROM tomcat:9-jdk17
COPY app.war /usr/local/tomcat/webapps/
```

**Vorteile:**
- Betrieb in Cloud-Umgebungen ohne Codeänderungen
- Schrittweiser Übergang zu Microservices

### Schulung, Demonstration & Prototyping
Ideal für Demos, Workshops und Bildung.

```bash
docker run -d -p 8080:80 nginx
```

## Container vs. Virtuelle Maschinen (VMs)
Architektur – wo wird isoliert?
```bash
[Hardware]
 ├─ [Host-OS]
 │    └─ [Container-Laufzeit (z. B. Docker)]
 │         └─ [Container A] [Container B] ...

[Hardware]
 └─ [Hypervisor]
      ├─ [Gast-OS 1] └─ [App(s)]
      ├─ [Gast-OS 2] └─ [App(s)]
```

- Container: Isolieren auf OS-/Prozess-Ebene (Namespaces, Cgroups).
- VMs: Isolieren auf Hardware-Ebene über Hypervisor.

**Fazit:** Container sind leichter und starten schneller, VMs bieten stärkere Isolation.

### Startzeit, Dichte & Overhead

| **Kategorie**       | **Container**     | **Virtuelle Maschinen** |
|----------------------|------------------|--------------------------|
| **Startzeit**        | Sekunden         | Minuten                  |
| **Ressourcendichte** | Hoch             | Gering                   |
| **Performance**      | Nahe nativ       | Minimaler Overhead       |

### Isolation & Sicherheit

**Container:**
- Isolationsmechanismen: Namespaces, cgroups, AppArmor/SELinux, Rootless Mode
- Risiko: Shared Kernel → Kernel-Exploits könnten mehrere Container betreffen
- Abhilfe: Minimal-Images, Non-Root-User, signierte Images, Network Policies

**VMs:**

- Eigener Kernel → stärkere Tenant-Trennung
- Gut für Multi-Tenancy und unsichere Binaries

Merksatz:
Container meist sicher genug für interne Nutzung, VMs für fremde Tenants.

### Betrieb & Lebenszyklus (Ops)

**Container-Flow:**
Build → Image → Run (ephemer)
→ Updates über Compose/Kubernetes automatisierbar.

**VM-Flow:**
Golden Images + Konfigurationsmanagement
→ Schwerfälliger, aber robuster für komplexe Systeme.

### Portabilität & Kompatibilität

- Container: Portabel über Hosts/Clouds, aber Kernel-abhängig

- VMs: Komplettes OS – portabel über Hypervisor

### Speicher & Persistenz

- Container: Layered File System (Copy-on-Write), Volumes

- VMs: Virtuelle Platten (Snapshots, Live-Migration)

### Netzwerk

- Container: Bridge/NAT, Overlay, Service Discovery, Network Policies

- VMs: VLANs/SDN – traditioneller, aber weniger automatisiert

### Observability & Troubleshooting

- Container: Standardisierte Logs (stdout/stderr), Prometheus, OpenTelemetry

- VMs: Klassische Agenten und OS-spezifische Logs

### Kosten & Lizenzierung

- Container: Ressourceneffizient, keine zusätzlichen OS-Lizenzen

- VMs: Lizenzkosten und Management-Overhead

### Typische Einsatzszenarien

- Container prädestiniert für:
- Microservices (API, Auth, Frontend)
- CI/CD-Runner
- Datenverarbeitung / ETL
- GIS-Stacks (PostGIS, GeoServer, Tile-Server)
- Autoscaling / Event-getriebene Workloads

**VMs prädestiniert für:**

- Strikte Mandantentrennung
- Legacy-/Monolith-Anwendungen
- Kernel-/Treiber-abhängige Software
- Compliance-Anforderungen

**Hybride Muster:**

- Container in VMs: Standard in der Cloud (z. B. Kubernetes-Worker in VMs)
- MicroVMs (Firecracker): Leichte VMs für Serverless/FaaS

### Praxis-Guidelines

| **Szenario**                     | **Empfehlung**                 |
|----------------------------------|--------------------------------|
| **Microservices & CI/CD**        | Container                      |
| **Strikte Mandantentrennung**    | VM oder MicroVM                |
| **Legacy / Treiberlastig**       | VM                             |
| **Kurze Build- / Test-Jobs**     | Container                      |
| **Hoch stateful + Migration**    | VM                             |
| **Hohe Sicherheitsanforderungen**| gVisor / Kata / Firecracker    |


## Beispielhafte GIS-Architektur mit Containern

In einer typischen containerisierten GIS-Umgebung könnten folgende Komponenten eingesetzt werden:

- **PostGIS** (Datenbank)
- **GeoServer** (WMS/WFS-Dienste)
- **MapProxy** oder **TileServer** (Caching)
- **Frontend** (z. B. React / Leaflet)

**Vorteile:**
Jeder Dienst läuft in seinem eigenen Container, ist skalierbar, updatesicher und reproduzierbar.  
So lassen sich komplexe GIS-Systeme modular und wartungsfreundlich betreiben.

**Alternative (VM-basiert):**
Ein Monolith mit allen Komponenten in einer einzelnen virtuellen Maschine – geeignet für Legacy-Systeme oder Umgebungen mit strikter Segmentierung.


---

## Podman – Eine Alternative zu Docker

**Was ist Podman?**

Podman (Pod Manager) ist ein containerbasiertes Tool von Red Hat, das – ähnlich wie Docker – Container erstellt, verwaltet und ausführt.
Es ist vollständig kompatibel mit Docker-Images und Dockerfiles, aber verfolgt einen etwas anderen Ansatz in Architektur und Sicherheit.
Außerdem ist Podman komplett Open Source und steht unter einer Apache 2.0-Lizenz, was es besonders für Forschung, Lehre und offene Softwareprojekte attraktiv macht.

### Grundlagen von Podman

Podman ist ein Tool zur Erstellung, Verwaltung und Ausführung von Containern – ganz ohne zentralen Daemon.  
Es arbeitet nach dem gleichen **Image → Container**-Prinzip wie Docker und nutzt dabei dieselben **OCI-Standards** (Open Container Initiative).

### Zentrale Konzepte

| **Begriff** | **Erklärung** |
|--------------|---------------|
| **Container Image** | Eine unveränderliche Vorlage (Snapshot) mit allem, was eine Anwendung braucht – Code, Laufzeit, Bibliotheken, Konfiguration. Kompatibel mit Docker-Images. |
| **Container** | Eine laufende Instanz eines Images. Podman startet diese direkt als Benutzerprozess, ohne zentralen Hintergrunddienst (`dockerd`). |
| **Pod** | Eine logische Gruppe mehrerer Container, die sich Netzwerk und Speicher teilen – identisch zum Kubernetes-Pod-Modell. |
| **Containerfile (Dockerfile-kompatibel)** | Eine Textdatei mit Anweisungen, wie ein Image gebaut wird (`podman build` nutzt sie wie Docker). |
| **Registry** | Öffentliche oder private Container-Registries (z. B. Docker Hub, Quay.io, GHCR), aus denen Images heruntergeladen werden können. |
| **Podman Engine** | Die eigentliche Laufzeit – sie führt Containerprozesse direkt aus, ohne Daemon. Unterstützt Rootless- und Root-Modus. |

---

### Beispiel

```bash
# Image bauen (Dockerfile-kompatibel)
podman build -t myapp .

# Container starten
podman run -p 8080:80 myapp

```

### Wichtige Unterschiede zu Docker

| **Aspekt** | **Docker** | **Podman** |
|-------------|-------------|-------------|
| **Daemon** | Läuft mit einem zentralen Daemon-Prozess (`dockerd`) | Kein zentraler Daemon – Prozesse laufen direkt als Subprozesse |
| **Rootless Mode** | Unterstützt, aber optional und teils eingeschränkt | Standardmäßig rootless, sehr sicher |
| **Kompatibilität** | Eigenes CLI & Engine | CLI ist Docker-kompatibel (`alias docker=podman`) |
| **Systemintegration** | Nutzt Docker Compose oder Swarm | Nutzt `pods` (wie in Kubernetes) und Systemd-Integration |
| **Sicherheit** | Root-Prozess kann Angriffsfläche bieten | Besser durch Rootless, User-Namespace & SELinux |
| **Orchestrierung** | Docker Compose / Swarm / Kubernetes | Pods nativ wie in Kubernetes, unterstützt `podman kube generate` |
| **API / Remote Control** | Docker-API (REST) | Podman-API (Socket, kompatibel mit Docker-Clients) |

### Beispiel für gleiche Befehle wie bei Docker

Podman ist CLI-kompatibel mit Docker, d. h. du kannst fast alle Docker-Befehle identisch verwenden:
```bash
podman build -t myapp .
podman run -p 8080:80 myapp
podman ps
podman images

# man kann auch
alias docker=podman
# nutzen und die Docker-Workflows direkt weiterverwenden
```
### Pods und Kubernetes

Ein Pod ist eine logische Gruppe mehrerer Container, die sich Netzwerk und Speicher teilen – genauso wie im Kubernetes-Modell.
Damit ist Podman besonders gut geeignet für lokale Kubernetes-nahe Entwicklung.

Beispiel:
```bash
podman pod create --name mypod -p 8080:80
podman run --pod mypod nginx
podman run --pod mypod redis
```
### Integration mit Systemd

Podman kann automatisch Systemd-Service-Dateien generieren, um Container oder Pods als Linux-Services zu starten.Das macht es ideal für serverseitige Deployments ohne Docker-Daemon.

### Kompatibilität & Ecosystem

- Nutzt dieselben OCI-Standards (Open Container Initiative) wie Docker
- Arbeitet mit denselben Container-Registries (z. B. Docker Hub, Quay.io, GHCR)
- Läuft auf Linux, macOS und Windows (über WSL2)

### Wann ist Podman sinnvoll?

- **Sichere Rootless-Umgebungen:**  
  Podman läuft standardmäßig ohne Root-Rechte und bietet dadurch ein höheres Sicherheitsniveau
- **Linux-Server ohne Docker-Daemon:**  
  Ideal für Systeme, auf denen kein dauerhaft laufender Daemon-Prozess erwünscht ist
- **Kubernetes-nahe Entwicklung / Pods:**  
  Podman arbeitet mit demselben Pod-Konzept wie Kubernetes – ideal für lokale Tests und Entwicklung
- **Bestehende Docker-Workflows:**  
  CLI-kompatibel – vorhandene Docker-Befehle und Workflows können fast unverändert genutzt werden (`alias docker=podman`)
- **Windows- oder macOS-Entwicklung mit Desktop-Integration:**  
  Docker Desktop bietet hier oft eine komfortablere Integration, während Podman etwas mehr Setup-Aufwand benötigt

---

  # Quellen
Die vollständigen Quellen und weiterführende Literatur zu Docker, Containerisierung und Podman  
finden sich in der separaten Datei: [sources.md](./sources.md)