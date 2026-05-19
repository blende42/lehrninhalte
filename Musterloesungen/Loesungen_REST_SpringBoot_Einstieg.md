# Lösungen – REST-Schnittstellen mit Spring Boot einführen

Diese Musterlösung zeigt eine kompakte Standardlösung für den ersten REST-Einstieg mit Spring Boot.

Kernidee:

```text
REST ist eine neue Zugriffsschicht.
Der Controller verwendet den bestehenden Service.
Service, Repository und H2 bleiben in ihrer Verantwortung.
```

Bewusst nicht verwendet werden Security, JPA, Spring Data, DTOs, Validation, Swagger/OpenAPI, Lombok oder komplexe Fehlerbehandlung.

---

## 1. Spring Boot Startklasse

Datei `src/main/java/ch/allianz/youngoitv/lager/LagerverwaltungApplication.java`:

```java
package ch.allianz.youngoitv.lager;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class LagerverwaltungApplication {

    public static void main(String[] args) {
        SpringApplication.run(LagerverwaltungApplication.class, args);
    }
}
```

Start:

```bash
mvn spring-boot:run
```

Erwartung:

```text
Die Anwendung startet lokal auf localhost:8080.
```

---

## 2. Maven Dependency

Im `pom.xml` wird für den Einstieg der Web-Starter benötigt:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Falls das Projekt bereits ein Spring-Boot-Projekt ist, ist diese Dependency oft schon vorhanden.

Für diese Einheit wird vorausgesetzt, dass die bestehende Lagerverwaltung schrittweise in ein Spring-Boot-Projekt überführt wird. Es wird kein JPA, kein Spring Data und keine zusätzliche Persistenzabstraktion eingeführt.

---

## 3. REST Controller

Datei `src/main/java/ch/allianz/youngoitv/lager/api/ProduktController.java`:

```java
package ch.allianz.youngoitv.lager.api;

import ch.allianz.youngoitv.lager.LagerService;
import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.List;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/produkte")
public class ProduktController {

    private final LagerService lagerService;

    public ProduktController(LagerService lagerService) {
        this.lagerService = lagerService;
    }

    @GetMapping
    public List<Produkt> alleProdukte() {
        return lagerService.alleProdukte();
    }

    @GetMapping("/{id}")
    public Produkt produktNachId(@PathVariable long id) {
        return lagerService.produktNachId(id);
    }

    @PostMapping
    public Produkt produktErstellen(@RequestBody Produkt produkt) {
        return lagerService.produktErstellen(produkt);
    }
}
```

Wichtig: Die Methodennamen im Service können im eigenen Projekt anders heissen. Entscheidend ist die Richtung:

```text
Controller -> Service -> Repository -> H2
```

---

## 4. Service bleibt fachlich

Beispielhafte Service-Struktur:

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import ch.allianz.youngoitv.lager.repository.ProduktRepository;
import java.util.List;
import org.springframework.stereotype.Service;

@Service
public class LagerService {

    private final ProduktRepository produktRepository;

    public LagerService(ProduktRepository produktRepository) {
        this.produktRepository = produktRepository;
    }

    public List<Produkt> alleProdukte() {
        return produktRepository.alleProdukte();
    }

    public Produkt produktNachId(long id) {
        return produktRepository.produktNachId(id);
    }

    public Produkt produktErstellen(Produkt produkt) {
        if (produkt.getPreis() < 0) {
            throw new IllegalArgumentException("Preis darf nicht negativ sein.");
        }
        return produktRepository.speichern(produkt);
    }
}
```

Die Preisregel bleibt im Service. Sie wandert nicht in den Controller.

Falls `ProduktRepository` noch keine Spring Bean ist, kann es für den Einstieg ebenfalls mit einer passenden Spring-Annotation oder über eine einfache Konfigurationsmethode bereitgestellt werden. Wichtig bleibt: Der Controller kennt das Repository nicht direkt.

---

## 5. `GET /produkte`

Aufruf:

```bash
curl http://localhost:8080/produkte
```

Mögliche Antwort:

```json
[
  {
    "id": 1,
    "name": "Tastatur",
    "preis": 49.9
  },
  {
    "id": 2,
    "name": "Maus",
    "preis": 24.9
  }
]
```

Einordnung:

- `curl` ist der Client.
- `localhost:8080` ist der lokale Server.
- `/produkte` ist der Endpoint.
- `GET` liest Daten.
- Spring Boot erzeugt JSON aus der Java-Rückgabe.

---

## 6. `GET /produkte/{id}`

Aufruf:

```bash
curl http://localhost:8080/produkte/1
```

Mögliche Antwort:

```json
{
  "id": 1,
  "name": "Tastatur",
  "preis": 49.9
}
```

`@PathVariable` liest den Wert aus dem Pfad:

```text
/produkte/1 -> id = 1
```

---

## 7. `POST /produkte`

Aufruf:

```bash
curl -X POST http://localhost:8080/produkte \
  -H "Content-Type: application/json" \
  -d '{"name":"Monitor","preis":179.9}'
