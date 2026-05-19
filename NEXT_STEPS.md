# Übergabe – aktueller Stand

## Aktueller Block

Die Unterrichtsreihe befindet sich aktuell am Übergang von:
- technischer Infrastruktur
- Persistenz
- Architekturgrundlagen

hin zu:
- REST
- Spring Boot
- HTTP-basierter Zugriffsschicht.

Die bisherige Architekturentwicklung wurde bewusst problemgetrieben aufgebaut:
- Services nach verteilter Fachlogik
- Repository nach wachsendem JDBC-/Mapping-Code
- Logging nach technischer Komplexität
- Konfiguration nach hartcodierter Infrastruktur
- I18N nach hartcodierten sichtbaren Texten

## Letzte abgeschlossene Einheiten

40. Technisches Logging in Java einführen
41. Technische Konfiguration in Java
42. Mehrsprachigkeit mit Locale und ResourceBundle

Die Einheit zu I18N verwendet:
- `Locale`
- `ResourceBundle`
- `messages_*.properties`

und trennt technische Konfiguration bewusst von sprachabhängigen Texten.

## Aktuelle Architektur

Die bekannte Lagerverwaltung umfasst inzwischen:
- Maven
- JUnit
- CSV-Persistenz
- JDBC/H2
- mehrere Tabellen
- Beziehungen
- Objekt-Datenbank-Mapping
- Repository-Klassen
- SLF4J + logback-classic
- `.properties`
- technische Konfiguration
- I18N mit `Locale` und `ResourceBundle`

## Nächste geplante Einheiten

43. REST-Einstieg mit Spring Boot
44. REST Controller und HTTP-Grundlagen
45. JSON und DTOs
46. Fehlerbehandlung bei REST
47. REST-Tests und API-Workflow

## Didaktische Leitidee

Architektur wird nicht abstrakt eingeführt.

Neue Konzepte entstehen aus konkreten Problemen:
- Interface nach austauschbarer Persistenz
- Service nach verteilter Fachlogik
- Repository nach wachsendem JDBC-/Mapping-Code
- Logging nach technischer Komplexität
- REST als neue Zugriffsschicht auf bestehende Fachlogik

## Wichtige Referenzen

- CONTENT.md
- docs/didaktik/entwicklungslogik.md

## Offene didaktische Entscheidungen

- REST-Einstieg bewusst klein halten
- noch keine Security
- noch kein JPA/Hibernate
- noch keine komplexen DTO-Mappings
- Spring zunächst nur als Infrastruktur verwenden