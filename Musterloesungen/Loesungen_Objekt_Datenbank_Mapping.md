# Lösungen – Mapping zwischen Objekten und Datenbank

Diese Musterlösung zeigt kompaktes manuelles Mapping im `DbProduktSpeicher`.

Kernidee:

```text
Objekte existieren im Java-Programm.
Tabellenzeilen existieren in der Datenbank.
DbProduktSpeicher übersetzt zwischen beiden.
```

Bewusst nicht verwendet werden ORM, Hibernate, JPA, Reflection, generische Mapper, Annotationen, Spring Data oder automatische Persistenz.

---

## 1. Mapping-Tabelle

| `Produkt` | Tabelle `PRODUKT` | Java-Typ | SQL-Typ | Lesen | Schreiben |
|---|---|---|---|---|---|
| `id` | `ID` | `int` | `INT` | `getInt("ID")` | `setInt(...)` |
| `name` | `NAME` | `String` | `VARCHAR(100)` | `getString("NAME")` | `setString(...)` |
| `preis` | `PREIS` | `double` | `DOUBLE` | `getDouble("PREIS")` | `setDouble(...)` |
| `bestand` | `BESTAND` | `int` | `INT` | `getInt("BESTAND")` | `setInt(...)` |

Die Zuordnung ist einfach, aber nicht automatisch. JDBC liefert Werte aus Spalten, keine fertigen Fachobjekte.

---

## 2. Kompakte Klassenbasis

Beispiel für `Produkt`:

```java
package ch.allianz.youngoitv.lager.model;

public class Produkt {
    private final int id;
    private final String name;
    private final double preis;
    private final int bestand;

    public Produkt(int id, String name, double preis, int bestand) {
        this.id = id;
        this.name = name;
        this.preis = preis;
        this.bestand = bestand;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getPreis() {
        return preis;
    }

    public int getBestand() {
        return bestand;
    }
}
```

---

## 3. `ResultSet` zu `Produkt`

```java
private Produkt leseProdukt(ResultSet resultSet) throws SQLException {
    int id = resultSet.getInt("ID");
    String name = resultSet.getString("NAME");
    double preis = resultSet.getDouble("PREIS");
    int bestand = resultSet.getInt("BESTAND");

    return new Produkt(id, name, preis, bestand);
}
```

Diese Methode übersetzt die aktuelle Zeile des `ResultSet` in ein `Produkt`.

Wichtig: Vorher muss `resultSet.next()` aufgerufen worden sein.

---

## 4. `Produkt` zu `PreparedStatement`

```java
private void setzeProduktWerte(PreparedStatement statement, Produkt produkt)
        throws SQLException {
    statement.setString(1, produkt.getName());
    statement.setDouble(2, produkt.getPreis());
    statement.setInt(3, produkt.getBestand());
}
```

Diese Methode passt zu SQL-Befehlen, bei denen die Platzhalter so angeordnet sind:

```sql
NAME = ?
PREIS = ?
BESTAND = ?
```

Die `ID` wird hier nicht gesetzt, weil sie je nach Operation anders behandelt wird.

---

## 5. INSERT-Mapping

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

Beim `INSERT` wird die `ID` nicht gesetzt. Die Tabelle erzeugt sie mit `AUTO_INCREMENT`.

---

## 6. UPDATE-Mapping

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

Die `ID` steht an Position `4`, weil sie zum vierten Platzhalter `WHERE ID = ?` gehört.

---

## 7. SELECT-Mapping für mehrere Produkte

```java
public ArrayList<Produkt> ladeProdukte(String quelle) {
    ArrayList<Produkt> produkte = new ArrayList<>();
    String sql = "SELECT ID, NAME, PREIS, BESTAND FROM PRODUKT ORDER BY ID";

    try (Connection connection = verbindungHerstellen(quelle)) {
        tabelleErstellen(connection);

        try (PreparedStatement statement = connection.prepareStatement(sql);
             ResultSet resultSet = statement.executeQuery()) {

            while (resultSet.next()) {
                produkte.add(leseProdukt(resultSet));
            }
        }
    } catch (SQLException exception) {
        throw new IllegalStateException("Produkte konnten nicht geladen werden.", exception);
    }

    return produkte;
}
```

`while (resultSet.next())` bewegt den Cursor von Zeile zu Zeile. Jede Zeile wird mit `leseProdukt(...)` in ein Objekt übersetzt.

---

## 8. Kompakter `DbProduktSpeicher`

`DbProduktSpeicher` bleibt eine konkrete Implementierung von `ProduktSpeicher`. Das Interface bleibt der Vertrag, das Mapping bleibt in der Datenbankklasse.

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;

public class DbProduktSpeicher implements ProduktSpeicher {
    private Connection verbindungHerstellen(String jdbcUrl) throws SQLException {
        return DriverManager.getConnection(jdbcUrl);
    }

