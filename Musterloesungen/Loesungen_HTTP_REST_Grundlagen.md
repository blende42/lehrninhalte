# Lösungen – HTTP und REST-Grundlagen vertiefen

Diese Musterlösung zeigt kompakte Standardantworten zur Analyse von HTTP und REST an der bestehenden Spring-Boot-Lagerverwaltung.

Kernidee:

```text
REST nutzt HTTP.
HTTP transportiert Request und Response.
Die Fachlogik bleibt im Service.
```

Bewusst nicht behandelt werden Security, DTOs, Validation, JPA, Swagger/OpenAPI, Spring Security, HATEOAS und komplexe Fehlerbehandlung.

---

## 1. GET-Request analysieren

Aufruf:

```bash
curl -i http://localhost:8080/produkte
```

Einordnung:

| Teil | Beispiel |
|---|---|
| Methode | `GET` |
| URL | `http://localhost:8080/produkte` |
| Endpoint | `/produkte` |
| Body im Request | keiner |
| Ziel | Produktliste lesen |

`GET` liest Daten. Der Aufruf soll keine Produkte verändern.

---

## 2. Response analysieren

Mögliche Antwort:

```text
HTTP/1.1 200
Content-Type: application/json
```

Möglicher Body:

```json
[
  {
    "id": 1,
    "name": "Tastatur",
    "preis": 49.9
  }
]
```

Einordnung:

- `200` bedeutet: Anfrage erfolgreich.
- `Content-Type: application/json` bedeutet: Der Body enthält JSON.
- Der Body ist eine JSON-Liste.
- Ein einzelnes Element der Liste passt zur Java-Klasse `Produkt`.

---

## 3. URL-Struktur

Vollständige URL:

```text
http://localhost:8080/produkte
```

Zerlegung:

| Teil | Bedeutung |
|---|---|
| `http` | Protokoll |
| `localhost` | lokaler Server |
| `8080` | Port |
| `/produkte` | Endpoint |

Vergleich:

```text
/produkte      -> Sammlung von Produkten
/produkte/1    -> einzelnes Produkt mit ID 1
```

---

## 4. POST-Request analysieren

Aufruf:

```bash
curl -i -X POST http://localhost:8080/produkte \
  -H "Content-Type: application/json" \
  -d '{"name":"Maus","preis":24.9}'
```

Einordnung:

| Teil | Beispiel |
|---|---|
| Methode | `POST` |
| URL | `http://localhost:8080/produkte` |
| Header | `Content-Type: application/json` |
| Body | `{"name":"Maus","preis":24.9}` |
| Ziel | Produkt an die Sammlung senden |

Typische Antwort:

```text
HTTP/1.1 200
```

oder, wenn der Controller das so umsetzt:

```text
HTTP/1.1 201
```

Für diese Einheit reicht: Beide zeigen einen erfolgreichen Ablauf. `201 Created` ist fachlich genauer, wenn wirklich eine neue Ressource erstellt wurde.

---

## 5. Header

Der Header:

```text
Content-Type: application/json
```

bedeutet:

```text
Der Request Body enthält JSON.
```

Der Header beschreibt die technische Form der Nachricht. Er prüft keine Preisregel und speichert kein Produkt.

---

## 6. JSON lesen

JSON:

```json
{
  "name": "Tastatur",
  "preis": 49.9
}
```

Einordnung:

| JSON-Teil | Bedeutung |
|---|---|
| `name` | Feldname |
| `"Tastatur"` | Textwert |
| `preis` | Feldname |
| `49.9` | Zahlenwert |

Passende Java-Klasse: `Produkt`.

JSON ist ein Datenformat. Es ist nicht Java-Code und nicht SQL.

---

## 7. Statuscodes

Typische Beobachtungen:

| Aufruf | Typischer Statuscode | Bedeutung |
|---|---|---|
| `GET /produkte` | `200` | erfolgreich |
| `POST /produkte` | `200` oder `201` | erfolgreich erstellt oder zurückgegeben |
| falscher Pfad | `404` | Endpoint nicht gefunden |
| ungültiges JSON | `400` | Request fehlerhaft |
| unerwarteter Serverfehler | `500` | Fehler im Server |

Nicht jedes Projekt liefert in dieser Phase schon für jeden fachlichen Fehler den perfekten Statuscode. Das wird später vertieft.

---

