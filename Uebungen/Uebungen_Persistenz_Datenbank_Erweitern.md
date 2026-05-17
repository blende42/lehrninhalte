# Übungen – Bestehende Persistenz auf Datenbank erweitern

## Vorwissen

Du brauchst:

- bekannte Lagerverwaltung
- `Produkt`, `LagerService`, `Main`
- `ProduktSpeicher` mit `CsvProduktSpeicher` und `DbProduktSpeicher`
- JDBC-Grundlagen mit H2 Embedded
- `Connection`, `PreparedStatement`, `ResultSet`
- einfache SQL-Befehle
- `ArrayList`

Nicht verwendet werden:

- ORM
- Hibernate
- JPA
- Spring Data
- `GenericRepository`
- DAO-Frameworks
- Connection Pooling
- komplexe SQL-Joins
- vertiefte Transaktionen
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
      AenderungsEintrag.java
      AenderungsSpeicher.java
      CsvAenderungsSpeicher.java
      DbAenderungsSpeicher.java
      model/Produkt.java
```

Prüfe nach praktischen Änderungen:

```bash
mvn package
```

Wenn Tests vorhanden sind:

```bash
mvn test
```

Ziel dieser Übung:

```text
Die bestehende Anwendung wächst um eine weitere Persistenz.
Die Fachlogik bleibt möglichst stabil.
JDBC-Code bleibt in Speicherklassen.
```

---

## Basis

### Aufgabe 1 – Bestehende Struktur einordnen

Zeichne oder notiere die aktuelle Struktur:

```text
ProduktSpeicher
├── CsvProduktSpeicher
└── DbProduktSpeicher
```

Auftrag:

1. Markiere, wo Produktdaten gespeichert werden.
2. Markiere, wo Fachlogik steht.
3. Markiere, was `Main` tun soll.
4. Notiere, welche Klassen beim Hinzufügen einer Änderungshistorie möglichst stabil bleiben sollen.

---

### Aufgabe 2 – `AenderungsEintrag` erstellen

Erstelle eine Klasse `AenderungsEintrag`.

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

Auftrag:

1. Lege die Klasse im gleichen Package wie `LagerService` ab.
2. Passe das Package an, falls dein Projekt anders aufgebaut ist.
3. Führe `mvn package` aus.

---

### Aufgabe 3 – `AenderungsSpeicher` erstellen

Erstelle ein Interface.

```java
package ch.allianz.youngoitv.lager;

import java.util.ArrayList;

public interface AenderungsSpeicher {
    void speichereAenderung(AenderungsEintrag eintrag, String ziel);

    ArrayList<AenderungsEintrag> ladeAenderungen(String quelle);
}
```

Auftrag:

1. Prüfe, ob der Code kompiliert.
2. Erkläre, warum ein Interface auch hier hilfreich sein kann.
3. Notiere, welche Klassen dieses Interface später implementieren können.

---

### Aufgabe 4 – Tabelle `AENDERUNG` planen

Notiere die Tabelle:

```sql
CREATE TABLE IF NOT EXISTS AENDERUNG (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    PRODUKT_NAME VARCHAR(100) NOT NULL,
    ART VARCHAR(30) NOT NULL,
    ALTER_WERT VARCHAR(50) NOT NULL,
    NEUER_WERT VARCHAR(50) NOT NULL,
    ZEITPUNKT VARCHAR(30) NOT NULL
);
```

Auftrag:

1. Erkläre jede Spalte in einem Satz.
2. Erkläre, warum `IF NOT EXISTS` nützlich ist.
3. Erkläre, warum `ART` zum Beispiel `PREIS` oder `BESTAND` enthalten kann.

---

### Aufgabe 5 – `DbAenderungsSpeicher` erstellen

Erstelle die Klasse.

```java
package ch.allianz.youngoitv.lager;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.ArrayList;

public class DbAenderungsSpeicher implements AenderungsSpeicher {
    private Connection verbindungHerstellen(String jdbcUrl) throws SQLException {
        return DriverManager.getConnection(jdbcUrl);
    }

    @Override
    public void speichereAenderung(AenderungsEintrag eintrag, String ziel) {
    }

