[handout.md](https://github.com/user-attachments/files/22926116/handout.md)
@<VincentKuehn>

# Testing – Test-Driven Development; Unit vs. Integration Testing; Common Test Software

## 1. Introduction / Motivation

Den eigenen Code zu testen ist immer sinnvoll. In der Softwareentwicklung und gerade bei Geosoftware-Projekten ist das Testen allerdings besonders wichtig: Viele Komponenten (Datenbank, API, STAC Index, …) treffen auf viele verschiedene Datenformate. Das erhöht die Fehleranfälligkeit. Testen verschafft dabei Vertrauen in die Funktionalität und verbessert die Reproduzierbarkeit sowie die Wartbarkeit.

## 2. The Test Pyramid

Die Test-Pyramide wird oft genutzt, um die Balance zwischen den verschiedenen Testtypen zu visualisieren.

- Unit Tests: testen einzelne Komponenten oder Funktionen (Funktionen, Klassen, Methoden).
- Integration Tests: testen, wie mehrere Komponenten zusammenarbeiten (z. B. API + Datenbank).
- End-to-End Tests: testen das System als Ganzes über Benutzer- oder API-Schnittstellen.

In Bezug auf die Test-Pyramide: Insgesamt viele kleine und schnelle Unit-Tests, ein paar gröbere Integration Tests und nur ganz wenige Tests mit hohem Niveau, die das gesamte System End-to-End testen. Schwere End-to-End Tests sind weniger praktikabel für frühe Phasen der Projektentwicklung. Unit- und Integration Tests sind effizienter. End-to-End Tests werden erst in der Systemvalidierung wertvoll.

Quelle: Fowler, M. (2012). The Practical Test Pyramid. MartinFowler.com. https://martinfowler.com/articles/practical-test-pyramid.html

## 3. Test-Driven Development (TDD)

### 3.1 Grundidee

Tests werden vor dem Code geschrieben. TDD folgt einem einfachen Zyklus: Red-Green-Refactor.

Red: Zu einem gewollten Feature der Software wird ein Test geschrieben, der zunächst scheitert, weil das Feature noch nicht implementiert ist. Der Test braucht die neue Funktionalität, um zu bestehen.

Green: Minimalen Code schreiben, der genau dieses Feature implementiert. Der Test soll so schnell und einfach wie möglich bestehen. Kein Fokus auf „schönen“ Code.

Refactor: Wenn der Test besteht, Code umgestalten, um Struktur und Qualität zu verbessern. Duplikate entfernen, Code dahin bewegen, wo er hingehört, selbsterklärende Namen verwenden, Methoden in kleinere Teile spalten usw. Dabei darauf achten, dass der Test weiterhin besteht.

### 3.2 Warum TDD

- Softwarequalität: Änderungen im Nachhinein einfacher, Code zuverlässiger, einfachere Pflege.
- Besseres Debugging: Schnelleres Debugging im weiteren Verlauf.
- Höhere Qualität der Schnittstellen: Tests vor dem Code zwingen dazu, das Verhalten vor der Implementierung zu definieren (wie wird Funktion oder API von außen benutzt, welche Parameter und Rückgaben braucht sie, wie soll der Output aussehen). Die API wird gezielt entworfen, Tests definieren das gewünschte Verhalten und bilden automatisch eine Dokumentation.
- Allerdings: TDD muss gelernt und geübt werden. Es kann die frühen Phasen der Softwareentwicklung verlangsamen, auch wenn es hinterher viel Zeit bei der Wartung erspart.

Quelle: Codurance Ltd. (n.d.). Test-Driven Development Guide. https://www.codurance.com/test-driven-development-guide

## 4. TDD-Schulen: London vs. Chicago

Im TDD gibt es unterschiedliche Herangehensweisen und zwei „Schulen“ des TDD werden im Allgemeinen bevorzugt praktiziert: die Chicago School (Kent Beck) und die London School (London XP Group).

| Merkmal | Chicago / Detroit School | London / Mockist School |
| --- | --- | --- |
| Ursprung | Kent Beck, Ron Jeffries (Extreme Programming) | London XP Community (z. B. Steve Freeman, Nat Pryce) |
| Philosophie | Fokus auf State – man testet Verhalten über echte Objekte | Fokus auf Interaction – man testet Zusammenarbeit über Mocks/Stubs |
| Testart | Classicist: Tests prüfen das Ergebnis des Systems | Mockist: Tests prüfen, wie Objekte miteinander interagieren |
| Abhängigkeiten | Echte Objekte, wenige Mocks | Intensive Nutzung von Mocks und Spies |
| Beispiel | Test prüft, ob search_collections das richtige Ergebnis liefert | Test prüft, ob search_collections die Datenbank korrekt aufruft |
| Vorteile | Realistischere Tests, refactoringfreundlich | Schnellere, isolierte Tests, gute Fehlerlokalisierung |
| Nachteile | Komplexere Integration, langsamer | Tests brechen bei Refactoring oft (hohe Kopplung an Implementierung) |

Beide Ansätze sind nützlich. In komplexen Systemen wie STAC Index empfiehlt sich allerdings ein hybrider Stil: Unit Tests im London-Stil, Integrationstests im Chicago-Stil.

## 5. Test Doubles: Mocks, Stubs und Spies

Die London School achtet stark auf Interaktionen, daher die Verwendung sogenannter Test-Doubles.

Warum: In Programmen hängen viele Funktionen voneinander ab (z. B. API ruft Datenbank ab). Beim Testen einzelner Komponenten oder Funktionen sind Abhängigkeiten wie echte Datenbankaufrufe oder Internetverbindungen unerwünscht. Diese Abhängigkeiten werden durch kontrollierte Doubles ersetzt.

Definition: Test Doubles sind „Fake-Versionen“ von echten Objekten wie z. B. Klassen oder Funktionen. Sie verhalten sich wie die echten Objekte, antworten auf dieselben Methodenaufrufe, aber mit Antworten, die man selbst am Anfang eines Tests definiert. Sie können genutzt werden, um einzelne Komponenten zu testen, oder für ganze Systeme ausgelegt werden.

Arten:

- Mocks: Überprüfen Interaktionen. Test schlägt fehl, wenn erwarteter Aufruf nicht erfolgt.
- Stubs: Geben vorgefertigte Antworten zurück. Haben kein echtes Verhalten, sondern liefern die definierte Antwort. Beispiel im STAC-Kontext: Eine Stub-Datenbankfunktion gibt eine feste Liste von STAC-Collections zurück, ohne eine echte Datenbankabfrage.
- Spies: Beobachten, was passiert, ohne Verhalten zu erzwingen. Zeichnen z. B. auf, wie viele Aufrufe oder Parameter verwendet wurden.

Quellen:
- Steve Freeman & Nat Pryce – Growing Object-Oriented Software, Guided by Tests (2009)
- Kent Beck – Test-Driven Development: By Example (2003)

## 6. Unit Tests vs. Integration Tests

### Unit Tests

Testen eine Komponente oder Funktion des Codes in Isolation (Funktion, Klasse, Methode).  
Schnelle Tests, einfach zu schreiben.  
Helfen, Bugs früh zu erkennen.

### Integration Tests

Testen, wie mehrere Komponenten zusammenarbeiten (z. B. API + Datenbank).  
Identifizieren Probleme im Datenfluss und in Integrationspunkten.  
Langsamer als Unit Tests, aber realistischer.  
Werden oft nach Unit Tests durchgeführt.

### Integration vs. Unit

Für ein Softwareprojekt, in Bezug auf die Test-Pyramide: Insgesamt viele kleine und schnelle Unit-Tests, ein paar gröbere Integration Tests und nur ganz wenige End-to-End Tests, die das gesamte System prüfen. Schwere End-to-End Tests sind weniger praktikabel für frühe Phasen der Projektentwicklung, Unit- und Integrationstests sind effizienter. End-to-End Tests sind erst in der Systemvalidierung wertvoll.

### Code Beispiel Unit Test

Testet einzelne Funktion: Erstellung einer Datenbankabfrage für /collections?keyword=

```javascript
// searchUtils.js
export function buildCollectionQuery(keyword) {
  return { name: { $regex: keyword, $options: "i" } };
}

// searchUtils.test.js
import { buildCollectionQuery } from "./searchUtils.js";

test("buildCollectionQuery creates a regex filter", () => {
  const query = buildCollectionQuery("landsat");
  expect(query).toEqual({ name: { $regex: "landsat", $options: "i" } });
});

Keine echte API, kein Serverstart.

## 7. Common Test Frameworks

- **Jest** → Test-Framework  
- **supertest** → API-Integration-Tests  
- **Mocha/Chai** → Alternative für Unit-Tests  

### Quellen

**Jest**  
- [https://jestjs.io/docs/getting-started](https://jestjs.io/docs/getting-started)  
- [https://github.com/jestjs/jest](https://github.com/jestjs/jest)

**supertest**  
- [https://github.com/forwardemail/supertest](https://github.com/forwardemail/supertest)

**Mocha/Chai**  
- [https://www.chaijs.com/](https://www.chaijs.com/)  
- [https://mochajs.org/](https://mochajs.org/)

## 8. References

- Beck, K. (2003). *Test-Driven Development: By Example.* Addison-Wesley.  
- Freeman, S. & Pryce, N. (2009). *Growing Object-Oriented Software, Guided by Tests.* Addison-Wesley.  
- Fowler, M. (2012). *The Practical Test Pyramid.* MartinFowler.com. [https://martinfowler.com/articles/practical-test-pyramid.html](https://martinfowler.com/articles/practical-test-pyramid.html)  
- Codurance Ltd. (n.d.). *Test-Driven Development Guide.* [https://www.codurance.com/test-driven-development-guide](https://www.codurance.com/test-driven-development-guide)
