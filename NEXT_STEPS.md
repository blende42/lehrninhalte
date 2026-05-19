# Übergabe – Abschluss Repo efz-entwicklung-j2a

## Status dieses Repos

Dieses Repo bildet den Ausbildungsblock:

- Java-Grundlagen
- OOP
- Maven
- Tests
- Refactoring
- Persistenz
- JDBC/H2
- Repository
- Logging
- technische Konfiguration
- I18N
- REST-Einstieg

ab.

Didaktischer Schwerpunkt:
Architektur entsteht aus konkreten Problemen und wachsender technischer Komplexität.

Dieses Repo endet bewusst:
- nach dem REST-Einstieg
- nach HTTP-/JSON-Grundlagen
- nach reproduzierbaren API-Workflows mit Bruno

und vor:
- DTOs
- Validation
- komplexerer REST-Strukturierung
- JPA/Hibernate
- Spring Data
- Security

---

## Letzte abgeschlossene Einheiten

40. Technisches Logging in Java einführen
41. Technische Konfiguration in Java
42. Mehrsprachigkeit mit Locale und ResourceBundle
43. REST-Schnittstellen mit Spring Boot einführen
44. HTTP und REST-Grundlagen vertiefen
45. REST-Workflows mit Bruno

---

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
- HTTP-/JSON-Zugriff über `localhost:8080`
- Bruno-Collections mit gespeicherten API-Requests

---

## Didaktische Leitidee

Neue Konzepte entstehen aus konkreten Problemen:

- Interface nach austauschbarer Persistenz
- Service nach verteilter Fachlogik
- Repository nach wachsendem JDBC-/Mapping-Code
- Logging nach technischer Komplexität
- Konfiguration nach hartcodierter Infrastruktur
- I18N nach hartcodierten sichtbaren Texten
- REST als neue Zugriffsschicht auf bestehende Fachlogik
- Bruno nach `curl` als reproduzierbarer REST-Workflow

Architektur wird evolutionär entwickelt und nicht abstrakt vorgegeben.

---

## Fortsetzung im Folge-Repo

Die Weiterentwicklung erfolgt im Repo:

`efz-entwicklung-j2b`

Geplante nächste Themen:
- JSON-Strukturen und DTOs
- REST-Fehlerbehandlung
- Validation bei REST-Requests
- Services mit Spring sauber integrieren
- Vorbereitung auf JPA/Spring Data

---

## Wichtige Referenzen

- CONTENT.md
- docs/didaktik/entwicklungslogik.md
- efz-entwicklung-meta