## 8. Ungültiger Request

Aufruf:

```bash
curl -i -X POST http://localhost:8080/produkte \
  -H "Content-Type: application/json" \
  -d '{"name":"Monitor","preis":}'
```

Erwartung:

```text
HTTP/1.1 400
```

Begründung:

Das JSON ist formal ungültig. Spring kann daraus kein `Produkt` erzeugen. Das Problem liegt im Request.

---

## 9. Weiterer Endpunkt

Beispiel:

```java
@GetMapping("/{id}")
public Produkt produktNachId(@PathVariable long id) {
    return lagerService.produktNachId(id);
}
```

Wichtig:

- `@PathVariable` liest die ID aus `/produkte/1`.
- Der Controller ruft den Service auf.
- Das Repository wird nicht direkt aus dem Controller verwendet.
- Fachlogik bleibt im Service.

---

## 10. JSON-Struktur erweitern

Beispiel:

```json
{
  "name": "Maus",
  "preis": 24.9,
  "bestand": 12
}
```

Wenn `Produkt` ein Feld `bestand` mit passenden Getter/Setter-Methoden hat, kann Spring den Wert zuordnen.

Wenn das Feld nicht existiert, hängt das Verhalten von der Projektkonfiguration ab. Für diese Einheit genügt:

```text
JSON-Felder müssen zur Java-Struktur passen.
```

Es wird noch keine DTO-Klasse eingeführt.

---

## 11. Request und Response dokumentieren

Beispiel:

```text
Request
Methode: POST
URL: http://localhost:8080/produkte
Header: Content-Type: application/json
Body: {"name":"Maus","preis":24.9}

Response
Statuscode: 200 oder 201
Header: Content-Type: application/json
Body: gespeichertes Produkt als JSON
```

Trennung:

- HTTP: Methode, URL, Header, Statuscode
- JSON: Body
- Fachlogik: Service-Regeln

---

## 12. Logging mit HTTP kombinieren

Sinnvolle Beobachtung:

- HTTP-Aufruf kommt beim Controller an.
- Controller ruft den Service auf.
- Service ruft Repository auf.
- Repository liest oder speichert Daten.

Logging kann diesen Ablauf sichtbar machen.

Logging ersetzt nicht:

- Statuscodes
- Tests
- Fachregeln im Service

---

## 13. Transferantworten

**Warum basiert REST auf HTTP?**

REST verwendet HTTP als Kommunikationsprotokoll. Requests und Responses transportieren Methode, URL, Header, Body und Statuscode.

**Warum ist JSON sinnvoll?**

JSON ist strukturiert, gut lesbar und kann von vielen Clients verarbeitet werden. Es eignet sich besser als freie Konsolentexte.

**Was ist der Unterschied zwischen Konsole und HTTP?**

Bei der Konsole gibt eine Person direkt Text in ein Menü ein. Bei HTTP sendet ein Client eine strukturierte Anfrage an einen Server. Die Service-Regeln können gleich bleiben.

**Warum sind Statuscodes wichtig?**

Ein Client erkennt damit, ob eine Anfrage erfolgreich war, ob die URL falsch war oder ob ein Serverproblem aufgetreten ist.

**Warum ist REST nur eine Zugriffsschicht?**

REST beschreibt den Zugriff von aussen. Die Fachlogik bleibt im `LagerService`, und die Persistenz bleibt im Repository.

---

## 14. Typische Fehlerhinweise

- Methode und Ressource werden verwechselt.
- Endpoint heisst `/produktSpeichern` statt `/produkte`.
- `GET` verändert Daten.
- `Content-Type` fehlt beim JSON-Body.
- JSON ist ungültig.
- Controller enthält Fachregeln.
- Repository wird direkt im Controller verwendet.
- HTTP und Spring werden gleichgesetzt.
- Statuscodes werden nicht angeschaut.
- URL-Struktur beschreibt Aktionen statt Ressourcen.

---

## 15. Verifikation

Die Beispiele verwenden bestehende Spring-Boot-REST-Endpunkte der Lagerverwaltung. Technisch geprüft wurde die lokale Maven-Verfügbarkeit mit `mvn -v`. Ein vollständiger Spring-Boot-Build wurde nicht ausgeführt, weil in diesem Repository kein konkretes Maven-Projekt mit `pom.xml` im Wurzelverzeichnis liegt.
