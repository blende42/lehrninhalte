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
15. Repetition Java Intro
16. Java-Packages
17. Algorithmen und Datenstrukturen
18. Maven Einstieg
19. Maven-Projekte ausführen und paketieren
20. Maven-Projekte mit einfachen Tests vorbereiten
21. Von manuellen Tests zu automatisierten Tests mit JUnit
22. Wenn automatisierte Tests fehlschlagen
23. Refactoring mit Tests absichern
24. Produktdaten aus CSV-Dateien laden
25. Produktdaten als CSV-Dateien speichern
26. Persistenzablauf vertiefen
27. Code strukturieren und Verantwortlichkeiten aufteilen
28. Interfaces für austauschbare Services
29. Mehrere Klassen mit demselben Interface
30. Unterschiedliche Objekte über dasselbe Interface verwenden
31. Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden
32. Gemeinsamen Code mit Vererbung wiederverwenden

Die zuletzt erstellte Unterrichtseinheit ist **Gemeinsamen Code mit Vererbung wiederverwenden**. Zusätzlich wurde eine kleine Prozess- und Begriffsbibliothek für KI-gestützte Lehrmittel-Erstellung angelegt.

Neue Projektstruktur für grössere Mini-Projekte:

- [Projekte](./Projekte/README.md)
  - eigener Bereich für grössere, zusammenhängende Mini-Projekte
  - trennt Projekte klar von normalen Übungen
  - führt Lernenden- und Lehrpersonen-Versionen getrennt
- [Lagerverwaltung Light](./Projekte/Lagerverwaltung_Light/README.md)
  - ausgearbeitetes Mini-Projekt im Kontext einer einfachen Lagerverwaltung
- [Projektauftrag_Lagerverwaltung_Light.md](./Projekte/Lagerverwaltung_Light/Lernende/Projektauftrag_Lagerverwaltung_Light.md)
  - Lernenden-Version mit offenem Projektauftrag, realen Lagerfällen, Pflichtanforderungen, optionalen Erweiterungen, Tests, Abgabe und Reflexion
- [Projektauftrag_Lagerverwaltung_Light_LP.md](./Projekte/Lagerverwaltung_Light/Lehrperson/Projektauftrag_Lagerverwaltung_Light_LP.md)
  - Lehrpersonen-Version mit Beobachtungspunkten, typischen Schwierigkeiten, Hilfestellungen, Bewertungsideen und möglichen Lösungsrichtungen ohne vollständige Musterlösung
- [projekt_erstellen.md](./docs/prozesse/projekt_erstellen.md)
  - wiederverwendbarer Prozess für Mini-Projekte mit Pflichtanforderungen, optionalen Erweiterungen, technischem Rahmen und Reflexion
- [projekt_review.md](./docs/prozesse/projekt_review.md)
  - wiederverwendbarer Prozess für individuelle Projekt-Reviews mit Architekturgespräch, Testreview, Refactoring-Ideen und nächsten Lernschritten
- [projekt-erstellen](./.agents/skills/projekt-erstellen/SKILL.md)
  - Repo-Skill für das Erstellen strukturierter Mini-Projekte unter `Projekte/<Projektname>/`
- [projekt-review](./.agents/skills/projekt-review/SKILL.md)
  - Repo-Skill für individuelle Projekt-Reviews mit Coaching-Fokus
- [projekt_review_template.md](./templates/projekt_review_template.md)
  - wiederverwendbare Vorlage für kurze Review-Protokolle mit Beobachtungen, Reflexion und nächsten Lernschritten

Neue Repetitions- und Vertiefungsübung:

- [Repetition_Java_Intro.md](./Repetitionen/Repetition_Java_Intro/Lernende/Repetition_Java_Intro.md)
- [Repetition_Java_Intro_LP.md](./Repetitionen/Repetition_Java_Intro/Lehrperson/Repetition_Java_Intro_LP.md)
  - kombiniert Klassen und Objekte, Kapselung, `ArrayList` und Methoden
  - nutzt die bekannte Produktverwaltung
  - enthält viele kleine Pflichtaufgaben, optionale Transferaufgaben und eine separate Lehrpersonen-Version mit diagnostischen Hinweisen
  - neue Repetitionsserien sollen standardmässig unter `Repetitionen/<Name>/Lernende` und `Repetitionen/<Name>/Lehrperson` abgelegt werden

Neue Dateien im Maven-, Testing-, Refactoring- und Persistenz-Block:

