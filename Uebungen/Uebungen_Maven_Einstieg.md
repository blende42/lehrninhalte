# Übungen – Maven Einstieg

## Basis

### Aufgabe 1 – Begriffe zuordnen

Ordne die Begriffe den passenden Erklärungen zu.

Begriffe:

```text
Maven
javac
java
src/main/java
target
pom.xml
Convention over Configuration
orchestrieren
```

Erklärungen:

- kompiliert Java-Quellcode
- startet ein kompiliertes Java-Programm
- Build-Tool, das bekannte Schritte geordnet ausführt
- Standardordner für Java-Quellcode in Maven
- Ausgabeordner für erzeugte Build-Dateien
- zentrale Projektdatei von Maven
- Maven erwartet Standardstrukturen, damit weniger konfiguriert werden muss
- mehrere Schritte passend koordinieren

---

### Aufgabe 2 – Manuell oder Maven?

Ordne die Einträge der passenden Spalte zu.

```text
src
out
javac -d out
java -cp out
src/main/java
target
mvn compile
mvn clean
```

Tabelle:

| Manuell ohne Maven | Mit Maven |
|---|---|
| | |

---

### Aufgabe 3 – Orchestrieren erklären

Erkläre in zwei bis drei Sätzen, was **orchestrieren** bei Maven bedeutet.

Verwende die Dirigent-/Orchester-Analogie:

- Wer ist in der Analogie Maven?
- Wer oder was sind die Werkzeuge wie `javac`?
- Was bedeutet die geordnete Reihenfolge?

---

### Aufgabe 4 – Maven-Struktur lesen

Welche Datei liegt am richtigen Ort?

```text
produktverwaltung-maven/src/main/java/ch/allianz/youngoitv/produktverwaltung/Main.java
produktverwaltung-maven/src/ch/allianz/youngoitv/produktverwaltung/Main.java
produktverwaltung-maven/target/ch/allianz/youngoitv/produktverwaltung/Main.java
produktverwaltung-maven/src/main/java/produktverwaltung/ch/allianz/youngoitv/Main.java
```

Begründe kurz.

---

## Aufbau

### Aufgabe 5 – Produktverwaltung nach Maven migrieren

Ausgangslage ohne Maven:

```text
produktverwaltung-packages/
  src/
    ch/
      allianz/
        youngoitv/
          produktverwaltung/
            Main.java
            model/
              Produkt.java
            service/
              ProduktVerwaltung.java
  out/
```

Erstelle daraus ein Maven-Projekt mit dieser Zielstruktur:

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

Vorgaben:

- Verwende die Dateien aus dem Package-Block. Falls du sie nicht mehr hast, erstelle mindestens die Struktur und die `pom.xml`.
- Lege `pom.xml` direkt in `produktverwaltung-maven/` ab.
- Lege Java-Dateien unter `src/main/java` ab.
- Ändere die Package-Deklarationen nicht, wenn sie vorher korrekt waren.
- Verwende keine externen Dependencies.
- Verwende kein JUnit.
- Verwende kein Maven Central und keine Multi-Module-Projekte.

---

### Aufgabe 6 – Minimale pom.xml schreiben

Schreibe eine minimale `pom.xml`.

Vorgaben:

- `groupId`: `ch.allianz.youngoitv`
- `artifactId`: `produktverwaltung`
- `version`: `1.0.0`
- Java-Version: `17`
- Encoding: `UTF-8`
- kein `dependencies`-Abschnitt
- kein Maven Central
- kein Multi-Module-Projekt

---

### Aufgabe 7 – Maven ausführen

Führe im Projektordner diese Befehle aus:

```bash
mvn clean
mvn compile
```

Falls du in Aufgabe 5 nur einen Textbaum erstellt hast, beantworte die Fragen anhand der Zielstruktur und führe die Befehle nicht aus.

Beantworte danach:

1. Wo muss dein Terminal stehen?
2. Welcher Ordner wird durch `mvn clean` standardmässig entfernt?
3. Wo liegen nach `mvn compile` die `.class`-Dateien?
4. Warum ist `target` kein Ort für eigenen Quellcode?

