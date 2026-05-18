# Lösungen – Mehrere Tabellen, Beziehungen und Repository

Diese Musterlösung zeigt eine kompakte Standardlösung für mehrere zusammengehörige Tabellen und einfache Repository-Klassen.

Kernidee:

```text
Fachlich gehören Produkt, Preisänderungen und Bestandsänderungen zusammen.
In der Datenbank liegen sie in mehreren Tabellen.
Repository-Klassen bündeln JDBC-Code und Mapping.
LagerService bleibt für Fachlogik zuständig.
```

Bewusst nicht verwendet werden ORM, Hibernate, JPA, Spring Data, automatische Persistenz, Generic Repository, Dependency Injection oder Enterprise-Architektur.

---

## 1. Tabellen und Beziehung

Eine mögliche Datenbankstruktur:

```sql
CREATE TABLE IF NOT EXISTS PRODUKT (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    NAME VARCHAR(100) NOT NULL,
    PREIS DOUBLE NOT NULL,
    BESTAND INT NOT NULL
);

CREATE TABLE IF NOT EXISTS PREISAENDERUNG (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    PRODUKT_ID INT NOT NULL,
    ALTER_PREIS DOUBLE NOT NULL,
    NEUER_PREIS DOUBLE NOT NULL,
    GRUND VARCHAR(200),
    ZEITPUNKT VARCHAR(30) NOT NULL,
    FOREIGN KEY (PRODUKT_ID) REFERENCES PRODUKT(ID)
);

CREATE TABLE IF NOT EXISTS BESTANDSAENDERUNG (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    PRODUKT_ID INT NOT NULL,
    ALTER_BESTAND INT NOT NULL,
    NEUER_BESTAND INT NOT NULL,
    GRUND VARCHAR(200),
    ZEITPUNKT VARCHAR(30) NOT NULL,
    FOREIGN KEY (PRODUKT_ID) REFERENCES PRODUKT(ID)
);
```

`PRODUKT_ID` verbindet die Änderungstabellen mit `PRODUKT.ID`.

```text
Ein Produkt kann mehrere Preisänderungen haben.
Ein Produkt kann mehrere Bestandsänderungen haben.
Jede Änderung gehört zu genau einem Produkt.
```

---

## 2. Modellklassen

Kompakte Datenklassen reichen für diese Einheit aus.

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

```java
package ch.allianz.youngoitv.lager.model;

public class PreisAenderung {
    private final int id;
    private final int produktId;
    private final double alterPreis;
    private final double neuerPreis;
    private final String grund;
    private final String zeitpunkt;

    public PreisAenderung(int id, int produktId, double alterPreis,
                          double neuerPreis, String grund, String zeitpunkt) {
        this.id = id;
        this.produktId = produktId;
        this.alterPreis = alterPreis;
        this.neuerPreis = neuerPreis;
        this.grund = grund;
        this.zeitpunkt = zeitpunkt;
    }

    public int getId() {
        return id;
    }

    public int getProduktId() {
        return produktId;
    }

    public double getAlterPreis() {
        return alterPreis;
    }

    public double getNeuerPreis() {
        return neuerPreis;
    }

    public String getGrund() {
        return grund;
    }

    public String getZeitpunkt() {
        return zeitpunkt;
    }
}
```

```java
package ch.allianz.youngoitv.lager.model;

public class BestandsAenderung {
    private final int id;
    private final int produktId;
    private final int alterBestand;
    private final int neuerBestand;
    private final String grund;
    private final String zeitpunkt;

    public BestandsAenderung(int id, int produktId, int alterBestand,
                             int neuerBestand, String grund, String zeitpunkt) {
        this.id = id;
        this.produktId = produktId;
        this.alterBestand = alterBestand;
        this.neuerBestand = neuerBestand;
        this.grund = grund;
        this.zeitpunkt = zeitpunkt;
    }

    public int getId() {
        return id;
    }

    public int getProduktId() {
        return produktId;
    }

    public int getAlterBestand() {
        return alterBestand;
    }

    public int getNeuerBestand() {
        return neuerBestand;
    }

    public String getGrund() {
        return grund;
    }

    public String getZeitpunkt() {
        return zeitpunkt;
    }
}
```

---

## 3. `ProduktRepository`

