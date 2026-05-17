# Lösungen – JDBC mit eingebetteter H2-Datenbank

Diese Musterlösung zeigt eine kompakte Standardlösung für den ersten JDBC-Einstieg.

Ziel ist nicht eine grosse Datenbankarchitektur, sondern ein nachvollziehbarer Ablauf:

```text
Maven Dependency
-> H2 Embedded
-> Connection
-> CREATE TABLE
-> INSERT / SELECT / UPDATE / DELETE
-> PreparedStatement
-> ResultSet lesen
```

Bewusst nicht verwendet werden ORM, Hibernate, JPA, Spring Data, Connection Pooling oder komplexe SQL-Abfragen.

---

## Basis

### Aufgabe 1 – Maven Dependency für H2

In `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <version>2.2.224</version>
    </dependency>
</dependencies>
```

Bei einem neuen Maven-Projekt soll Java 21 konfiguriert sein:

```xml
<properties>
    <maven.compiler.release>21</maven.compiler.release>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

Hinweis: Wenn Maven mit `Source option 5` oder `Target option 5` fehlschlägt, fehlt eine aktuelle Compiler-Konfiguration.

---

## Kompakte Standardlösung `DbDemo`

```java
package ch.allianz.youngoitv.lager;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class DbDemo {
    private static final String URL = "jdbc:h2:./data/lager";

    public static void main(String[] args) throws SQLException {
        try (Connection connection = DriverManager.getConnection(URL)) {
            tabelleZuruecksetzen(connection);
            tabelleErstellen(connection);

            produktEinfuegen(connection, "Maus", 24.90, 10);
            produktEinfuegen(connection, "Tastatur", 79.90, 5);

            System.out.println("Nach dem Einfügen:");
            produkteAusgeben(connection);

            bestandAktualisieren(connection, 1, 7);

            System.out.println("Nach dem Aktualisieren:");
            produkteAusgeben(connection);

            produktLoeschen(connection, 2);

            System.out.println("Nach dem Löschen:");
            produkteAusgeben(connection);
        }
    }

    private static void tabelleZuruecksetzen(Connection connection) throws SQLException {
        String sql = "DROP TABLE IF EXISTS PRODUKT";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.executeUpdate();
        }
    }

    private static void tabelleErstellen(Connection connection) throws SQLException {
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

    private static void produktEinfuegen(Connection connection, String name, double preis, int bestand)
            throws SQLException {
        String sql = "INSERT INTO PRODUKT (NAME, PREIS, BESTAND) VALUES (?, ?, ?)";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setString(1, name);
            statement.setDouble(2, preis);
            statement.setInt(3, bestand);
            statement.executeUpdate();
        }
    }

    private static void produkteAusgeben(Connection connection) throws SQLException {
        String sql = "SELECT ID, NAME, PREIS, BESTAND FROM PRODUKT ORDER BY ID";

        try (PreparedStatement statement = connection.prepareStatement(sql);
             ResultSet resultSet = statement.executeQuery()) {

            while (resultSet.next()) {
                int id = resultSet.getInt("ID");
                String name = resultSet.getString("NAME");
                double preis = resultSet.getDouble("PREIS");
                int bestand = resultSet.getInt("BESTAND");

                System.out.println(id + ": " + name + " / " + preis + " / " + bestand);
            }
        }
    }

    private static void bestandAktualisieren(Connection connection, int id, int neuerBestand)
            throws SQLException {
        String sql = "UPDATE PRODUKT SET BESTAND = ? WHERE ID = ?";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setInt(1, neuerBestand);
            statement.setInt(2, id);
            statement.executeUpdate();
        }
    }

    private static void produktLoeschen(Connection connection, int id) throws SQLException {
        String sql = "DELETE FROM PRODUKT WHERE ID = ?";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setInt(1, id);
            statement.executeUpdate();
        }
    }
}
```

Bei einer frischen Datenbank ist eine Ausgabe sinngemäss:

```text
Nach dem Einfügen:
1: Maus / 24.9 / 10
2: Tastatur / 79.9 / 5
Nach dem Aktualisieren:
1: Maus / 24.9 / 7
2: Tastatur / 79.9 / 5
Nach dem Löschen:
1: Maus / 24.9 / 7
```

Die Methode `tabelleZuruecksetzen(...)` macht die Demo reproduzierbar. In einer echten Anwendung würde man Daten nicht bei jedem Start löschen.

---

## Vertiefung

### Mehrere Produkte speichern

Eine einfache Variante:

```java
ArrayList<Produkt> produkte = new ArrayList<>();
produkte.add(new Produkt("Maus", 24.90, 10));
produkte.add(new Produkt("Tastatur", 79.90, 5));
produkte.add(new Produkt("Monitor", 249.00, 3));