    private void tabelleErstellen(Connection connection) throws SQLException {
        String sql = """
                CREATE TABLE IF NOT EXISTS PRODUKT (
                    ID INT AUTO_INCREMENT PRIMARY KEY,
                    NAME VARCHAR(100) NOT NULL,
                    PREIS DOUBLE NOT NULL,
                    BESTAND INT NOT NULL
                )
                """;

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.executeUpdate();
        }
    }

    @Override
    public void speichereProdukte(ArrayList<Produkt> produkte, String ziel) {
        try (Connection connection = verbindungHerstellen(ziel)) {
            tabelleErstellen(connection);
            produkteLoeschen(connection);

            for (Produkt produkt : produkte) {
                produktEinfuegen(connection, produkt);
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkte konnten nicht gespeichert werden.", exception);
        }
    }

    public void aktualisiereProdukt(String ziel, Produkt produkt) {
        try (Connection connection = verbindungHerstellen(ziel)) {
            tabelleErstellen(connection);
            produktAktualisieren(connection, produkt);
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkt konnte nicht aktualisiert werden.", exception);
        }
    }

    @Override
    public ArrayList<Produkt> ladeProdukte(String quelle) {
        ArrayList<Produkt> produkte = new ArrayList<>();
        String sql = "SELECT ID, NAME, PREIS, BESTAND FROM PRODUKT ORDER BY ID";

        try (Connection connection = verbindungHerstellen(quelle)) {
            tabelleErstellen(connection);

            try (PreparedStatement statement = connection.prepareStatement(sql);
                 ResultSet resultSet = statement.executeQuery()) {

                while (resultSet.next()) {
                    produkte.add(leseProdukt(resultSet));
                }
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkte konnten nicht geladen werden.", exception);
        }

        return produkte;
    }

    private void produktEinfuegen(Connection connection, Produkt produkt)
            throws SQLException {
        String sql = "INSERT INTO PRODUKT (NAME, PREIS, BESTAND) VALUES (?, ?, ?)";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            setzeProduktWerte(statement, produkt);
            statement.executeUpdate();
        }
    }

    private void produkteLoeschen(Connection connection) throws SQLException {
        String sql = "DELETE FROM PRODUKT";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.executeUpdate();
        }
    }

    private void produktAktualisieren(Connection connection, Produkt produkt)
            throws SQLException {
        String sql = "UPDATE PRODUKT SET NAME = ?, PREIS = ?, BESTAND = ? WHERE ID = ?";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            setzeProduktWerte(statement, produkt);
            statement.setInt(4, produkt.getId());
            statement.executeUpdate();
        }
    }

    private void setzeProduktWerte(PreparedStatement statement, Produkt produkt)
            throws SQLException {
        statement.setString(1, produkt.getName());
        statement.setDouble(2, produkt.getPreis());
        statement.setInt(3, produkt.getBestand());
    }

    private Produkt leseProdukt(ResultSet resultSet) throws SQLException {
        int id = resultSet.getInt("ID");
        String name = resultSet.getString("NAME");
        double preis = resultSet.getDouble("PREIS");
        int bestand = resultSet.getInt("BESTAND");

        return new Produkt(id, name, preis, bestand);
    }
}
```

Die Mapping-Methoden sind privat, weil sie Hilfslogik des `DbProduktSpeicher` sind.

---

## 9. Kurze Antworten zu Vertiefung und Transfer

**Warum ist Mapping notwendig?**
JDBC kennt Tabellen, Zeilen und Spalten. Die Anwendung arbeitet aber mit Objekten. Darum muss Code aus Spaltenwerten ein `Produkt` bauen und aus einem `Produkt` wieder SQL-Parameter setzen.

**Warum gehört Mapping nicht in `Main`?**
`Main` soll den Ablauf starten und Objekte verbinden. Wenn `Main` `ResultSet` liest oder `PreparedStatement` befüllt, vermischen sich Ablaufsteuerung und Persistenz.

**Warum bleibt `LagerService` frei von Mapping?**
`LagerService` enthält Fachlogik. Er soll mit `Produkt` arbeiten und nicht wissen, ob diese Produkte aus CSV, H2 oder einer anderen Persistenz kommen.

**CSV-Mapping vs. DB-Mapping**

| Frage | CSV | Datenbank |
|---|---|---|
| Rohdaten | Textzeile | Tabellenzeile im `ResultSet` |
| Werte trennen | `split(";")` | Spaltennamen oder Spaltenindex |
| Objekt erzeugen | Werte parsen und Konstruktor aufrufen | Werte mit `get...` lesen und Konstruktor aufrufen |
| typische Fehler | falsches Trennzeichen, falsche Reihenfolge | falscher Spaltenname, fehlendes `next()`, falscher Typ |

**Warum gibt es ORM-Frameworks?**
Mapping wiederholt sich häufig: Spaltennamen, Typumwandlung, `INSERT`, `UPDATE`, `SELECT` und Objekt-Erzeugung. ORM-Frameworks können Teile davon automatisieren. Für diese Einheit bleibt manuelles Mapping aber wichtig, damit klar wird, welches Problem solche Frameworks später lösen.

---

## 10. Typische Fehlerhinweise

- `ResultSet` ohne `next()` lesen: Es gibt keine aktuelle Zeile.
- Spaltennamen falsch schreiben: Der Code kompiliert, aber die Datenbankabfrage scheitert zur Laufzeit.
- Platzhalter falsch befüllen: Werte landen in falschen Spalten.
- `Statement` statt `PreparedStatement` verwenden: SQL wird fehleranfälliger und unsicherer.
- Mapping-Code in `Main` schreiben: Verantwortlichkeiten werden vermischt.
- Fachlogik im Mapping ergänzen: `DbProduktSpeicher` entscheidet dann fachlich statt technisch.
- Objekt unvollständig erzeugen: Spätere Fachlogik arbeitet mit fehlenden oder falschen Daten.
- Mapping mehrfach kopieren: Änderungen werden leicht an einer Stelle vergessen.

---

## 11. Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt mit H2 Embedded geprüft:

```text
mvn package
```

Ergebnis: `BUILD SUCCESS`.

Zusätzlich wurde eine kleine `Main` ausgeführt, die Produkte speichert, lädt und aktualisiert.

```text
Geladene Produkte: 2
Aktualisierte Produkte: 3
```
