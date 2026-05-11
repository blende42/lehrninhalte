# Lösungen – Maven-Projekte ausführen und paketieren

## Aufgabe 1 – Compile, Run oder Package?

- `mvn compile`: kompiliert den Quellcode
- `java -cp target/classes ...Main`: startet ein kompiliertes Programm
- `mvn package`: erzeugt ein Build-Artefakt
- `target/classes`: enthält kompilierte `.class`-Dateien
- JAR-Datei: bündelt Build-Ergebnisse in einer Datei
- Build-Artefakt: erzeugtes Ergebnis eines Build-Prozesses
- Java package: strukturiert Java-Klassen im Code
- Maven package: Maven-Phase zum Paketieren

Typischer Fehler: `package` bedeutet bei Java und Maven nicht dasselbe.

---

## Aufgabe 2 – Befehle in die richtige Reihenfolge bringen

Sinnvolle Reihenfolge:

```bash
mvn clean
mvn compile
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
mvn package
```

Antworten:

1. Das Programm wird mit `java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main` gestartet.
2. `.class`-Dateien entstehen durch `mvn compile`.
3. Eine JAR-Datei entsteht durch `mvn package`.
4. Wenn du nur ein JAR erzeugen willst, ist ein vorheriges separates `mvn compile` technisch nicht zwingend nötig, weil `mvn package` die notwendigen früheren Phasen mit ausführt.

Hinweis: `mvn package` kompiliert notwendige vorherige Schritte mit. Für den Lernweg ist die getrennte Reihenfolge trotzdem hilfreich.

---

## Aufgabe 3 – `target/classes` untersuchen

Erwartete Dateien:

```text
target/classes/ch/allianz/youngoitv/produktverwaltung/Main.class
target/classes/ch/allianz/youngoitv/produktverwaltung/model/Produkt.class
target/classes/ch/allianz/youngoitv/produktverwaltung/service/ProduktVerwaltung.class
```

Die Ordnerstruktur unter `target/classes` entspricht der Java-`package`-Struktur.

Beispiel:

```java
package ch.allianz.youngoitv.produktverwaltung.model;
```

passt zu:

```text
target/classes/ch/allianz/youngoitv/produktverwaltung/model/Produkt.class
```

Dort liegen keine `.java`-Dateien, weil `target/classes` erzeugte Build-Ergebnisse enthält. Der Quellcode liegt unter `src/main/java`.

Typischer Fehler: `target/classes` nicht als Ort für eigenen Code verwenden.

---

## Aufgabe 4 – Produktverwaltung starten

1. Der Classpath `target/classes` ist nötig, weil dort die kompilierten `.class`-Dateien liegen.
2. `Main` reicht nicht, weil die Klasse in einem Java-`package` liegt. Java braucht den vollständigen Namen:

```text
ch.allianz.youngoitv.produktverwaltung.Main
```

3. `mvn compile` ist Maven. `java -cp target/classes ...` ist Java.

Typischer Fehler: Den Ordner der `.java`-Datei als Classpath verwenden. Gestartet wird mit den kompilierten Klassen unter `target/classes`.

---

## Aufgabe 5 – JAR-Datei erzeugen

Bei dieser `pom.xml`:

```xml
<artifactId>produktverwaltung</artifactId>
<version>1.0.0</version>
```

ist eine typische JAR-Datei:

```text
target/produktverwaltung-1.0.0.jar
```

Antworten:

1. Der genaue Name hängt von `artifactId` und `version` ab.
2. Maven bildet den Dateinamen typischerweise aus `artifactId` und `version`.
3. Die JAR-Datei ist ein Build-Artefakt, weil sie durch den Build erzeugt wird.
4. Die JAR-Datei ist nicht der Quellcode. Der Quellcode liegt weiterhin als `.java`-Dateien unter `src/main/java`.

Hinweis: In diesem Block wird noch kein direkt startbares JAR mit Manifest gebaut.

---

## Aufgabe 6 – Java package und Maven package vergleichen

| Frage | Java-`package` | Maven `package` |
|---|---|---|
| Wo kommt es vor? | in Java-Dateien | als Maven-Phase, aufgerufen mit `mvn package` |
| Beispiel | `package ch.allianz.youngoitv.produktverwaltung.model;` | `mvn package` |
| Wozu dient es? | ordnet Klassen im Code | erzeugt ein Build-Artefakt |
| Typischer Fehler | `src/main/java` in die Package-Deklaration aufnehmen | erwarten, dass Java-Packages verändert werden |

