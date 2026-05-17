# Projektauftrag Änderungshistorie für Lagerverwaltung

[Zur Projektübersicht](../README.md) | [Hinweise für Lehrperson](../Lehrperson/Projektauftrag_Aenderungshistorie_Lagerverwaltung_LP.md)

## Ausgangslage

Du kennst bereits eine einfache Lagerverwaltung mit Produkten, Preisen, Lagerbeständen, Maven, Packages, JUnit-Tests, CSV-Persistenz, Verantwortlichkeiten, Services und Interfaces.

Bisher steht meist der aktuelle Zustand im Zentrum:

- Wie heisst das Produkt?
- Wie hoch ist der Preis?
- Wie viele Stück sind an Lager?

In echten Anwendungen ist zusätzlich wichtig, wie dieser Zustand entstanden ist. Wenn ein Bestand tiefer ist oder ein Preis geändert wurde, soll nachvollziehbar sein, was passiert ist.

Beispiel:

Nach einer Inventur fällt auf, dass der Bestand eines Produkts nicht mehr stimmt. Gleichzeitig wurde der Preis eines anderen Produkts für eine Aktion angepasst. Ohne Änderungshistorie sieht man nur den aktuellen Zustand. Mit Änderungshistorie ist nachvollziehbar, wann und warum sich Bestand oder Preis verändert haben.

Typische Fragen sind:

- Was wurde geändert?
- Wann wurde es geändert?
- Warum wurde es geändert?
- Was war der alte Wert?
- Was ist der neue Wert?

In diesem Projekt erweiterst du eine bekannte Lagerverwaltung um eine Änderungshistorie.

## Ziel des Projekts

Am Ende hat deine Lagerverwaltung eine nachvollziehbare Änderungshistorie.

Deine Anwendung soll:

- Bestandsänderungen protokollieren
- Preisänderungen protokollieren
- Änderungen mit Zeitpunkt erfassen
- alten und neuen Wert speichern
- Änderungsart und Grund festhalten
- die Änderungshistorie anzeigen
- die Änderungshistorie als CSV-Datei speichern
- die Änderungshistorie aus CSV-Datei laden
- zentrale Fachlogik mit JUnit-Tests prüfen

Wichtig ist nicht nur, dass die Historie ausgegeben wird. Deine Struktur soll zeigen, dass du Verantwortlichkeiten bewusst aufteilst und begründen kannst.

## Technischer Rahmen

- Java 21
- Maven
- sinnvolle Packages
- JUnit-Tests
- CSV-Persistenz
- keine externen Libraries ausser JUnit
- keine Datenbank
- kein Spring
- keine REST-API
- keine GUI

Die bestehende Lagerverwaltung dient als Ausgangspunkt. Du darfst vorhandene Klassen erweitern oder neue Klassen ergänzen, wenn du ihre Verantwortung begründen kannst.

Erwartete Maven-Struktur:

- `pom.xml` liegt im Projektordner
- Produktivcode liegt unter `src/main/java`
- Testcode liegt unter `src/test/java`
- CSV-Beispieldaten liegen sinnvoll abgelegt, zum Beispiel unter `data`
- `mvn test` funktioniert aus dem Projektordner

Mögliche Begriffe für deine Struktur:

- `AenderungsEintrag`
- `BestandsAenderung`
- `PreisAenderung`
- `AenderungsJournal`
- `JournalService`
- `LagerService`

Diese Begriffe sind Vorschläge, keine Zielarchitektur. Entscheide selbst, welche Klassen für deine Lösung sinnvoll sind.

Ein mögliches CSV-Format für die Historie:

```text
zeitpunkt;produkt;art;alterWert;neuerWert;grund
2026-05-17T10:15:30;Tastatur;BESTAND;12;9;Verkauf
2026-05-17T10:22:05;Maus;PREIS;24.50;19.90;Aktion
```

Du darfst ein anderes einfaches Format verwenden, wenn du es dokumentierst und sauber speichern kannst.

Für die Historie gilt:

- Als CSV speichern ist Pflicht.
- Aus CSV wieder laden ist Pflicht.

## Pflichtanforderungen

Deine Lösung muss diese fachlichen Anforderungen erfüllen:

1. Bestandsänderungen werden protokolliert.
2. Preisänderungen werden protokolliert.
3. Jede Änderung enthält einen Zeitpunkt.
4. Jede Änderung enthält den alten Wert und den neuen Wert.
5. Jede Änderung enthält eine Änderungsart, zum Beispiel `BESTAND` oder `PREIS`.
6. Jede Änderung enthält einen Grund, zum Beispiel `Verkauf`, `Aktion` oder `Inventur`.
7. Negative Preise und negative Bestände werden nicht als gültige Änderung protokolliert.
8. Die Änderungshistorie kann angezeigt werden.
9. Die Änderungshistorie kann als CSV-Datei gespeichert werden.
10. Die Änderungshistorie kann aus einer CSV-Datei geladen werden.
11. Die bestehende Lagerverwaltung bleibt weiterhin sinnvoll nutzbar.
12. Mindestens 3 fachliche JUnit-Tests prüfen die neue Logik.
13. Du begründest kurz, welche Klasse welche Verantwortung hat.

