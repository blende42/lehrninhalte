# Lösungen – Technisches Logging in Java einführen

Diese Musterlösung zeigt eine kompakte Standardlösung für praktisches Logging in der bekannten Lagerverwaltung mit JDBC/H2 und Repositorys.

Kernidee:

```text
Logger machen technische Abläufe sichtbar.
Repositorys sind gute Orte für Logs zum Datenzugriff.
Logging ersetzt weder Fachlogik noch Tests.
```

Bewusst nicht verwendet werden Spring Boot, komplexe Logback-Konfiguration, Monitoring, Observability, ELK oder OpenTelemetry.

---

## 1. Maven-Dependencies

In `pom.xml` werden SLF4J und Logback ergänzt:

```xml
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>2.0.13</version>
</dependency>
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.5.6</version>
</dependency>
```

Prüfung:

```bash
mvn package
```

---

## 2. Logger deklarieren

In jeder Klasse, die loggt, wird ein Logger einmal pro Klasse angelegt.

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class ProduktRepository {

    private static final Logger logger =
            LoggerFactory.getLogger(ProduktRepository.class);
}
```

Wichtig:

- `private`, weil der Logger nur in dieser Klasse verwendet wird
- `static final`, weil der Logger zur Klasse gehört
- `ProduktRepository.class`, damit die Logausgabe zur richtigen Klasse zeigt

---

## 3. `System.out.println` ersetzen

Technische Ausgaben in Repositorys werden durch Logger-Aufrufe ersetzt.

Vorher:

```java
System.out.println("Produkte werden geladen");
```

Nachher:

```java
logger.info("Lade Produkte aus der Datenbank.");
```

Eine fachliche Konsolenausgabe in `Main` darf bleiben, wenn sie bewusst zur einfachen Benutzer-Ausgabe gehört. Technische Beobachtung gehört dagegen in Logs.

---

## 4. Logging in `ProduktRepository`

Beispiel für eine kompakte Repository-Methode:

```java
public ArrayList<Produkt> ladeProdukte() {
    logger.info("Lade Produkte aus der Datenbank.");

    ArrayList<Produkt> produkte = new ArrayList<>();
    String sql = "SELECT ID, NAME, PREIS, BESTAND FROM PRODUKT ORDER BY ID";

    logger.debug("Bereite SELECT auf Tabelle PRODUKT vor.");

    try (Connection connection = verbindungHerstellen();
         PreparedStatement statement = connection.prepareStatement(sql);
         ResultSet resultSet = statement.executeQuery()) {

        while (resultSet.next()) {
            produkte.add(leseProdukt(resultSet));
        }

        logger.info("{} Produkte geladen.", produkte.size());
        return produkte;
    } catch (SQLException exception) {
        logger.error("Produkte konnten nicht geladen werden.", exception);
        throw new IllegalStateException("Produkte konnten nicht geladen werden.", exception);
    }
}
```

Beispiel für den Verbindungsaufbau:

```java
private Connection verbindungHerstellen() throws SQLException {
    logger.debug("Öffne Datenbankverbindung zu {}.", jdbcUrl);
    return DriverManager.getConnection(jdbcUrl);
}
```

Das Passwort wird nicht geloggt.

---

## 5. Logging in `AenderungsRepository`

Beispiel für das Laden von Preisänderungen:

```java
public ArrayList<PreisAenderung> ladePreisAenderungen(int produktId) {
    logger.info("Lade Preisänderungen für Produkt-ID {}.", produktId);

    ArrayList<PreisAenderung> aenderungen = new ArrayList<>();
    String sql = """
            SELECT ID, PRODUKT_ID, ALTER_PREIS, NEUER_PREIS, GRUND, ZEITPUNKT
            FROM PREISAENDERUNG
            WHERE PRODUKT_ID = ?
            ORDER BY ZEITPUNKT
            """;

    logger.debug("Bereite SELECT auf Tabelle PREISAENDERUNG vor.");

    try (Connection connection = verbindungHerstellen();
         PreparedStatement statement = connection.prepareStatement(sql)) {

        statement.setInt(1, produktId);

        try (ResultSet resultSet = statement.executeQuery()) {
            while (resultSet.next()) {
                aenderungen.add(lesePreisAenderung(resultSet));
            }
        }

        if (aenderungen.isEmpty()) {
            logger.warn("Erwartete Preisänderungen für Produkt-ID {} fehlen.", produktId);
        }

        return aenderungen;
    } catch (SQLException exception) {
        logger.error("Preisänderungen konnten nicht geladen werden.", exception);
        throw new IllegalStateException("Preisänderungen konnten nicht geladen werden.", exception);
    }
}
```

Das `WARN`-Log ist passend, wenn in diesem Ablauf Änderungen erwartet wurden. Ist eine leere Änderungsliste normal, wäre eher `DEBUG` oder kein Log sinnvoll.

---

## 6. Log-Level kurz begründet

| Meldung | Level | Begründung |
|---|---|---|
| `Lade Produkte aus der Datenbank.` | `INFO` | normaler wichtiger Ablauf |
| `Bereite PreparedStatement für SELECT vor.` | `DEBUG` | technisches Detail für Fehlersuche |
| `5 Produkte geladen.` | `INFO` | nützliche Zusammenfassung eines Ablaufs |
| `Setze Parameter 1 auf Produkt-ID 12.` | `DEBUG` | sehr detaillierter JDBC-Schritt |
| `Preisänderung wird gespeichert.` | `INFO` | normale technische Aktion |
| Datenbankverbindung konnte nicht geöffnet werden | `ERROR` | technische Aktion ist fehlgeschlagen |
| Erwartete Änderungen für Produkt-ID fehlen | `WARN` | ungewöhnlich, aber behandelbar |

---

## 7. Zu viele Logs reduzieren

Aus diesem Ausschnitt:

```java
logger.info("Starte Methode ladeProdukte.");
logger.info("Erstelle ArrayList.");
logger.info("Erstelle SQL-String.");
logger.info("Öffne Verbindung.");
logger.info("Erstelle PreparedStatement.");
logger.info("Starte Schleife.");
logger.info("Lese nächste Zeile.");
logger.info("Lese nächste Zeile.");
logger.info("Lese nächste Zeile.");
logger.info("Gebe Produkte zurück.");
```

wird zum Beispiel:

```java
logger.info("Lade Produkte aus der Datenbank.");
logger.debug("Bereite SELECT auf Tabelle PRODUKT vor.");
logger.info("{} Produkte geladen.", produkte.size());
```

Begründung: Die neue Version zeigt Start, technisches Detail und Ergebnis. Sie loggt nicht jeden kleinen Zwischenschritt.

---

## 8. Exception mit Kontext loggen

Schlecht:

```java
catch (SQLException exception) {
    logger.error("Fehler");
}
```

Besser:

```java
catch (SQLException exception) {
    logger.error("Produkt konnte nicht gespeichert werden.", exception);
    throw new IllegalStateException("Produkt konnte nicht gespeichert werden.", exception);
}
```

Die Meldung sagt, welche Aktion fehlgeschlagen ist. Die Exception liefert die technische Ursache.

---

## 9. Einfache `logback.xml`

Falls eine eigene Ausgabe gewünscht ist, reicht für diese Einheit eine kleine Konfiguration zum Übernehmen:

```xml
<configuration>
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="INFO">
        <appender-ref ref="CONSOLE" />
    </root>