`ProduktRepository` kennt die Tabelle `PRODUKT`. Es enthält SQL, JDBC und Mapping für Produkte.

```java
package ch.allianz.youngoitv.lager.repository;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;

public class ProduktRepository {
    private final String jdbcUrl;

    public ProduktRepository(String jdbcUrl) {
        this.jdbcUrl = jdbcUrl;
    }

    private Connection verbindungHerstellen() throws SQLException {
        return DriverManager.getConnection(jdbcUrl);
    }

    public void tabellenErstellen() {
        String sql = """
                CREATE TABLE IF NOT EXISTS PRODUKT (
                    ID INT AUTO_INCREMENT PRIMARY KEY,
                    NAME VARCHAR(100) NOT NULL,
                    PREIS DOUBLE NOT NULL,
                    BESTAND INT NOT NULL
                )
                """;

        try (Connection connection = verbindungHerstellen();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.executeUpdate();
        } catch (SQLException exception) {
            throw new IllegalStateException("Tabelle PRODUKT konnte nicht erstellt werden.", exception);
        }
    }

    public void speichereProdukt(Produkt produkt) {
        String sql = "INSERT INTO PRODUKT (NAME, PREIS, BESTAND) VALUES (?, ?, ?)";

        try (Connection connection = verbindungHerstellen();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            setzeProduktWerte(statement, produkt);
            statement.executeUpdate();
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkt konnte nicht gespeichert werden.", exception);
        }
    }

    public ArrayList<Produkt> ladeProdukte() {
        ArrayList<Produkt> produkte = new ArrayList<>();
        String sql = "SELECT ID, NAME, PREIS, BESTAND FROM PRODUKT ORDER BY ID";

        try (Connection connection = verbindungHerstellen();
             PreparedStatement statement = connection.prepareStatement(sql);
             ResultSet resultSet = statement.executeQuery()) {

            while (resultSet.next()) {
                produkte.add(leseProdukt(resultSet));
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Produkte konnten nicht geladen werden.", exception);
        }

        return produkte;
    }

    private Produkt leseProdukt(ResultSet resultSet) throws SQLException {
        int id = resultSet.getInt("ID");
        String name = resultSet.getString("NAME");
        double preis = resultSet.getDouble("PREIS");
        int bestand = resultSet.getInt("BESTAND");

        return new Produkt(id, name, preis, bestand);
    }

    private void setzeProduktWerte(PreparedStatement statement, Produkt produkt)
            throws SQLException {
        statement.setString(1, produkt.getName());
        statement.setDouble(2, produkt.getPreis());
        statement.setInt(3, produkt.getBestand());
    }
}
```

Wichtig:

- `leseProdukt(...)` zeigt `ResultSet` -> Objekt.
- `setzeProduktWerte(...)` zeigt Objekt -> `PreparedStatement`.
- `Main` und `LagerService` kennen keine Spaltennamen.

---

## 4. `AenderungsRepository`

`AenderungsRepository` kennt die Tabellen `PREISAENDERUNG` und `BESTANDSAENDERUNG`.

