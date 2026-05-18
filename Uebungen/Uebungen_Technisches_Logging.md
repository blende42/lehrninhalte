# Übungen – Technisches Logging in Java einführen

## Vorwissen

Du brauchst:

- bekannte Lagerverwaltung
- Maven-Projektstruktur
- `LagerService`
- `ProduktRepository`
- `AenderungsRepository`
- JDBC mit H2
- `Connection`, `PreparedStatement` und `ResultSet`
- Grundidee von Verantwortlichkeiten

Nicht verwendet werden:

- Spring Boot
- komplexe Logback-Konfiguration
- Appender-Vertiefung
- MDC
- strukturierte Logs
- Monitoring
- OpenTelemetry
- ELK

---

## Vorbereitung

Arbeite mit der bekannten Lagerverwaltung mit Repositorys.

Beispielstruktur:

```text
lagerverwaltung-db/
  pom.xml
  src/main/java/
    ch/allianz/youngoitv/lager/
      Main.java
      LagerService.java
      repository/ProduktRepository.java
      repository/AenderungsRepository.java
      model/Produkt.java
      model/PreisAenderung.java
      model/BestandsAenderung.java
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
Du machst technische Abläufe in Repository-Klassen gezielt sichtbar.
```

---

## Basis

### Aufgabe 1 – Maven-Dependencies ergänzen

Ergänze in `pom.xml` die Dependencies für SLF4J und Logback.

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

Auftrag:

1. Füge die Dependencies in den bestehenden `<dependencies>`-Block ein.
2. Lege keinen neuen Build-Mechanismus an.
3. Führe aus:

```bash
mvn package
```

Erwartung:

```text
Das Projekt baut weiterhin mit Maven.
```

---

### Aufgabe 2 – Logger in einer Klasse anlegen

