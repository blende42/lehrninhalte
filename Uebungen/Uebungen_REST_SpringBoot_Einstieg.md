# Übungen – REST-Schnittstellen mit Spring Boot einführen

## Vorwissen

Du brauchst:

- bekannte Lagerverwaltung
- Maven-Projektstruktur
- `LagerService`
- Repository-Klassen mit JDBC/H2
- Modellklasse `Produkt`
- Grundidee von Logging und technischer Konfiguration
- einfache Terminalbefehle

Nicht verwendet werden:

- Security
- JPA oder Hibernate
- Spring Data
- DTOs
- Validation
- Swagger oder OpenAPI
- Lombok
- komplexe Fehlerbehandlung

Prüfe nach praktischen Änderungen:

```bash
mvn package
```

Wenn Tests vorhanden sind:

```bash
mvn test
```

Ziel dieser Übungen:

```text
Du machst bestehende Fachlogik über HTTP erreichbar,
ohne Service und Repository fachlich umzubauen.
```

---

## Vorbereitung

Arbeite mit der bekannten Lagerverwaltung.

Beispielstruktur:

```text
lagerverwaltung-rest/
  pom.xml
  src/main/java/
    ch/allianz/youngoitv/lager/
      LagerverwaltungApplication.java
      LagerService.java
      model/Produkt.java
      repository/ProduktRepository.java
      api/ProduktController.java
  src/main/resources/
    application.properties
```

Falls dein Projekt leicht anders aufgebaut ist, passe die Package-Namen sinnvoll an.

Für Spring Boot brauchst du im `pom.xml` mindestens den Web-Starter:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

---

## Basis

### Aufgabe 1 – Spring Boot Projekt starten

Starte deine Spring-Boot-Anwendung.

Auftrag:

1. Prüfe, ob eine Startklasse mit `@SpringBootApplication` vorhanden ist.
2. Starte das Projekt mit Maven.
3. Beobachte in der Konsole, ob Spring Boot auf Port `8080` startet.

Beispiel:

```bash
mvn spring-boot:run
```

Erwartung:

```text
Tomcat started on port 8080
```

Wenn Port `8080` belegt ist, notiere den Fehler. Ändere den Port in dieser Übung nur, wenn die Lehrperson das vorgibt.

---

### Aufgabe 2 – Ersten REST Controller erstellen

Erstelle die Klasse `ProduktController` im Package `api`.

Auftrag:

1. Annotiere die Klasse mit `@RestController`.
2. Setze `@RequestMapping("/produkte")`.
3. Verwende den bestehenden `LagerService` über den Konstruktor.
4. Prüfe, ob der `LagerService` für Spring als Bean verfügbar ist, zum Beispiel mit `@Service`.
5. Rufe kein Repository direkt aus dem Controller auf.

Startstruktur:

```java
package ch.allianz.youngoitv.lager.api;

import ch.allianz.youngoitv.lager.LagerService;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/produkte")
public class ProduktController {

    private final LagerService lagerService;

    public ProduktController(LagerService lagerService) {
        this.lagerService = lagerService;
    }
}
```

---

### Aufgabe 3 – `GET /produkte` ergänzen

Ergänze einen Endpoint, der alle Produkte zurückgibt.

Auftrag:

1. Ergänze eine Methode mit `@GetMapping`.
2. Gib eine Liste von Produkten zurück.
3. Verwende dafür eine bestehende Service-Methode.
4. Ergänze nötige Imports wie `java.util.List`, `Produkt` und `GetMapping`.

Beispiel:

```java
@GetMapping
public List<Produkt> alleProdukte() {
    return lagerService.alleProdukte();
}
```

Falls deine Service-Methode anders heisst, verwende den Namen aus deinem Projekt.

---

### Aufgabe 4 – Produkte als JSON ausgeben

Starte die Anwendung und rufe den Endpoint auf.

```bash
curl http://localhost:8080/produkte
```

Auftrag:

1. Kopiere die JSON-Antwort in deine Notizen.
2. Markiere ein Produktobjekt.
3. Markiere eine Eigenschaft wie `name` oder `preis`.
4. Erkläre kurz, warum du keinen eigenen JSON-Code schreiben musstest.

---

### Aufgabe 5 – `POST /produkte` ergänzen

Ergänze einen Endpoint, der ein Produkt aus JSON entgegennimmt.

Auftrag:

1. Ergänze eine Methode mit `@PostMapping`.
2. Verwende `@RequestBody Produkt produkt`.
3. Rufe eine bestehende Service-Methode zum Speichern oder Erstellen auf.
4. Gib das gespeicherte Produkt zurück.
5. Ergänze nötige Imports wie `PostMapping` und `RequestBody`.

Beispiel:

```java
@PostMapping
public Produkt produktErstellen(@RequestBody Produkt produkt) {
    return lagerService.produktErstellen(produkt);
}
```

Falls deine Service-Methode anders heisst, passe nur diesen Methodenaufruf an.

Hinweis: Damit Spring JSON in ein `Produkt` umwandeln kann, muss die Modellklasse passende Getter und Setter oder eine andere einfache JavaBean-Struktur haben. Baue dafür noch keine DTO-Klasse.

---

### Aufgabe 6 – JSON mit `curl` senden

Sende ein Produkt an den Server.

```bash
curl -X POST http://localhost:8080/produkte \
  -H "Content-Type: application/json" \
  -d '{"name":"Maus","preis":24.9}'
```

Auftrag:

1. Prüfe die Antwort.
2. Rufe danach wieder `GET /produkte` auf.
3. Prüfe, ob das neue Produkt sichtbar ist.
4. Notiere, welche Teile des Befehls HTTP-Methode, Header und Body sind.

---

## Vertiefung

### Aufgabe 7 – Mehrere Endpunkte ergänzen

Ergänze einen Endpoint für ein einzelnes Produkt.

Beispiel-Endpoint:

```text
GET /produkte/1
```

Auftrag:

1. Verwende `@GetMapping("/{id}")`.
2. Lies die ID mit `@PathVariable`.
3. Rufe eine passende Service-Methode auf.
4. Gib das Produkt zurück.

Hinweis: Wenn dein Service noch keine passende Methode hat, notiere nur, welche Methode im Service fehlen würde. Baue keine Fachlogik in den Controller.

---

### Aufgabe 8 – HTTP-Statuscodes beobachten

Rufe vorhandene und nicht vorhandene URLs auf.

```bash
curl -i http://localhost:8080/produkte
curl -i http://localhost:8080/falscher-pfad
```

Auftrag:

1. Notiere den Statuscode für den richtigen Endpoint.
2. Notiere den Statuscode für den falschen Pfad.
3. Erkläre kurz, was der Unterschied bedeutet.

Noch nicht verlangt: eigene Fehlerbehandlung bauen.

---

### Aufgabe 9 – `curl` mit Header verwenden

Sende ein Produkt einmal mit und einmal ohne Header.

Mit Header:

```bash
curl -X POST http://localhost:8080/produkte \
  -H "Content-Type: application/json" \
  -d '{"name":"Monitor","preis":179.9}'
```

Ohne Header:

```bash
curl -X POST http://localhost:8080/produkte \
  -d '{"name":"Monitor","preis":179.9}'
```

Auftrag:

1. Beobachte, ob beide Aufrufe gleich funktionieren.
2. Notiere die Antwort oder Fehlermeldung.
3. Erkläre, warum der Header für REST-Aufrufe wichtig ist.

---

### Aufgabe 10 – Mehrere Produkte senden

Sende mindestens drei Produkte.

Testdaten:

```json
{"name":"Tastatur","preis":49.9}
{"name":"Maus","preis":24.9}
{"name":"Monitor","preis":179.9}
```

Auftrag:

1. Sende jedes Produkt mit `POST /produkte`.
2. Rufe danach `GET /produkte` auf.
3. Prüfe die JSON-Liste.
4. Erkläre, ob die Produkte durch REST oder durch die bestehende Service- und Repository-Struktur gespeichert wurden.

---

### Aufgabe 11 – JSON-Struktur analysieren

Untersuche die Antwort von `GET /produkte`.

Auftrag:

1. Ist die Antwort ein JSON-Objekt oder ein JSON-Array?
2. Welche Felder enthält ein Produkt?
3. Welche Java-Klasse passt zu einem einzelnen JSON-Produkt?
4. Welche Java-Rückgabe passt zur ganzen JSON-Liste?

---

### Aufgabe 12 – Logging bei REST-Aufrufen beobachten

Rufe mehrere Endpoints auf und beobachte die Log-Ausgabe.

Auftrag:

1. Starte die Anwendung.
2. Führe `GET /produkte` aus.
3. Führe `POST /produkte` aus.
4. Beobachte Logs in Controller, Service oder Repository.
5. Notiere, welche Logs technische Abläufe zeigen.

Wichtig: Logging ersetzt keine Fachlogik und keine Tests.

---

## Transfer

### Aufgabe 13 – Fachlogik bleibt unverändert

Erkläre schriftlich:

1. Welche Fachregeln bleiben im Service?
2. Warum soll der Controller diese Regeln nicht neu implementieren?
3. Was wäre das Risiko von Fachlogik im Controller?

---

### Aufgabe 14 – REST ist nur eine Zugriffsschicht

Ergänze das Architekturdiagramm:

```text
curl
-> HTTP / JSON
-> __________
-> LagerService
-> ProduktRepository
-> H2
```

Auftrag:

1. Fülle die Lücke.
2. Markiere die neue Schicht.
3. Markiere die bereits bekannten Schichten.
4. Begründe, warum die Datenbank nicht direkt vom Client angesprochen wird.

---

### Aufgabe 15 – Konsole und HTTP vergleichen

Vergleiche die bisherige Konsolenanwendung mit REST.

Auftrag:

1. Wie wurde vorher ein Produkt erfasst?
2. Wie wird jetzt ein Produkt per HTTP gesendet?
3. Was bleibt im Service gleich?
4. Was ändert sich an der Zugriffsschicht?

---

### Aufgabe 16 – Warum JSON sinnvoll ist

Erkläre:

1. Warum eignet sich JSON für den Austausch zwischen Client und Server?
2. Warum ist JSON besser als eine zufällige Konsolenausgabe?
3. Warum ist JSON trotzdem nicht die Fachlogik?

---

### Aufgabe 17 – Warum `curl` hilfreich ist

Erkläre:

1. Warum kann `curl` beim Lernen von REST helfen?
2. Was zeigt `curl`, das im Browser nicht immer sichtbar ist?
3. Welche typischen Fehler kann man mit `curl` gut untersuchen?

---

## Reflexion

Beantworte am Schluss:

1. Was war an REST neu?
2. Welche Teile der Lagerverwaltung blieben gleich?
3. Wo würdest du als nächstes genauer hinschauen: HTTP, JSON oder Controller-Struktur?
