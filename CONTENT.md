# Lerninhalte

Diese Übersicht listet die vorhandenen Lerninhalte des Repositories nach Materialtyp und Thema. Sie dient als Orientierung für Unterrichtsplanung, Wiederholung und Weiterentwicklung der Unterlagen.

## Arbeitsblätter

Arbeitsblätter führen neue Konzepte ein, enthalten kurze Theorie, Beispiele, typische Stolpersteine und Reflexionsfragen.

### Primitive Datentypen, Wrapper und Parsing

- [Tag 1 – Primitive Datentypen & Wrapper](./Arbeitsblaetter/arbeitsblatt_java_wrapper.md)
  - Primitive Datentypen vs. Wrapper-Klassen
  - Autoboxing und Autounboxing
  - `null` bei Wrapper-Objekten
  - `String` zu Zahl mit Parsing
  - Vergleich mit `==` und `equals()`
  - Sichere Eingabe und Fehlerbehandlung
- [Tag 1 – Primitive Datentypen & Wrapper, String und Visualisierungen](./Arbeitsblaetter/arbeitsblatt_theorie_kombiniert.md)
  - Kombinierte Theorie zu Wrapper-Klassen und `String`
  - Autoboxing, Autounboxing und Parsing
  - String-Grundlagen, Immutability, Methoden und Vergleich
  - Einbindung von Konzeptgrafiken

### Strings

- [Tag 2 – String-Klasse](./Arbeitsblaetter/string_arbeitsblatt.md)
  - String-Grundlagen
  - String-Vergleich
  - Immutability
  - Wichtige Methoden
- [Tag 3 – String-Klasse, Vertiefung](./Arbeitsblaetter/string_arbeitsblatt_v2.md)
  - Kombination von String-Methoden
  - Teilstrings, Prüfung und Ersetzung
  - Vergleich als Wiederholung

### Strings und StringBuilder

- [Arbeitsblatt – Strings & StringBuilder](./Arbeitsblaetter/arbeitsblatt_stringbuilder.md)
  - Problem häufiger String-Verkettung
  - `StringBuilder` als veränderbare Alternative
  - Methoden wie `append()`, `insert()`, `delete()`, `replace()` und `reverse()`
- [Tag 5 – StringBuilder](./Arbeitsblaetter/tag5_stringbuilder_arbeitsblatt.md)
  - Konzeptgrafiken zu String-Verkettung und Immutability
  - Vergleich `String` und `StringBuilder`
  - Kurze Theorie und Übung
- [Tag 5 – StringBuilder mit eingebetteten Grafiken](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_stringbuilder_arbeitsblatt.md)
  - Variante im Grafik-Unterverzeichnis mit denselben Tag-5-Inhalten

### Arrays

- [Arbeitsblatt – Arrays](./Arbeitsblaetter/Arbeitsblatt_Arrays.md)
  - Zweck von Arrays
  - Index und Zugriff auf Elemente
  - Arrays mit Schleifen
  - Typische Fehler
- [Arbeitsblatt – Arrays, Vertiefung](./Arbeitsblaetter/Arbeitsblatt_Arrays_Vertiefung.md)
  - Muster beim Durchlaufen von Arrays
  - Maximum, Suche, Zählen und Kombinationen
  - Transferaufgaben und Reflexion
- [Arbeitsblatt – Arrays 2D, Vertiefung](./Arbeitsblaetter/Arbeitsblatt_2D_Arrays_Vertiefung.md)
  - 2D-Arrays als Tabelle
  - Zeilenweise Auswertung
  - Summe, Durchschnitt und Maximum
  - Edge Cases wie unterschiedliche Zeilenlängen und leere Zeilen

## Konzeptgrafiken

Konzeptgrafiken visualisieren Beziehungen, Abläufe und typische Denkmodelle. Sie ergänzen Arbeitsblätter und Theorieblätter.

### Allgemeine Unterrichtsgrafiken

- [Arrays – Konzept](./graphics/grafik_arrays_konzept.svg)
  - Array als zusammengehörige Reihe von Werten
  - Indexbasierter Zugriff
- [Arrays – Konzept mit Beispiel](./graphics/grafik_arrays_konzept_beispiel.svg)
  - Konkretes Beispiel für Werte, Indizes und Zugriff
- [Primitive Werte vs. Wrapper-Objekte](./graphics/java_wert_vs_objekt_wrapper.svg)
  - Unterschied zwischen Wert und Objekt
  - Grundlage für Wrapper-Klassen und `null`
- [Parser-Grafik](./graphics/parser_grafik.svg)
  - Verarbeitung eines Textes in einzelne Bestandteile
  - Bezug zu String- und Parser-Aufgaben

### Arbeitsblattgrafiken zu StringBuilder

- [String-Immutability](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_konzept_immutability_string.svg)
  - `String` als unveränderbarer Wert
  - Neue Objekte bei Veränderung
- [String-Verkettung mit Plus](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_prozess_string_verketten_plus.svg)
  - Ablauf und Kosten wiederholter Verkettung