for (Produkt produkt : produkte) {
    produktEinfuegen(connection, produkt.getName(), produkt.getPreis(), produkt.getBestand());
}
```

Die Schleife ist nur Ablauf. Das eigentliche `INSERT` bleibt in `produktEinfuegen(...)`.

### Produkt nach ID suchen

```java
private static void produktNachIdAusgeben(Connection connection, int id) throws SQLException {
    String sql = "SELECT ID, NAME, PREIS, BESTAND FROM PRODUKT WHERE ID = ?";

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        statement.setInt(1, id);

        try (ResultSet resultSet = statement.executeQuery()) {
            if (resultSet.next()) {
                System.out.println(
                        resultSet.getInt("ID") + ": "
                                + resultSet.getString("NAME") + " / "
                                + resultSet.getDouble("PREIS") + " / "
                                + resultSet.getInt("BESTAND"));
            } else {
                System.out.println("Kein Produkt mit ID " + id + " gefunden");
            }
        }
    }
}
```

Für genau ein erwartetes Produkt ist `if (resultSet.next())` passend. Für mehrere Zeilen verwendet man `while`.

### Ungültige Werte behandeln

Eine einfache Prüfung vor dem Speichern:

```java
private static boolean istGueltig(String name, double preis, int bestand) {
    return name != null && !name.isBlank() && preis >= 0 && bestand >= 0;
}
```

In einer sauberen Lagerverwaltung wäre diese Entscheidung fachliche Logik. Sie gehört deshalb eher in `LagerService` oder in eine fachliche Validierung, nicht direkt in SQL-Code.

---

## CSV und H2 vergleichen

| Frage | CSV | H2-Datenbank |
|---|---|---|
| Speicherung | Textdatei | Tabellen |
| Lesen | Zeilen parsen | `SELECT` |
| Ändern | Datei neu schreiben | `UPDATE` oder `DELETE` |
| Struktur | durch Format vereinbart | durch `CREATE TABLE` definiert |
| Einfachheit | sehr sichtbar | mehr Technik |
| Gezielte Abfrage | eingeschränkt | gut mit `WHERE` |

CSV reicht, wenn Daten klein, einfach und gut sichtbar bleiben sollen. Eine Datenbank hilft, wenn Daten gezielter gesucht, geändert oder strukturiert gespeichert werden sollen.

---

## Transfer

### H2 Embedded

```java
private static final String URL = "jdbc:h2:./data/lager";
```

H2 läuft im gleichen Java-Prozess. Das ist für den Einstieg einfach, weil kein separater Datenbankserver gestartet werden muss.

### H2 Server-Modus

H2 kann testweise als separater Prozess gestartet werden:

```bash
java -cp ~/.m2/repository/com/h2database/h2/2.2.224/h2-2.2.224.jar org.h2.tools.Server -tcp -ifNotExists
```

Dann wird die JDBC-URL angepasst:

```java
private static final String URL = "jdbc:h2:tcp://localhost/./data/lager";
```

Der neue Teil ist:

```text
tcp://localhost/
```

Damit verbindet sich Java nicht direkt mit einer eingebetteten Datenbankdatei, sondern mit einem laufenden H2-Server.

### `DbProduktSpeicher` als Idee

Eine spätere Klasse könnte so eingeordnet werden:

```text
ProduktSpeicher
├── CsvProduktSpeicher
└── DbProduktSpeicher
```

`DbProduktSpeicher` würde SQL und JDBC enthalten. `LagerService` bleibt für Fachlogik zuständig und soll keine SQL-Befehle kennen.

---

## Typische Fehlerhinweise

| Fehler | Folge | Verbesserung |
|---|---|---|
| `Connection` nicht schliessen | Ressource bleibt offen | `try (Connection ...)` verwenden |
| SQL mit `+` zusammenbauen | fehleranfällig und unsauber | `PreparedStatement` mit `?` verwenden |
| `ResultSet.next()` vergessen | Werte werden nicht korrekt gelesen | vor dem Lesen `next()` aufrufen |
| `executeQuery()` für `INSERT` verwenden | falsche JDBC-Methode | `executeUpdate()` für Änderungen |
| Embedded- und Server-URL verwechseln | Datenbank wird nicht gefunden oder neu erstellt | URL bewusst vergleichen |
| SQL in `LagerService` schreiben | Fachlogik und Persistenz vermischt | SQL in Speicherklasse verschieben |
| Exception leer abfangen | Fehlerursache verschwindet | Fehlermeldung ausgeben oder weiterreichen |

---

## Kurze Reflexion

- CSV ist ausreichend, wenn wenige Daten sichtbar und einfach gespeichert werden sollen.
- Eine Datenbank hilft, wenn gezielte Abfragen, Änderungen und klarere Tabellenstruktur wichtig werden.
- `LagerService` bleibt für fachliche Regeln zuständig.
- Persistenz ist austauschbar, weil `ProduktSpeicher` als gemeinsamer Vertrag dienen kann.
- Embedded-H2 läuft im Java-Prozess, H2 im Server-Modus läuft als separater Prozess.

---

## Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/jdbc-h2-loesungen-validierung` geprüft.

Ausgeführt:

```bash
mvn package
java -cp target/classes:/home/pm/.m2/repository/com/h2database/h2/2.2.224/h2-2.2.224.jar ch.allianz.youngoitv.lager.DbDemo
```

Ergebnis:

```text
BUILD SUCCESS
Nach dem Einfügen:
1: Maus / 24.9 / 10
2: Tastatur / 79.9 / 5
Nach dem Aktualisieren:
1: Maus / 24.9 / 7
2: Tastatur / 79.9 / 5
Nach dem Löschen:
1: Maus / 24.9 / 7
```

Hinweis: Für die technische Prüfung wurde eine frische temporäre H2-Datenbank unter `target/data` verwendet.
