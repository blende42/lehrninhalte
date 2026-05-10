# Übergabe – aktueller Stand und nächste Schritte

Diese Datei dient als kurzer Einstiegspunkt für eine neue Session.

## Aktueller Stand

Die Unterrichtssequenz ist in [CONTENT.md](./CONTENT.md) als empfohlene Reihenfolge dokumentiert.

Aktuell vorbereitet sind:

1. Primitive Datentypen, Wrapper und Parsing
2. String-Grundlagen
3. String-Vertiefung und einfache Textverarbeitung
4. Mini-Projekt Parser
5. StringBuilder
6. Arrays
7. Arrays vertiefen
8. 2D-Arrays
9. Methoden
10. Methoden festigen und Refactoring
11. Klassen und Objekte
12. Kapselung, Getter und Setter
13. Objektarrays und Verwaltungslogik
14. ArrayList
15. Java-Packages
16. Algorithmen und Datenstrukturen
17. Maven Einstieg

Die zuletzt erstellte Unterrichtseinheit ist **Maven Einstieg**. Zusätzlich wurde eine kleine Prozess- und Begriffsbibliothek für KI-gestützte Lehrmittel-Erstellung angelegt.

Neue Maven-Dateien:

- [Arbeitsblatt_Maven_Einstieg.md](./Arbeitsblaetter/Arbeitsblatt_Maven_Einstieg.md)
- [Uebungen_Maven_Einstieg.md](./Uebungen/Uebungen_Maven_Einstieg.md)
- [Loesungen_Maven_Einstieg.md](./Musterloesungen/Loesungen_Maven_Einstieg.md)
- [maven_orchestriert_build.svg](./graphics/maven_orchestriert_build.svg)

Neue Dokumentations- und Skill-Bereiche:

- [docs/begriffe](./docs/begriffe/) – kurze unterrichtstaugliche Begriffserklärungen
- [docs/prozesse](./docs/prozesse/) – Checklisten für Erstellung und Review
- [.codex/skills](./.codex/skills/) – lokale Skills für wiederkehrende Arbeitsabläufe
- [.agents/skills/git-repo-updaten](./.agents/skills/git-repo-updaten/SKILL.md) – kontrollierter Git-Abschluss nur bei ausdrücklichem Benutzerauftrag

## Prozess- und Begriffsbibliothek

Die neuen Dateien unter `docs/begriffe` erklären zentrale Begriffe kurz und unterrichtstauglich. Die Dateien unter `docs/prozesse` formulieren konkrete Checklisten für Erstellung und Review von Lehrmitteln. Die lokalen Skills unter `.codex/skills` verweisen auf diese Prozesse und auf [AGENTS.md](./AGENTS.md), ohne die Repo-Regeln vollständig zu duplizieren. Der Agent-Skill `git-repo-updaten` beschreibt einen kontrollierten Git-Abschluss und bleibt ausdrücklich an einen Benutzerauftrag gebunden.

## Wichtige Inhalte aus dem Maven-Einstieg

- Maven wird als Build-Tool eingeführt, das Java nicht ersetzt.
- Maven orchestriert bekannte Build-Schritte und ruft Werkzeuge wie `javac` in einem geordneten Ablauf auf.
- Der Begriff **orchestrieren** wird mit einer Dirigent-/Orchester-Analogie erklärt.
- Die Grafik `maven_orchestriert_build.svg` zeigt Quellcode, Maven, `javac` und `target/classes`.
- `Convention over Configuration` ist der rote Faden.
- Vergleich ohne Maven:
  - `src`
  - `out`
  - `javac -d out`
  - `java -cp out`
- Vergleich mit Maven:
  - `src/main/java`
  - `target`
  - `mvn compile`
  - `mvn clean`
- Es werden bewusst noch keine externen Dependencies, kein Maven Central, kein JUnit und kein Multi-Module eingeführt.
- Kernübung: Produktverwaltung aus dem Package-Block von manueller Struktur in Maven-Struktur migrieren.
- Transfer: Pensionskassen-Simulation in eine Maven-Struktur übertragen.
- Typische Fehler:
  - `target` mit `src` verwechseln
  - aus dem falschen Arbeitsverzeichnis starten
  - Package-Struktur falsch unter `src/main/java` abbilden
  - Maven als Magie missverstehen
  - `pom.xml` am falschen Ort ablegen

## Nächster geplanter Block

Als nächstes bietet sich **Maven-Projekte ausführen und paketieren** an.

Sinnvolle Inhalte:

- Produktverwaltung nach `mvn compile` gezielt starten
- Unterschied zwischen Kompilieren, Ausführen und Paketieren erklären
- `target/classes` und Classpath wieder sichtbar machen
- einfache JAR-Idee vorbereiten
- eventuell `mvn package` einführen
- externe Dependencies, Maven Central und JUnit weiterhin erst später behandeln

## Passender Anschluss

Der nächste Block sollte an diese Maven-Struktur anschliessen:

```text
produktverwaltung-maven/
  pom.xml
  src/main/java/
    ch/allianz/youngoitv/produktverwaltung/
      Main.java
      model/Produkt.java
      service/ProduktVerwaltung.java
  target/
```

Didaktisch sinnvoll ist als nächstes ein Vergleich:

- `mvn compile` erzeugt `.class`-Dateien unter `target/classes`
- Starten ist weiterhin ein Java-Thema
- Maven kann später weitere Phasen orchestrieren, zum Beispiel Paketieren

## Verifikation der zuletzt erstellten Einheiten

Für die früheren Java-Einheiten wurden temporäre Testklassen unter `/tmp` erstellt und geprüft:

- Methoden
- Methoden-Festigung
- Klassen und Objekte
- Kapselung, Getter und Setter
- Objektarrays und Verwaltungslogik
- ArrayList
- Java-Packages
- Algorithmen und Datenstrukturen

Die Java-Beispiele wurden mit `javac` kompiliert und mit `java` ausgeführt. Der Package-Block wurde ohne Maven mit Ausgabe nach `out` geprüft, inklusive Vertiefung mit `ArrayAlgorithmen`, `SortierAlgorithmen` und aufgeteilter Pensionskassen-Simulation. Der Algorithmen-Block wurde mit temporären Testklassen kompiliert und ausgeführt, inklusive Zinseszins, Sortierung und Pensionskassen-Simulation mit CSV-Ausgabe. SVG-Grafiken zu Klassen/Kapselung wurden mit `xmllint` geprüft und mit `rsvg-convert` gerendert.

Für den Maven-Einstieg wurden Markdown-Struktur, Dateiverweise und Schreibweise geprüft. Die SVG-Grafik wurde auf XML-Wohlgeformtheit geprüft. Es wurden keine ausführbaren Projektdateien im Repository angelegt.

## Wichtige Repo-Regeln

- Deutsch mit Locale `de_CH`.
- Schweizer Hochdeutsch mit `ss` statt Eszett.
- Dateinamen nur mit ASCII-Zeichen.
- Bei neuen oder geänderten Inhalten `README.md` und `CONTENT.md` mitführen.
- Java-Beispiele klein und auf EFZ-Niveau halten.
- Keine Git-Schreibaktionen ausführen, ausser sie werden ausdrücklich verlangt.
