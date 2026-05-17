# Lösungen – Bestehende Persistenz auf Datenbank erweitern

Diese Musterlösung zeigt eine kompakte Standardlösung für eine wachsende Persistenz. Die bestehende Produkt-Persistenz bleibt erhalten. Neu kommt eine Persistenz für Änderungsdaten dazu.

Kernidee:

```text
Die Architektur wächst.
Fachlogik bleibt im LagerService.
JDBC-Code bleibt in DB-Speicherklassen.
Main bleibt Ablaufsteuerung.
```

Bewusst nicht verwendet werden ORM, Hibernate, JPA, Spring Data, generische Persistence-Abstraktionen, DAO-Frameworks, Connection Pooling oder komplexe Joins.

---

## Maven-Dependency

Für H2 braucht das Projekt:

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.2.224</version>
</dependency>
```

Bei einem neuen Maven-Projekt sollte Java 21 konfiguriert sein.

```xml
<properties>
    <maven.compiler.release>21</maven.compiler.release>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

---

## Struktur

Vorher:

```text
ProduktSpeicher
├── CsvProduktSpeicher
└── DbProduktSpeicher
```

Neu:

```text
AenderungsSpeicher
├── CsvAenderungsSpeicher
└── DbAenderungsSpeicher
```

`DbProduktSpeicher` speichert Produktdaten. `DbAenderungsSpeicher` speichert Änderungsdaten. Beide dürfen JDBC verwenden. `LagerService` soll weiterhin keine SQL-Befehle enthalten.

---

## `AenderungsEintrag`

```java
package ch.allianz.youngoitv.lager;

public class AenderungsEintrag {
    private final String produktName;
    private final String art;
    private final String alterWert;
    private final String neuerWert;
    private final String zeitpunkt;

    public AenderungsEintrag(String produktName, String art, String alterWert,
                             String neuerWert, String zeitpunkt) {
        this.produktName = produktName;
        this.art = art;
        this.alterWert = alterWert;
        this.neuerWert = neuerWert;
        this.zeitpunkt = zeitpunkt;
    }

    public String getProduktName() {
        return produktName;
    }

    public String getArt() {
        return art;
    }

    public String getAlterWert() {
        return alterWert;
    }

    public String getNeuerWert() {
        return neuerWert;
    }

    public String getZeitpunkt() {
        return zeitpunkt;
    }
}
```

`AenderungsEintrag` hält Daten. Die Klasse enthält keine SQL-Logik.

---

## `AenderungsSpeicher`

```java
package ch.allianz.youngoitv.lager;

import java.util.ArrayList;

public interface AenderungsSpeicher {
    void speichereAenderung(AenderungsEintrag eintrag, String ziel);

    ArrayList<AenderungsEintrag> ladeAenderungen(String quelle);
}
```

Das Interface beschreibt den Vertrag. CSV und Datenbank können ihn unterschiedlich umsetzen.

---

## `DbAenderungsSpeicher`

