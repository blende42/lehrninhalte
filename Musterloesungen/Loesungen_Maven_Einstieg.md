# Lösungen – Maven Einstieg

## Aufgabe 1 – Begriffe zuordnen

- `Maven`: Build-Tool, das bekannte Schritte geordnet ausführt
- `javac`: kompiliert Java-Quellcode
- `java`: startet ein kompiliertes Java-Programm
- `src/main/java`: Standardordner für Java-Quellcode in Maven
- `target`: Ausgabeordner für erzeugte Build-Dateien
- `pom.xml`: zentrale Projektdatei von Maven
- `Convention over Configuration`: Maven erwartet Standardstrukturen, damit weniger konfiguriert werden muss
- `orchestrieren`: mehrere Schritte passend koordinieren

Typischer Fehler: Maven nicht mit `javac` gleichsetzen. Maven ruft den Compiler im Build-Ablauf auf.

---

## Aufgabe 2 – Manuell oder Maven?

| Thema | Manuell ohne Maven | Mit Maven |
|---|---|---|
| Quellcode | `src` | `src/main/java` |
| Ausgabeordner | `out` | `target` |
| Kompilieren | `javac -d out` | `mvn compile` |
| Starten | `java -cp out` | noch nicht Teil dieses Blocks |
| Aufräumen | `out` löschen | `mvn clean` |

Hinweise:

- `src` und `src/main/java` sind die Quellcode-Orte.
- `out` und `target` sind Ausgabeordner für erzeugte Dateien.
- `javac -d out` und `mvn compile` gehören zum Kompilieren.
- `java -cp out` startet ein manuell kompiliertes Programm.
- `mvn clean` startet kein Programm. Es löscht Build-Ergebnisse, standardmässig den Ordner `target`.

---

## Aufgabe 3 – Orchestrieren erklären

Maven ist wie ein Dirigent: Es spielt nicht selbst jedes Instrument, sondern koordiniert den Ablauf. Werkzeuge wie `javac` sind wie einzelne Instrumente im Orchester. Bei `mvn compile` sorgt Maven dafür, dass der Quellcode am erwarteten Ort gesucht und in der richtigen Phase kompiliert wird.

---

## Aufgabe 4 – Maven-Struktur lesen

Richtig ist:

```text
produktverwaltung-maven/src/main/java/ch/allianz/youngoitv/produktverwaltung/Main.java
```

Begründung:

- `src/main/java` ist der Maven-Quellwurzelordner.
- Danach folgt die Package-Struktur `ch/allianz/youngoitv/produktverwaltung`.
- `target` ist für erzeugte Dateien, nicht für eigenen Quellcode.

---

## Aufgabe 5 – Produktverwaltung nach Maven migrieren

Korrekte Zielstruktur:

```text
produktverwaltung-maven/
  pom.xml
  src/
    main/
      java/
        ch/
          allianz/
            youngoitv/
              produktverwaltung/
                Main.java
                model/
                  Produkt.java
                service/
                  ProduktVerwaltung.java
```

Die Package-Deklarationen bleiben:

```java
package ch.allianz.youngoitv.produktverwaltung;
```

```java
package ch.allianz.youngoitv.produktverwaltung.model;
```

```java
package ch.allianz.youngoitv.produktverwaltung.service;
```

Typischer Fehler: `src/main/java` gehört nicht in die Package-Deklaration. Es ist nur der Quellwurzelordner.

---

## Aufgabe 6 – Minimale pom.xml schreiben

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>ch.allianz.youngoitv</groupId>
    <artifactId>produktverwaltung</artifactId>
    <version>1.0.0</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