---

## Vertiefung

### Aufgabe 8 – Fehlerdiagnose: falsche Projektstruktur

Ein Lernender hat diese Struktur erstellt:

Die Datei `Main.java` beginnt mit:

```java
package ch.allianz.youngoitv.produktverwaltung;
```

```text
produktverwaltung-maven/
  src/
    main/
      java/
        pom.xml
        produktverwaltung/
          ch/
            allianz/
              youngoitv/
                Main.java
  target/
    ch/
      allianz/
        youngoitv/
          produktverwaltung/
            model/
              Produkt.java
```

Finde mindestens vier Fehler.

Korrigiere die Struktur als Textbaum.

Hinweise:

- Wo gehört `pom.xml` hin?
- Wo gehört Quellcode hin?
- Darf eigener Quellcode in `target` liegen?
- Wo beginnt die Package-Struktur?

---

### Aufgabe 9 – Fehlerdiagnose: falsches Arbeitsverzeichnis

Eine Person führt diesen Befehl aus:

```bash
mvn compile
```

Das Terminal steht hier:

```text
produktverwaltung-maven/src/main/java/ch/allianz/youngoitv/produktverwaltung/
```

Beantworte:

1. Was ist daran falsch?
2. In welchem Ordner sollte der Befehl ausgeführt werden?
3. Woran erkennt Maven den Projektordner?

---

### Aufgabe 10 – Maven ist keine Magie

Formuliere eine kurze Erklärung für eine Mitschülerin oder einen Mitschüler:

- Was macht Maven bei `mvn compile`?
- Welche bekannte Aufgabe steckt dahinter?
- Warum hilft die Maven-Konvention?

Verwende die Wörter:

```text
orchestrieren
javac
src/main/java
target
Convention over Configuration
```

---

### Aufgabe 11 – Reflexion zu Convention over Configuration

Beantworte schriftlich:

1. Was gewinnt man, wenn alle Maven-Projekte `src/main/java` verwenden?
2. Was könnte passieren, wenn jedes Projekt eine eigene freie Struktur hätte?
3. Warum ist eine Konvention für Teams hilfreich?
4. Welche Konvention aus dem Package-Block kennst du bereits?

---

## Transfer

### Aufgabe 12 – Pensionskassen-Simulation als Maven-Projekt strukturieren

Übertrage die bekannte Pensionskassen-Simulation in eine Maven-Struktur.

Ausgangsidee:

```text
src/
  ch/allianz/youngoitv/pensionskasse/
    Main.java
    simulation/PensionskassenSimulation.java
    service/Beitragssaetze.java
```

Ziel:

```text
pensionskasse-maven/
  pom.xml
  src/main/java/
    ch/allianz/youngoitv/pensionskasse/
      Main.java
      simulation/PensionskassenSimulation.java
      service/Beitragssaetze.java
```

Auftrag:

- Erstelle die Struktur und eine passende `pom.xml`.
- Falls du die bekannten Java-Dateien hast, lege sie an die passenden Orte.
- Verwende keine externen Dependencies.
- Verwende kein Maven Central und keine Multi-Module-Projekte.
- Kompiliere mit `mvn compile`, wenn die Java-Dateien vorhanden sind.
- Notiere, welche Package-Deklaration in jeder Datei stehen muss.

---

### Aufgabe 13 – Optionaler Ausblick: Konventionen in weiteren Tools

Später können auch andere Werkzeuge mit Konventionen arbeiten.

Recherchiere noch nicht im Internet. Überlege nur aus dem Unterricht heraus:

- Warum könnte ein `Jenkinsfile` immer gleich heissen?
- Warum könnte ein `Dockerfile` im Projektordner liegen?
- Warum könnten Kubernetes-Manifests in einem festen Ordner gesammelt werden?

Schreibe zu jedem Beispiel einen Satz.

Ziel: Erkenne, dass Konventionen nicht nur bei Maven helfen.