```java
package ch.allianz.youngoitv.lager.repository;

import ch.allianz.youngoitv.lager.model.BestandsAenderung;
import ch.allianz.youngoitv.lager.model.PreisAenderung;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;

public class AenderungsRepository {
    private final String jdbcUrl;

    public AenderungsRepository(String jdbcUrl) {
        this.jdbcUrl = jdbcUrl;
    }

    private Connection verbindungHerstellen() throws SQLException {
        return DriverManager.getConnection(jdbcUrl);
    }

    public void tabellenErstellen() {
        try (Connection connection = verbindungHerstellen()) {
            erstellePreisAenderungTabelle(connection);
            erstelleBestandsAenderungTabelle(connection);
        } catch (SQLException exception) {
            throw new IllegalStateException("Aenderungstabellen konnten nicht erstellt werden.", exception);
        }
    }

    private void erstellePreisAenderungTabelle(Connection connection) throws SQLException {
        String sql = """
                CREATE TABLE IF NOT EXISTS PREISAENDERUNG (
                    ID INT AUTO_INCREMENT PRIMARY KEY,
                    PRODUKT_ID INT NOT NULL,
                    ALTER_PREIS DOUBLE NOT NULL,
                    NEUER_PREIS DOUBLE NOT NULL,
                    GRUND VARCHAR(200),
                    ZEITPUNKT VARCHAR(30) NOT NULL,
                    FOREIGN KEY (PRODUKT_ID) REFERENCES PRODUKT(ID)
                )
                """;

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.executeUpdate();
        }
    }

    private void erstelleBestandsAenderungTabelle(Connection connection) throws SQLException {
        String sql = """
                CREATE TABLE IF NOT EXISTS BESTANDSAENDERUNG (
                    ID INT AUTO_INCREMENT PRIMARY KEY,
                    PRODUKT_ID INT NOT NULL,
                    ALTER_BESTAND INT NOT NULL,
                    NEUER_BESTAND INT NOT NULL,
                    GRUND VARCHAR(200),
                    ZEITPUNKT VARCHAR(30) NOT NULL,
                    FOREIGN KEY (PRODUKT_ID) REFERENCES PRODUKT(ID)
                )
                """;

        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.executeUpdate();
        }
    }

    public void speicherePreisAenderung(PreisAenderung aenderung) {
        String sql = """
                INSERT INTO PREISAENDERUNG
                (PRODUKT_ID, ALTER_PREIS, NEUER_PREIS, GRUND, ZEITPUNKT)
                VALUES (?, ?, ?, ?, ?)
                """;

        try (Connection connection = verbindungHerstellen();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setInt(1, aenderung.getProduktId());
            statement.setDouble(2, aenderung.getAlterPreis());
            statement.setDouble(3, aenderung.getNeuerPreis());
            statement.setString(4, aenderung.getGrund());
            statement.setString(5, aenderung.getZeitpunkt());
            statement.executeUpdate();
        } catch (SQLException exception) {
            throw new IllegalStateException("Preisänderung konnte nicht gespeichert werden.", exception);
        }
    }

    public void speichereBestandsAenderung(BestandsAenderung aenderung) {
        String sql = """
                INSERT INTO BESTANDSAENDERUNG
                (PRODUKT_ID, ALTER_BESTAND, NEUER_BESTAND, GRUND, ZEITPUNKT)
                VALUES (?, ?, ?, ?, ?)
                """;

        try (Connection connection = verbindungHerstellen();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setInt(1, aenderung.getProduktId());
            statement.setInt(2, aenderung.getAlterBestand());
            statement.setInt(3, aenderung.getNeuerBestand());
            statement.setString(4, aenderung.getGrund());
            statement.setString(5, aenderung.getZeitpunkt());
            statement.executeUpdate();
        } catch (SQLException exception) {
            throw new IllegalStateException("Bestandsänderung konnte nicht gespeichert werden.", exception);
        }
    }

    public ArrayList<PreisAenderung> ladePreisAenderungen(int produktId) {
        ArrayList<PreisAenderung> aenderungen = new ArrayList<>();
        String sql = """
                SELECT ID, PRODUKT_ID, ALTER_PREIS, NEUER_PREIS, GRUND, ZEITPUNKT
                FROM PREISAENDERUNG
                WHERE PRODUKT_ID = ?
                ORDER BY ZEITPUNKT
                """;

        try (Connection connection = verbindungHerstellen();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setInt(1, produktId);

            try (ResultSet resultSet = statement.executeQuery()) {
                while (resultSet.next()) {
                    aenderungen.add(lesePreisAenderung(resultSet));
                }
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Preisänderungen konnten nicht geladen werden.", exception);
        }

        return aenderungen;
    }

    public ArrayList<BestandsAenderung> ladeBestandsAenderungen(int produktId) {
        ArrayList<BestandsAenderung> aenderungen = new ArrayList<>();
        String sql = """
                SELECT ID, PRODUKT_ID, ALTER_BESTAND, NEUER_BESTAND, GRUND, ZEITPUNKT
                FROM BESTANDSAENDERUNG
                WHERE PRODUKT_ID = ?
                ORDER BY ZEITPUNKT
                """;

        try (Connection connection = verbindungHerstellen();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setInt(1, produktId);

            try (ResultSet resultSet = statement.executeQuery()) {
                while (resultSet.next()) {
                    aenderungen.add(leseBestandsAenderung(resultSet));
                }
            }
        } catch (SQLException exception) {
            throw new IllegalStateException("Bestandsänderungen konnten nicht geladen werden.", exception);
        }

        return aenderungen;
    }

    private PreisAenderung lesePreisAenderung(ResultSet resultSet) throws SQLException {
        int id = resultSet.getInt("ID");
        int produktId = resultSet.getInt("PRODUKT_ID");
        double alterPreis = resultSet.getDouble("ALTER_PREIS");
        double neuerPreis = resultSet.getDouble("NEUER_PREIS");
        String grund = resultSet.getString("GRUND");
        String zeitpunkt = resultSet.getString("ZEITPUNKT");

        return new PreisAenderung(id, produktId, alterPreis, neuerPreis, grund, zeitpunkt);
    }

    private BestandsAenderung leseBestandsAenderung(ResultSet resultSet)
            throws SQLException {
        int id = resultSet.getInt("ID");
        int produktId = resultSet.getInt("PRODUKT_ID");
        int alterBestand = resultSet.getInt("ALTER_BESTAND");
        int neuerBestand = resultSet.getInt("NEUER_BESTAND");
        String grund = resultSet.getString("GRUND");
        String zeitpunkt = resultSet.getString("ZEITPUNKT");

        return new BestandsAenderung(id, produktId, alterBestand, neuerBestand, grund, zeitpunkt);
    }
}
```

