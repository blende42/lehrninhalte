# Übungen – Mapping zwischen Objekten und Datenbank

## Vorwissen

Du brauchst:

- bekannte Lagerverwaltung
- `Produkt`
- `DbProduktSpeicher`
- H2 Embedded
- JDBC mit `Connection`, `PreparedStatement` und `ResultSet`
- Tabelle `PRODUKT`
- einfache SQL-Befehle
- `LagerService` als Fachlogik

Nicht verwendet werden:

- ORM
- Hibernate
- JPA
- Reflection
- generische Mapper
- Annotationen
- Spring Data
- automatische Persistenzframeworks

---

## Vorbereitung

Arbeite mit der bekannten Lagerverwaltung.

Beispielstruktur:

```text
lagerverwaltung-db/
  pom.xml
  data/
  src/main/java/
    ch/allianz/youngoitv/lager/
      Main.java
      LagerService.java
      ProduktSpeicher.java
      CsvProduktSpeicher.java
      DbProduktSpeicher.java
      model/Produkt.java
```

Die Tabelle `PRODUKT` soll diese Spalten besitzen:

```sql
CREATE TABLE IF NOT EXISTS PRODUKT (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    NAME VARCHAR(100) NOT NULL,
    PREIS DOUBLE NOT NULL,
    BESTAND INT NOT NULL
);
```

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
Du machst sichtbar, wo zwischen Objekt und Datenbankzeile übersetzt wird.
```

---

## Basis

### Aufgabe 1 – Mapping-Tabelle notieren

Erstelle eine kleine Zuordnungstabelle.

Auftrag:

1. Notiere alle Attribute von `Produkt`.
2. Notiere daneben die passenden Spalten der Tabelle `PRODUKT`.
3. Notiere den passenden Java-Typ.
4. Notiere den passenden SQL-Typ.

Erwartung:

```text
id      -> ID      -> int    -> INT
name    -> NAME    -> String -> VARCHAR
preis   -> PREIS   -> double -> DOUBLE
bestand -> BESTAND -> int    -> INT
```

---

### Aufgabe 2 – `Produkt` aus `ResultSet` erzeugen

Ergänze in `DbProduktSpeicher` eine private Methode.

```java
private Produkt leseProdukt(ResultSet resultSet) throws SQLException {
    int id = resultSet.getInt("ID");
    String name = resultSet.getString("NAME");
    double preis = resultSet.getDouble("PREIS");
    int bestand = resultSet.getInt("BESTAND");

    return new Produkt(id, name, preis, bestand);
}
```

Auftrag:

1. Ergänze die Imports für `ResultSet` und `SQLException`, falls sie fehlen.
2. Passe den Konstruktor an, falls deine `Produkt`-Klasse anders aufgebaut ist.
3. Erkläre in einem Satz, was diese Methode übersetzt.

---

### Aufgabe 3 – `ResultSet` korrekt lesen

Ergänze oder prüfe die Methode zum Laden aller Produkte.

```java
ArrayList<Produkt> produkte = new ArrayList<>();

