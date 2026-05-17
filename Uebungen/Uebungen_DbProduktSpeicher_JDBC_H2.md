# Übungen – DbProduktSpeicher mit JDBC und H2

## Vorwissen

Du brauchst:

- Maven-Projektstruktur
- Klassen und Objekte
- Packages
- `ArrayList`
- CSV-Persistenz
- `ProduktSpeicher` als Interface
- `CsvProduktSpeicher` als bekannte Implementierung
- `LagerService` für Fachlogik
- JDBC-Grundlagen mit H2 Embedded

Nicht verwendet werden:

- ORM
- Hibernate
- JPA
- Spring Data
- formales Repository Pattern
- Connection Pooling
- komplexe SQL-Joins
- Migrationstools
- Dependency Injection

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
  src/test/java/
    ch/allianz/youngoitv/lager/
      LagerServiceTest.java
```

Ein Produkt besitzt mindestens:

```text
Name
Preis
Bestand
```

Das Interface bleibt die gemeinsame Grundlage:

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public interface ProduktSpeicher {
    ArrayList<Produkt> ladeProdukte(String quelle);

    void speichereProdukte(ArrayList<Produkt> produkte, String ziel);
}
```

Falls dein Projekt ein anderes Package verwendet, passe `package` und Imports an deine bestehende Struktur an.

Prüfe nach praktischen Änderungen:

```bash
mvn package
```

Wenn Tests vorhanden sind:

```bash
mvn test
```

Hinweis:

```text
H2 Embedded legt die Datenbank zum Beispiel unter data/lager.mv.db ab.
Wenn du frisch beginnen willst, stoppe das Programm und lösche diese Datei.
```

---

## Basis

### Aufgabe 1 – H2-Dependency prüfen

Prüfe, ob deine `pom.xml` H2 enthält.

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.2.224</version>
</dependency>
```

Auftrag:

1. Ergänze die Dependency, falls sie fehlt.
2. Prüfe, ob Java 21 in der `pom.xml` konfiguriert ist.
3. Führe `mvn package` aus.

Erwartung:

```text
BUILD SUCCESS
```

---

### Aufgabe 2 – `DbProduktSpeicher` erstellen

Erstelle die Klasse `DbProduktSpeicher` im gleichen Package wie `CsvProduktSpeicher`.

Startstruktur:

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public class DbProduktSpeicher implements ProduktSpeicher {
    @Override
    public ArrayList<Produkt> ladeProdukte(String quelle) {
        return new ArrayList<>();
    }

    @Override
    public void speichereProdukte(ArrayList<Produkt> produkte, String ziel) {
    }
}
```

Auftrag:

1. Prüfe, ob die Klasse `ProduktSpeicher` korrekt implementiert.
2. Prüfe, ob `@Override` ohne Fehler akzeptiert wird.
3. Führe `mvn package` aus.

---

### Aufgabe 3 – Verbindung zu H2 herstellen

Ergänze in `DbProduktSpeicher` eine private Hilfsmethode.

```java
private Connection verbindungHerstellen(String jdbcUrl) throws SQLException {
    return DriverManager.getConnection(jdbcUrl);
}
```

Auftrag:

1. Ergänze die Imports für `Connection`, `DriverManager` und `SQLException`.
2. Verwende als JDBC-URL später `jdbc:h2:./data/lager`.
3. Schreibe keinen JDBC-Code in `Main`.

Kontrollfrage:

```text
Warum ist die Verbindungsmethode im DbProduktSpeicher und nicht in Main?
```

---

### Aufgabe 4 – Tabelle `PRODUKT` erstellen

Ergänze:

```java
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
```

Auftrag:

1. Ergänze den Import für `PreparedStatement`.
2. Rufe `tabelleErstellen(connection)` beim Laden und Speichern auf.
3. Erkläre, warum `IF NOT EXISTS` hilfreich ist.

---

### Aufgabe 5 – Datenbank leeren

Ergänze eine Hilfsmethode:

```java
private void datenbankLeeren(Connection connection) throws SQLException {
    String sql = "DELETE FROM PRODUKT";

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        statement.executeUpdate();
    }
}
```

Auftrag:

1. Verwende diese Methode nur bewusst vor dem Neuspeichern der ganzen Produktliste.
2. Notiere, warum diese Methode gefährlich wäre, wenn sie versehentlich an der falschen Stelle aufgerufen wird.

Hinweis: Das ist eine einfache Einstiegsstrategie. Sie ist gut nachvollziehbar, aber bestehende Datenbank-IDs bleiben dabei nicht stabil.

---

### Aufgabe 6 – Produkte speichern

Ergänze eine Hilfsmethode:

