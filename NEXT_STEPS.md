# Übergabe – aktueller Stand

## Aktueller Block

Die Unterrichtsreihe befindet sich aktuell im Einstieg zu:
- REST
- Spring Boot
- HTTP-basierter Zugriffsschicht
- Client/Server und JSON.

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
43. REST-Schnittstellen mit Spring Boot einführen
44. HTTP und REST-Grundlagen vertiefen

Die Einheit zu HTTP/REST verwendet:
- HTTP Request und HTTP Response
- Header und Body
- Statuscodes `200`, `201`, `400`, `404` und `500`
- JSON als Body-Format
- `curl -i`
- Ressourcenmodell mit `/produkte` und `/produkte/1`

Die vorherige Einheit zu REST verwendet:
- Spring Boot
- `@RestController`
- `@GetMapping`
- `@PostMapping`
- automatische JSON-Ausgabe
- `curl`
- `localhost:8080`

Die Einheit hält die bestehende Architektur bewusst stabil:
- REST Controller als neue Zugriffsschicht
- `LagerService` als bestehende Fachlogik
- Repositorys als bestehender Datenzugriff
- JDBC/H2 als bestehende Persistenz

Die vorherige Einheit zu I18N verwendet:
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
- REST Controller mit Spring Boot
- HTTP/JSON-Zugriff über `localhost:8080`
- vertiefte HTTP-Analyse mit Request, Response, Header, Body und Statuscodes

## Nächste geplante Einheiten

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

- JSON weiter vertiefen und DTOs erst kontrolliert in der nächsten Einheit einführen
- noch keine Security
- noch kein JPA/Hibernate
- noch keine komplexen DTO-Mappings
- Spring zunächst nur als Infrastruktur und Controller-Framework verwenden