    @Override
    public ArrayList<AenderungsEintrag> ladeAenderungen(String quelle) {
        return new ArrayList<>();
    }
}
```

Auftrag:

1. Prüfe, ob `implements AenderungsSpeicher` funktioniert.
2. Prüfe, ob `@Override` keine Fehler zeigt.
3. Schreibe keinen JDBC-Code in `Main`.
4. Führe `mvn package` aus.

---

### Aufgabe 6 – Tabelle in `DbAenderungsSpeicher` erstellen

Ergänze eine Hilfsmethode.

```java
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
```

Auftrag:

1. Ergänze den Import für `PreparedStatement`.
2. Rufe `tabelleErstellen(connection)` beim Speichern und Laden auf.
3. Erkläre, warum diese Methode in `DbAenderungsSpeicher` steht.

---

### Aufgabe 7 – Änderungen speichern

Setze `speichereAenderung(...)` um.

```java
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
        throw new IllegalStateException("Änderung konnte nicht gespeichert werden.", exception);
    }
}
```

Auftrag:

1. Speichere eine Preisänderung.
2. Speichere eine Bestandsänderung.
3. Verwende `PreparedStatement`.
4. Verkette keine Produktwerte direkt in SQL-Strings.

---

### Aufgabe 8 – Mapping vorbereiten

Ergänze eine private Hilfsmethode.

```java
private AenderungsEintrag eintragAusResultSet(ResultSet resultSet) throws SQLException {
    String produktName = resultSet.getString("PRODUKT_NAME");
    String art = resultSet.getString("ART");
    String alterWert = resultSet.getString("ALTER_WERT");
    String neuerWert = resultSet.getString("NEUER_WERT");
    String zeitpunkt = resultSet.getString("ZEITPUNKT");

    return new AenderungsEintrag(produktName, art, alterWert, neuerWert, zeitpunkt);
}
```

Auftrag:

1. Ergänze den Import für `ResultSet`.
2. Erkläre, was Mapping bedeutet.
3. Prüfe, ob die Spaltennamen zur Tabelle passen.

---

### Aufgabe 9 – Änderungen lesen

Setze `ladeAenderungen(...)` um.

```java
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
        throw new IllegalStateException("Änderungen konnten nicht geladen werden.", exception);
    }

    return eintraege;
}
```

Auftrag:

1. Lade alle gespeicherten Änderungen.
2. Gib Anzahl und Inhalt kurz auf der Konsole aus.
3. Erkläre, warum `while (resultSet.next())` nötig ist.

---

### Aufgabe 10 – Änderungen nach Produkt filtern

Ergänze eine Methode.

```java
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
        throw new IllegalStateException("Änderungen konnten nicht gefiltert werden.", exception);
    }

    return eintraege;
}
```

Auftrag:

1. Speichere Änderungen für mindestens zwei Produkte.
2. Lade nur Änderungen für ein Produkt.
3. Erkläre, warum `WHERE PRODUKT_NAME = ?` hilfreich ist.

---

### Aufgabe 11 – Bestehende Services weiterverwenden

Führe eine bekannte fachliche Aktion aus:

```text
Produkt verkaufen
Bestand erhöhen
Preis ändern
```

Auftrag:

1. Verwende weiterhin `LagerService` für Fachlogik.
2. Speichere Produkte weiterhin mit `DbProduktSpeicher`.
3. Speichere Änderungen mit `DbAenderungsSpeicher`.
4. Schreibe kein SQL in `LagerService`.

Kontrollfrage:

```text
Welche Klasse entscheidet fachlich, ob eine Aktion erlaubt ist?
```

---

### Aufgabe 12 – `Main` als Ablaufsteuerung behalten

`Main` darf die Objekte verbinden.

```java
String ziel = "jdbc:h2:./data/lager";