Hinweise:

- `PRODUKT` muss vor den Änderungstabellen existieren, weil die Fremdschlüssel auf `PRODUKT(ID)` zeigen.
- `ORDER BY ZEITPUNKT` macht eine Änderungshistorie besser lesbar, wenn Zeitpunkte als ISO-Text wie `2026-05-18T09:00` gespeichert werden.
- Die Mapping-Methoden halten die Lade-Methoden kurz.

---

## 5. `LagerService` bleibt fachlich

Der Service darf Repositorys verwenden, enthält aber keinen SQL-Code.

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.BestandsAenderung;
import ch.allianz.youngoitv.lager.model.PreisAenderung;
import ch.allianz.youngoitv.lager.model.Produkt;
import ch.allianz.youngoitv.lager.repository.AenderungsRepository;
import ch.allianz.youngoitv.lager.repository.ProduktRepository;

public class LagerService {
    private final ProduktRepository produktRepository;
    private final AenderungsRepository aenderungsRepository;

    public LagerService(ProduktRepository produktRepository,
                        AenderungsRepository aenderungsRepository) {
        this.produktRepository = produktRepository;
        this.aenderungsRepository = aenderungsRepository;
    }

    public void produktAnlegen(Produkt produkt) {
        produktRepository.speichereProdukt(produkt);
    }

    public void preisAenderungProtokollieren(PreisAenderung aenderung) {
        if (aenderung.getNeuerPreis() < 0) {
            throw new IllegalArgumentException("Preis darf nicht negativ sein.");
        }

        aenderungsRepository.speicherePreisAenderung(aenderung);
    }

    public void bestandsAenderungProtokollieren(BestandsAenderung aenderung) {
        if (aenderung.getNeuerBestand() < 0) {
            throw new IllegalArgumentException("Bestand darf nicht negativ sein.");
        }

        aenderungsRepository.speichereBestandsAenderung(aenderung);
    }
}
```

Der Service prüft fachliche Regeln. Die Repositorys speichern und laden Daten. Falls die bestehende Lagerverwaltung bereits einen `LagerService` besitzt, muss er nur gezielt erweitert werden.

---

## 6. `Main` bleibt Ablaufsteuerung

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.BestandsAenderung;
import ch.allianz.youngoitv.lager.model.PreisAenderung;
import ch.allianz.youngoitv.lager.model.Produkt;
import ch.allianz.youngoitv.lager.repository.AenderungsRepository;
import ch.allianz.youngoitv.lager.repository.ProduktRepository;

public class Main {
    public static void main(String[] args) {
        String jdbcUrl = "jdbc:h2:./data/lager";

        ProduktRepository produktRepository = new ProduktRepository(jdbcUrl);
        AenderungsRepository aenderungsRepository = new AenderungsRepository(jdbcUrl);

        produktRepository.tabellenErstellen();
        aenderungsRepository.tabellenErstellen();

        LagerService lagerService = new LagerService(produktRepository, aenderungsRepository);
        lagerService.produktAnlegen(new Produkt(0, "Maus", 24.90, 10));

        lagerService.preisAenderungProtokollieren(
                new PreisAenderung(0, 1, 24.90, 22.90, "Aktion", "2026-05-18T09:00"));
        lagerService.bestandsAenderungProtokollieren(
                new BestandsAenderung(0, 1, 10, 15, "Lieferung", "2026-05-18T10:00"));

        System.out.println(aenderungsRepository.ladePreisAenderungen(1).size());
        System.out.println(aenderungsRepository.ladeBestandsAenderungen(1).size());
    }
}
```

