# Übungen – Maven-Projekte ausführen und paketieren

## Basis

### Aufgabe 1 – Compile, Run oder Package?

Ordne die Begriffe den passenden Erklärungen zu.

Begriffe:

```text
mvn compile
java -cp target/classes ...Main
mvn package
target/classes
JAR-Datei
Build-Artefakt
Java package
Maven package
```

Erklärungen:

- kompiliert den Quellcode
- startet ein kompiliertes Programm
- erzeugt ein Build-Artefakt
- enthält kompilierte `.class`-Dateien
- bündelt Build-Ergebnisse in einer Datei
- erzeugtes Ergebnis eines Build-Prozesses
- strukturiert Java-Klassen im Code
- Maven-Phase zum Paketieren

---

### Aufgabe 2 – Befehle in die richtige Reihenfolge bringen

Du willst die Produktverwaltung zuerst sauber neu bauen, dann starten und danach ein JAR erzeugen.

Für diese Übung trennen wir die Schritte bewusst, auch wenn `mvn package` notwendige frühere Phasen mit ausführt.

Ordne die Befehle sinnvoll:

```bash
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
mvn package
mvn clean
mvn compile
```

Beantworte zusätzlich:

1. Welcher Befehl startet das Programm?
2. Welcher Befehl erzeugt `.class`-Dateien?
3. Welcher Befehl erzeugt eine JAR-Datei?
4. Welcher Schritt wäre technisch nicht zwingend nötig, wenn du nur ein JAR erzeugen willst?

---

### Aufgabe 3 – `target/classes` untersuchen

Führe im Ordner `produktverwaltung-maven` aus:

```bash
mvn clean compile
```

Untersuche danach den Ordner:

```text
target/classes
```

Beantworte:

1. Welche `.class`-Dateien findest du?
2. Welche Ordnerstruktur steht unter `target/classes`?
3. Welche Verbindung gibt es zur Java-`package`-Deklaration?
4. Warum liegen dort keine `.java`-Dateien?

Falls du das Projekt nicht ausführbar vorliegen hast, beantworte die Fragen anhand dieser erwarteten Struktur:

```text
target/classes/ch/allianz/youngoitv/produktverwaltung/Main.class
target/classes/ch/allianz/youngoitv/produktverwaltung/model/Produkt.class
target/classes/ch/allianz/youngoitv/produktverwaltung/service/ProduktVerwaltung.class
```

---

## Aufbau

Falls du das Projekt nicht ausführbar vorliegen hast, beantworte Aufgabe 4 und 5 anhand der erwarteten Befehle und Ordnerstruktur.

### Aufgabe 4 – Produktverwaltung starten

Starte die Produktverwaltung nach dem Kompilieren.

Schritte:

```bash
mvn compile
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Beantworte:

1. Warum braucht der `java`-Befehl den Classpath `target/classes`?
2. Warum reicht `Main` als Klassenname nicht?
3. Welcher Teil des Befehls ist Maven, welcher Teil ist Java?

---

### Aufgabe 5 – JAR-Datei erzeugen

Führe im Projektordner aus:

```bash
mvn clean package
```

Suche danach im Ordner `target` den Dateinamen der `.jar`-Datei. Du musst die JAR-Datei noch nicht öffnen oder starten.

```text
target
```

Beantworte:

1. Wie heisst die erzeugte JAR-Datei?
2. Welche Verbindung siehst du zu `artifactId` und `version` aus der `pom.xml` aus dem Maven-Einstieg?
3. Warum ist die JAR-Datei ein Build-Artefakt?
4. Warum ist die JAR-Datei nicht dein Quellcode?

Hinweis: In diesem Block muss die JAR-Datei noch nicht direkt mit `java -jar` startbar sein.

---

### Aufgabe 6 – Java package und Maven package vergleichen

Ergänze die Tabelle.

| Frage | Java-`package` | Maven `package` |
|---|---|---|
| Wo kommt es vor? | | |
| Beispiel | | |
| Wozu dient es? | | |
| Was ist ein typischer Fehler? | | |

Verwende diese Beispiele:

```java
package ch.allianz.youngoitv.produktverwaltung.model;
```

```bash
mvn package
```

---

## Vertiefung

### Aufgabe 7 – Fehlerdiagnose: `package` verwechselt

Eine Lernende sagt:

```text
Ich habe mvn package ausgeführt. Jetzt müssten meine Java-Packages korrigiert sein.
```

Beantworte:

1. Was ist an dieser Aussage falsch?
2. Was macht `mvn package` wirklich?
3. Wer oder was bestimmt die Java-`package`-Struktur?

---

### Aufgabe 8 – Fehlerdiagnose: `target` und `src` verwechselt

Ein Lernender legt nach `mvn compile` eine neue Datei hier an:

```text
produktverwaltung-maven/target/classes/ch/allianz/youngoitv/produktverwaltung/Hilfsprogramm.java
```

Beantworte:

1. Warum ist dieser Ort falsch?
2. Wohin gehört die Datei korrekt?
3. Was kann mit dem Ordner `target` bei `mvn clean` passieren?

---

### Aufgabe 9 – Fehlerdiagnose: falsches Arbeitsverzeichnis

Eine Person führt aus:

```bash
mvn package
```

Das Terminal steht hier:

```text
produktverwaltung-maven/src/main/java/ch/allianz/youngoitv/produktverwaltung/model/
```

Beantworte:

1. Warum ist das problematisch?
2. In welchem Ordner muss der Befehl ausgeführt werden?
3. Woran erkennt Maven den Projektordner?

---

### Aufgabe 10 – Maven ist keine Magie

Formuliere eine kurze Erklärung für eine Mitschülerin oder einen Mitschüler.

Verwende diese Wörter:

```text
orchestrieren
javac
java
src/main/java
target/classes
JAR-Datei
```

Erkläre:

- Was macht Maven bei `mvn compile`?
- Was macht Java beim Starten?
- Was macht Maven bei `mvn package`?

---

## Transfer

### Aufgabe 11 – Reproduzierbarer Build

Ein Team möchte vermeiden, dass jede Person anders baut.

Beantworte:

1. Warum ist `mvn clean package` ein standardisierter Ablauf?
2. Warum ist es hilfreich, wenn alle denselben Befehl verwenden?
3. Welche Dateien und Ordner entstehen dadurch neu?
4. Warum sollte man `target` nicht von Hand als Quellcodeordner verwenden?

---

### Aufgabe 12 – Kleiner Ausblick auf Build-Server

Stell dir vor, ein Build-Server wie Jenkins führt nach jeder Änderung diesen Befehl aus:

```bash
mvn clean package
```

Beantworte ohne technische Details zu Jenkins:

1. Warum kann ein Build-Server denselben Befehl verwenden wie du lokal?
2. Was müsste im Projekt vorhanden sein, damit Maven weiss, was zu tun ist?
3. Warum ist ein reproduzierbarer Build eine gute Vorbereitung für CI/CD?
4. Welche Themen behandeln wir in diesem Block bewusst noch nicht?

Nenne mindestens drei ausgeschlossene Themen.
