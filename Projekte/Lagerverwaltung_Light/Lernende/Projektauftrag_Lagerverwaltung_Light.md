# Projektauftrag Lagerverwaltung Light

[Zur Projektübersicht](../README.md) | [Hinweise für Lehrperson](../Lehrperson/Projektauftrag_Lagerverwaltung_Light_LP.md)

## Ausgangslage

Du kennst aus der bisherigen Produktverwaltung bereits Produkte, Sammlungen, CSV-Dateien, Maven, JUnit-Tests, Verantwortlichkeiten, Interfaces und einfache Wiederverwendung.

In diesem Projekt baust du daraus eine kleine Lagerverwaltung. Die Anwendung verwaltet Produkte mit Preis und Lagerbestand. Produktdaten können aus einer CSV-Datei geladen, angezeigt, verändert und wieder gespeichert werden.

Typische Situationen aus dem Lager:

- Ein Produkt wird verkauft, aber der Bestand reicht nicht aus.
- Eine CSV-Datei enthält eine ungültige Zeile oder ungültige Werte.
- Ein Produkt soll neu aufgenommen werden, obwohl bereits ein Produkt mit gleichem Namen vorhanden ist.

Das Projekt ist bewusst offen formuliert. Du bekommst Anforderungen und technische Leitplanken, aber keine Schritt-für-Schritt-Anleitung.

## Ziel des Projekts

Am Ende hast du eine kleine Java-Anwendung, die eine Lagerverwaltung für Produkte umsetzt.

Deine Anwendung soll:

- Produktdaten aus einer CSV-Datei laden
- Produkte mit Name, Preis und Lagerbestand verwalten
- Verkäufe durchführen und dabei den Bestand korrekt reduzieren
- neue Produkte hinzufügen
- ungültige Eingaben oder Werte kontrolliert behandeln
- den aktuellen Stand wieder als CSV-Datei speichern
- zentrale Fachlogik mit JUnit-Tests prüfen

Wichtig ist nicht nur, dass die Anwendung funktioniert. Deine Struktur soll zeigen, dass du Verantwortlichkeiten bewusst aufteilst und bekannte Konzepte sinnvoll kombinierst.

## Technischer Rahmen

- Java 21
- Maven
- sinnvolle Packages
- CSV-Dateien für Persistenz
- JUnit für Tests
- keine externen Libraries ausser JUnit
- keine Datenbank
- kein Spring
- keine GUI
- keine REST-API

Erwartete Projektstruktur:

- Produktivcode liegt unter `src/main/java`
- Testcode liegt unter `src/test/java`
- CSV-Test- oder Beispieldaten liegen sinnvoll abgelegt, zum Beispiel unter `data`
- Maven-Befehle wie `mvn test` funktionieren aus dem Projektordner

Das CSV-Format soll einfach bleiben. Ein mögliches Format ist:

```text
name;preis;bestand
Tastatur;49.90;12
Maus;24.50;20
Monitor;199.00;5
```

Verwende eine Kopfzeile. Du darfst die Spaltennamen anders wählen, wenn du die CSV-Struktur nachvollziehbar dokumentierst.

## Pflichtanforderungen

Deine Lösung muss diese fachlichen Anforderungen erfüllen:

1. Produkte mit Name, Preis und Lagerbestand verwalten.
2. Produktdaten aus einer CSV-Datei laden.
3. Produktdaten als CSV-Datei speichern.
4. Produkte sinnvoll anzeigen.
5. Einen Verkauf durchführen.
6. Einen Verkauf nur erlauben, wenn genug Bestand vorhanden ist.
7. Den Bestand nach einem erfolgreichen Verkauf reduzieren.
8. Ein neues Produkt hinzufügen.
9. Doppelte Produktnamen beim Hinzufügen oder Laden bewusst behandeln.
10. Ungültige Werte kontrolliert behandeln, zum Beispiel:
   - leerer Produktname
   - negativer Preis
   - negativer Lagerbestand
   - Verkaufsmenge kleiner oder gleich `0`
   - Verkauf von mehr Stück als vorhanden
   - ungültige oder unvollständige CSV-Zeile
11. Eine einfache Konsolen-Demo oder einen nachvollziehbaren Programmablauf in `main` bereitstellen.
12. Mindestens 4 fachliche JUnit-Tests schreiben.