```java
package ch.allianz.youngoitv.lager;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;

public class DbAenderungsSpeicher implements AenderungsSpeicher {
    private Connection verbindungHerstellen(String jdbcUrl) throws SQLException {
        return DriverManager.getConnection(jdbcUrl);
    }

    private void tabelleErstellen(Connection connection) throws SQLException {
        String sql = """
                CREATE TABLE IF NOT EXISTS AENDERUNG (
                    ID INT AUTO_INCREMENT PRIMARY KEY,
                    PRODUKT_NAME VARCHAR(100) NOT NULL,
                    ART VARCHAR(30) NOT NULL,
                    ALTER_WERT VARCHAR(50) NOT NULL,
                    NEUER_WERT VARCHAR(50) NOT NULL,
                    ZEITPUNKT VARCHAR(30) NOT NULL
                )
                """;

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.executeUpdate();
        }
    }

    @Override
    public void speichereAenderung(AenderungsEintrag eintrag, String ziel) {
        String sql = """
                INSERT INTO AENDERUNG
                (PRODUKT_NAME, ART, ALTER_WERT, NEUER_WERT, ZEITPUNKT)
                VALUES (?, ?, ?, ?, ?)
                """;

        try (Connection connection = verbindungHerstellen(ziel)) {
            tabelleErstellen(connection);

            try (PreparedStatement statement = connection.prepareStatement(sql)) {
                statement.setString(1, eintrag.getProduktName());
                statement.setString(2, eintrag.getArt());
                statement.setString(3, eintrag.getAlterWert());
                statement.setString(4, eintrag.getNeuerWert());
                statement.setString(5, eintrag.getZeitpunkt());
                statement.executeUpdate();
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Aenderung konnte nicht gespeichert werden.", exception);
        }
    }

    @Override
    public ArrayList<AenderungsEintrag> ladeAenderungen(String quelle) {
        ArrayList<AenderungsEintrag> eintraege = new ArrayList<>();
        String sql = """
                SELECT PRODUKT_NAME, ART, ALTER_WERT, NEUER_WERT, ZEITPUNKT
                FROM AENDERUNG
                ORDER BY ID
                """;

        try (Connection connection = verbindungHerstellen(quelle)) {
            tabelleErstellen(connection);

            try (PreparedStatement statement = connection.prepareStatement(sql);
                 ResultSet resultSet = statement.executeQuery()) {

                while (resultSet.next()) {
                    eintraege.add(eintragAusResultSet(resultSet));
                }
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Aenderungen konnten nicht geladen werden.", exception);
        }

        return eintraege;
    }

    public ArrayList<AenderungsEintrag> ladeAenderungenFuerProdukt(String jdbcUrl, String produktName) {
        ArrayList<AenderungsEintrag> eintraege = new ArrayList<>();
        String sql = """
                SELECT PRODUKT_NAME, ART, ALTER_WERT, NEUER_WERT, ZEITPUNKT
                FROM AENDERUNG
                WHERE PRODUKT_NAME = ?
                ORDER BY ID
                """;

        try (Connection connection = verbindungHerstellen(jdbcUrl)) {
            tabelleErstellen(connection);

            try (PreparedStatement statement = connection.prepareStatement(sql)) {
                statement.setString(1, produktName);

                try (ResultSet resultSet = statement.executeQuery()) {
                    while (resultSet.next()) {
                        eintraege.add(eintragAusResultSet(resultSet));
                    }
                }
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Aenderungen konnten nicht gefiltert werden.", exception);
        }

        return eintraege;
    }

    public ArrayList<AenderungsEintrag> ladeAenderungenNachArt(String jdbcUrl, String art) {
        ArrayList<AenderungsEintrag> eintraege = new ArrayList<>();
        String sql = """
                SELECT PRODUKT_NAME, ART, ALTER_WERT, NEUER_WERT, ZEITPUNKT
                FROM AENDERUNG
                WHERE ART = ?
                ORDER BY ID
                """;

        try (Connection connection = verbindungHerstellen(jdbcUrl)) {
            tabelleErstellen(connection);

            try (PreparedStatement statement = connection.prepareStatement(sql)) {
                statement.setString(1, art);

                try (ResultSet resultSet = statement.executeQuery()) {
                    while (resultSet.next()) {
                        eintraege.add(eintragAusResultSet(resultSet));
                    }
                }
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Aenderungen konnten nicht nach Art geladen werden.", exception);
        }

        return eintraege;
    }

    public void neuerWertAktualisieren(String jdbcUrl, int id, String neuerWert) {
        String sql = "UPDATE AENDERUNG SET NEUER_WERT = ? WHERE ID = ?";

        try (Connection connection = verbindungHerstellen(jdbcUrl);
             PreparedStatement statement = connection.prepareStatement(sql)) {

            statement.setString(1, neuerWert);
            statement.setInt(2, id);
            statement.executeUpdate();
        } catch (SQLException exception) {
            throw new IllegalStateException("Aenderung konnte nicht aktualisiert werden.", exception);
        }
    }

    public void loescheAenderung(String jdbcUrl, int id) {
        String sql = "DELETE FROM AENDERUNG WHERE ID = ?";

        try (Connection connection = verbindungHerstellen(jdbcUrl);
             PreparedStatement statement = connection.prepareStatement(sql)) {

            statement.setInt(1, id);
            statement.executeUpdate();
        } catch (SQLException exception) {
            throw new IllegalStateException("Aenderung konnte nicht geloescht werden.", exception);
        }
    }

    private AenderungsEintrag eintragAusResultSet(ResultSet resultSet) throws SQLException {
        String produktName = resultSet.getString("PRODUKT_NAME");
        String art = resultSet.getString("ART");
        String alterWert = resultSet.getString("ALTER_WERT");
        String neuerWert = resultSet.getString("NEUER_WERT");
        String zeitpunkt = resultSet.getString("ZEITPUNKT");

        return new AenderungsEintrag(produktName, art, alterWert, neuerWert, zeitpunkt);
    }
}
```

Hinweise:

- `CREATE TABLE IF NOT EXISTS` erzeugt die Tabelle nur, wenn sie noch fehlt.
- `INSERT`, `SELECT`, `UPDATE` und `DELETE` zeigen CRUD auf Änderungsdaten.
- `WHERE ID = ?` verhindert, dass zu viele Zeilen geändert oder gelöscht werden.
- `eintragAusResultSet(...)` bündelt das Mapping von Datenbankzeile zu Objekt.
- Jede JDBC-Ressource wird mit `try-with-resources` geschlossen.

---

## `Main` bleibt klein

`Main` verbindet die Bausteine. SQL steht weiterhin nicht in `Main`.

