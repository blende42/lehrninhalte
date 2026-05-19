# Übungen – HTTP und REST-Grundlagen vertiefen

## Vorwissen

Du brauchst:

- bestehende REST-Lagerverwaltung mit Spring Boot
- `GET /produkte`
- `POST /produkte`
- `ProduktController`
- `LagerService`
- Grundidee von JSON
- `curl` im Terminal

Nicht verwendet werden:

- Security
- Spring Security
- DTOs
- Validation
- JPA oder Hibernate
- Swagger oder OpenAPI
- HATEOAS
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
Du analysierst HTTP Requests und Responses
an der bestehenden REST-Lagerverwaltung.
```

---

## Vorbereitung

Starte die bestehende Spring-Boot-Anwendung.

```bash
mvn spring-boot:run
```

Die Anwendung soll lokal erreichbar sein:

```text
http://localhost:8080
```

Falls dein Port anders ist, notiere ihn und passe die `curl`-Befehle entsprechend an.

---

## Basis

### Aufgabe 1 – GET-Request mit `curl` senden

Rufe die Produktliste auf.

```bash
curl -i http://localhost:8080/produkte
```

Auftrag:

1. Markiere die Statuszeile.
2. Markiere mindestens einen Header.
3. Markiere den Body.
4. Notiere, welche HTTP-Methode verwendet wurde.

Erwartung:

```text
GET liest Daten und verändert keine Produkte.
```

---

### Aufgabe 2 – Response analysieren

Untersuche die Antwort aus Aufgabe 1.

Auftrag:

1. Notiere den Statuscode.
2. Notiere, ob ein `Content-Type` sichtbar ist.
3. Prüfe, ob der Body JSON ist.
4. Entscheide, ob die JSON-Antwort ein Objekt oder eine Liste ist.

---

### Aufgabe 3 – URL-Struktur analysieren

Zerlege die URL:

```text
http://localhost:8080/produkte
```

Auftrag:

1. Markiere Protokoll, Host, Port und Endpoint.
2. Erkläre, warum `/produkte` eine Ressource beschreibt.
3. Vergleiche mit:

```text
http://localhost:8080/produkte/1
```

Erwartung:

```text
/produkte beschreibt eine Sammlung.
/produkte/1 beschreibt ein einzelnes Produkt.
```

---

### Aufgabe 4 – POST-Request mit `curl` senden

Sende ein neues Produkt.

```bash
curl -i -X POST http://localhost:8080/produkte \
  -H "Content-Type: application/json" \
  -d '{"name":"Maus","preis":24.9}'
```

Auftrag:

1. Markiere die HTTP-Methode.
2. Markiere den Header.
3. Markiere den Request Body.
4. Markiere den Response Statuscode.
5. Prüfe mit `GET /produkte`, ob das Produkt sichtbar ist.

---

### Aufgabe 5 – Header analysieren

Erkläre den Header:

```text
Content-Type: application/json
```

Auftrag:

1. Beschreibe, worauf sich `Content-Type` bezieht.
2. Erkläre, warum der Header bei einem JSON-Body wichtig ist.
3. Erkläre, warum der Header nicht die Fachlogik ist.

---

### Aufgabe 6 – JSON lesen

Analysiere diesen JSON-Body:

```json
{
  "name": "Tastatur",
  "preis": 49.9
}
```

Auftrag:

1. Markiere die Feldnamen.
2. Markiere die Werte.
3. Entscheide, welche Java-Klasse dazu passt.
4. Erkläre, warum JSON nicht Java-Code ist.

---

### Aufgabe 7 – HTTP-Statuscodes beobachten

Führe diese Aufrufe aus:

```bash
curl -i http://localhost:8080/produkte
curl -i http://localhost:8080/falscher-pfad
```

Auftrag:

1. Notiere beide Statuscodes.
2. Erkläre den Unterschied.
3. Entscheide, welcher Statuscode zu einem falschen Endpoint passt.

---

### Aufgabe 8 – Ungültigen Request erzeugen

Sende absichtlich ungültiges JSON.

```bash
curl -i -X POST http://localhost:8080/produkte \
  -H "Content-Type: application/json" \
  -d '{"name":"Monitor","preis":}'