- [Arbeitsblatt_Maven_Einstieg.md](./Arbeitsblaetter/Arbeitsblatt_Maven_Einstieg.md)
- [Uebungen_Maven_Einstieg.md](./Uebungen/Uebungen_Maven_Einstieg.md)
- [Loesungen_Maven_Einstieg.md](./Musterloesungen/Loesungen_Maven_Einstieg.md)
- [Arbeitsblatt_Maven_Ausfuehren_und_Paketieren.md](./Arbeitsblaetter/Arbeitsblatt_Maven_Ausfuehren_und_Paketieren.md)
- [Uebungen_Maven_Ausfuehren_und_Paketieren.md](./Uebungen/Uebungen_Maven_Ausfuehren_und_Paketieren.md)
- [Loesungen_Maven_Ausfuehren_und_Paketieren.md](./Musterloesungen/Loesungen_Maven_Ausfuehren_und_Paketieren.md)
- [Arbeitsblatt_Maven_Einfache_Tests_Vorbereiten.md](./Arbeitsblaetter/Arbeitsblatt_Maven_Einfache_Tests_Vorbereiten.md)
- [Uebungen_Maven_Einfache_Tests_Vorbereiten.md](./Uebungen/Uebungen_Maven_Einfache_Tests_Vorbereiten.md)
- [Loesungen_Maven_Einfache_Tests_Vorbereiten.md](./Musterloesungen/Loesungen_Maven_Einfache_Tests_Vorbereiten.md)
- [Arbeitsblatt_JUnit_Einstieg.md](./Arbeitsblaetter/Arbeitsblatt_JUnit_Einstieg.md)
- [Uebungen_JUnit_Einstieg.md](./Uebungen/Uebungen_JUnit_Einstieg.md)
- [Loesungen_JUnit_Einstieg.md](./Musterloesungen/Loesungen_JUnit_Einstieg.md)
- [Arbeitsblatt_JUnit_Fehleranalyse.md](./Arbeitsblaetter/Arbeitsblatt_JUnit_Fehleranalyse.md)
- [Uebungen_JUnit_Fehleranalyse.md](./Uebungen/Uebungen_JUnit_Fehleranalyse.md)
- [Loesungen_JUnit_Fehleranalyse.md](./Musterloesungen/Loesungen_JUnit_Fehleranalyse.md)
- [Arbeitsblatt_Refactoring_mit_Tests.md](./Arbeitsblaetter/Arbeitsblatt_Refactoring_mit_Tests.md)
- [Uebungen_Refactoring_mit_Tests.md](./Uebungen/Uebungen_Refactoring_mit_Tests.md)
- [Loesungen_Refactoring_mit_Tests.md](./Musterloesungen/Loesungen_Refactoring_mit_Tests.md)
- [Arbeitsblatt_CSV_Laden.md](./Arbeitsblaetter/Arbeitsblatt_CSV_Laden.md)
- [Uebungen_CSV_Laden.md](./Uebungen/Uebungen_CSV_Laden.md)
- [Loesungen_CSV_Laden.md](./Musterloesungen/Loesungen_CSV_Laden.md)
- [csv_laden_produktverwaltung.svg](./graphics/csv_laden_produktverwaltung.svg)
- [Arbeitsblatt_CSV_Speichern.md](./Arbeitsblaetter/Arbeitsblatt_CSV_Speichern.md)
- [Uebungen_CSV_Speichern.md](./Uebungen/Uebungen_CSV_Speichern.md)
- [Loesungen_CSV_Speichern.md](./Musterloesungen/Loesungen_CSV_Speichern.md)
- [csv_speichern_produktverwaltung.svg](./graphics/csv_speichern_produktverwaltung.svg)
- [Arbeitsblatt_Persistenzablauf_Vertiefen.md](./Arbeitsblaetter/Arbeitsblatt_Persistenzablauf_Vertiefen.md)
- [Uebungen_Persistenzablauf_Vertiefen.md](./Uebungen/Uebungen_Persistenzablauf_Vertiefen.md)
- [Loesungen_Persistenzablauf_Vertiefen.md](./Musterloesungen/Loesungen_Persistenzablauf_Vertiefen.md)
- [persistenzablauf_laden_bearbeiten_speichern.svg](./graphics/persistenzablauf_laden_bearbeiten_speichern.svg)
- [Arbeitsblatt_Verantwortlichkeiten_Aufteilen.md](./Arbeitsblaetter/Arbeitsblatt_Verantwortlichkeiten_Aufteilen.md)
- [Uebungen_Verantwortlichkeiten_Aufteilen.md](./Uebungen/Uebungen_Verantwortlichkeiten_Aufteilen.md)
- [Loesungen_Verantwortlichkeiten_Aufteilen.md](./Musterloesungen/Loesungen_Verantwortlichkeiten_Aufteilen.md)
- [verantwortlichkeiten_aufteilen.svg](./graphics/verantwortlichkeiten_aufteilen.svg)
- [Arbeitsblatt_Interfaces_Austauschbare_Services.md](./Arbeitsblaetter/Arbeitsblatt_Interfaces_Austauschbare_Services.md)
- [Uebungen_Interfaces_Austauschbare_Services.md](./Uebungen/Uebungen_Interfaces_Austauschbare_Services.md)
- [Loesungen_Interfaces_Austauschbare_Services.md](./Musterloesungen/Loesungen_Interfaces_Austauschbare_Services.md)
- [Arbeitsblatt_Mehrere_Implementierungen_Interface.md](./Arbeitsblaetter/Arbeitsblatt_Mehrere_Implementierungen_Interface.md)
- [Uebungen_Mehrere_Implementierungen_Interface.md](./Uebungen/Uebungen_Mehrere_Implementierungen_Interface.md)
- [Loesungen_Mehrere_Implementierungen_Interface.md](./Musterloesungen/Loesungen_Mehrere_Implementierungen_Interface.md)
- [Arbeitsblatt_Polymorphie_Interface.md](./Arbeitsblaetter/Arbeitsblatt_Polymorphie_Interface.md)
- [Uebungen_Polymorphie_Interface.md](./Uebungen/Uebungen_Polymorphie_Interface.md)
- [Loesungen_Polymorphie_Interface.md](./Musterloesungen/Loesungen_Polymorphie_Interface.md)
- [Arbeitsblatt_Code_Wiederverwenden.md](./Arbeitsblaetter/Arbeitsblatt_Code_Wiederverwenden.md)
- [Uebungen_Code_Wiederverwenden.md](./Uebungen/Uebungen_Code_Wiederverwenden.md)
- [Loesungen_Code_Wiederverwenden.md](./Musterloesungen/Loesungen_Code_Wiederverwenden.md)
- [Arbeitsblatt_Vererbung_Code_Wiederverwenden.md](./Arbeitsblaetter/Arbeitsblatt_Vererbung_Code_Wiederverwenden.md)
- [Uebungen_Vererbung_Code_Wiederverwenden.md](./Uebungen/Uebungen_Vererbung_Code_Wiederverwenden.md)
- [Loesungen_Vererbung_Code_Wiederverwenden.md](./Musterloesungen/Loesungen_Vererbung_Code_Wiederverwenden.md)
- [interface_produkt_speicher.svg](./graphics/interface_produkt_speicher.svg)
- [mehrere_implementierungen_interface.svg](./graphics/mehrere_implementierungen_interface.svg)
- [polymorphie_interface.svg](./graphics/polymorphie_interface.svg)
- [code_wiederverwenden.svg](./graphics/code_wiederverwenden.svg)
- [vererbung_code_wiederverwenden.svg](./graphics/vererbung_code_wiederverwenden.svg)
- [maven_orchestriert_build.svg](./graphics/maven_orchestriert_build.svg)
- [maven_compile_run_package.svg](./graphics/maven_compile_run_package.svg)
- [maven_tests_vorbereiten.svg](./graphics/maven_tests_vorbereiten.svg)
- [junit_manuell_zu_automatisiert.svg](./graphics/junit_manuell_zu_automatisiert.svg)
- [junit_test_fehlschlag_workflow.svg](./graphics/junit_test_fehlschlag_workflow.svg)
- [refactoring_mit_tests_workflow.svg](./graphics/refactoring_mit_tests_workflow.svg)