```java
package ch.allianz.youngoitv.lager;

public class Main {
    public static void main(String[] args) {
        String ziel = "jdbc:h2:./data/lager";

        AenderungsSpeicher aenderungsSpeicher = new DbAenderungsSpeicher();

        aenderungsSpeicher.speichereAenderung(
                new AenderungsEintrag("Maus", "PREIS", "24.90", "22.90", "2026-05-17T10:15"),
                ziel);

        aenderungsSpeicher.speichereAenderung(
                new AenderungsEintrag("Tastatur", "BESTAND", "5", "8", "2026-05-17T10:20"),
                ziel);

        for (AenderungsEintrag eintrag : aenderungsSpeicher.ladeAenderungen(ziel)) {
            System.out.println(eintrag.getProduktName()
                    + " / " + eintrag.getArt()
                    + " / " + eintrag.getAlterWert()
                    + " -> " + eintrag.getNeuerWert());
        }
    }
}
```

In einem vollständigen Projekt kann `Main` zusätzlich `DbProduktSpeicher` und `LagerService` verwenden. Die Grundregel bleibt gleich: `Main` steuert, Services entscheiden fachlich, Speicherklassen speichern.

---

## `LagerService` bleibt stabil

Der bestehende `LagerService` soll fachliche Regeln enthalten, aber keine Datenbankdetails.

```java
public class LagerService {
    public boolean verkaufen(Produkt produkt, int menge) {
        if (menge <= 0 || produkt.getBestand() < menge) {
            return false;
        }

        produkt.setBestand(produkt.getBestand() - menge);
        return true;
    }
}
```

Wichtig:

```text
Kein SQL im LagerService.
Keine Connection im LagerService.
Keine Tabelle AENDERUNG im LagerService.
```

---

## CSV vs. Datenbank

| Frage | CSV | H2-Datenbank |
|---|---|---|
| Produktdaten | eine Produktdatei | Tabelle `PRODUKT` |
| Änderungsdaten | weitere CSV-Datei | Tabelle `AENDERUNG` |
| Filtern | Datei lesen und im Java-Code prüfen | `WHERE` |
| Struktur | Dateiformat muss stimmen | Tabellenschema |
| Wachstum | mehrere Dateien und Parser | mehrere Tabellen und SQL |

Beides ist möglich. In beiden Fällen sollen Fachlogik und Persistenz getrennt bleiben.

---

## Typische Fehlerhinweise

| Fehler | Korrektur |
|---|---|
| JDBC-Code steht in `Main` | SQL in `DbAenderungsSpeicher` verschieben |
| SQL steht im `LagerService` | Fachlogik und Persistenz wieder trennen |
| `ResultSet` wird mehrfach gleich ausgelesen | Mapping in `eintragAusResultSet(...)` bündeln |
| `Statement` statt `PreparedStatement` | Platzhalter `?` verwenden |
| `Connection` bleibt offen | `try-with-resources` verwenden |
| `UPDATE` oder `DELETE` ohne `WHERE` | immer gezielt einschränken |
| neue generische Architektur wird zu früh gebaut | zuerst konkrete Speicherklassen verständlich halten |
| Speicherklasse entscheidet fachlich | fachliche Entscheidung in den Service verschieben |

---

## Hinweise zu zukünftigem Refactoring

Wiederholungen zwischen `DbProduktSpeicher` und `DbAenderungsSpeicher` sind jetzt sichtbar:

- Verbindung herstellen
- Tabelle erstellen
- `try-with-resources`
- Exceptions verpacken
- `ResultSet` zu Objekt mappen

Für diese Einheit ist die Wiederholung akzeptiert, weil sie das JDBC-Muster trainiert. Später könnte man kleine Hilfsmethoden prüfen. Eine generische Persistenzarchitektur wäre hier noch zu früh.

---

## Reflexionsantworten

1. Stabil bleiben vor allem `LagerService`, `Produkt`, `ProduktSpeicher` und die Grundrolle von `Main`.
2. Ergänzt werden `AenderungsEintrag`, `AenderungsSpeicher` und `DbAenderungsSpeicher`.
3. Interfaces helfen, weil Aufrufer mit einem Vertrag arbeiten und die konkrete Speicherart austauschbar bleibt.
4. Schwieriger wird die Struktur durch mehrere Tabellen und mehrere Speicherklassen.
5. Wiederholungen sieht man bei Verbindung, `PreparedStatement`, `ResultSet`, Mapping und Exception-Behandlung.
6. Refactoring wird sinnvoll, wenn dieselbe technische Logik an vielen Stellen geändert werden muss.

---

## Verifikation

Die Java-Beispiele wurden in einem temporären Maven-Projekt unter `/tmp/persistenz_db_erweitern_validation` geprüft.

Ausgeführt:

```bash
mvn package
```

Ergebnis:

```text
BUILD SUCCESS
```

Zusätzlich wurde `Main` mit H2 ausgeführt.

Ausgabe sinngemäss:

```text
2
1
21.90
1
```

Die erste Zahl zeigt alle gespeicherten Änderungen. Die zweite Zahl zeigt die gefilterten Änderungen für ein Produkt.
`21.90` zeigt das aktualisierte Feld. Die letzte Zahl zeigt die Anzahl nach dem Löschen einer Änderung.

Einschränkung: Geprüft wurde ein kompaktes temporäres Beispielprojekt, nicht ein vollständiges Lernendenprojekt mit bestehendem `DbProduktSpeicher`.