```

Auftrag:

1. Notiere den Statuscode.
2. Notiere, ob ein Fehlerbody zurückkommt.
3. Erkläre, warum das ein Request-Problem ist.

Noch nicht verlangt: eigene Fehlerbehandlung bauen.

---

## Vertiefung

### Aufgabe 9 – Weiteren Endpunkt ergänzen

Ergänze oder prüfe einen Endpoint für ein einzelnes Produkt.

```text
GET /produkte/{id}
```

Auftrag:

1. Verwende `@GetMapping("/{id}")`, falls der Endpunkt noch fehlt.
2. Lies die ID mit `@PathVariable`.
3. Rufe eine passende Service-Methode auf.
4. Baue keine Fachlogik in den Controller.

Hinweis: Wenn die Service-Methode noch nicht existiert, notiere die nötige Service-Methode, statt Repository-Code in den Controller zu schreiben.

---

### Aufgabe 10 – Verschiedene Statuscodes erzeugen

Versuche, unterschiedliche Statuscodes zu beobachten.

Beispiele:

```bash
curl -i http://localhost:8080/produkte
curl -i http://localhost:8080/produkte/9999
curl -i http://localhost:8080/falscher-pfad
```

Auftrag:

1. Notiere, welche Statuscodes dein Projekt tatsächlich zurückgibt.
2. Ordne die beobachteten Codes ein.
3. Notiere, welche Fälle noch keine saubere fachliche Antwort liefern.

Wichtig: Nicht jedes Projekt liefert bereits `404` für ein nicht vorhandenes Produkt. Das wird später sauberer behandelt.

---

### Aufgabe 11 – Header gezielt setzen

Sende denselben POST-Request einmal mit und einmal ohne `Content-Type`.

Mit Header:

```bash
curl -i -X POST http://localhost:8080/produkte \
  -H "Content-Type: application/json" \
  -d '{"name":"Kabel","preis":9.9}'
```

Ohne Header:

```bash
curl -i -X POST http://localhost:8080/produkte \
  -d '{"name":"Kabel","preis":9.9}'
```

Auftrag:

1. Vergleiche die Antworten.
2. Notiere Statuscode und Body.
3. Erkläre, warum Header wichtig sind.

---

### Aufgabe 12 – JSON-Struktur erweitern

Erweitere den JSON-Body um ein Feld, das deine `Produkt`-Klasse kennt.

Beispiel:

```json
{
  "name": "Maus",
  "preis": 24.9,
  "bestand": 12
}
```

Auftrag:

1. Sende den erweiterten Body.
2. Prüfe die Response.
3. Prüfe mit `GET /produkte`, ob das Feld sichtbar ist.
4. Erkläre, was passiert, wenn das Feld in deiner Java-Klasse nicht existiert.

---

### Aufgabe 13 – Request und Response dokumentieren

Dokumentiere einen erfolgreichen `POST /produkte`-Aufruf.

Vorlage:

```text
Request
Methode:
URL:
Header:
Body:

Response
Statuscode:
Header:
Body:
```

Auftrag:

1. Fülle die Vorlage mit einem echten Aufruf aus.
2. Markiere JSON getrennt von HTTP.
3. Erkläre, welche Service-Methode dahinter aufgerufen wird.

---

### Aufgabe 14 – Logging mit HTTP kombinieren

Beobachte Logs während HTTP-Aufrufen.

Auftrag:

1. Starte die Anwendung.
2. Führe `GET /produkte` aus.
3. Führe `POST /produkte` aus.
4. Beobachte Logs aus Controller, Service oder Repository.
5. Entscheide, ob ein Log fachlich oder technisch ist.

Wichtig:

```text
Logging macht Abläufe sichtbar.
Logging ersetzt keine Statuscodes und keine Tests.
```

---

## Transfer

### Aufgabe 15 – Warum REST auf HTTP basiert

Erkläre schriftlich:

1. Welche Rolle HTTP bei REST spielt.
2. Warum ein REST Controller HTTP-Anfragen entgegennimmt.
3. Warum der `LagerService` trotzdem keine HTTP-Klasse sein soll.

---

### Aufgabe 16 – Warum JSON sinnvoll ist

Erkläre:

1. Warum JSON für Request und Response hilfreich ist.
2. Warum JSON besser strukturiert ist als eine freie Konsolenausgabe.
3. Warum JSON trotzdem keine Fachlogik enthält.

---

### Aufgabe 17 – Konsole und HTTP vergleichen

Vergleiche:

```text
Konsolenanwendung -> Benutzer gibt Text im Menü ein
REST-Anwendung    -> Client sendet HTTP Request
```

Auftrag:

1. Beschreibe den Unterschied der Zugriffsschicht.
2. Beschreibe, was im Service gleich bleibt.
3. Erkläre, warum die bestehende Architektur dadurch stabil bleibt.

---

### Aufgabe 18 – Warum Statuscodes wichtig sind

Erkläre:

1. Warum ein Client einen Statuscode braucht.
2. Warum `404` hilfreicher ist als nur ein leerer Body.
3. Warum `500` auf ein Serverproblem hinweist.
4. Warum wir komplexe Fehlerbehandlung trotzdem noch nicht ausbauen.

---

### Aufgabe 19 – REST als Zugriffsschicht

Ergänze:

```text
curl Client
-> HTTP Request
-> __________
-> LagerService
-> Repository
-> H2
```

Auftrag:

1. Fülle die Lücke.
2. Markiere, welche Schicht neu ist.
3. Erkläre, warum der Controller nicht direkt mit H2 sprechen soll.

---

## Reflexion

Beantworte am Schluss:

1. Was ist an HTTP technischer als an der bisherigen Konsoleneingabe?
2. Welche Informationen stehen in einem Request?
3. Welche Informationen stehen in einer Response?
4. Was bleibt Aufgabe des Service?