Lege in `ProduktRepository` einen Logger an.

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class ProduktRepository {

    private static final Logger logger =
            LoggerFactory.getLogger(ProduktRepository.class);
}
```

Auftrag:

1. Ergänze die Imports.
2. Ergänze das Logger-Attribut.
3. Achte darauf, dass die Klasse im `getLogger`-Aufruf stimmt.

Kurze Kontrolle:

```text
Der Logger wird einmal pro Klasse angelegt.
Der Logger wird nicht in jeder Methode neu erstellt.
```

---

### Aufgabe 3 – `System.out.println` durch `logger.info` ersetzen

Suche eine technische Ausgabe in einer Repository-Klasse.

Beispiel vorher:

```java
System.out.println("Produkte werden geladen");
```

Beispiel nachher:

```java
logger.info("Lade Produkte aus der Datenbank.");
```

Auftrag:

1. Ersetze nur technische Ausgaben.
2. Lasse fachliche Konsolenausgaben in `Main` stehen, wenn sie bewusst zur Benutzer-Ausgabe gehören.
3. Formuliere die Logmeldung als technischen Ablauf.

---

### Aufgabe 4 – DEBUG-Log für Repository-Schritte ergänzen

Ergänze ein `DEBUG`-Log vor einer SQL-Aktion.

Beispiel:

```java
logger.debug("Bereite SELECT auf Tabelle PRODUKT vor.");
```

Auftrag:

1. Wähle eine Methode wie `ladeProdukte`.
2. Ergänze ein `DEBUG`-Log vor dem `PreparedStatement`.
3. Begründe kurz, warum diese Meldung eher `DEBUG` als `INFO` ist.

---

### Aufgabe 5 – WARN-Log für ungewöhnliche Situationen ergänzen

Ergänze ein `WARN`-Log für eine ungewöhnliche, aber behandelbare Situation. Eine leere Änderungsliste ist nur dann `WARN`, wenn in diesem Ablauf Änderungen erwartet wurden. Sonst reicht `DEBUG` oder gar kein Log.

Beispiel:

```java
if (aenderungen.isEmpty()) {
    logger.warn("Erwartete Preisänderungen für Produkt-ID {} fehlen.", produktId);
}
```

Auftrag:

1. Verwende einen Platzhalter mit `{}`.
2. Logge keine sensiblen Daten.
3. Das Programm soll wegen dieser Situation nicht automatisch abbrechen.

---

### Aufgabe 6 – ERROR-Log bei Exceptions ergänzen

Ergänze in einem `catch`-Block ein `ERROR`-Log mit Exception.

```java
catch (SQLException exception) {
    logger.error("Produkte konnten nicht geladen werden.", exception);
    throw new IllegalStateException("Produkte konnten nicht geladen werden.", exception);
}
```

Auftrag:

1. Schreibe eine konkrete Meldung mit Kontext.
2. Übergib die Exception als zweiten Parameter.
3. Verschlucke die Exception nicht.

---

### Aufgabe 7 – Anwendung ausführen und Logs beobachten

Baue zuerst das Projekt und führe danach die Anwendung aus.

Build-Prüfung:

```bash
mvn package
```

Anwendung starten, falls in deinem Projekt so vorbereitet:

```bash
mvn exec:java
```

Auftrag:

1. Beobachte die Logausgabe.
2. Notiere zwei hilfreiche Logzeilen.
3. Notiere eine Logzeile, die du entfernen oder auf `DEBUG` ändern würdest.

---

## Vertiefung

### Aufgabe 8 – Logging in `ProduktRepository` ergänzen

Ergänze sinnvolle Logs in `ProduktRepository`.

Mögliche Stellen:

- Produkte laden
- Produkt speichern
- Produkt aktualisieren
- Produkt löschen
- Datenbankverbindung öffnen
- Fehler bei SQL-Zugriff

Auftrag:

1. Verwende mindestens ein `INFO`-Log.
2. Verwende mindestens ein `DEBUG`-Log.
3. Verwende ein `ERROR`-Log in einem Fehlerfall.
4. Prüfe mit `mvn package`.

---

### Aufgabe 9 – Logging in `AenderungsRepository` ergänzen

Ergänze sinnvolle Logs in `AenderungsRepository`.

Mögliche Stellen:

- Preisänderung speichern
- Bestandsänderung speichern
- Preisänderungen zu Produkt laden
- Bestandsänderungen zu Produkt laden

Auftrag:

1. Logge die technische Aktion.
2. Verwende Produkt-IDs nur, wenn sie für die Fehlersuche hilfreich sind.
3. Logge keine vollständigen sensiblen Datensätze.

---

### Aufgabe 10 – INFO und DEBUG unterscheiden

Ordne die Meldungen einem Level zu.

| Meldung | Level |
|---|---|
| `Lade Produkte aus der Datenbank.` |  |
| `Bereite PreparedStatement für SELECT vor.` |  |
| `5 Produkte geladen.` |  |
| `Setze Parameter 1 auf Produkt-ID 12.` |  |
| `Preisänderung wird gespeichert.` |  |

Auftrag:

1. Wähle jeweils `INFO` oder `DEBUG`.
2. Begründe jede Wahl in einem kurzen Satz.

---

### Aufgabe 11 – Zu viele Logs reduzieren

Gegeben ist ein übertriebener Ausschnitt:

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

Auftrag:

1. Streiche überflüssige Logs.
2. Wähle maximal drei sinnvolle Logs.
3. Entscheide, ob sie `INFO` oder `DEBUG` sein sollen.
4. Begründe deine Auswahl.

---

### Aufgabe 12 – Exception mit Kontext loggen

Verbessere diesen Fehlerfall:

```java
catch (SQLException exception) {
    logger.error("Fehler");
}
```

Auftrag:

1. Formuliere eine konkrete Meldung.
2. Übergib die Exception an den Logger.
3. Entscheide, ob die Exception weitergeworfen werden soll.
4. Begründe deine Entscheidung.

---

### Aufgabe 13 – Einfache `logback.xml` verwenden

Diese Aufgabe ist optional, wenn die Standardausgabe von Logback für deine Gruppe ausreicht.

Lege diese Datei an:

```text
src/main/resources/logback.xml
```

Minimaler Inhalt zum Übernehmen:

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

Wenn dein Projekt damit nicht startet, verwende stattdessen die Standardausgabe von Logback. Vertiefe die Konfiguration nicht und ändere nur den Root-Level.

Auftrag:

1. Besprich, warum `DEBUG`-Logs bei `INFO` nicht erscheinen.
2. Ändere testweise `INFO` auf `DEBUG`.
3. Stelle danach wieder die ursprüngliche Einstellung her.

Hinweis: Wenn eure Lehrperson keine eigene Logback-Konfiguration vorsieht, überspringe diese Aufgabe.

---

## Transfer

### Aufgabe 14 – Logging ist kein Ersatz für Tests

Erkläre schriftlich:

```text
Warum zeigt ein Log nicht automatisch, dass das Programm korrekt funktioniert?
```

Nutze ein Beispiel aus der Lagerverwaltung.

---

### Aufgabe 15 – Logging ist keine Fachlogik

Prüfe diesen Ausschnitt:

```java
if (neuerPreis < 0) {
    logger.warn("Preis ist negativ, Produkt wird nicht gespeichert.");
    return;
}
```

Auftrag:

1. Erkläre, warum der Log nicht die Fachregel ersetzt.
2. Formuliere eine bessere Lösung mit echter Fachentscheidung.
3. Entscheide, ob zusätzlich ein Log sinnvoll ist.

---

### Aufgabe 16 – Geeignete Log-Level wählen

Wähle passende Level:

1. Datenbankverbindung konnte nicht geöffnet werden.
2. Produkte werden geladen.
3. SQL-Abfrage wird vorbereitet.
4. Erwartete Änderungen für eine Produkt-ID fehlen.
5. Passwort wurde falsch eingegeben.

Auftrag:

1. Wähle `DEBUG`, `INFO`, `WARN` oder `ERROR`.
2. Begründe jede Wahl.
3. Markiere, welche Information nicht im Klartext geloggt werden darf.

---

### Aufgabe 17 – Welche Daten sollten nicht geloggt werden?

Diskutiert in Zweiergruppen:

- Welche Daten aus einer Lagerverwaltung sind harmlos?
- Welche Daten könnten sensibel sein?
- Welche technischen Daten helfen bei der Fehlersuche?
- Welche Daten gehören nie in ein Log?

Notiert drei Regeln für euer Projekt.

---

### Aufgabe 18 – Warum Logging später wichtig wird

Erkläre:

```text
Warum wird Logging in Server-Anwendungen wichtiger als in kleinen Konsolenprogrammen?
```

Beziehe dich auf:

- mehrere Benutzerinnen und Benutzer
- Fehler, die nicht direkt vor dir auf der Konsole passieren
- spätere Fehlersuche
- technische Abläufe im Hintergrund

---

## Reflexion

Beantworte zum Schluss:

1. Wann hat Logging bei der Fehlersuche geholfen?
2. Welche Logs waren wirklich hilfreich?
3. Welche Logs waren überflüssig?
4. Warum ersetzt Logging keine Tests?
5. Warum gehört Logging nicht in die Fachlogik?