Neue Dokumentations- und Skill-Bereiche:

- [docs/begriffe](./docs/begriffe/) – kurze unterrichtstaugliche Begriffserklärungen
- [docs/prozesse](./docs/prozesse/) – Checklisten für Erstellung und Review
- [.agents/skills](./.agents/skills/) – aktuelle Repo-Skills für wiederkehrende und kontrollierte Arbeitsabläufe
- [.codex/skills](./.codex/skills/) – veraltete Skill-Ablage; die aktuellen Skills liegen unter `.agents/skills`

## Prozess- und Begriffsbibliothek

Die Dateien unter `docs/begriffe` erklären zentrale Begriffe kurz und unterrichtstauglich. Die Dateien unter `docs/prozesse` formulieren konkrete Checklisten für Erstellung und Review von Lehrmitteln. Die aktuellen Repo-Skills unter `.agents/skills` verweisen auf diese Prozesse und auf [AGENTS.md](./AGENTS.md), ohne die Repo-Regeln vollständig zu duplizieren. Die frühere Ablage `.codex/skills` ist veraltet. Der Skill `git-repo-updaten` beschreibt einen kontrollierten Git-Abschluss und bleibt ausdrücklich an einen Benutzerauftrag gebunden.

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

## Wichtige Inhalte aus Maven-Projekte ausführen und paketieren

- `mvn compile` erzeugt `.class`-Dateien unter `target/classes`.
- Ein Programmstart bleibt sichtbar ein Java-Thema, zum Beispiel mit `java -cp target/classes ...Main`.
- `mvn package` erzeugt ein Build-Artefakt, zum Beispiel `target/produktverwaltung-1.0.0.jar`.
- Eine einfache JAR-Datei wird als Build-Ergebnis eingeordnet, noch nicht als speziell konfiguriertes startbares JAR.
- Die Grafik `maven_compile_run_package.svg` zeigt `compile`, `run` und `package` als getrennte Schritte und hebt `target/classes` sowie eine JAR-Datei nach dem Schema `target/<artifactId>-<version>.jar` als Build-Ergebnisse hervor.
- Java-`package` und Maven `package` werden ausdrücklich getrennt:
  - Java-`package` strukturiert Klassen im Code.
  - Maven `package` ist eine Build-Phase.
- Maven-Lifecycle wird nur grob vorbereitet: `compile` vor `package`.
- Reproduzierbare Builds werden über standardisierte Befehle wie `mvn clean package` erklärt.
- Build-Server, Jenkins und CI/CD werden nur als Ausblick erwähnt.
- Es werden bewusst noch keine externen Dependencies, kein Maven Central, kein JUnit, keine Plugin-Details, keine Fat Jars, kein Spring Boot und kein `install`/`deploy` eingeführt.

## Nächster geplanter Block

Als nächstes bietet sich eine **Repetition zu Interface, Polymorphie, Refactoring und Vererbung oder eine Service-/Schichten-Vorbereitung** an.

Sinnvolle Inhalte:

- Interface als Vertrag diagnostisch prüfen
- konkrete Implementierung und Interface-Typ weiter unterscheiden
- gleiche Methodenaufrufe mit unterschiedlichen Implementierungen reflektieren
- eine Variable vom Interface-Typ mit unterschiedlichen konkreten Objekten erklären
- Code-Duplikate erkennen und kleine Hilfsmethoden sinnvoll einsetzen
- `extends` als Wiederverwendungsidee reflektieren
- Grenzen von Vererbung und Alternative mit Hilfsklasse besprechen
- einfache Service- und Schichten-Idee vorbereiten
- weiterhin keine Datenbank und keine komplexen Frameworks

## Passender Anschluss

Der nächste Block kann weiterhin an diese Maven-Struktur anschliessen:

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

Für den nächsten Block kann an diesen Vergleich angeschlossen werden:

- konkrete Klasse direkt verwenden
- Interface als Vertrag verwenden
- `ProduktSpeicher speicher = new CsvProduktSpeicher();`
- `ProduktSpeicher speicher = new KonsolenProduktSpeicher();`
- gleiche Methodensignatur, anderes Verhalten

## Wichtige Inhalte aus Interfaces für austauschbare Services

- Ein Interface beschreibt einen Vertrag.
- Eine Klasse kann diesen Vertrag mit `implements` erfüllen.
- Es wird bewusst nur ein Interface eingeführt: `ProduktSpeicher`.
- `ProduktSpeicher` beschreibt eine Methode `speichern(...)`.
- `CsvProduktSpeicher` bleibt die konkrete Implementierung und schreibt Produkte als CSV-Datei.
- `Main` kann eine Variable vom Interface-Typ verwenden:
  - `ProduktSpeicher speicher = new CsvProduktSpeicher();`