while (resultSet.next()) {
    Produkt produkt = leseProdukt(resultSet);
    produkte.add(produkt);
}
```

Auftrag:

1. Verwende `while (resultSet.next())`.
2. Rufe `leseProdukt(resultSet)` innerhalb der Schleife auf.
3. Erkläre, warum `resultSet.next()` nötig ist.

Kontrollfrage:

```text
Was passiert, wenn du vor dem Lesen kein next() aufrufst?
```

---

### Aufgabe 4 – `PreparedStatement` mit Produktdaten befüllen

Ergänze eine private Hilfsmethode.

```java
private void setzeProduktWerte(PreparedStatement statement, Produkt produkt)
        throws SQLException {
    statement.setString(1, produkt.getName());
    statement.setDouble(2, produkt.getPreis());
    statement.setInt(3, produkt.getBestand());
}
```

Auftrag:

1. Ergänze den Import für `PreparedStatement`.
2. Prüfe die Reihenfolge der Platzhalter.
3. Erkläre, warum die `ID` hier noch nicht gesetzt wird.

---

### Aufgabe 5 – INSERT-Mapping erstellen

Verwende die Hilfsmethode beim Einfügen.

```java
private void produktEinfuegen(Connection connection, Produkt produkt)
        throws SQLException {
    String sql = "INSERT INTO PRODUKT (NAME, PREIS, BESTAND) VALUES (?, ?, ?)";

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        setzeProduktWerte(statement, produkt);
        statement.executeUpdate();
    }
}
```

Auftrag:

1. Prüfe, ob die drei Platzhalter zu `NAME`, `PREIS` und `BESTAND` passen.
2. Führe dein Programm aus oder starte passende Tests.
3. Prüfe, ob die Produkte danach in der Datenbank vorhanden sind.

---

### Aufgabe 6 – UPDATE-Mapping erstellen

Ergänze eine Aktualisierung.

```java
private void produktAktualisieren(Connection connection, Produkt produkt)
        throws SQLException {
    String sql = "UPDATE PRODUKT SET NAME = ?, PREIS = ?, BESTAND = ? WHERE ID = ?";

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        setzeProduktWerte(statement, produkt);
        statement.setInt(4, produkt.getId());
        statement.executeUpdate();
    }
}
```

Auftrag:

1. Erkläre, warum die `ID` beim `UPDATE` gebraucht wird.
2. Prüfe, warum die `ID` an Position `4` gesetzt wird.
3. Ändere ein Produkt und prüfe, ob nur dieses Produkt geändert wird.

---

### Aufgabe 7 – SELECT-Ergebnis in Objekte umwandeln

Schreibe oder prüfe eine Methode `ladeProdukte`.

Minimaler Ablauf:

```text
Verbindung herstellen
Tabelle erstellen
SELECT vorbereiten
ResultSet lesen
pro Zeile ein Produkt erzeugen
Liste zurückgeben
```

Auftrag:

1. Verwende `SELECT ID, NAME, PREIS, BESTAND FROM PRODUKT ORDER BY ID`.
2. Verwende `leseProdukt(resultSet)`.
3. Gib eine `ArrayList<Produkt>` zurück.
4. Schreibe keinen SQL-Code in `Main`.

---

### Aufgabe 8 – Mapping-Code strukturieren

Prüfe deinen `DbProduktSpeicher`.

Auftrag:

1. Markiere alle Stellen, an denen aus Datenbankwerten ein Objekt entsteht.
2. Markiere alle Stellen, an denen aus einem Objekt Datenbankwerte entstehen.
3. Lagere doppelte Stellen in private Hilfsmethoden aus.
4. Führe `mvn package` aus.

Erwartung:

```text
DbProduktSpeicher bleibt die Klasse für JDBC und Mapping.
LagerService bleibt fachlich.
Main bleibt Ablaufsteuerung.
```

Kurze Prüfung:

1. `mvn package` läuft ohne Fehler.
2. Ein Produkt kann gespeichert werden.
3. Mehrere Produkte können geladen werden.
4. Ein Produkt kann aktualisiert werden.
5. `Main` enthält keinen SQL-Code.

---

## Vertiefung

### Aufgabe 9 – Fehlerhafte Datensätze behandeln

Diskutiere oder teste einfache Fehlerfälle.

Auftrag:

1. Was passiert, wenn `NAME` in der Datenbank `NULL` wäre?
2. Was passiert, wenn `PREIS` als falscher Typ gelesen wird?
3. Was passiert, wenn eine Spalte falsch geschrieben ist?
4. Notiere, welcher Fehler zur Datenbank gehört und welcher zur Fachlogik gehört.

Hinweis: Die Tabelle verwendet aktuell `NOT NULL`. Dadurch werden einige Fehler bereits durch die Datenbank verhindert.

---

### Aufgabe 10 – `null`-Werte diskutieren

Beantworte schriftlich:

1. Darf ein Produkt ohne Name existieren?
2. Soll diese Regel in der Datenbank, im Konstruktor oder im `LagerService` geprüft werden?
3. Welche Rolle hat `DbProduktSpeicher` dabei?

Ziel:

```text
Mapping soll übersetzen, aber nicht unnötig Fachlogik übernehmen.
```

---

### Aufgabe 11 – Datentypen vergleichen

Erstelle eine Tabelle mit diesen Spalten:

```text
Feld
Java-Typ
SQL-Typ
JDBC-Lesemethode
JDBC-Schreibmethode
```

Nutze:

- `id`
- `name`
- `preis`
- `bestand`

---

### Aufgabe 12 – Doppelte Mapping-Logik erkennen

Suche in deinem Code nach wiederholten Stellen.

Auftrag:

1. Wo werden `NAME`, `PREIS` und `BESTAND` mehrfach erwähnt?
2. Wo werden `setString`, `setDouble` und `setInt` wiederholt?
3. Welche Wiederholung ist für EFZ-Niveau noch gut verständlich?
4. Welche Wiederholung würdest du in eine private Methode verschieben?

Nicht umsetzen:

- generischer Mapper
- Reflection
- Annotationen
- ORM

---

### Aufgabe 13 – Mapping für Änderungsobjekte ergänzen

Übertrage die Idee auf `AenderungsEintrag`.

Auftrag:

1. Notiere die Spalten der Tabelle `AENDERUNG`.
2. Notiere die Attribute von `AenderungsEintrag`.
3. Erstelle eine Mapping-Tabelle.
4. Beschreibe, welche Methode aus einem `ResultSet` einen `AenderungsEintrag` erzeugen könnte.

Du musst hier keinen vollständigen Code schreiben, wenn die Struktur klar ist.

---

## Transfer

### Aufgabe 14 – Warum Mapping notwendig ist

Erkläre in eigenen Worten:

```text
Warum kann JDBC nicht einfach ein Produkt-Objekt aus der Datenbank zurückgeben?
```

Nutze in deiner Antwort die Begriffe:

- Objekt
- Tabelle
- Zeile
- Spalte
- `ResultSet`
- Mapping

---

### Aufgabe 15 – CSV-Mapping vs. DB-Mapping

Vergleiche:

| Frage | CSV | Datenbank |
|---|---|---|
| Woher kommen die Rohdaten? |  |  |
| Wie werden Werte getrennt? |  |  |
| Wie entsteht ein `Produkt`? |  |  |
| Welche Fehler sind typisch? |  |  |

Ergänze die Tabelle.

---

### Aufgabe 16 – Warum gibt es ORM-Frameworks?

Diskutiere kurz:

1. Welche Arbeit wiederholt sich beim Mapping?
2. Was könnten Frameworks später automatisieren?
3. Warum ist es trotzdem sinnvoll, Mapping zuerst von Hand zu verstehen?

Verwende keine ORM-Frameworks in deinem Code.

---

### Aufgabe 17 – Mapping gehört nicht in `Main`

Begründe schriftlich:

1. Welche Aufgaben hat `Main`?
2. Welche Aufgaben hat `DbProduktSpeicher`?
3. Was würde unübersichtlich, wenn `Main` direkt `ResultSet` liest?
4. Warum bleibt `LagerService` dadurch einfacher testbar?

---

### Aufgabe 18 – Weitere Persistenzarten

Diskutiere weitere mögliche Speicherarten:

- JSON-Datei
- REST-API
- andere relationale Datenbank
- In-Memory-Speicher für Tests

Auftrag:

1. Wäre auch dort Mapping nötig?
2. Was müsste übersetzt werden?
3. Welche Klasse sollte diese Übersetzung übernehmen?

---

## Reflexion

Beantworte zum Schluss:

1. Warum existiert ein Objekt nicht direkt in der Datenbank?
2. Welche Verantwortung besitzt `DbProduktSpeicher`?
3. Warum wird Mapping repetitiv?
4. Welche Teile des Codes waren fehleranfällig?
5. Warum helfen klare Verantwortlichkeiten?
6. Welche Teile der Anwendung mussten wegen Mapping nicht geändert werden?
