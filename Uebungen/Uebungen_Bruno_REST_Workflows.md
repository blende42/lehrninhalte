# Übungen – REST-Workflows mit Bruno

## Vorwissen

Du kennst bereits:

- REST Controller mit Spring Boot
- `GET /produkte`
- `POST /produkte`
- HTTP Request und HTTP Response
- Header, Body und Statuscodes
- JSON als Austauschformat
- `curl` für einfache REST-Aufrufe

In diesen Übungen verwendest du dieselbe REST-Lagerverwaltung weiter.

---

## Rahmenbedingungen

- Spring Boot läuft lokal auf `localhost:8080`.
- Die bestehende Fachlogik bleibt im `LagerService`.
- Bruno wird als lokales Werkzeug für gespeicherte Requests verwendet.
- Du baust keine automatischen Tests.
- Du führst keine Security, JWT, DTOs, OpenAPI oder komplexe Environments ein.

---

## Basis

### Aufgabe 1 – Bruno installieren oder öffnen

Installiere Bruno nach Vorgabe der Lehrperson oder öffne die bereits installierte Version.

Prüfe:

- Bruno startet.
- Du kannst eine neue Collection erstellen.
- Die Spring-Boot-Anwendung läuft auf `localhost:8080`.

Notiere kurz:

```text
Bruno bereit: ja/nein
Spring Boot auf localhost:8080: ja/nein
```

---

### Aufgabe 2 – Collection erstellen

Erstelle eine neue Collection mit dem Namen:

```text
Lagerverwaltung API
```

Lege darin einen Bereich oder Ordner an:

```text
Produkte
```

Falls deine Bruno-Version anders aussieht, wähle eine einfache Struktur, in der alle Produkt-Requests zusammen sichtbar sind.

---

### Aufgabe 3 – GET /produkte speichern

Erstelle einen Request:

```text
Name: GET Produkte
Methode: GET
URL: http://localhost:8080/produkte
```

Führe den Request aus.

Notiere:

- Statuscode
- Content-Type der Response, falls sichtbar
- ob der Body JSON enthält

---

### Aufgabe 4 – Response analysieren

Betrachte die Response von `GET /produkte`.

Beantworte:

1. Ist der Body ein JSON-Objekt oder eine JSON-Liste?
2. Welche Felder hat ein Produkt?
3. Siehst du einen Unterschied zwischen Statuscode, Header und Body?

---

### Aufgabe 5 – POST /produkte speichern

Erstelle einen zweiten Request:

```text
Name: POST Produkt erfassen
Methode: POST
URL: http://localhost:8080/produkte
```

Setze den Header:

```text
Content-Type: application/json
```

Setze diesen JSON-Body:

```json
{
  "name": "Maus",
  "preis": 24.9
}
```

Führe den Request aus.

Notiere:

- Statuscode
- Response Body
- ob das Produkt in der Antwort sichtbar ist

---

### Aufgabe 6 – Gespeicherten Request erneut ausführen

Führe den gespeicherten Request `GET Produkte` erneut aus.

Prüfe:

- Ist das Produkt aus Aufgabe 5 sichtbar?
- Hat sich die JSON-Liste verändert?
- Musstest du den GET-Request neu schreiben?

---

### Aufgabe 7 – JSON ändern

Kopiere den `POST Produkt erfassen`-Request oder passe ihn an.

Sende ein zweites Produkt:

```json
{
  "name": "Monitor",
  "preis": 199.0
}
```

Führe danach `GET Produkte` erneut aus.

Erwartetes Resultat:

```text
Die Produktliste enthält mindestens die neu gesendeten Produkte, sofern die Anwendung Produkte speichert.
```

---

### Aufgabe 8 – curl und Bruno vergleichen

Vergleiche diesen `curl`-Aufruf mit deinem Bruno-Request:

```bash
curl -i http://localhost:8080/produkte
```

Notiere zwei Gemeinsamkeiten und zwei Unterschiede.

---

## Vertiefung

### Aufgabe 9 – Requests sinnvoll umbenennen

Prüfe deine Request-Namen.

Verbessere sie, falls nötig:

```text
GET Produkte
POST Produkt erfassen
POST Produkt fehlerhaftes JSON
```

Ziel:

```text
Eine andere Person soll ohne Erklärung erkennen, wofür der Request gedacht ist.
```

---

### Aufgabe 10 – Mehrere Requests strukturieren

Ordne deine Requests in der Collection.

Eine mögliche Struktur:

```text
Lagerverwaltung API
+-- Produkte
    +-- GET Produkte
    +-- POST Produkt erfassen
    +-- POST Produkt fehlerhaftes JSON
```

Beschreibe kurz, warum diese Struktur verständlich ist.

---

### Aufgabe 11 – Fehlerfall dokumentieren

Erstelle einen Request:

```text
Name: POST Produkt fehlerhaftes JSON
Methode: POST
URL: http://localhost:8080/produkte
Header: Content-Type: application/json
```

Verwende absichtlich ungültiges JSON:

```json
{
  "name": "Tastatur",
  "preis": 
}
```

Führe den Request aus.

Notiere:

- Statuscode
- kurze Beschreibung der Response
- warum der Request fehlerhaft ist

---

### Aufgabe 12 – Fehlenden Header beobachten

Kopiere den gültigen `POST Produkt erfassen`-Request.

Entferne den Header:

```text
Content-Type: application/json
```

Führe den Request aus.

Notiere:

- Was passiert?
- Unterscheidet sich die Response vom gültigen POST?
- Warum ist der Header für JSON wichtig?

---

### Aufgabe 13 – Verschiedene JSON-Daten testen

Teste mindestens drei verschiedene Produkte.

Beispiel:

```json
{
  "name": "USB-Kabel",
  "preis": 9.9
}
```

Halte in einer kleinen Tabelle fest:

| Produktname | Preis | Statuscode | Beobachtung |
|---|---:|---|---|
| | | | |

---

### Aufgabe 14 – Logging beobachten

Starte die Spring-Boot-Anwendung so, dass du die Log-Ausgabe siehst.

Führe in Bruno aus:

1. `GET Produkte`
2. `POST Produkt erfassen`
3. `GET Produkte`

Beobachte:

- Gibt es Log-Ausgaben pro Request?
- Siehst du Fehler bei ungültigem JSON?
- Welche Information gehört ins Log und welche in die Response?

---

### Aufgabe 15 – API-Workflow dokumentieren

Dokumentiere deinen Bruno-Workflow kurz:

```text
1. Spring Boot starten
2. GET Produkte ausführen
3. POST Produkt erfassen ausführen
4. GET Produkte erneut ausführen
5. Response prüfen
```

Ergänze bei jedem Schritt:

- Request-Name
- erwarteter Statuscode
- was du im Body erwartest

---

## Transfer

### Aufgabe 16 – Warum Requests speichern?

Erkläre in eigenen Worten:

```text
Warum ist ein gespeicherter Request hilfreicher als ein einmalig getippter curl-Befehl?
```

---

### Aufgabe 17 – Reproduzierbarkeit erklären

Erkläre den Begriff reproduzierbar anhand deines Bruno-Workflows.

Verwende diese Begriffe:

- gleiche Methode
- gleiche URL
- gleiche Header
- gleicher Body
- vergleichbare Response

---

### Aufgabe 18 – curl und Bruno diskutieren

Vergleiche `curl` und Bruno.

Beantworte:

1. Wann ist `curl` besonders hilfreich?
2. Wann ist Bruno besonders hilfreich?
3. Warum ist es sinnvoll, beide Werkzeuge zu kennen?

---

### Aufgabe 19 – Versionierbare API-Requests

Erkläre:

```text
Warum können gespeicherte Bruno-Requests Teil eines Projekts sein?
```

Gehe darauf ein:

- Requests liegen als Dateien vor
- Änderungen können nachvollziehbar werden
- andere Personen können dieselben Requests ausführen

---

### Aufgabe 20 – REST-Workflow und Fachlogik trennen

Erkläre:

```text
Warum ändert Bruno nichts an der Fachlogik im LagerService?
```

Verwende die Begriffe:

- API-Werkzeug
- HTTP Request
- REST Controller
- Service
- Repository