ProduktSpeicher produktSpeicher = new DbProduktSpeicher();
AenderungsSpeicher aenderungsSpeicher = new DbAenderungsSpeicher();
LagerService lagerService = new LagerService();
```

Auftrag:

1. Verwende `Main` nur für den Ablauf.
2. Erzeuge keine SQL-Strings in `Main`.
3. Rufe die passenden Speicherklassen auf.
4. Prüfe mit `mvn package`.

---

## Vertiefung

### Aufgabe 13 – Preisänderungen separat speichern

Speichere Preisänderungen mit `ART = "PREIS"`.

Beispiel:

```java
new AenderungsEintrag("Maus", "PREIS", "24.90", "22.90", "2026-05-17T10:15")
```

Auftrag:

1. Speichere mindestens zwei Preisänderungen.
2. Lade alle Änderungen.
3. Prüfe, ob die Art korrekt gespeichert wurde.

---

### Aufgabe 14 – Bestandsänderungen separat speichern

Speichere Bestandsänderungen mit `ART = "BESTAND"`.

Beispiel:

```java
new AenderungsEintrag("Tastatur", "BESTAND", "5", "8", "2026-05-17T10:20")
```

Auftrag:

1. Speichere mindestens zwei Bestandsänderungen.
2. Lade alle Änderungen.
3. Beschreibe, woran du Preis- und Bestandsänderungen unterscheiden kannst.

---

### Aufgabe 15 – Mehrere Tabellen verwenden

Vergleiche die Tabellen:

| Tabelle | Zweck |
|---|---|
| `PRODUKT` | aktueller Produktzustand |
| `AENDERUNG` | protokollierte Änderungen |

Auftrag:

1. Erkläre den Unterschied zwischen aktuellem Zustand und Änderungshistorie.
2. Erkläre, warum nicht alles in einer einzigen Tabelle stehen muss.
3. Erkläre, warum trotzdem keine komplexen Joins nötig sind.

---

### Aufgabe 16 – Zusätzliche Suchmethode ergänzen

Ergänze eine Methode, die nach Änderungsart filtert.

```text
ladeAenderungenNachArt(String jdbcUrl, String art)
```

Auftrag:

1. Verwende `WHERE ART = ?`.
2. Verwende wieder `eintragAusResultSet(...)`.
3. Prüfe mit Preis- und Bestandsänderungen.

---

### Aufgabe 17 – Fehlerfälle behandeln

Prüfe mindestens drei Fehlerfälle.

| Fehlerfall | Erwartetes Verhalten |
|---|---|
| falsche JDBC-URL | Exception ist sichtbar |
| leere Tabelle | leere Liste wird zurückgegeben |
| unbekannter Produktname | leere Liste wird zurückgegeben |
| falscher Spaltenname im Mapping | Fehler ist sichtbar |

Auftrag:

1. Ignoriere Exceptions nicht.
2. Fange Exceptions nicht leer ab.
3. Unterscheide technische und fachliche Fehler.

---

### Aufgabe 18 – Mapping vereinfachen

Prüfe deinen Code.

Auftrag:

1. Suche alle Stellen, an denen `ResultSet` gelesen wird.
2. Prüfe, ob du `eintragAusResultSet(...)` verwendest.
3. Entferne doppelte Mapping-Logik.
4. Erkläre, warum diese kleine Hilfsmethode sinnvoll ist.

---

### Aufgabe 19 – Bestehende Struktur verbessern

Markiere Wiederholungen zwischen `DbProduktSpeicher` und `DbAenderungsSpeicher`.

Mögliche Wiederholungen:

- Verbindung herstellen
- Tabelle erstellen
- `try-with-resources`
- Exception in `IllegalStateException` verpacken
- Mapping aus `ResultSet`

Auftrag:

1. Markiere die Wiederholungen.
2. Entscheide, welche Wiederholung für den Moment akzeptabel ist.
3. Baue noch keine grosse gemeinsame Architektur.

---

## Transfer

### Aufgabe 20 – Warum bleiben Services stabil?

Beantworte schriftlich:

1. Warum muss `LagerService` nicht wissen, ob CSV oder H2 verwendet wird?
2. Warum muss `LagerService` nicht wissen, wie `AENDERUNG` gespeichert wird?
3. Was wäre ein Warnsignal in deinem Code?

---

### Aufgabe 21 – Weitere Persistenzarten diskutieren

Diskutiere, welche weiteren Implementierungen möglich wären.

Beispiele:

- `JsonAenderungsSpeicher`
- `XmlAenderungsSpeicher`
- `InMemoryAenderungsSpeicher`
- `RestAenderungsSpeicher`

Auftrag:

1. Wähle zwei Varianten.
2. Beschreibe, wo die Daten liegen.
3. Beschreibe, was an `LagerService` gleich bleiben sollte.

---

### Aufgabe 22 – Wann wird Architektur unübersichtlich?

Beschreibe drei Warnsignale.

Mögliche Warnsignale:

- `Main` wird sehr lang
- Services enthalten SQL
- Speicherklassen enthalten Fachentscheidungen
- sehr viele ähnliche Methoden werden kopiert
- niemand weiss mehr, welche Klasse zuständig ist

---

### Aufgabe 23 – Mehrere Tabellen beurteilen

Beschreibe Vorteile und Nachteile mehrerer Tabellen.

| Sicht | Notizen |
|---|---|
| Vorteil | |
| Nachteil | |
| Worauf muss man achten? | |

---

### Aufgabe 24 – Wann ist Refactoring sinnvoll?

Beantworte:

1. Welche Wiederholung stört wirklich?
2. Welche Wiederholung hilft beim Lernen noch?
3. Welche kleine Verbesserung wäre sinnvoll?
4. Welche Verbesserung wäre zu gross für diese Einheit?

---

## Typische Fehlerbilder prüfen

Markiere, ob der Fehler in deinem Code vorkommt.

| Fehlerbild | Kommt vor? | Korrektur |
|---|---|---|
| JDBC-Code steht in `Main` | | |
| SQL und Fachlogik sind vermischt | | |
| Mapping-Code ist mehrfach kopiert | | |
| Tabellenstruktur und Objektstruktur werden verwechselt | | |
| `Connection` wird nicht geschlossen | | |
| Services werden mit zu vielen Aufgaben aufgebläht | | |
| Speicherklassen enthalten Fachentscheidungen | | |
| unnötige neue Abstraktionen wurden gebaut | | |

---

## Reflexion

Beantworte zum Abschluss:

1. Welche Teile der Anwendung blieben stabil?
2. Welche Klassen mussten erweitert werden?
3. Warum helfen Interfaces weiterhin?
4. Welche Struktur wurde schwieriger?
5. Welche Wiederholungen im JDBC-Code fallen auf?
6. Wann könnte weiteres Refactoring sinnvoll werden?