```

Mögliche Antwort:

```json
{
  "id": 3,
  "name": "Monitor",
  "preis": 179.9
}
```

Einordnung:

| Teil | Bedeutung |
|---|---|
| `-X POST` | HTTP-Methode |
| `/produkte` | Endpoint |
| `Content-Type: application/json` | Body enthält JSON |
| `-d ...` | Request Body |

---

## 8. HTTP-Statuscodes beobachten

Richtiger Endpoint:

```bash
curl -i http://localhost:8080/produkte
```

Typisch:

```text
HTTP/1.1 200
```

Falscher Endpoint:

```bash
curl -i http://localhost:8080/falscher-pfad
```

Typisch:

```text
HTTP/1.1 404
```

In dieser Einheit wird nur beobachtet. Eine eigene Fehlerbehandlung wird noch nicht gebaut.

---

## 9. JSON-Struktur

`GET /produkte` liefert normalerweise ein JSON-Array:

```json
[
  {
    "id": 1,
    "name": "Tastatur",
    "preis": 49.9
  }
]
```

Ein einzelnes Produkt ist ein JSON-Objekt:

```json
{
  "id": 1,
  "name": "Tastatur",
  "preis": 49.9
}
```

Passende Java-Rückgaben:

| JSON | Java |
|---|---|
| Produktobjekt | `Produkt` |
| Produktliste | `List<Produkt>` |

---

## 10. Logging beobachten

Sinnvolle Beobachtung:

- Beim Start sieht man Spring-Boot-Logs.
- Beim Aufruf von Endpoints sieht man je nach Konfiguration technische Logs.
- Repository-Logs können zeigen, wann Daten gelesen oder gespeichert werden.

Nicht sinnvoll:

- Fachregeln nur durch Logs prüfen.
- jeden Controller-Aufruf mit vielen `INFO`-Logs überladen.
- sensible Daten vollständig loggen.

---

## 11. Typische Fehlerhinweise

- Fachlogik steht im Controller statt im Service.
- Der Controller ruft direkt das Repository auf.
- Die URL ist falsch, zum Beispiel `/produkt` statt `/produkte`.
- Bei `POST` fehlt `Content-Type: application/json`.
- Der JSON-Body ist ungültig.
- Controller werden zu gross und enthalten Ablaufsteuerung, Validierung, Mapping und Fachregeln gleichzeitig.
- Spring-Boot-Infrastruktur und Lager-Fachlogik werden vermischt.
- `curl` wird ohne Anführungszeichen oder mit falscher HTTP-Methode ausgeführt.

---

## 12. Kurze Reflexionsantworten

**Warum bleibt die Fachlogik unverändert?**

REST ändert nur den Zugriffsweg. Die Regeln der Lagerverwaltung bleiben im `LagerService`.

**Warum ist REST nur eine Zugriffsschicht?**

Der REST Controller nimmt HTTP-Anfragen entgegen und ruft den Service auf. Er ersetzt weder Service noch Repository.

**Was ist der Unterschied zwischen Konsole und HTTP?**

Bei der Konsole bedient eine Person direkt die Anwendung. Bei HTTP sendet ein Client eine Anfrage an einen Server. Die Fachlogik dahinter kann gleich bleiben.

**Warum ist JSON sinnvoll?**

JSON ist ein klares, weit verbreitetes Austauschformat. Clients können es lesen, erzeugen und weiterverarbeiten.

**Warum ist `curl` hilfreich?**

Mit `curl` sieht man Methode, URL, Header, Body und Response direkt. Dadurch werden HTTP-Grundlagen sichtbar.

---

## 13. Verifikation

Die Codebeispiele sind als Spring-Boot-Beispiele formuliert und hängen von den konkreten Methodennamen der bestehenden Lagerverwaltung ab. Technisch geprüft wurde die lokale Maven-Verfügbarkeit mit `mvn -v`. Ein vollständiger Spring-Boot-Build wurde nicht ausgeführt, weil in diesem Repository kein konkretes REST-Projekt mit den verwendeten Klassen angelegt wurde.