Deine Lösung muss diese strukturellen Anforderungen erfüllen:

1. `Main` bleibt hauptsächlich Ablaufsteuerung.
2. Fachlogik liegt nicht vollständig in `Main`.
3. CSV-Laden und CSV-Speichern der Historie sind von der Fachlogik getrennt.
4. Die Historie hat eine erkennbare eigene Verantwortung.
5. Klassen und Methoden haben verständliche Namen.
6. Die Struktur bleibt auf EFZ-Niveau nachvollziehbar.

Eine eigene Verantwortung für die Historie ist Pflicht. Ob du diese Verantwortung mit `AenderungsJournal`, `JournalService`, einer Erweiterung des bestehenden `LagerService` oder einer anderen einfachen Struktur löst, entscheidest du selbst.

Du musst keine bestimmte Zielarchitektur exakt nachbauen.

## Optionale Erweiterungen

Diese Erweiterungen sind freiwillig. Wähle höchstens so viele, dass der Pflichtteil sauber bleibt.

- Historie nach Produkt filtern
- Historie nach Änderungsart filtern
- zusätzliche Exportdatei erzeugen
- einfache Statistik über Änderungen anzeigen
- `JournalService` als eigene Verantwortung einführen
- Bestandskorrektur und Verkauf als unterschiedliche Gründe behandeln
- weitere ungültige Änderungen kontrolliert ablehnen, zum Beispiel leeren Grund oder fehlenden Produktnamen

Optionale Erweiterungen zählen nur, wenn der Pflichtteil weiterhin verständlich und stabil bleibt.

## Qualitätsanforderungen

- Die Historie ist fachlich nachvollziehbar.
- Die aktuelle Lagerverwaltung wird nicht unnötig kompliziert.
- Verantwortlichkeiten sind erkennbar getrennt.
- Fachlogik, CSV-Persistenz und Programmstart sind nicht vermischt.
- Der Code ist lesbar und auf EFZ-Niveau verständlich.
- Namen von Klassen, Methoden und Variablen sind klar.
- Fehlerfälle werden bewusst behandelt.
- Keine unnötig komplexen Frameworks, Muster oder Abstraktionen.
- Du kannst erklären, warum deine Struktur so gewählt wurde.

## Testanforderungen

Schreibe mindestens 3 fachliche JUnit-Tests.

Diese Mindesttests sollen enthalten sein:

- 1 Test für eine Bestandsänderung
- 1 Test für eine Preisänderung
- 1 Test für Pflichtdaten im Historieneintrag oder für eine ungültige Änderung

Zusätzlich muss das Laden der gespeicherten Historie manuell oder mit einem weiteren Test nachgewiesen werden.

Weitere geeignete Testideen:

- Eine Bestandsänderung erzeugt einen Historieneintrag mit altem und neuem Wert.
- Eine Preisänderung erzeugt einen Historieneintrag mit altem und neuem Wert.
- Eine ungültige Änderung wird verhindert oder kontrolliert behandelt.
- Die Historie enthält mehrere Einträge in der erwarteten Reihenfolge.
- Ein Historieneintrag enthält Änderungsart und Grund.

Die Tests sollen Fachlogik prüfen. Reine Getter- und Setter-Tests reichen nicht.

Wenn du CSV-Persistenz testest, halte den Test einfach und nachvollziehbar. Der wichtigste Teil ist die fachliche Protokollierung.

## Abgabe

Gib dein Maven-Projekt vollständig ab.

Die Abgabe soll enthalten:

- `pom.xml`
- Produktivcode unter `src/main/java`
- Testcode unter `src/test/java`
- Beispiel-CSV-Datei für Produkte
- erzeugte oder beispielhafte CSV-Datei für die Historie
- kurzer Nachweis, dass die Historie wieder aus CSV geladen werden kann
- kurze Verantwortlichkeitsbegründung, zum Beispiel als Tabelle `Klasse | Verantwortung | Begründung`
- kurze Reflexion als Markdown-Datei oder im vereinbarten Abgabeformat

Vor der Abgabe:

1. Führe `mvn test` aus.
2. Starte deine Anwendung oder Demo mit sinnvollen Beispieldaten.
3. Prüfe, ob die Historie angezeigt wird.
4. Prüfe, ob die Historie als CSV-Datei gespeichert wird.
5. Prüfe, ob die gespeicherte Historie wieder aus CSV geladen werden kann.
6. Prüfe, ob keine unnötigen Build-Dateien abgegeben werden.

## Reflexionsfragen

Beantworte kurz:

1. Welche Klassen hast du für die Änderungshistorie gewählt, und warum?
2. Welche Klasse erstellt einen Historieneintrag?
3. Welche Klasse speichert und lädt die Historie als CSV?
4. Warum gehört die Änderungshistorie nicht vollständig in `Main`?
5. Warum ist die Änderungshistorie nicht dasselbe wie die Produkt-CSV?
6. Welche Fachlogik hast du mit JUnit getestet?
7. Welche Verantwortung war schwierig zuzuordnen?
8. Wo wurde dein Code zuerst unübersichtlich?
9. Welche optionale Erweiterung wäre fachlich sinnvoll, auch wenn du sie nicht umgesetzt hast?
10. Was würdest du beim nächsten Projekt früher entscheiden?