- Die Grafik `interface_produkt_speicher.svg` zeigt `Main`, das Interface `ProduktSpeicher`, die konkrete Umsetzung `CsvProduktSpeicher` und die CSV-Datei als Ablauf von Vertrag zu Umsetzung.
- Das Verhalten bleibt gleich: Produkte werden weiterhin als CSV-Datei gespeichert.
- Die Struktur wird etwas austauschbarer, weil `Main` den Vertrag kennt und nicht überall die konkrete Speicherart wissen muss.
- Basisaufgaben erstellen das Interface, passen `CsvProduktSpeicher` mit `implements` an, ändern `Main` und prüfen das unveränderte Verhalten.
- Vertiefungsaufgaben unterscheiden Vertrag und Umsetzung, ordnen Codeabschnitte zu und prüfen Methodensignaturen.
- Transferaufgaben beschreiben mögliche spätere Implementierungen wie `KonsolenProduktSpeicher` oder `BackupProduktSpeicher`, ohne sie verpflichtend zu implementieren.
- Die Musterlösung `Loesungen_Interfaces_Austauschbare_Services.md` zeigt eine kompakte Standardlösung mit `ProduktSpeicher`, `CsvProduktSpeicher implements ProduktSpeicher`, `Main` mit Interface-Typ, unverändertem Verhalten, typischen Fehlerhinweisen und kurzen Transferantworten.
- Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/interfaces-services-validierung` mit `mvn package` geprüft; die Produktionsklassen kompilierten erfolgreich. Es waren keine Testklassen hinterlegt. Zusätzlich wurde die kompilierte `Main`-Klasse mit `java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main` ausgeführt.
- Bewusst nicht behandelt werden Spring, Dependency Injection, abstrakte Klassen, komplexe Polymorphie, Datenbanken, ORM und formales Repository-Pattern.

## Wichtige Inhalte aus Mehrere Klassen mit demselben Interface

- Das bestehende Interface `ProduktSpeicher` bleibt unverändert.
- Neu wird genau eine zweite konkrete Implementierung eingeführt: `KonsolenProduktSpeicher`.
- `CsvProduktSpeicher` und `KonsolenProduktSpeicher` implementieren beide denselben Vertrag.
- Beide Klassen besitzen dieselbe Methodensignatur `speichern(...)`, zeigen aber unterschiedliches Verhalten:
  - `CsvProduktSpeicher` schreibt eine CSV-Datei.
  - `KonsolenProduktSpeicher` gibt Produkte auf der Konsole aus.
- `Main` arbeitet weiterhin mit dem Interface-Typ:
  - `ProduktSpeicher speicher = new CsvProduktSpeicher();`
  - `ProduktSpeicher speicher = new KonsolenProduktSpeicher();`
- Beim Wechsel der Implementierung wird nur die konkrete Klasse rechts von `new` ausgetauscht.
- Basisaufgaben erstellen `KonsolenProduktSpeicher`, implementieren `ProduktSpeicher`, setzen `speichern(...)` für die Konsole um und wechseln in `Main` zwischen beiden Implementierungen.
- Vertiefungsaufgaben vergleichen gemeinsame Elemente und Unterschiede, trennen Vertrag, Umsetzung und Nutzung und prüfen Methodensignaturen mit `mvn test` oder `mvn package`.
- Transferaufgaben diskutieren `BackupProduktSpeicher`, `StatistikProduktSpeicher` und `JsonProduktSpeicher` bewusst nur als Ideen.
- Die Musterlösung `Loesungen_Mehrere_Implementierungen_Interface.md` zeigt eine kompakte Standardlösung mit `ProduktSpeicher`, `CsvProduktSpeicher implements ProduktSpeicher`, `KonsolenProduktSpeicher implements ProduktSpeicher`, `Main` mit Interface-Typ, typischen Fehlerhinweisen und dokumentierter Maven-Verifikation.
- Die Grafik `mehrere_implementierungen_interface.svg` zeigt `ProduktSpeicher` als gemeinsamen Vertrag, zwei konkrete Implementierungen, `Main` mit Interface-Typ sowie gleichbleibenden Vertrag bei unterschiedlichem Verhalten.
- Typische Fehlerbilder:
  - Interface wird verändert statt implementiert
  - Methodensignatur stimmt nicht überein
  - `Main` verwendet wieder nur konkrete Klassen
  - `KonsolenProduktSpeicher` verletzt den Vertrag
  - beide Klassen verhalten sich identisch ohne erkennbaren Unterschied
  - zu viele neue Implementierungen auf einmal
  - Verwechslung zwischen Vertrag und konkreter Klasse
- Bewusst nicht behandelt werden Spring, Dependency Injection, Factory, abstrakte Klassen, Datenbanken, Repository-Pattern und komplexe Polymorphie.

## Wichtige Inhalte aus Unterschiedliche Objekte über dasselbe Interface verwenden

- Eine Variable vom Interface-Typ `ProduktSpeicher` kann nacheinander unterschiedliche konkrete Objekte enthalten.
- Die bekannten Klassen bleiben im Fokus:
  - `ProduktSpeicher`
  - `CsvProduktSpeicher`
  - `KonsolenProduktSpeicher`
  - `Main`
- Der Methodenaufruf bleibt gleich:
  - `speicher.speichern(produkte, "data/produkte.csv");`
- Die konkrete Klasse entscheidet das Verhalten:
  - `CsvProduktSpeicher` schreibt eine CSV-Datei.
  - `KonsolenProduktSpeicher` gibt Produkte auf der Konsole aus.
- Die Einheit führt Polymorphie praktisch über Beobachtung ein:
  - gleiche Variable
  - gleicher Interface-Typ
  - gleicher Methodenaufruf
  - unterschiedliches konkretes Objekt
  - unterschiedliche Wirkung
- Die Grafik `polymorphie_interface.svg` zeigt `ProduktSpeicher speicher` als Interface-Variable, zwei austauschbare konkrete Objekte, den gleichen Methodenaufruf und die unterschiedlichen Wirkungen CSV-Datei oder Konsolenausgabe.
- Basisaufgaben lassen zuerst `CsvProduktSpeicher` und danach `KonsolenProduktSpeicher` über dieselbe `ProduktSpeicher`-Variable verwenden.
- Vertiefungsaufgaben dokumentieren den Ablauf, vergleichen Ausgaben und ergänzen eine Verantwortlichkeitstabelle.
- Transferaufgaben skizzieren doppeltes Speichern, `LoggingProduktSpeicher` und `BackupProduktSpeicher` nur als Ideen.
- Die Musterlösung `Loesungen_Polymorphie_Interface.md` zeigt eine kompakte Standardlösung mit `ProduktSpeicher` als Interface-Typ, `CsvProduktSpeicher`, `KonsolenProduktSpeicher`, gleichem Methodenaufruf, unterschiedlichem beobachtbarem Verhalten, typischen Fehlerhinweisen und dokumentierter Maven-Verifikation.
- Typische Fehlerbilder:
  - Interface und konkrete Klasse verwechseln
  - `ProduktSpeicher` direkt instanziieren wollen
  - Verhalten der konkreten Klasse falsch einschätzen
  - `Main` wieder unnötig stark an konkrete Klassen koppeln
  - gleiche Methode mit gleichem Verhalten verwechseln
  - zu viele neue Implementierungen gleichzeitig einführen
- Bewusst nicht behandelt werden abstrakte Klassen, `instanceof`, Downcasting, Dependency Injection, Spring, Factory, Datenbanken und komplexe Vererbung.

## Wichtige Inhalte aus Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden

- Mehrfach kopierter Code erschwert spätere Änderungen.
- Die bekannten Speicherklassen bleiben im Fokus:
  - `ProduktSpeicher`
  - `CsvProduktSpeicher`
  - `KonsolenProduktSpeicher`
- Ähnliche Codeblöcke werden zuerst sichtbar gemacht, bevor eine Lösung eingeführt wird.
- Gemeinsamkeiten:
  - Produkte iterieren
  - Produktnamen lesen
  - Produktpreis lesen
  - Produkt als Text formatieren
- Unterschiede bleiben bewusst erhalten:
  - CSV-Datei nutzt `;`
  - Konsolenausgabe nutzt lesbaren Text mit `:`
- Basisaufgaben markieren doppelte und ähnliche Codeabschnitte, beschreiben Gemeinsamkeiten und lagern Formatierung in kleine Hilfsmethoden aus.
- Vertiefungsaufgaben verwenden Hilfsmethoden mehrfach, prüfen Änderungen an einer Stelle und beschreiben die Auswirkungen auf Wartbarkeit.
- Transferaufgaben behandeln weitere mögliche Duplikate, Logging-Ausgabe, Statistik-Hilfsmethoden und Vor- und Nachteile gemeinsamer Basisklassen.
- Die Musterlösung `Loesungen_Code_Wiederverwenden.md` zeigt kompakte Standardlösungen mit Hilfsmethoden in `CsvProduktSpeicher` und `KonsolenProduktSpeicher`, Verhaltensprüfung nach dem Refactoring, typischen Fehlerhinweisen und dokumentierter Maven-Verifikation.
- Die Grafik `code_wiederverwenden.svg` zeigt ähnliche Logik in `CsvProduktSpeicher` und `KonsolenProduktSpeicher`, das gemeinsame Auslagern in Hilfsmethoden und die Vorteile weniger Duplikate, Änderungen an einer Stelle, bessere Wartbarkeit und Vorbereitung auf Vererbung.
- `extends` wird nur als vorsichtiger Ausblick erwähnt:
  - Vererbung ist kein Selbstzweck.
  - Sie kann später helfen, wenn wirklich gemeinsamer Code vorhanden ist.
- Typische Fehlerbilder:
  - zu früh komplexe Vererbung einführen
  - Unterschiede zwischen Klassen ignorieren
  - gemeinsame Methode zu allgemein machen
  - Verhalten unabsichtlich verändern
  - Duplikate nur umbenennen statt reduzieren
  - alles in eine einzige Hilfsklasse verschieben
  - Wiederverwendung mit Kopieren verwechseln
- Bewusst nicht behandelt werden tiefe Vererbungshierarchien, abstrakte Klassen, Mehrfachvererbung, `instanceof`, Downcasting, UML-Formalismus und komplexe OOP-Theorie.

## Wichtige Inhalte aus Gemeinsamen Code mit Vererbung wiederverwenden

- Vererbung wird vorsichtig aus einem echten Wiederverwendungsproblem heraus eingeführt.
- Die bekannten Klassen bleiben im Fokus:
  - `ProduktSpeicher`
  - `ProduktSpeicherBasis`
  - `CsvProduktSpeicher`
  - `KonsolenProduktSpeicher`
- `ProduktSpeicher` bleibt das Interface und beschreibt den Vertrag `speichern(...)`.
- `ProduktSpeicherBasis` ist eine kleine Basisklasse für gemeinsame Hilfsmethoden.
- `CsvProduktSpeicher` und `KonsolenProduktSpeicher` verwenden:
  - `extends ProduktSpeicherBasis`
  - `implements ProduktSpeicher`
- Die gemeinsame Methode `produktZeile(Produkt produkt, String trennzeichen)` zeigt Wiederverwendung, ohne CSV- und Konsolenlogik in die Basisklasse zu verschieben.
- `speichern(...)` bleibt bewusst in den konkreten Klassen.
- Die Grafik `vererbung_code_wiederverwenden.svg` zeigt `ProduktSpeicher` als Interface, `ProduktSpeicherBasis` als kleine Basisklasse, die beiden konkreten Speicherklassen mit `extends` und `implements` sowie ihr unterschiedliches Verhalten.
- Basisaufgaben markieren doppelte Hilfsmethoden, erstellen `ProduktSpeicherBasis`, passen beide Speicherklassen mit `extends` an und prüfen das Verhalten erneut.
- Vertiefungsaufgaben unterscheiden Interface, Basisklasse und konkrete Klasse, ordnen Methoden zu und prüfen Lesbarkeit sowie Wartbarkeit.
- Transferaufgaben behandeln weitere Hilfsmethoden, ungeeignete Auslagerungen, Grenzen von Vererbung und eine Alternative mit Hilfsklasse.
- Die Musterlösung `Loesungen_Vererbung_Code_Wiederverwenden.md` zeigt eine kompakte Standardlösung mit `ProduktSpeicher`, `ProduktSpeicherBasis`, `CsvProduktSpeicher extends ProduktSpeicherBasis implements ProduktSpeicher` und `KonsolenProduktSpeicher extends ProduktSpeicherBasis implements ProduktSpeicher`.
- Die gemeinsame Hilfsmethode `produktZeile(...)` liegt in der Basisklasse; Datei- und Konsolenlogik bleiben in den konkreten Klassen.
- Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/vererbung-loesung-validierung` mit `mvn package` geprüft. Zusätzlich wurde die kompilierte `Main`-Klasse mit `java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main` ausgeführt und die erzeugte CSV-Datei kontrolliert. Es waren keine JUnit-Tests hinterlegt.
- Typische Fehlerbilder:
  - zu viel Code in die Basisklasse verschieben
  - Unterschiede zwischen Klassen ignorieren
  - Interface und Basisklasse verwechseln
  - Vererbung nur verwenden, weil es technisch möglich ist
  - Verhalten beim Refactoring verändern
  - Tests nach der Änderung vergessen
  - Basisklasse zu allgemein benennen