Dieses Demo-Beispiel nimmt eine frische H2-Datenbank an, in der das erste Produkt die ID `1` erhält. In einer robusteren Lösung würde `speichereProdukt(...)` die erzeugte ID zurückgeben oder das Produkt nach dem Speichern wieder laden.

`Main` erzeugt Objekte und ruft Methoden auf. Die technische Initialisierung und die direkte Ladeausgabe dienen hier nur der Demo; SQL-Anweisungen stehen weiterhin in den Repositorys.

---

## 7. Repository als Evolutionsschritt

Vorher war `DbProduktSpeicher` noch überschaubar:

```text
eine Tabelle
ein Objekt
ein Mapping
```

Mit Preis- und Bestandsänderungen wächst die Persistenz:

```text
mehrere Tabellen
mehrere Objektklassen
mehrere SELECT- und INSERT-Anweisungen
mehrere Mapping-Methoden
```

Das Repository ist hier ein natürlicher nächster Schritt. Es ist keine magische Architektur, sondern eine normale Java-Klasse mit klarer Verantwortung:

```text
Repository = strukturierter Ort für Datenzugriff und Mapping
```

Dadurch bleiben die anderen Teile stabil:

- `Main` bleibt Ablaufsteuerung.
- `LagerService` bleibt Fachlogik.
- Modellklassen bleiben Datenobjekte.
- JDBC-Code bleibt in Repositorys.

---

## 8. Typische Fehlerhinweise

- `PRODUKT_ID` vergessen: Die Änderung kann keinem Produkt zugeordnet werden.
- Falsche Reihenfolge im `PreparedStatement`: Werte landen in falschen Spalten.
- `resultSet.next()` vergessen: Das `ResultSet` steht noch vor der ersten Zeile.
- SQL in `Main`: Ablaufsteuerung und Persistenz werden vermischt.
- Mapping im `LagerService`: Fachlogik kennt plötzlich Datenbankspalten.
- Repository mit Fachlogik überladen: Das Repository soll nicht entscheiden, ob ein Preis fachlich erlaubt ist.
- Änderungstabellen vor `PRODUKT` erstellen: Der Fremdschlüssel kann fehlschlagen.
- Zu früh generische Hilfsklassen bauen: Für EFZ-Niveau reichen klare kleine Methoden.

---

## 9. Kurze Transferantworten

Warum wird Mapping repetitiv?

```text
Jede Tabelle braucht Spaltennamen, JDBC-Lesemethoden und Objektkonstruktion.
Beim Speichern braucht jede Tabelle passende PreparedStatement-Positionen.
```

Warum bleibt Fachlogik getrennt?

```text
Fachregeln sollen unabhängig davon verständlich bleiben, ob Daten aus CSV,
H2 oder später aus einer anderen Persistenz kommen.
```

Warum könnten spätere Frameworks interessant sein?

```text
Sie können repetitives Mapping reduzieren.
In dieser Einheit wird zuerst bewusst sichtbar gemacht, welches Problem sie lösen.
```

---

## Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/tabellen_repository_solution` geprüft.

Ausgeführt:

```bash
mvn package
```

Ergebnis: Build erfolgreich. Es wurden keine Tests ausgeführt, weil das temporäre Prüfprojekt keine Testklassen enthält.

`Main` wurde nicht ausgeführt, weil die Musterlösung als Lehrmittel-Snippet gedacht ist und das temporäre Prüfprojekt bewusst keine H2-Abhängigkeit und keine lokale Datenbankdatei verwendet. Die JDBC-Struktur wurde syntaktisch mit Maven geprüft.