</configuration>
```

Bei `INFO` erscheinen `INFO`, `WARN` und `ERROR`. `DEBUG` erscheint erst, wenn der Root-Level auf `DEBUG` gesetzt wird. Weitere Logback-Konfiguration wird hier bewusst nicht vertieft.

---

## 10. Logging ist keine Fachlogik

Problematischer Ausschnitt:

```java
if (neuerPreis < 0) {
    logger.warn("Preis ist negativ, Produkt wird nicht gespeichert.");
    return;
}
```

Besser ist eine echte Fachentscheidung:

```java
if (neuerPreis < 0) {
    throw new IllegalArgumentException("Preis darf nicht negativ sein.");
}
```

Ein Log kann zusätzlich helfen, ersetzt aber die Fachregel nicht. Die Regel muss im Code stehen und testbar sein.

---

## 11. Logging ist kein Ersatz für Tests

Ein Log zeigt nur, was technisch passiert ist. Es prüft nicht automatisch, ob das Ergebnis korrekt ist.

Beispiel:

```text
Log: 5 Produkte geladen.
Test: Prüft, ob genau die erwarteten 5 Produkte mit korrekten Preisen geladen wurden.
```

Darum braucht die Anwendung weiterhin Tests für Fachlogik, Mapping und wichtige Fehlerfälle.

---

## 12. Was nicht geloggt werden sollte

Nicht in Logs gehören:

- Passwörter
- Tokens
- vollständige sensible Datensätze
- unnötige Personendaten
- jede einzelne Schleifeniteration ohne Nutzen
- Fachentscheidungen als Ersatz für Code

Beispiel:

```java
logger.debug("Öffne Datenbankverbindung zu {}.", jdbcUrl);
```

Nicht:

```java
logger.debug("Öffne Verbindung mit Passwort {}.", passwort);
```

---

## 13. Kurze Reflexionsantworten

**Wann hilft Logging bei der Fehlersuche?**  
Wenn unklar ist, welche technische Aktion gerade passiert oder wo ein Fehler entsteht, zum Beispiel beim Datenbankzugriff.

**Welche Logs waren wirklich hilfreich?**  
Logs zu Start und Ergebnis einer Repository-Aktion sowie `ERROR`-Logs mit Exception.

**Welche Logs waren überflüssig?**  
Logs zu jedem kleinen Zwischenschritt wie «ArrayList erstellt» oder jede einzelne Schleifenzeile.

**Warum ersetzt Logging keine Tests?**  
Logs beobachten Abläufe. Tests prüfen erwartetes Verhalten.

**Warum gehört Logging nicht in die Fachlogik?**  
Logging beschreibt technische Beobachtbarkeit. Fachregeln müssen als Code formuliert und testbar bleiben.

---

## 14. Typische Fehlerhinweise

- `System.out.println` dauerhaft für technische Fehlersuche verwenden
- Logger in jeder Methode neu erstellen
- Logger mit der falschen Klasse initialisieren
- alles mit `INFO` loggen
- `DEBUG` und `INFO` nicht unterscheiden
- Exceptions ohne Kontext loggen
- Exceptions verschlucken
- Passwörter oder andere sensible Daten loggen
- Logging als Ersatz für Tests oder Fachentscheidungen verwenden

---

## 15. Verifikation

Die zentralen Maven-/Java-Beispiele wurden mit einem temporären Maven-Projekt geprüft:

```bash
mvn package
mvn exec:java
```

Geprüft wurden:

- Dependencies `slf4j-api` und `logback-classic`
- Logger-Deklaration mit `LoggerFactory`
- `logger.info`, `logger.debug`, `logger.warn` und `logger.error`
- einfache `logback.xml`
- Ausführung einer kleinen `Main`

Ergebnis der Prüfung: `mvn package` baute das temporäre Projekt erfolgreich, `mvn exec:java` gab `INFO`, `DEBUG`, `WARN` und `ERROR` aus. `DEBUG` erschien, weil im temporären Prüfprojekt der Root-Level bewusst auf `DEBUG` gesetzt war.

Die Prüfung ersetzt nicht den Build eines konkreten Lernenden-Projekts, weil diese Musterlösung bewusst als kompakte Referenzlösung und nicht als vollständige Lagerverwaltungsanwendung aufgebaut ist.