- Bewusst nicht behandelt werden abstrakte Klassen als Vertiefung, tiefe Vererbungshierarchien, komplexes `super(...)`, `instanceof`, Downcasting, Template Method, Spring und Dependency Injection.

## Wichtige Inhalte aus Code strukturieren und Verantwortlichkeiten aufteilen

- Eine Klasse soll nicht alles machen.
- `Main` startet das Programm und orchestriert den Ablauf, enthält aber keine Fachlogik.
- Fachlogik gehört in passende Klassen wie `ProduktVerwaltung`:
  - Produkte suchen
  - Preise ändern
  - Gesamtwert berechnen
  - Produkte zählen
- Dateilogik gehört in passende Klassen wie `CsvProduktLeser` und `CsvProduktSpeicher`:
  - CSV-Dateien lesen
  - CSV-Zeilen parsen
  - Produkte als CSV-Zeilen schreiben
- `Produkt` bleibt ein einfaches Datenobjekt.
- Basisaufgaben ordnen Verantwortlichkeiten zu und verschieben Fach- und Dateilogik aus `Main`.
- Vertiefungsaufgaben behandeln schrittweises Refactoring, doppelte Logik, sprechende Methodennamen, Tests und Verantwortlichkeitstabellen.
- Transferaufgaben behandeln:
  - einfachen Statistik-Service entwerfen
  - Export-Service als Idee skizzieren
  - Backup-Funktion passend zuordnen
  - entscheiden, ob eine neue Verantwortung eine neue Klasse rechtfertigt