Merksatz:

```text
Java package ist Code-Struktur. Maven package ist ein Build-Schritt.
```

---

## Aufgabe 7 – Fehlerdiagnose: `package` verwechselt

1. Die Aussage ist falsch, weil `mvn package` keine Java-`package`-Deklarationen korrigiert.
2. `mvn package` erzeugt ein Build-Artefakt, zum Beispiel eine JAR-Datei unter `target`.
3. Die Java-`package`-Struktur wird durch die `package`-Deklaration in der `.java`-Datei und die passende Ordnerstruktur unter `src/main/java` bestimmt.

Typischer Fehler: Gleiches Wort, andere Bedeutung.

---

## Aufgabe 8 – Fehlerdiagnose: `target` und `src` verwechselt

1. Der Ort ist falsch, weil `target` ein Ausgabeordner für erzeugte Dateien ist.
2. Die Datei gehört hierhin:

```text
produktverwaltung-maven/src/main/java/ch/allianz/youngoitv/produktverwaltung/Hilfsprogramm.java
```

3. `mvn clean` kann den Ordner `target` löschen. Eigener Quellcode wäre dort also gefährdet.

Hinweis: Eigene `.java`-Dateien gehören unter `src/main/java`, nicht unter `target/classes`.

---

## Aufgabe 9 – Fehlerdiagnose: falsches Arbeitsverzeichnis

1. Der Befehl wird zu tief in der Quellcode-Struktur ausgeführt. Dort liegt normalerweise keine `pom.xml`.
2. Richtig ist der Projektordner:

```text
produktverwaltung-maven/
```

3. Maven erkennt den Projektordner an der `pom.xml`.

Typischer Fehler: Der Ordner einer Java-Klasse ist nicht automatisch der Maven-Projektordner.

---

## Aufgabe 10 – Maven ist keine Magie

Mögliche Antwort:

- `mvn compile`: Maven orchestriert den Kompilierschritt, sucht Quellcode unter `src/main/java` und legt Ergebnisse unter `target/classes` ab.
- `java`: Danach startet Java das Programm mit den kompilierten Klassen.
- `mvn package`: Maven erzeugt zusätzlich ein Build-Artefakt, zum Beispiel eine JAR-Datei.

Hinweis: Maven ersetzt Java nicht. Maven ordnet und automatisiert bekannte Schritte.

---

## Aufgabe 11 – Reproduzierbarer Build

1. `mvn clean package` ist standardisiert, weil Maven standardisierte Phasen und Standardordner verwendet, solange das Projekt nicht anders konfiguriert wird.
2. Wenn alle denselben Befehl verwenden, entstehen weniger Unterschiede zwischen einzelnen Arbeitsumgebungen.
3. Neu entstehen zum Beispiel:

```text
target/classes
target/produktverwaltung-1.0.0.jar
```

4. `target` ist ein erzeugter Ausgabeordner. Er kann gelöscht und neu erstellt werden. Quellcode gehört deshalb nicht dorthin.

Reproduzierbar bedeutet hier: Der Build kann mit denselben Projektdateien und demselben Maven-Befehl erneut ausgeführt werden; alte Ergebnisse werden durch `clean` zuerst entfernt.

Typischer Fehler: Build-Ergebnisse wie festen Quellcode behandeln.

---

## Aufgabe 12 – Kleiner Ausblick auf Build-Server

1. Ein Build-Server kann denselben Befehl verwenden, weil Maven-Projekte standardisierte Strukturen und Befehle haben.
2. Im Projekt muss vor allem die `pom.xml` vorhanden sein. Der Quellcode muss an der erwarteten Stelle liegen, zum Beispiel unter `src/main/java`.
3. Ein reproduzierbarer Build ist eine gute Vorbereitung für CI/CD, weil der Ablauf wiederholt und automatisiert werden kann.
4. Bewusst noch nicht behandelt werden zum Beispiel:

- externe Dependencies
- Maven Central
- JUnit
- Plugins im Detail
- Fat Jars
- Spring Boot
- `install`
- `deploy`

Hinweis: Jenkins und CI/CD werden hier nur als Ausblick genannt. Die technische Umsetzung kommt später.