- [String vs. StringBuilder](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_vergleich_string_vs_stringbuilder.svg)
  - Vergleich von unveränderbaren Strings und veränderbarem Builder

## Übungen

Übungen dienen der Anwendung und Vertiefung. Sie sind teilweise nach Basis, Aufbau, Vertiefung und Transfer gestaffelt.

### Primitive Datentypen, Wrapper und Parsing

- [Übungen – Primitive Datentypen & Wrapper](./Uebungen/uebungen_java_wrapper.md)
  - Fehler durch `null`
  - Primitive vs. Wrapper
  - `String` zu Zahl
  - `==` oder `equals()`
  - Sichere Eingabe und Schleifen
- [Theorie – Wrapper-Klassen](./Uebungen/theorie_wrapper.md)
  - Grundidee von Wrapper-Klassen
  - Autoboxing und Unboxing
  - Methoden erkunden
  - Merksätze und Arbeitsauftrag

### Strings

- [Theorie – String](./Uebungen/theorie_string.md)
  - Grundidee von `String`
  - Immutability
  - Methoden, Vergleich und Eingabe
- [Übungen – String-Klasse](./Uebungen/string_uebungen.md)
  - Vergleich und `equals()`
  - Gross- und Kleinschreibung
  - Immutability
  - Umlaute und Eingaben
- [Übungen – String-Klasse, Vertiefung](./Uebungen/string_uebungen_v2.md)
  - Methoden kombinieren
  - Teilstrings
  - Text prüfen und ersetzen
  - Eingabe validieren
  - Mini-Projekt
- [Tag 4 – String-Klasse, Mini-Projekt Parser](./Uebungen/string_mini_projekt_v3.md)
  - Einfacher Wort-Parser
  - Wortgrenzen und Delimiter
  - Bereinigte Ausgabe
  - Wortklassifikation und Statistik
- [Tag 4 – String-Klasse, Mini-Projekt Parser erweitert](./Uebungen/string_mini_projekt_v3_updated.md)
  - Erweiterte Parser-Anforderungen
  - Delimiter definieren
  - Verarbeitung, Klassifikation und Statistik

### StringBuilder und Parser

- [Übungen – StringBuilder & Parser](./Uebungen/uebungen_stringbuilder.md)
  - `append()`, `insert()`, `delete()`, `replace()` und `reverse()`
  - Kombination mehrerer Operationen
  - Vereinfachte Parser-Hauptaufgabe

### Arrays

- [Übungen – Arrays](./Uebungen/Uebungen_Arrays.md)
  - Basis: Arrays anlegen und ausgeben
  - Aufbau: Summe, Maximum und Zählen
  - Vertiefung: Suche und Index
  - Transfer: Temperaturen und Noten
- [Übungen – Arrays, Vertiefung](./Uebungen/Uebungen_Arrays_Vertiefung.md)
  - Muster erkennen
  - Variation von Such- und Auswertungsaufgaben
  - Kombination mit Messwerten
  - Edge Cases und Reflexion
- [Übungen – 2D Arrays, Vertiefung](./Uebungen/Uebungen_2D_Arrays.md)
  - Ausgabe von 2D-Arrays
  - Summe und Durchschnitt pro Zeile
  - Gesamtmaximum und Gesamtdurchschnitt
  - Beste Messreihe
  - Edge Cases mit unterschiedlichen Längen und leeren Zeilen

## Musterlösungen

Musterlösungen halten kompakte Referenzlösungen und Bewertungshilfen bereit.

- [Lösungen – Arrays](./Musterloesungen/Loesungen_Arrays.md)
  - Einstiegslösung zu Arrays
- [Lösungen – Arrays im Stil](./Musterloesungen/Loesungen_Arrays_im_Stil.md)
  - Summe, Maximum, Zählen, Suche, Index, Temperaturen und Noten
- [Lösungen – 2D Arrays](./Musterloesungen/Loesungen_2D_Arrays.md)
  - Ausgabe, Zeilensummen, Durchschnitt, Maximum und Edge Cases
- [Musterlösungen – StringBuilder & Parser](./Musterloesungen/musterloesungen_stringbuilder.md)
  - StringBuilder-Methoden und vereinfachter Parser
- [Musterlösungen – Mini-Projekt String Parser](./Musterloesungen/string_parser_loesungen.md)
  - Naive, strukturierte und erweiterte Lösung
  - Bewertungsskala und Lehrerhinweise

## Ergänzende Vorlagen und Workflows

Diese Dateien sind keine direkten Lerninhalte für Java, unterstützen aber die Erstellung konsistenter Unterrichtsgrafiken.

- [SVG-Workflow-Sheet](./templates/svg_workflow_sheet.md)
- [SVG-Workflow-Sheet für Lernende](./templates/lernende/svg_workflow_sheet_lernende.md)
- [Arbeitsblatt SVG-Grafiken](./templates/lernende/arbeitsblatt_svg_grafiken.md)
- [SVG-Templates](./templates/)
- [Prompts für Grafiktypen](./templates/prompts/)