- Die Grafik `verantwortlichkeiten_aufteilen.svg` zeigt `Main`, `Produkt`, `ProduktVerwaltung`, `CsvProduktLeser` und `CsvProduktSpeicher` als getrennte Rollen. Sie macht sichtbar, dass `Main` nicht alles selbst macht, Fachlogik und Dateilogik getrennt bleiben und die Struktur Tests sowie spätere Erweiterungen erleichtert.
- Die Musterlösung `Loesungen_Verantwortlichkeiten_Aufteilen.md` zeigt eine kompakte Standardlösung mit Verantwortlichkeitstabelle, entlasteter `Main`, `ProduktVerwaltung` für Fachlogik, CSV-Klassen für Dateilogik, sprechenden Methodennamen und einfachen Transferentscheidungen.
- Die Java-Beispiele der Musterlösung wurden als temporäres Maven-Projekt unter `/tmp/verantwortlichkeiten-loesung-validierung` mit `mvn package` geprüft; die Produktionsklassen kompilierten erfolgreich. Zusätzlich wurde die kompilierte `Main`-Klasse mit `java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main` ausgeführt. Die JUnit-Beispiele sind im Lösungstext enthalten, waren im temporären Projekt aber nicht als Testdateien hinterlegt.
- Typische Fehlerbilder:
  - alles bleibt in `Main`
  - Datei- und Fachlogik werden vermischt
  - Klassen werden nur umbenannt, aber nicht entlastet
  - Methodennamen bleiben unklar
  - Tests werden nach dem Refactoring nicht ausgeführt
  - neue Klassen haben keine klare Verantwortung
  - zu viele kleine Klassen ohne Nutzen
- Datenbanken, ORM, Spring, Clean Architecture, formales Repository-Pattern, REST-APIs und generische CSV-Frameworks werden bewusst nicht behandelt.

## Wichtige Inhalte aus Persistenzablauf vertiefen

- Persistenz wird als vollständiger Ablauf verstanden:
  - laden
  - bearbeiten
  - speichern
  - erneut laden
  - prüfen
- Daten im Arbeitsspeicher sind temporär; CSV-Dateien speichern einen Zustand dauerhaft.
- Änderungen an einer `ArrayList<Produkt>` werden erst durch bewusstes Speichern dauerhaft.
- Die bekannte Produktverwaltung wird weiterverwendet:
  - `Produkt`
  - `ProduktVerwaltung`
  - `CsvProduktLeser`
  - `CsvProduktSpeicher`
  - `Main`
- Basisaufgaben führen durch Laden, Ausgeben, Hinzufügen, Preisänderung, Speichern und erneutes Laden.
- Vertiefungsaufgaben behandeln Gesamtwertvergleich, ungültige CSV-Zeilen, leere Produktlisten, nicht gefundene Produkte und Formatvergleich.
- Transferaufgaben sind fest integriert und behandeln:
  - Backup-Datei vor dem Überschreiben
  - Exportdatei mit anderem Namen
  - Kopfzeile `name;preis`
  - einfache Änderungsstatistik
- Die Grafik `persistenzablauf_laden_bearbeiten_speichern.svg` zeigt den vollständigen Ablauf von CSV-Datei über Laden, `ArrayList<Produkt>`, Bearbeiten, `ProduktVerwaltung`, Speichern, erneutes Laden und Änderung prüfen. Sie macht temporären Arbeitsspeicher, dauerhafte Datei, passende Formate sowie getrennte Datei- und Fachlogik sichtbar.
- Die Musterlösung `Loesungen_Persistenzablauf_Vertiefen.md` zeigt eine kompakte Standardlösung mit `Produkt`, `ProduktVerwaltung`, `CsvProduktLeser`, `CsvProduktSpeicher` und `Main`.
- Die Java-Beispiele der Musterlösung wurden als temporäres Maven-Projekt unter `/tmp/persistenzablauf-validierung` mit `mvn package` geprüft; zusätzlich wurde die kompilierte `Main`-Klasse mit `java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main` ausgeführt.
- Typische Fehlerbilder:
  - Änderung wird nicht gespeichert
  - Speicher- und Ladeformat passen nicht zusammen
  - alles landet wieder in `main`
  - Datei wird unbewusst überschrieben
  - Preis bleibt `String` statt `double`
  - Änderungen passieren an falscher Liste
  - leere oder fehlerhafte Zeilen werden ignoriert, ohne gezählt zu werden
  - Zielordner existiert nicht
  - Datei- und Fachlogik werden vermischt
- Datenbanken, ORM, JSON, Streams API, GUI, Spring, generische CSV-Frameworks und formales Repository-Pattern werden bewusst nicht behandelt.

## Wichtige Inhalte aus Produktdaten als CSV-Dateien speichern

- Persistenz wird um den Rückweg von Objekten in Dateien ergänzt.
- `Produkt`-Objekte werden mit einfacher String-Verkettung in CSV-Zeilen umgewandelt.
- Mehrere Produkte werden aus einer `ArrayList<Produkt>` mit einer Schleife in `ArrayList<String>` übertragen.
- `Files.write(...)` wird als einfache Datei-Ausgabe verwendet; Überschreiben wird bewusst thematisiert.
- Gespeicherte Dateien werden erneut geladen, um Speicher- und Ladeformat zu prüfen.
- `CsvProduktSpeicher` übernimmt Dateilogik, `ProduktVerwaltung` bleibt für Fachlogik zuständig.
- Einfache Fehlerfälle werden sichtbar behandelt:
  - Datei kann nicht geschrieben werden
  - Zielordner fehlt
  - leerer Produktname
  - ungültiger Preis
  - leere Produktliste
  - Speicher- und Ladeformat passen nicht zusammen
