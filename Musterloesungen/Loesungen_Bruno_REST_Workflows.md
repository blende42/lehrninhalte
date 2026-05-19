# Lösungen – REST-Workflows mit Bruno

## Basis

### Aufgabe 1 – Bruno installieren oder öffnen

Eine mögliche Notiz:

```text
Bruno bereit: ja
Spring Boot auf localhost:8080: ja
```

Falls Spring Boot nicht läuft, können die Requests zwar gespeichert, aber nicht erfolgreich ausgeführt werden.

In dieser Einheit werden keine automatischen Tests, keine Security und kein JWT eingerichtet.

---

### Aufgabe 2 – Collection erstellen

Sinnvolle Struktur:

```text
Lagerverwaltung API
+-- Produkte
```

Wichtig ist nicht der exakte UI-Klickpfad. Wichtig ist, dass die Produkt-Requests gesammelt und wieder auffindbar sind.

---

### Aufgabe 3 – GET /produkte speichern

Request:

```text
Name: GET Produkte
Methode: GET
URL: http://localhost:8080/produkte
```

Mögliche Beobachtung:

```text
Statuscode: 200 OK
Content-Type: application/json
Body: JSON-Liste mit Produkten
```

Je nach Startdaten kann die Liste leer oder gefüllt sein.

---

### Aufgabe 4 – Response analysieren

Mögliche Antworten:

1. Der Body ist bei `GET /produkte` normalerweise eine JSON-Liste.
2. Ein Produkt enthält zum Beispiel `id`, `name` und `preis`.
3. Der Statuscode zeigt das Ergebnis der Anfrage. Header beschreiben technische Zusatzinformationen. Der Body enthält die Nutzdaten.

---

### Aufgabe 5 – POST /produkte speichern

Request:

```text
Name: POST Produkt erfassen
Methode: POST
URL: http://localhost:8080/produkte
Header: Content-Type: application/json
```

Body:

```json
{
  "name": "Maus",
  "preis": 24.9
}
```

Mögliche Beobachtung:

```text
Statuscode: 200 OK oder 201 Created
Response Body: JSON zum erstellten Produkt
```

Der genaue Statuscode hängt von der vorhandenen Controller-Implementierung ab.

---

### Aufgabe 6 – Gespeicherten Request erneut ausführen

Mögliche Antwort:

```text
Das Produkt ist in der Produktliste sichtbar.
Die JSON-Liste enthält einen zusätzlichen Eintrag.
Der GET-Request musste nicht neu geschrieben werden, weil er gespeichert war.
```

Falls die Anwendung keine dauerhafte Speicherung zwischen Neustarts hat, kann das Produkt nach einem Neustart fehlen.

---

### Aufgabe 7 – JSON ändern

Body:

```json
{
  "name": "Monitor",
  "preis": 199.0
}
```

Mögliche Beobachtung:

```text
Der POST-Request kann mit anderen JSON-Daten erneut verwendet werden.
Nach dem nächsten GET ist das neue Produkt sichtbar, sofern die Anwendung es speichert.
```

---

### Aufgabe 8 – curl und Bruno vergleichen

Mögliche Gemeinsamkeiten:

- Beide senden HTTP-Requests.
- Beide können `GET http://localhost:8080/produkte` ausführen.
- Beide zeigen eine Response des Servers.

Mögliche Unterschiede:

- `curl` ist ein Terminalbefehl.
- Bruno speichert Requests in einer Collection.
- Bruno macht Header, Body und Response in einer Oberfläche sichtbar.
- Bruno-Requests können später wieder geöffnet werden.

---

## Vertiefung

### Aufgabe 9 – Requests sinnvoll umbenennen

Gute Namen:

```text
GET Produkte
POST Produkt erfassen
POST Produkt fehlerhaftes JSON
```

Diese Namen zeigen Methode und Zweck. Das ist besser als Namen wie `Test1` oder `Request neu`.

---

### Aufgabe 10 – Mehrere Requests strukturieren

Sinnvolle Struktur:

```text
Lagerverwaltung API
+-- Produkte
    +-- GET Produkte
    +-- POST Produkt erfassen
    +-- POST Produkt fehlerhaftes JSON
```

Begründung:

```text
Alle Requests zur Ressource Produkte liegen zusammen.
Die Namen zeigen Methode und Zweck.
Fehlerfälle sind bewusst dokumentiert.
```

---

### Aufgabe 11 – Fehlerfall dokumentieren

Fehlerhafter Body:

```json
{
  "name": "Tastatur",
  "preis": 
}
```

Mögliche Beobachtung:

```text
Statuscode: häufig 400 Bad Request
Grund: Das JSON ist ungültig, weil nach "preis" kein Wert steht.
```

Der genaue Response-Text hängt von Spring Boot und der vorhandenen Fehlerbehandlung ab.

---

### Aufgabe 12 – Fehlenden Header beobachten

Mögliche Beobachtung:

```text
Ohne Content-Type: application/json erkennt der Server den Body je nach Implementierung nicht als JSON.
Die Response kann ein Fehler sein.
```

Warum der Header wichtig ist:

```text
Der Header beschreibt, welches Format der Body hat.
```

---

### Aufgabe 13 – Verschiedene JSON-Daten testen

Beispieltabelle:

| Produktname | Preis | Statuscode | Beobachtung |
|---|---:|---|---|
| USB-Kabel | 9.9 | 200 oder 201 | Produkt wurde angenommen |
| Mauspad | 14.5 | 200 oder 201 | Produkt wurde angenommen |
| Monitor | 199.0 | 200 oder 201 | Produkt wurde angenommen |

Falls ein Produkt nicht angenommen wird, sollte die Response notiert werden.

---

### Aufgabe 14 – Logging beobachten

Mögliche Beobachtung:

```text
Bei einem Request kann Spring Boot oder die Anwendung Log-Ausgaben schreiben.
Bei ungültigem JSON ist oft eine Fehlermeldung sichtbar.
```

Einordnung:

- Logs helfen Entwickelnden beim Beobachten der Anwendung.
- Die Response ist die Antwort an den Client.
- Logs ersetzen keine Response.
- Die Fachlogik bleibt im Service.

---

### Aufgabe 15 – API-Workflow dokumentieren

Mögliche Dokumentation:

| Schritt | Request | Erwartung |
|---|---|---|
| 1 | Spring Boot starten | Server läuft auf `localhost:8080` |
| 2 | `GET Produkte` | Status `200`, JSON-Liste |
| 3 | `POST Produkt erfassen` | Status `200` oder `201`, Produkt als JSON |
| 4 | `GET Produkte` | Produktliste enthält neues Produkt |
| 5 | Response prüfen | Statuscode, Header und Body passen zusammen |

---

## Transfer

### Aufgabe 16 – Warum Requests speichern?

Mögliche Antwort:

```text
Ein gespeicherter Request kann später erneut ausgeführt werden.
Methode, URL, Header und Body müssen nicht jedes Mal neu geschrieben werden.
Dadurch werden API-Aufrufe nachvollziehbarer und weniger fehleranfällig.
```

---

### Aufgabe 17 – Reproduzierbarkeit erklären

Mögliche Antwort:

```text
Ein Request ist reproduzierbar, wenn ich ihn mit gleicher Methode, gleicher URL,
gleichen Headern und gleichem Body erneut ausführen kann. Dann kann ich die
Response vergleichen und Fehler besser nachvollziehen.
```

---

### Aufgabe 18 – curl und Bruno diskutieren

Mögliche Antwort:

```text
curl ist besonders hilfreich, wenn ich HTTP im Terminal direkt sehen und schnell
einen einzelnen Aufruf prüfen will. Bruno ist besonders hilfreich, wenn ich mehrere
Requests speichern, ordnen und später wieder ausführen will. Beide Werkzeuge
senden HTTP-Requests und helfen beim Verstehen von REST.
```

---

### Aufgabe 19 – Versionierbare API-Requests

Mögliche Antwort:

```text
Gespeicherte Bruno-Requests können Teil eines Projektordners sein. Wenn sie als
Dateien vorliegen, können Änderungen daran nachvollziehbar werden. Andere
Personen können dieselben Requests öffnen und gegen die gleiche lokale API
ausführen.
```

In dieser Einheit wird Git nur als Idee erwähnt. Es werden keine Git-Schritte benötigt.

---

### Aufgabe 20 – REST-Workflow und Fachlogik trennen

Mögliche Antwort:

```text
Bruno ist ein API-Werkzeug. Es sendet HTTP Requests an den REST Controller.
Der Controller ruft den Service auf. Der Service enthält die Fachlogik. Das
Repository kümmert sich um den Datenzugriff. Bruno verändert diese Schichten
nicht, sondern macht die Aufrufe reproduzierbar.
```

Typischer Fehler:

```text
Man sollte wegen Bruno keine Fachlogik in den Controller verschieben.
```