```java
private void produktEinfuegen(Connection connection, Produkt produkt) throws SQLException {
    String sql = "INSERT INTO PRODUKT (NAME, PREIS, BESTAND) VALUES (?, ?, ?)";

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        statement.setString(1, produkt.getName());
        statement.setDouble(2, produkt.getPreis());
        statement.setInt(3, produkt.getBestand());
        statement.executeUpdate();
    }
}
```

Setze danach `speichereProdukte(...)` um:

```java
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
```

Auftrag:

1. Speichere mindestens ein Produkt.
2. Verwende `PreparedStatement`.
3. Verwende keine SQL-String-Verkettung mit Produktwerten.

---

### Aufgabe 7 – Produkte laden

Setze `ladeProdukte(...)` um:

```java
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
```

Auftrag:

1. Ergänze den Import für `ResultSet`.
2. Erkläre, warum `while (resultSet.next())` nötig ist.
3. Speichere Produkte und lade sie danach erneut.

---

### Aufgabe 8 – Produkte aktualisieren

Ergänze eine zusätzliche Methode in `DbProduktSpeicher`:

```java
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
```

Auftrag:

1. Aktualisiere den Bestand eines Produkts.
2. Lade danach alle Produkte neu.
3. Prüfe, ob nur das gewünschte Produkt geändert wurde.
4. Erkläre, warum `WHERE ID = ?` wichtig ist.

Wichtig: Ermittle die ID zuerst über die Datenbank oder eine Suchmethode. Verlasse dich nicht blind darauf, dass eine ID immer `1` oder `2` ist.

Fachliche Regeln wie "Bestand darf nicht negativ werden" gehören weiterhin in den `LagerService`. Diese Methode zeigt nur das technische `UPDATE`.

---

### Aufgabe 9 – Produkte löschen

Ergänze:

```java
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
```

Auftrag:

1. Ermittle zuerst eine vorhandene ID.
2. Lösche ein Produkt nach ID.
3. Lade danach alle Produkte neu.
4. Prüfe, ob nicht versehentlich alle Produkte gelöscht wurden.

---

### Aufgabe 10 – `Main` auf `DbProduktSpeicher` umstellen

Ändere in `Main` nur die konkrete Speicherklasse und das Ziel.

Vorher:

```java
ProduktSpeicher speicher = new CsvProduktSpeicher();
String ziel = "data/produkte.csv";
```

Nachher:

```java
ProduktSpeicher speicher = new DbProduktSpeicher();
String ziel = "jdbc:h2:./data/lager";
```

Auftrag:

1. Lasse `LagerService` unverändert.
2. Lasse Fachlogik unverändert.
3. Schreibe keinen SQL-Code in `Main`.
4. Führe das Programm aus.
5. Prüfe, ob Speichern und Laden mit H2 funktionieren.

---

### Aufgabe 11 – Bestehende Fachlogik weiterverwenden

Führe eine bekannte fachliche Aktion aus, zum Beispiel:

```text
Produkt verkaufen.
Bestand erhöhen.
Warnung bei tiefem Bestand prüfen.
```

Auftrag:

1. Verwende dafür weiterhin `LagerService`.
2. Speichere danach über `ProduktSpeicher`.
3. Lade die Produkte erneut.
4. Prüfe, ob die fachliche Änderung erhalten bleibt.

Kontrollfrage:

```text
Welche Klasse hat sich für die Fachlogik geändert?
```

Erwartete Antwort:

```text
Keine. Der LagerService bleibt unverändert.
```

---

## Vertiefung

### Aufgabe 12 – Mehrere Produkte speichern

Erstelle eine Liste mit mindestens drei Produkten.

Beispiel:

```text
Maus, 24.90, 10
Tastatur, 79.90, 5
Monitor, 249.00, 3
```

Auftrag:

1. Speichere die Liste mit `DbProduktSpeicher`.
2. Lade die Liste erneut.
3. Vergleiche Anzahl, Namen, Preise und Bestände.

---

### Aufgabe 13 – Produkt nach ID suchen

Ergänze eine Methode:

```java
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
```

Auftrag:

1. Suche eine vorhandene ID.
2. Suche eine nicht vorhandene ID.
3. Erkläre, warum hier `if (resultSet.next())` statt `while` passt.

---

### Aufgabe 14 – Fehlerfälle behandeln

Prüfe mindestens drei Fehlerfälle.

| Fehlerfall | Erwartetes Verhalten |
|---|---|
| falsche JDBC-URL | Fehlermeldung oder Exception sichtbar |
| Datenbankdatei gelöscht | Tabelle wird neu erstellt |
| Produkt-ID existiert nicht | Suche liefert `null` oder klare Meldung |
| negativer Bestand beim Aktualisieren | wird durch Fachlogik verhindert oder bewusst diskutiert |

