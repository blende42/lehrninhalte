# Lösungen – DbProduktSpeicher mit JDBC und H2

Diese Musterlösung zeigt eine kompakte Standardlösung für eine austauschbare Datenbank-Persistenz.

Kernidee:

```text
ProduktSpeicher bleibt der Vertrag.
CsvProduktSpeicher und DbProduktSpeicher sind konkrete Implementierungen.
LagerService bleibt unverändert.
JDBC-Code gehört in DbProduktSpeicher, nicht in Main.
```

Bewusst nicht verwendet werden ORM, Hibernate, JPA, Spring Data, Connection Pooling, Migrationstools oder komplexe Architektur.

---

## Maven-Dependency

In `pom.xml` braucht das Projekt H2.

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.2.224</version>
</dependency>
```

Falls der kurze Test übernommen wird und JUnit noch nicht vorhanden ist, braucht das Projekt zusätzlich JUnit Jupiter.

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.2</version>
    <scope>test</scope>
</dependency>
```

Bei einem neuen Maven-Projekt soll Java 21 sauber konfiguriert sein.

```xml
<properties>
    <maven.compiler.release>21</maven.compiler.release>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

Falls Maven trotzdem mit `Source option 5` oder `Target option 5` fehlschlägt, hilft eine aktuelle Compiler-Plugin-Konfiguration.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.12.1</version>
    <configuration>
        <release>21</release>
    </configuration>
</plugin>
```

---

## `ProduktSpeicher`

Das Interface bleibt der gemeinsame Vertrag.

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public interface ProduktSpeicher {
    ArrayList<Produkt> ladeProdukte(String quelle);

    void speichereProdukte(ArrayList<Produkt> produkte, String ziel);
}
```

Für CSV ist `quelle` oder `ziel` ein Dateipfad. Für H2 ist es eine JDBC-URL.

---

## `Produkt`

```java
package ch.allianz.youngoitv.lager.model;

public class Produkt {
    private final String name;
    private final double preis;
    private int bestand;

    public Produkt(String name, double preis, int bestand) {
        this.name = name;
        this.preis = preis;
        this.bestand = bestand;
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

    public void setBestand(int bestand) {
        this.bestand = bestand;
    }
}
```

`Produkt` hält Daten. Es enthält keine SQL-Logik.

---

## `LagerService` bleibt unverändert

Der Service enthält Fachlogik. Er weiss nicht, ob CSV oder H2 verwendet wird.

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;

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
Keine Connection.
Kein SQL.
Kein PreparedStatement.
```

---

## `DbProduktSpeicher`

Diese Klasse implementiert `ProduktSpeicher` und enthält den JDBC-Code.

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