- Nicht behandelt werden Datenbanken, ORM, JSON, Streams API, generische CSV-Frameworks, Serialisierung, Multi-Threading und komplexe Exception-Strukturen.
- Die Musterlösung `Loesungen_CSV_Speichern.md` zeigt eine kompakte Standardlösung mit `CsvProduktSpeicher`, erneutem Laden über `CsvProduktLeser`, `ProduktVerwaltung`, `Files.write(...)`, leeren Listen, Überschreiben und einfachen Fehlerfällen.
- Die Grafik `csv_speichern_produktverwaltung.svg` zeigt den Ablauf von `ArrayList<Produkt>` über CSV-Zeilen und `Files.write(...)` bis zur CSV-Datei sowie die Trennung von Datei- und Fachlogik.

## Wichtige Inhalte aus Produktdaten aus CSV-Dateien laden

- Persistenz wird als dauerhafte Speicherung ausserhalb des Programms eingeführt.
- CSV wird als einfache strukturierte Textdatei mit einer Produktzeile pro Datensatz verwendet.
- Produktdaten werden mit `split(";")`, `trim()` und `Double.parseDouble(...)` aus Text in Objekte umgewandelt.
- Mehrere Produkte werden in einer `ArrayList<Produkt>` gesammelt und an die bekannte Produktverwaltung übergeben.
- `CsvProduktLeser` übernimmt Dateilogik, `ProduktVerwaltung` bleibt für Fachlogik wie Zählen und Gesamtwert zuständig.
- Einfache Fehlerfälle werden sichtbar behandelt:
  - Datei nicht gefunden
  - leere Zeile
  - fehlende oder zusätzliche Spalten
  - ungültiger Preis
- Nicht behandelt werden Datenbanken, ORM, JSON, Streams API, generische Parser, Multi-Threading und komplexe Dateiformate.
- Die Musterlösung `Loesungen_CSV_Laden.md` zeigt eine kompakte Standardlösung mit `CsvProduktLeser`, `Produkt`, `ProduktVerwaltung`, `ArrayList`, einfachen Fehlerfällen und dokumentierter `mvn test`-Verifikation.
- Die Grafik `csv_laden_produktverwaltung.svg` zeigt den Ablauf von CSV-Text über `split(";")` und Parsing bis zur `ArrayList<Produkt>` sowie die Trennung von Datei- und Fachlogik.

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

Für **Maven-Projekte ausführen und paketieren** wurden Markdown-Struktur, Dateiverweise, de-CH-Schreibweise und die Maven-/Java-Begriffstrennung geprüft. Die Grafik `maven_compile_run_package.svg` wurde ergänzt und im Arbeitsblatt eingebunden. Es wurden keine ausführbaren Projektdateien im Repository angelegt.

Für **Produktdaten aus CSV-Dateien laden** wurden Arbeitsblatt, Übungen, Musterlösung, Übersichtseinträge und de-CH-Schreibweise geprüft. Die Java-Beispiele der Musterlösung wurden als temporäres Maven-Projekt unter `/tmp/csv-laden-validierung` mit `mvn test` geprüft; zusätzlich wurde die kompilierte `Main`-Klasse mit `java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main` ausgeführt. Die Grafik `csv_laden_produktverwaltung.svg` wurde mit `xmllint` validiert und mit `rsvg-convert` gerendert.

Für **Produktdaten als CSV-Dateien speichern** wurden Arbeitsblatt, Übungen, Musterlösung, Übersichtseinträge, Markdown-Codeblöcke und de-CH-Schreibweise geprüft. Die zentralen Java-Beispiele zu `Produkt`, `CsvProduktLeser`, `CsvProduktSpeicher`, `ProduktVerwaltung`, `ArrayList`, `Files.write(...)` und `Main` wurden als temporäre Maven-Projekte unter `/tmp/csv-speichern-validierung` und `/tmp/csv-speichern-loesung-validierung` mit `mvn test` geprüft; zusätzlich wurde die kompilierte `Main`-Klasse mit `java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main` ausgeführt und die erzeugte CSV-Datei kontrolliert. Die Grafik `csv_speichern_produktverwaltung.svg` wurde mit `xmllint` validiert und mit `rsvg-convert` gerendert.

Für **Persistenzablauf vertiefen** wurden Arbeitsblatt, Übungen, Musterlösung, Grafik, Übersichtseinträge, Markdown-Codeblöcke und de-CH-Schreibweise geprüft. Die Java-Beispiele der Musterlösung wurden als temporäres Maven-Projekt unter `/tmp/persistenzablauf-validierung` mit `mvn package` geprüft; zusätzlich wurde die kompilierte `Main`-Klasse mit `java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main` ausgeführt. Backup- und Exportdatei wurden erzeugt und kontrolliert. Die Grafik `persistenzablauf_laden_bearbeiten_speichern.svg` wurde mit `xmllint --noout` validiert und mit `rsvg-convert` gerendert.

## Wichtige Inhalte aus Maven-Projekte mit einfachen Tests vorbereiten

- Der Block trennt manuelle Testausgaben von systematischer Prüfung.
- Zentrale Testidee: erwartetes Resultat mit tatsächlichem Resultat vergleichen.
- `main` wird als Startpunkt verstanden, nicht als Ort für die eigentliche Fachlogik.
- Kleine Methoden mit Parametern und Rückgabewerten werden als prüfbare Fachlogik eingeübt.
- Die Produktverwaltung dient weiter als Kontext:
  - Rabattpreis berechnen
  - Produkt suchen
  - Gesamtwert berechnen