</project>
```

Hinweis: Für diesen Einstieg gibt es keinen `dependencies`-Abschnitt.

---

## Aufgabe 7 – Maven ausführen

1. Das Terminal muss im Projektordner stehen, also dort, wo `pom.xml` liegt.
2. `mvn clean` entfernt standardmässig den Ordner `target`.
3. Nach `mvn compile` liegen die `.class`-Dateien standardmässig unter `target/classes`.
4. `target` ist ein Ausgabeordner. Er darf gelöscht und neu erzeugt werden. Eigener Quellcode gehört deshalb nicht dorthin.

Typischer Fehler: Den Befehl aus `src/main/java` starten. Maven sucht die `pom.xml` im aktuellen Projektkontext.

---

## Aufgabe 8 – Fehlerdiagnose: falsche Projektstruktur

Fehler:

- `pom.xml` liegt unter `src/main/java`, gehört aber direkt in den Projektordner.
- Die Package-Struktur beginnt falsch mit `produktverwaltung/ch/...`.
- `Main.java` liegt nicht passend zur Package-Deklaration.
- Eigener Quellcode liegt in `target`.
- `target` wurde vermutlich manuell als Quellcodeordner verwendet.

Korrektur:

```text
produktverwaltung-maven/
  pom.xml
  src/
    main/
      java/
        ch/
          allianz/
            youngoitv/
              produktverwaltung/
                Main.java
                model/
                  Produkt.java
                service/
                  ProduktVerwaltung.java
```

Nach `mvn compile` erzeugt Maven selbst:

```text
target/
  classes/
    ch/
      allianz/
        youngoitv/
          produktverwaltung/
            Main.class
```

---

## Aufgabe 9 – Fehlerdiagnose: falsches Arbeitsverzeichnis

1. Der Befehl wird zu tief in der Quellcode-Struktur ausgeführt.
2. Richtig ist der Projektordner:

```text
produktverwaltung-maven/
```

3. Maven erkennt das Projekt an der `pom.xml`.

Typischer Fehler: Der Ordner der `Main.java` ist nicht automatisch der Projektordner.

---

## Aufgabe 10 – Maven ist keine Magie

Maven orchestriert bei `mvn compile` den Kompilierschritt. Es sucht den Quellcode gemäss `Convention over Configuration` unter `src/main/java`, ruft den Java-Compiler `javac` im Build-Ablauf auf und legt die Ergebnisse in `target` ab. Maven ist dadurch kein Ersatz für Java, sondern automatisiert bekannte Schritte.

---

## Aufgabe 11 – Reflexion zu Convention over Configuration

Mögliche Antworten:

1. Man findet Quellcode in Maven-Projekten schneller, weil die Struktur gleich bleibt.
2. Jedes Projekt müsste zuerst erklärt oder konfiguriert werden.
3. Teams sparen Absprachen, weil alle dieselbe Grundstruktur erwarten.
4. Aus dem Package-Block ist die Konvention mit umgekehrter Domain bekannt, zum Beispiel `ch.allianz.youngoitv`.

---

## Aufgabe 12 – Pensionskassen-Simulation als Maven-Projekt strukturieren

Korrekte Struktur:

```text
pensionskasse-maven/
  pom.xml
  src/
    main/
      java/
        ch/
          allianz/
            youngoitv/
              pensionskasse/
                Main.java
                simulation/
                  PensionskassenSimulation.java
                service/
                  Beitragssaetze.java
```

Package-Deklarationen:

```java
package ch.allianz.youngoitv.pensionskasse;
```

```java
package ch.allianz.youngoitv.pensionskasse.simulation;
```

```java
package ch.allianz.youngoitv.pensionskasse.service;
```

Die `pom.xml` kann gleich wie in Aufgabe 6 aufgebaut sein, aber mit diesem `artifactId`:

```xml
<artifactId>pensionskasse</artifactId>
```

Typischer Fehler: `src/main/java` in die Package-Deklaration aufnehmen. Das ist falsch.

---

## Aufgabe 13 – Optionaler Ausblick

Mögliche Antworten:

- Ein `Jenkinsfile` kann gleich heissen, damit Jenkins die Pipeline-Datei zuverlässig findet.
- Ein `Dockerfile` liegt oft im Projektordner, damit der Build-Kontext klar ist.
- Kubernetes-Manifests können in einem festen Ordner liegen, damit Deployment-Dateien schnell gefunden und gemeinsam verwaltet werden.

Hinweis: Der Ausblick dient nur dem Wiedererkennen von Konventionen. Die Tools selbst werden hier noch nicht eingeführt.