Deine Lösung muss diese strukturellen Anforderungen erfüllen:

1. Verwende mindestens eine eigene Produktklasse.
2. Verwende Kapselung mit privaten Attributen und kontrolliertem Zugriff.
3. Verwende mindestens eine `ArrayList` für die Produktverwaltung.
4. Lagere Fachlogik aus `main` aus.
5. Verwende sinnvolle Methoden mit klaren Namen.
6. Verwende sinnvolle Packages.
7. Trenne Laden/Speichern, Fachlogik und Programmstart erkennbar voneinander.
8. Verwende mindestens ein Interface dort, wo Austauschbarkeit sinnvoll ist, zum Beispiel beim Laden und Speichern.
9. Zeige Polymorphie sinnvoll, zum Beispiel durch eine Variable vom Interface-Typ.
10. Vermeide unnötige Code-Duplikate.

Du musst keine bestimmte Zielarchitektur exakt nachbauen. Entscheide selbst, welche Klassen und Packages für deine Lösung sinnvoll sind.

## Optionale Erweiterungen

Diese Erweiterungen sind freiwillig. Wähle höchstens so viele, dass der Pflichtteil sauber bleibt.

- Warnung bei tiefem Lagerbestand
- einfache Statistik, zum Beispiel Gesamtwert des Lagers oder Anzahl Produkte mit tiefem Bestand
- Preisänderung mit kurzer Protokollausgabe
- Backup-Datei vor dem Speichern
- zusätzliche Exportdatei, zum Beispiel nur Produkte mit tiefem Bestand
- zweite Speicherart als Idee oder Umsetzung, zum Beispiel Konsolenausgabe oder andere CSV-Datei
- zusätzliche Tests für Randfälle

Optionale Erweiterungen zählen nur, wenn der Pflichtteil weiterhin verständlich und stabil bleibt.

## Qualitätsanforderungen

- Namen von Klassen, Methoden und Variablen sind verständlich.
- Klassen haben erkennbare Verantwortlichkeiten.
- Fachlogik ist nicht vollständig in `main`.
- Fehlerfälle werden bewusst behandelt.
- Die CSV-Verarbeitung bleibt einfach und nachvollziehbar.
- Der Code ist auf EFZ-Niveau lesbar.
- Keine unnötig komplexen Frameworks, Muster oder Abstraktionen.
- Du kannst erklären, warum du deine Struktur so gewählt hast.

## Testanforderungen

Schreibe mindestens 4 fachliche JUnit-Tests.

Geeignete Testideen:

- Verkauf reduziert den Bestand korrekt.
- Verkauf mit zu hoher Menge wird verhindert.
- Neues Produkt wird korrekt ergänzt.
- Ungültiger Preis oder Bestand wird abgelehnt.
- Doppelter Produktname wird kontrolliert behandelt.
- Laden oder Speichern erzeugt erwartete Produktdaten.

Die Tests sollen Fachlogik prüfen, nicht nur einfache Getter und Setter.

## Abgabe

Gib dein Maven-Projekt vollständig ab.

Die Abgabe soll enthalten:

- `pom.xml`
- Produktivcode unter `src/main/java`
- Testcode unter `src/test/java`
- Beispiel-CSV-Datei oder Testdaten
- kurze Reflexion als Markdown-Datei oder im vereinbarten Abgabeformat

Vor der Abgabe:

1. Führe `mvn test` aus.
2. Prüfe, ob die Anwendung mit deinen Beispieldaten sinnvoll gestartet werden kann.
3. Prüfe, ob keine temporären Build-Dateien unnötig abgegeben werden.

## Reflexion

Beantworte kurz:

1. Welche Klassen und Packages hast du gewählt, und warum?
2. Welche Verantwortung hat deine wichtigste Verwaltungsklasse?
3. Wo hast du Kapselung bewusst eingesetzt?
4. Welche Fachlogik hast du getestet?
5. Welche Randfälle waren beim Verkauf oder bei der CSV-Datei wichtig?
6. Wo wurde dein Code zuerst unübersichtlich?
7. Welche Entscheidung würdest du beim nächsten Projekt früher treffen?
8. Welche optionale Erweiterung wäre fachlich sinnvoll, auch wenn du sie nicht umgesetzt hast?
9. Wo hat dir ein Interface geholfen oder wo wäre es sinnvoll gewesen?