- Einfache Prüfhilfen werden mit `if`/`else`, `true` und `false` umgesetzt.
- Die Grafik `maven_tests_vorbereiten.svg` zeigt die Trennung von `main`, Fachlogik und manueller Prüfung.
- Edge Cases wie kein Rabatt, voller Rabatt, leeres Produktarray und nicht gefundene Produkte werden bewusst formuliert.
- Die Musterlösung zeigt eine kompakte Standardumsetzung mit `Produkt`, `ProduktVerwaltung` und `Main`.
- Es werden bewusst noch kein JUnit, keine Test-Annotationen, keine Assertions-Bibliothek, keine externen Dependencies, kein Maven Central, keine Plugin-Details und keine Test-Lifecycle-Details eingeführt.

## Wichtige Inhalte aus Von manuellen Tests zu automatisierten Tests mit JUnit

- JUnit Jupiter wird als Automatisierung der bekannten manuellen Testidee eingeführt.
- Die Kernidee bleibt: erwartetes Resultat mit tatsächlichem Resultat vergleichen.
- Aus `if (resultat == erwartet)` mit Ausgabe wird `assertEquals(erwartet, resultat)`.
- Testcode liegt unter `src/test/java`, Produktivcode unter `src/main/java`.
- `@Test` markiert Testmethoden.
- `assertEquals` wird als wichtigste Prüfung eingeführt; `assertTrue` wird nur sparsam für einfache Wahrheitsprüfungen verwendet.
- JUnit ist die erste externe Dependency in `pom.xml`.
- `scope test` wird grob als Test-Abhängigkeit erklärt.
- Maven Central wird nur kurz als Quelle externer Bibliotheken erwähnt.
- Das lokale `.m2`-Repository wird kurz als Cache für heruntergeladene Bibliotheken eingeordnet; der erste `mvn test` kann deshalb einen Download auslösen.
- `mvn test` wird als standardisierter Testlauf eingeführt.
- `target/surefire-reports` wird nur als Ergebnisort des Maven-Testlaufs erwähnt.
- Regressionstests werden einfach als Tests erklärt, die alte Fehler gegen Wiederauftreten absichern.
- Die Produktverwaltung bleibt Kontext für Rabattberechnung, Produktsuche und Gesamtwert.
- Die Musterlösung `Loesungen_JUnit_Einstieg.md` zeigt eine kompakte Standardlösung mit `pom.xml`, Produktivcode, Testcode, Fehlerdiagnose und dokumentierter `mvn test`-Verifikation.
- Die Grafik `junit_manuell_zu_automatisiert.svg` zeigt den Übergang von Ausgabe plus menschlichem Vergleich zu `assertEquals` und `mvn test` sowie die Trennung von Fachlogik und Tests.

## Wichtige Inhalte aus Wenn automatisierte Tests fehlschlagen

- Fehlgeschlagene Tests werden als hilfreiche Rückmeldung verstanden.
- `expected` und `actual` werden in `assertEquals`-Fehlermeldungen unterschieden.
- Stacktraces werden nur grob eingeordnet: Testklasse, Testmethode, Assert-Zeile und Werte.
- `mvn test` wird bei fehlerhaften Tests als reproduzierbarer Testlauf verwendet.
- Maven stoppt Builds, wenn Tests fehlschlagen; das macht Build-Qualität sichtbar.
- `target/surefire-reports` wird nur kurz als Ort technischer Testberichte erwähnt.
- Fehler werden bewusst provoziert, gelesen, korrigiert und erneut geprüft.
- Edge Cases wie voller Rabatt, leeres Produktarray und nicht gefundene Produkte werden ergänzt.
- Regressionstests werden als Schutz vor wiederkehrenden Fehlern erklärt.
- Tests werden als Sicherheitsnetz für spätere Refactorings vorbereitet.
- Die Musterlösung `Loesungen_JUnit_Fehleranalyse.md` zeigt kompakte Standardlösungen zu Fehlermeldungen, Ursachenanalyse, korrigierter Fachlogik, Regressionen und `mvn test`-Interpretation.
- Die Grafik `junit_test_fehlschlag_workflow.svg` zeigt den Ablauf von Codeänderung, rotem Test, Analyse, Korrektur und erneut grünem Testlauf.
- Nicht behandelt werden formales TDD, Mocking, komplexe Assertions, Coverage, technische CI/CD-Umsetzung, tiefer Debugger-Einsatz, Logging-Frameworks, Parameterized Tests und Integrationstests.

## Wichtige Inhalte aus Refactoring mit Tests absichern

- Refactoring wird als Strukturverbesserung verstanden, nicht als neue Funktion.
- Verhalten und Struktur werden klar getrennt.
- Vor einem Refactoring wird mit `mvn test` ein grüner Ausgangszustand hergestellt.
- Nach jedem kleinen Refactoring-Schritt wird `mvn test` erneut ausgeführt.
- Tests dienen als Sicherheitsnetz gegen Regressionen.
- Die Produktverwaltung bleibt Kontext:
  - Rabattberechnung
  - Gesamtwertberechnung
  - Produktsuche
- `main` wird von Fachlogik entlastet.
- Lange Methoden werden in kleinere Methoden mit sprechenden Namen aufgeteilt.
- Doppelte Rabattberechnung wird zentralisiert.
- Edge Cases wie `0` Prozent und `100` Prozent Rabatt bleiben durch Tests abgesichert.
- Die Musterlösung `Loesungen_Refactoring_mit_Tests.md` zeigt kompakte Standardlösungen zu grünen Ausgangszuständen, kleinen Refactoring-Schritten, entlasteter `main`, zentralisierter Rabattlogik, Regressionen und `mvn test`-Verifikation.
- Die Grafik `refactoring_mit_tests_workflow.svg` zeigt den Ablauf von grünem Ausgangszustand, kleinem Refactoring-Schritt, erneutem Testlauf und Korrektur bei Regression.
- Build-Server und CI/CD werden nur kurz als spätere automatische Ausführung derselben Tests erwähnt.
- Nicht behandelt werden formales TDD, Mocking, Test Doubles, komplexe Patterns, Clean Architecture, Coverage, Spring und Datenbanken.

## Wichtige Repo-Regeln

- Deutsch mit Locale `de_CH`.
- Schweizer Hochdeutsch mit `ss` statt Eszett.
- Dateinamen nur mit ASCII-Zeichen.
- Bei neuen oder geänderten Inhalten `README.md` und `CONTENT.md` mitführen.
- Java-Beispiele klein und auf EFZ-Niveau halten.
- Keine Git-Schreibaktionen ausführen, ausser sie werden ausdrücklich verlangt.