    private void datenbankLeeren(Connection connection) throws SQLException {
        String sql = "DELETE FROM PRODUKT";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.executeUpdate();
        }
    }

    private void produktEinfuegen(Connection connection, Produkt produkt) throws SQLException {
        String sql = "INSERT INTO PRODUKT (NAME, PREIS, BESTAND) VALUES (?, ?, ?)";

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setString(1, produkt.getName());
            statement.setDouble(2, produkt.getPreis());
            statement.setInt(3, produkt.getBestand());
            statement.executeUpdate();
        }
    }

    @Override
    public void speichereProdukte(ArrayList<Produkt> produkte, String ziel) {
        try (Connection connection = verbindungHerstellen(ziel)) {
            tabelleErstellen(connection);
            datenbankLeeren(connection);

            for (Produkt produkt : produkte) {
                produktEinfuegen(connection, produkt);
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkte konnten nicht gespeichert werden.", exception);
        }
    }

    @Override
    public ArrayList<Produkt> ladeProdukte(String quelle) {
        ArrayList<Produkt> produkte = new ArrayList<>();

        try (Connection connection = verbindungHerstellen(quelle)) {
            tabelleErstellen(connection);
            String sql = "SELECT NAME, PREIS, BESTAND FROM PRODUKT ORDER BY ID";

            try (PreparedStatement statement = connection.prepareStatement(sql);
                 ResultSet resultSet = statement.executeQuery()) {

                while (resultSet.next()) {
                    String name = resultSet.getString("NAME");
                    double preis = resultSet.getDouble("PREIS");
                    int bestand = resultSet.getInt("BESTAND");
                    produkte.add(new Produkt(name, preis, bestand));
                }
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkte konnten nicht geladen werden.", exception);
        }

        return produkte;
    }

    public void bestandAktualisieren(String jdbcUrl, int id, int neuerBestand) {
        String sql = "UPDATE PRODUKT SET BESTAND = ? WHERE ID = ?";

        try (Connection connection = verbindungHerstellen(jdbcUrl);
             PreparedStatement statement = connection.prepareStatement(sql)) {

            statement.setInt(1, neuerBestand);
            statement.setInt(2, id);
            statement.executeUpdate();
        } catch (SQLException exception) {
            throw new IllegalStateException("Bestand konnte nicht aktualisiert werden.", exception);
        }
    }

    public void produktLoeschen(String jdbcUrl, int id) {
        String sql = "DELETE FROM PRODUKT WHERE ID = ?";

        try (Connection connection = verbindungHerstellen(jdbcUrl);
             PreparedStatement statement = connection.prepareStatement(sql)) {

            statement.setInt(1, id);
            statement.executeUpdate();
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkt konnte nicht gelöscht werden.", exception);
        }
    }

    public Produkt produktNachIdSuchen(String jdbcUrl, int id) {
        String sql = "SELECT NAME, PREIS, BESTAND FROM PRODUKT WHERE ID = ?";

        try (Connection connection = verbindungHerstellen(jdbcUrl);
             PreparedStatement statement = connection.prepareStatement(sql)) {

            statement.setInt(1, id);

            try (ResultSet resultSet = statement.executeQuery()) {
                if (resultSet.next()) {
                    String name = resultSet.getString("NAME");
                    double preis = resultSet.getDouble("PREIS");
                    int bestand = resultSet.getInt("BESTAND");
                    return new Produkt(name, preis, bestand);
                }
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkt konnte nicht gesucht werden.", exception);
        }

        return null;
    }
}
```

Hinweise:

- `CREATE TABLE IF NOT EXISTS` sorgt dafür, dass die Tabelle beim ersten Zugriff angelegt wird.
- `speichereProdukte(...)` leert die Tabelle und schreibt die aktuelle Liste neu. Das ist für den Einstieg einfach nachvollziehbar.
- Diese einfache Speicherstrategie erhält Datenbank-IDs nicht dauerhaft stabil. Für diese Lerneinheit ist das bewusst akzeptiert.
- Jede Methode öffnet selbst eine Verbindung. Das ist für die Übung einfach, ersetzt aber kein Connection Pooling.
- `PreparedStatement` setzt Werte über Platzhalter ein.
- `ResultSet` wird immer zuerst mit `next()` bewegt.
- `UPDATE` und `DELETE` verwenden `WHERE ID = ?`.

---

## `Main` mit `DbProduktSpeicher`

`Main` wechselt nur die konkrete Implementierung. Die Fachlogik bleibt im `LagerService`.

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        String ziel = "jdbc:h2:./data/lager";
        ProduktSpeicher speicher = new DbProduktSpeicher();

        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Maus", 24.90, 10));
        produkte.add(new Produkt("Tastatur", 79.90, 5));
        speicher.speichereProdukte(produkte, ziel);

        ArrayList<Produkt> geladeneProdukte = speicher.ladeProdukte(ziel);
        LagerService lagerService = new LagerService();
        lagerService.verkaufen(geladeneProdukte.get(0), 3);

        speicher.speichereProdukte(geladeneProdukte, ziel);

        for (Produkt produkt : speicher.ladeProdukte(ziel)) {
            System.out.println(produkt.getName() + " / " + produkt.getPreis() + " / " + produkt.getBestand());
        }
    }
}
```

Ausgabe sinngemäss:

```text
Maus / 24.9 / 7
Tastatur / 79.9 / 5
```

Der Verkauf wurde vom `LagerService` ausgeführt. Das Speichern und Laden wurde von `DbProduktSpeicher` erledigt.

Die Startdaten in `Main` dienen nur als kurze Demo. In einer echten Anwendung würde `Main` nicht bei jedem Start dieselben Produktdaten neu speichern.

---

## Kurzer Test

Ein kleiner JUnit-Test kann Speichern, Laden, Aktualisieren und Löschen prüfen.

```java
package ch.allianz.youngoitv.lager;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertNotNull;
import static org.junit.jupiter.api.Assertions.assertNull;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;
import org.junit.jupiter.api.Test;

class DbProduktSpeicherTest {
    @Test
    void speichertLaedtAktualisiertUndLoeschtProdukte() {
        String url = "jdbc:h2:mem:lager_test;DB_CLOSE_DELAY=-1";
        DbProduktSpeicher speicher = new DbProduktSpeicher();

        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Maus", 24.90, 10));
        produkte.add(new Produkt("Tastatur", 79.90, 5));

        speicher.speichereProdukte(produkte, url);

        ArrayList<Produkt> geladen = speicher.ladeProdukte(url);
        assertEquals(2, geladen.size());
        assertEquals("Maus", geladen.get(0).getName());
        assertEquals(10, geladen.get(0).getBestand());

        speicher.bestandAktualisieren(url, 1, 7);
        Produkt produkt = speicher.produktNachIdSuchen(url, 1);
        assertNotNull(produkt);
        assertEquals(7, produkt.getBestand());

        speicher.produktLoeschen(url, 2);
        assertNull(speicher.produktNachIdSuchen(url, 2));
    }
}
```

Für Tests ist eine In-Memory-Datenbank praktisch:

```text
jdbc:h2:mem:lager_test;DB_CLOSE_DELAY=-1
```

Für die normale lokale Anwendung wird H2 Embedded mit Datei verwendet:

```text
jdbc:h2:./data/lager
```

---

## CSV und Datenbank vergleichen

| Frage | `CsvProduktSpeicher` | `DbProduktSpeicher` |
|---|---|---|
| Speicherort | Textdatei | H2-Datenbankdatei oder In-Memory-DB |
| Laden | Datei lesen, Zeilen parsen | `SELECT` mit `ResultSet` |
| Speichern | CSV-Zeilen schreiben | `INSERT` mit `PreparedStatement` |
| Ändern | meist Datei neu schreiben | `UPDATE` mit `WHERE` |
| Löschen | meist Datei neu schreiben | `DELETE` mit `WHERE` |
| Struktur | CSV-Format muss stimmen | Tabelle `PRODUKT` definiert Spalten |
| Fachlogik | gehört nicht hinein | gehört nicht hinein |

Merksatz:

```text
Persistenz ist austauschbar, weil Main und LagerService mit dem Vertrag ProduktSpeicher arbeiten.
```

---

## Typische Fehlerhinweise

| Fehler | Korrektur |
|---|---|
| JDBC-Code steht in `Main` | Code in `DbProduktSpeicher` verschieben |
| SQL steht im `LagerService` | Fachlogik und Persistenz wieder trennen |
| `Connection` wird nicht geschlossen | `try-with-resources` verwenden |
| Werte werden in SQL-Strings verkettet | `PreparedStatement` mit `?` verwenden |
| `ResultSet` wird ohne `next()` gelesen | zuerst `if` oder `while (resultSet.next())` verwenden |
| `UPDATE` oder `DELETE` ohne `WHERE` | immer gezielt einschränken |
| Exceptions werden leer abgefangen | Exception weitergeben oder sichtbar in `IllegalStateException` verpacken |
| Interface-Signatur passt nicht | `@Override` nutzen und Methodensignatur prüfen |
| Fachlogik wird in CSV und DB dupliziert | Fachlogik im `LagerService` belassen |

---

## Verifikation

Die Musterlösung wurde in einem temporären Maven-Projekt unter `/tmp/dbproduktspeicher_validation` geprüft.

Ausgeführt:

```bash
mvn test
```

Ergebnis:

```text
BUILD SUCCESS
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
```

Zusätzlich wurde `Main` mit H2 Embedded ausgeführt:

```bash
java -cp target/classes:$HOME/.m2/repository/com/h2database/h2/2.2.224/h2-2.2.224.jar ch.allianz.youngoitv.lager.Main
```

Ausgabe:

```text
Maus / 24.9 / 7
Tastatur / 79.9 / 5
```

Einschränkung: Geprüft wurde ein kompaktes temporäres Beispielprojekt, nicht ein vollständiges Lernendenprojekt aus dem Unterricht.