Auftrag:

1. Ignoriere Exceptions nicht.
2. Fange Exceptions nicht leer ab.
3. Notiere, welche Fehler technisch und welche fachlich sind.

---

### Aufgabe 15 – Ressourcen korrekt schliessen

Prüfe deinen Code.

Markiere jede Stelle mit:

- `Connection`
- `PreparedStatement`
- `ResultSet`

Auftrag:

1. Verwende `try-with-resources`.
2. Prüfe, ob jede Ressource automatisch geschlossen wird.
3. Erkläre, warum das bei Datenbankzugriff wichtig ist.

---

### Aufgabe 16 – CSV- und DB-Implementierung vergleichen

Fülle die Tabelle aus.

| Frage | `CsvProduktSpeicher` | `DbProduktSpeicher` |
|---|---|---|
| Wo liegen die Daten? | | |
| Wie werden Produkte gespeichert? | | |
| Wie werden Produkte geladen? | | |
| Wo liegt die Persistenzlogik? | | |
| Wo darf keine Fachlogik stehen? | | |
| Welche Implementierung ist einfacher sichtbar? | | |
| Welche Implementierung ist näher an einer realen Anwendung? | | |

Schreibe danach einen kurzen Merksatz:

```text
Persistenz ist austauschbar, weil ...
```

---

## Transfer

### Aufgabe 17 – Embedded vs. Server-Modus vergleichen

Vergleiche kurz:

| Frage | H2 Embedded | H2 Server-Modus |
|---|---|---|
| Wo läuft die Datenbank? | | |
| Welche JDBC-URL ist typisch? | | |
| Was ist für Übungen einfacher? | | |
| Was ist näher an einer gemeinsamen Datenbank? | | |

Beispiel-URLs:

```text
jdbc:h2:./data/lager
jdbc:h2:tcp://localhost/./data/lager
```

---

### Aufgabe 18 – Vorteile einer Datenbank beschreiben

Beschreibe mindestens drei Vorteile einer Datenbank gegenüber CSV.

Mögliche Aspekte:

- Tabellenstruktur
- gezielte Suche
- gezielte Aktualisierung
- eindeutige IDs
- bessere Erweiterbarkeit

Schreibe auch einen Nachteil für den Einstieg auf.

---

### Aufgabe 19 – Weitere Persistenzarten diskutieren

Diskutiere, welche weiteren Implementierungen von `ProduktSpeicher` denkbar wären.

Beispiele:

- `JsonProduktSpeicher`
- `XmlProduktSpeicher`
- `InMemoryProduktSpeicher`
- `RestProduktSpeicher`

Auftrag:

1. Wähle zwei Varianten.
2. Beschreibe, wo die Daten liegen.
3. Beschreibe, was in `Main` gleich bleiben sollte.

---

### Aufgabe 20 – Warum bleibt Fachlogik unverändert?

Beantworte schriftlich:

1. Warum muss `LagerService` nicht wissen, ob CSV oder H2 verwendet wird?
2. Welche Rolle spielt `ProduktSpeicher` dabei?
3. Was wäre ein schlechtes Zeichen in deinem Code?

Hinweis:

```text
Wenn LagerService SQL enthält, ist die Trennung verletzt.
```

---

### Aufgabe 21 – Warum sind Interfaces hilfreich?

Erkläre mit eigenen Worten:

```text
ProduktSpeicher speicher = new DbProduktSpeicher();
```

Gehe auf diese Punkte ein:

- linke Seite: Interface-Typ
- rechte Seite: konkrete Implementierung
- gleicher Methodenaufruf
- anderes Speicherverhalten

---

## Typische Fehlerbilder prüfen

Markiere, ob der Fehler in deinem Code vorkommt.

| Fehlerbild | Kommt vor? | Korrektur |
|---|---|---|
| JDBC-Code steht in `Main` | | |
| SQL und Fachlogik sind vermischt | | |
| `Connection` wird nicht geschlossen | | |
| `Statement` statt `PreparedStatement` wird verwendet | | |
| `ResultSet` wird ohne `next()` gelesen | | |
| `DbProduktSpeicher` implementiert `ProduktSpeicher` nicht korrekt | | |
| Fachlogik ist doppelt in CSV- und DB-Implementierung | | |
| Exceptions werden ignoriert | | |

---

## Reflexion

Beantworte zum Abschluss:

1. Welche Teile der Anwendung mussten nicht geändert werden?
2. Warum hilft `ProduktSpeicher`?
3. Welche Unterschiede bestehen zwischen CSV und Datenbank?
4. Welche Verantwortung besitzt `DbProduktSpeicher`?
5. Warum bleibt der `LagerService` unverändert?
6. Was würdest du beim nächsten Mal zuerst testen?
