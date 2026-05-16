# lehrninhalte

Dieses Repository dient zur Erstellung und Pflege von Lehrinhalten für die Ausbildung zum Applikationsentwickler mit eidgenössischem Fähigkeitsausweis.

Die verbindliche Policy für Codex mit `MUSS`, `SOLL`, `DARF NICHT`, Qualitätsgates, Entscheidungsregeln, Prioritäten bei Zielkonflikten und Arbeitsablauf ist in [AGENTS.md](./AGENTS.md) festgehalten.

## Inhaltsverzeichnis

- [AGENTS.md](./AGENTS.md)
- [CONTENT.md](./CONTENT.md) – empfohlene Unterrichtsreihenfolge und strukturierte Übersicht über Arbeitsblätter, Konzeptgrafiken, Übungen, Repetitionen, Projekte und Musterlösungen
- [NEXT_STEPS.md](./NEXT_STEPS.md) – Übergabe zum aktuellen Stand und nächstem geplanten Unterrichtsblock

### docs
Begriffs- und Prozessbibliothek für KI-gestützte Lehrmittel-Erstellung:

#### docs/begriffe

- [orchestrierung.md](./docs/begriffe/orchestrierung.md)
- [convention_over_configuration.md](./docs/begriffe/convention_over_configuration.md)
- [build_artifact.md](./docs/begriffe/build_artifact.md)
- [classpath.md](./docs/begriffe/classpath.md)
- [package_vs_directory.md](./docs/begriffe/package_vs_directory.md)

#### docs/prozesse

- [arbeitsblatt_erstellen.md](./docs/prozesse/arbeitsblatt_erstellen.md)
- [uebungen_erstellen.md](./docs/prozesse/uebungen_erstellen.md)
- [repetition_und_vertiefung_erstellen.md](./docs/prozesse/repetition_und_vertiefung_erstellen.md)
- [projekt_erstellen.md](./docs/prozesse/projekt_erstellen.md)
- [projekt_review.md](./docs/prozesse/projekt_review.md)
- [musterloesungen_erstellen.md](./docs/prozesse/musterloesungen_erstellen.md)
- [review_didaktik.md](./docs/prozesse/review_didaktik.md)
- [review_java_maven.md](./docs/prozesse/review_java_maven.md)

### .agents/skills
Repo-Skills für wiederkehrende und kontrollierte Arbeitsabläufe:

- [arbeitsblatt-erstellen](./.agents/skills/arbeitsblatt-erstellen/SKILL.md)
- [uebungen-erstellen](./.agents/skills/uebungen-erstellen/SKILL.md)
- [repetition-vertiefung-erstellen](./.agents/skills/repetition-vertiefung-erstellen/SKILL.md)
- [projekt-erstellen](./.agents/skills/projekt-erstellen/SKILL.md)
- [projekt-review](./.agents/skills/projekt-review/SKILL.md)
- [musterloesungen-erstellen](./.agents/skills/musterloesungen-erstellen/SKILL.md)
- [svg-pruefen](./.agents/skills/svg-pruefen/SKILL.md)
- [java-maven-validieren](./.agents/skills/java-maven-validieren/SKILL.md)
- [git-repo-updaten](./.agents/skills/git-repo-updaten/SKILL.md)

### .codex/skills
Veraltete Skill-Ablage. Die aktuellen Repo-Skills liegen unter `.agents/skills`.

### Repetitionen
Wiederverwendbare Repetitions- und Vertiefungsserien mit getrennten Versionen für Lernende und Lehrpersonen:

Standardstruktur:

```text
Repetitionen/<Name_der_Repetition>/Lernende/<Name_der_Repetition>.md
Repetitionen/<Name_der_Repetition>/Lehrperson/<Name_der_Repetition>_LP.md
```

Repetitionen werden nicht zusätzlich unter `Uebungen` geführt.

- [Repetition_Java_Intro.md](./Repetitionen/Repetition_Java_Intro/Lernende/Repetition_Java_Intro.md)
- [Repetition_Java_Intro_LP.md](./Repetitionen/Repetition_Java_Intro/Lehrperson/Repetition_Java_Intro_LP.md)

### Projekte
Grössere, zusammenhängende Mini-Projekte mit getrennten Versionen für Lernende und Lehrpersonen:

Standardstruktur:

```text
Projekte/<Projektname>/README.md
Projekte/<Projektname>/Lernende/Projektauftrag_<Projektname>.md
Projekte/<Projektname>/Lehrperson/Projektauftrag_<Projektname>_LP.md
```

Projekte kombinieren mehrere bisherige Konzepte, verlangen mehr Eigenständigkeit als normale Übungen und werden nicht zusätzlich unter `Uebungen` geführt.

- [Projekte README](./Projekte/README.md)
- [Lagerverwaltung Light](./Projekte/Lagerverwaltung_Light/README.md)
- [Projektauftrag_Lagerverwaltung_Light.md](./Projekte/Lagerverwaltung_Light/Lernende/Projektauftrag_Lagerverwaltung_Light.md)
- [Projektauftrag_Lagerverwaltung_Light_LP.md](./Projekte/Lagerverwaltung_Light/Lehrperson/Projektauftrag_Lagerverwaltung_Light_LP.md)

`Lagerverwaltung Light` ist als ausgearbeiteter Projektauftrag vorhanden. Die Lernenden-Version enthält Anforderungen, technische Leitplanken, reale Lagerfälle, Tests, Abgabe und Reflexion. Die Lehrpersonen-Version ergänzt Beobachtungspunkte, Hilfestellungen, Bewertungsideen und mögliche Lösungsrichtungen ohne vollständige Musterlösung.

### Arbeitsblaetter
Lehr- und Arbeitsblätter zu Java- und Grundlagenthemen:

- [Arbeitsblatt_Arrays.md](./Arbeitsblaetter/Arbeitsblatt_Arrays.md)
- [Arbeitsblatt_Arrays_Vertiefung.md](./Arbeitsblaetter/Arbeitsblatt_Arrays_Vertiefung.md)
- [Arbeitsblatt_2D_Arrays_Vertiefung.md](./Arbeitsblaetter/Arbeitsblatt_2D_Arrays_Vertiefung.md)
- [Arbeitsblatt_Methoden.md](./Arbeitsblaetter/Arbeitsblatt_Methoden.md)
- [Arbeitsblatt_Methoden_Festigung.md](./Arbeitsblaetter/Arbeitsblatt_Methoden_Festigung.md)
- [Arbeitsblatt_Klassen_und_Objekte.md](./Arbeitsblaetter/Arbeitsblatt_Klassen_und_Objekte.md)
- [Arbeitsblatt_Kapselung_Getter_Setter.md](./Arbeitsblaetter/Arbeitsblatt_Kapselung_Getter_Setter.md)
- [Arbeitsblatt_Objektarrays_Verwaltungslogik.md](./Arbeitsblaetter/Arbeitsblatt_Objektarrays_Verwaltungslogik.md)
- [Arbeitsblatt_ArrayList.md](./Arbeitsblaetter/Arbeitsblatt_ArrayList.md)
- [Arbeitsblatt_Packages.md](./Arbeitsblaetter/Arbeitsblatt_Packages.md)
- [Arbeitsblatt_Algorithmen_Datenstrukturen.md](./Arbeitsblaetter/Arbeitsblatt_Algorithmen_Datenstrukturen.md)
- [Arbeitsblatt_Sortieralgorithmen.md](./Arbeitsblaetter/Arbeitsblatt_Sortieralgorithmen.md)
- [Arbeitsblatt_Maven_Einstieg.md](./Arbeitsblaetter/Arbeitsblatt_Maven_Einstieg.md)
- [Arbeitsblatt_Maven_Ausfuehren_und_Paketieren.md](./Arbeitsblaetter/Arbeitsblatt_Maven_Ausfuehren_und_Paketieren.md)
- [Arbeitsblatt_Maven_Einfache_Tests_Vorbereiten.md](./Arbeitsblaetter/Arbeitsblatt_Maven_Einfache_Tests_Vorbereiten.md)
- [Arbeitsblatt_JUnit_Einstieg.md](./Arbeitsblaetter/Arbeitsblatt_JUnit_Einstieg.md)
- [Arbeitsblatt_JUnit_Fehleranalyse.md](./Arbeitsblaetter/Arbeitsblatt_JUnit_Fehleranalyse.md)
- [Arbeitsblatt_Refactoring_mit_Tests.md](./Arbeitsblaetter/Arbeitsblatt_Refactoring_mit_Tests.md)
- [Arbeitsblatt_CSV_Laden.md](./Arbeitsblaetter/Arbeitsblatt_CSV_Laden.md)
- [Arbeitsblatt_CSV_Speichern.md](./Arbeitsblaetter/Arbeitsblatt_CSV_Speichern.md)
- [Arbeitsblatt_Persistenzablauf_Vertiefen.md](./Arbeitsblaetter/Arbeitsblatt_Persistenzablauf_Vertiefen.md)
- [Arbeitsblatt_Verantwortlichkeiten_Aufteilen.md](./Arbeitsblaetter/Arbeitsblatt_Verantwortlichkeiten_Aufteilen.md)
- [Arbeitsblatt_Interfaces_Austauschbare_Services.md](./Arbeitsblaetter/Arbeitsblatt_Interfaces_Austauschbare_Services.md)
- [Arbeitsblatt_Mehrere_Implementierungen_Interface.md](./Arbeitsblaetter/Arbeitsblatt_Mehrere_Implementierungen_Interface.md)
- [Arbeitsblatt_Polymorphie_Interface.md](./Arbeitsblaetter/Arbeitsblatt_Polymorphie_Interface.md)
- [Arbeitsblatt_Code_Wiederverwenden.md](./Arbeitsblaetter/Arbeitsblatt_Code_Wiederverwenden.md)
- [arbeitsblatt_java_wrapper.md](./Arbeitsblaetter/arbeitsblatt_java_wrapper.md)
- [arbeitsblatt_stringbuilder.md](./Arbeitsblaetter/arbeitsblatt_stringbuilder.md)
- [arbeitsblatt_theorie_kombiniert.md](./Arbeitsblaetter/arbeitsblatt_theorie_kombiniert.md)
- [string_arbeitsblatt.md](./Arbeitsblaetter/string_arbeitsblatt.md)
- [string_arbeitsblatt_v2.md](./Arbeitsblaetter/string_arbeitsblatt_v2.md)
- [tag5_stringbuilder_arbeitsblatt.md](./Arbeitsblaetter/tag5_stringbuilder_arbeitsblatt.md)

### Arbeitsblaetter/arbeitsblatt_grafiken
SVG-Grafiken und zugehörige Datei für eingebettete Arbeitsblattgrafiken:

- [tag5_konzept_immutability_string.svg](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_konzept_immutability_string.svg)
- [tag5_prozess_string_verketten_plus.svg](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_prozess_string_verketten_plus.svg)
- [tag5_vergleich_string_vs_stringbuilder.svg](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_vergleich_string_vs_stringbuilder.svg)
- [tag5_stringbuilder_arbeitsblatt.md](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_stringbuilder_arbeitsblatt.md)

### Uebungen
Übungsblätter, Vertiefungen, Simulationen und Package-Strukturierungsaufgaben:

- [Uebungen_Arrays.md](./Uebungen/Uebungen_Arrays.md)
- [Uebungen_Arrays_Vertiefung.md](./Uebungen/Uebungen_Arrays_Vertiefung.md)
- [Uebungen_2D_Arrays.md](./Uebungen/Uebungen_2D_Arrays.md)
- [Uebungen_Methoden.md](./Uebungen/Uebungen_Methoden.md)
- [Uebungen_Methoden_Festigung.md](./Uebungen/Uebungen_Methoden_Festigung.md)
- [Uebungen_Klassen_und_Objekte.md](./Uebungen/Uebungen_Klassen_und_Objekte.md)
- [Uebungen_Kapselung_Getter_Setter.md](./Uebungen/Uebungen_Kapselung_Getter_Setter.md)
- [Uebungen_Objektarrays_Verwaltungslogik.md](./Uebungen/Uebungen_Objektarrays_Verwaltungslogik.md)
- [Uebungen_ArrayList.md](./Uebungen/Uebungen_ArrayList.md)
- [Uebungen_Packages.md](./Uebungen/Uebungen_Packages.md)
- [Uebungen_Algorithmen_Datenstrukturen.md](./Uebungen/Uebungen_Algorithmen_Datenstrukturen.md)
- [Uebungen_Maven_Einstieg.md](./Uebungen/Uebungen_Maven_Einstieg.md)
- [Uebungen_Maven_Ausfuehren_und_Paketieren.md](./Uebungen/Uebungen_Maven_Ausfuehren_und_Paketieren.md)
- [Uebungen_Maven_Einfache_Tests_Vorbereiten.md](./Uebungen/Uebungen_Maven_Einfache_Tests_Vorbereiten.md)
- [Uebungen_JUnit_Einstieg.md](./Uebungen/Uebungen_JUnit_Einstieg.md)
- [Uebungen_JUnit_Fehleranalyse.md](./Uebungen/Uebungen_JUnit_Fehleranalyse.md)
- [Uebungen_Refactoring_mit_Tests.md](./Uebungen/Uebungen_Refactoring_mit_Tests.md)
- [Uebungen_CSV_Laden.md](./Uebungen/Uebungen_CSV_Laden.md)
- [Uebungen_CSV_Speichern.md](./Uebungen/Uebungen_CSV_Speichern.md)
- [Uebungen_Persistenzablauf_Vertiefen.md](./Uebungen/Uebungen_Persistenzablauf_Vertiefen.md)
- [Uebungen_Verantwortlichkeiten_Aufteilen.md](./Uebungen/Uebungen_Verantwortlichkeiten_Aufteilen.md)
- [Uebungen_Interfaces_Austauschbare_Services.md](./Uebungen/Uebungen_Interfaces_Austauschbare_Services.md)
- [Uebungen_Mehrere_Implementierungen_Interface.md](./Uebungen/Uebungen_Mehrere_Implementierungen_Interface.md)
- [Uebungen_Polymorphie_Interface.md](./Uebungen/Uebungen_Polymorphie_Interface.md)
- [Uebungen_Code_Wiederverwenden.md](./Uebungen/Uebungen_Code_Wiederverwenden.md)
- [string_uebungen.md](./Uebungen/string_uebungen.md)
- [string_uebungen_v2.md](./Uebungen/string_uebungen_v2.md)
- [string_mini_projekt_v3.md](./Uebungen/string_mini_projekt_v3.md)
- [string_mini_projekt_v3_updated.md](./Uebungen/string_mini_projekt_v3_updated.md)
- [theorie_string.md](./Uebungen/theorie_string.md)
- [theorie_wrapper.md](./Uebungen/theorie_wrapper.md)
- [uebungen_java_wrapper.md](./Uebungen/uebungen_java_wrapper.md)
- [uebungen_stringbuilder.md](./Uebungen/uebungen_stringbuilder.md)

Hinweis: Die vorhandenen `string_mini_projekt_*`-Dateien sind Altbestand. Neue Mini-Projekte werden unter `Projekte` geführt.

### Musterloesungen
Kompakte Referenzlösungen zu den Übungen, Simulationen, Package-Strukturierungen und Arbeitsblättern:

- [Loesungen_Arrays.md](./Musterloesungen/Loesungen_Arrays.md)
- [Loesungen_Arrays_im_Stil.md](./Musterloesungen/Loesungen_Arrays_im_Stil.md)
- [Loesungen_2D_Arrays.md](./Musterloesungen/Loesungen_2D_Arrays.md)
- [Loesungen_Methoden.md](./Musterloesungen/Loesungen_Methoden.md)
- [Loesungen_Methoden_Festigung.md](./Musterloesungen/Loesungen_Methoden_Festigung.md)
- [Loesungen_Klassen_und_Objekte.md](./Musterloesungen/Loesungen_Klassen_und_Objekte.md)
- [Loesungen_Kapselung_Getter_Setter.md](./Musterloesungen/Loesungen_Kapselung_Getter_Setter.md)
- [Loesungen_Objektarrays_Verwaltungslogik.md](./Musterloesungen/Loesungen_Objektarrays_Verwaltungslogik.md)
- [Loesungen_ArrayList.md](./Musterloesungen/Loesungen_ArrayList.md)
- [Loesungen_Packages.md](./Musterloesungen/Loesungen_Packages.md)
- [Loesungen_Algorithmen_Datenstrukturen.md](./Musterloesungen/Loesungen_Algorithmen_Datenstrukturen.md)
- [Loesungen_Maven_Einstieg.md](./Musterloesungen/Loesungen_Maven_Einstieg.md)
- [Loesungen_Maven_Ausfuehren_und_Paketieren.md](./Musterloesungen/Loesungen_Maven_Ausfuehren_und_Paketieren.md)
- [Loesungen_Maven_Einfache_Tests_Vorbereiten.md](./Musterloesungen/Loesungen_Maven_Einfache_Tests_Vorbereiten.md)
- [Loesungen_JUnit_Einstieg.md](./Musterloesungen/Loesungen_JUnit_Einstieg.md)
- [Loesungen_JUnit_Fehleranalyse.md](./Musterloesungen/Loesungen_JUnit_Fehleranalyse.md)
- [Loesungen_Refactoring_mit_Tests.md](./Musterloesungen/Loesungen_Refactoring_mit_Tests.md)
- [Loesungen_CSV_Laden.md](./Musterloesungen/Loesungen_CSV_Laden.md)
- [Loesungen_CSV_Speichern.md](./Musterloesungen/Loesungen_CSV_Speichern.md)
- [Loesungen_Persistenzablauf_Vertiefen.md](./Musterloesungen/Loesungen_Persistenzablauf_Vertiefen.md)
- [Loesungen_Verantwortlichkeiten_Aufteilen.md](./Musterloesungen/Loesungen_Verantwortlichkeiten_Aufteilen.md)
- [Loesungen_Interfaces_Austauschbare_Services.md](./Musterloesungen/Loesungen_Interfaces_Austauschbare_Services.md)
- [Loesungen_Mehrere_Implementierungen_Interface.md](./Musterloesungen/Loesungen_Mehrere_Implementierungen_Interface.md)
- [Loesungen_Polymorphie_Interface.md](./Musterloesungen/Loesungen_Polymorphie_Interface.md)
- [Loesungen_Code_Wiederverwenden.md](./Musterloesungen/Loesungen_Code_Wiederverwenden.md)
- [musterloesungen_stringbuilder.md](./Musterloesungen/musterloesungen_stringbuilder.md)
- [string_parser_loesungen.md](./Musterloesungen/string_parser_loesungen.md)

### graphics
Allgemeine SVG-Grafiken für den Unterricht:

- [grafik_arrays_konzept.svg](./graphics/grafik_arrays_konzept.svg)
- [grafik_arrays_konzept_beispiel.svg](./graphics/grafik_arrays_konzept_beispiel.svg)
- [java_klasse_objekt_konzept.svg](./graphics/java_klasse_objekt_konzept.svg)
- [java_kapselung_private.svg](./graphics/java_kapselung_private.svg)
- [java_getter_setter_validierung.svg](./graphics/java_getter_setter_validierung.svg)
- [java_objekt_referenz.svg](./graphics/java_objekt_referenz.svg)
- [java_wert_vs_objekt_wrapper.svg](./graphics/java_wert_vs_objekt_wrapper.svg)
- [maven_orchestriert_build.svg](./graphics/maven_orchestriert_build.svg)
- [maven_compile_run_package.svg](./graphics/maven_compile_run_package.svg)
- [maven_tests_vorbereiten.svg](./graphics/maven_tests_vorbereiten.svg)
- [junit_manuell_zu_automatisiert.svg](./graphics/junit_manuell_zu_automatisiert.svg)
- [junit_test_fehlschlag_workflow.svg](./graphics/junit_test_fehlschlag_workflow.svg)
- [refactoring_mit_tests_workflow.svg](./graphics/refactoring_mit_tests_workflow.svg)
- [csv_laden_produktverwaltung.svg](./graphics/csv_laden_produktverwaltung.svg)
- [csv_speichern_produktverwaltung.svg](./graphics/csv_speichern_produktverwaltung.svg)
- [persistenzablauf_laden_bearbeiten_speichern.svg](./graphics/persistenzablauf_laden_bearbeiten_speichern.svg)
- [verantwortlichkeiten_aufteilen.svg](./graphics/verantwortlichkeiten_aufteilen.svg)
- [interface_produkt_speicher.svg](./graphics/interface_produkt_speicher.svg)
- [mehrere_implementierungen_interface.svg](./graphics/mehrere_implementierungen_interface.svg)
- [polymorphie_interface.svg](./graphics/polymorphie_interface.svg)
- [code_wiederverwenden.svg](./graphics/code_wiederverwenden.svg)
- [parser_grafik.svg](./graphics/parser_grafik.svg)

### templates
Vorlagen, Workflows und Prompts für Lehrmittel, SVG-Grafiken und Reviews:

- [template_architektur.svg](./templates/template_architektur.svg)
- [template_architektur_robust.svg](./templates/template_architektur_robust.svg)
- [template_konzept_robust.svg](./templates/template_konzept_robust.svg)
- [template_prozess_robust.svg](./templates/template_prozess_robust.svg)
- [template_vergleich_robust.svg](./templates/template_vergleich_robust.svg)
- [svg_workflow_sheet.md](./templates/svg_workflow_sheet.md)
- [projekt_review_template.md](./templates/projekt_review_template.md)

#### templates/prompts

- [Architekturgrafik_prompt.txt](./templates/prompts/Architekturgrafik_prompt.txt)
- [Konzeptgrafik_prompt.txt](./templates/prompts/Konzeptgrafik_prompt.txt)
- [Prozessgrafik_pompt.txt](./templates/prompts/Prozessgrafik_pompt.txt)
- [Vergleichsgrafik_prompt.txt](./templates/prompts/Vergleichsgrafik_prompt.txt)
- [SVG_Kompakt_Prompt_de-CH.md](./templates/prompts/SVG_Kompakt_Prompt_de-CH.md)
- [svg_playbook.md](./templates/prompts/svg_playbook.md)

#### templates/lernende

- [arbeitsblatt_svg_grafiken.md](./templates/lernende/arbeitsblatt_svg_grafiken.md)
- [svg_workflow_sheet_lernende.md](./templates/lernende/svg_workflow_sheet_lernende.md)

## Pflegehinweis

`README.md` beschreibt den aktuellen Stand des Repository-Inhalts. Bei künftigen Änderungen an Struktur oder Inhalt ist diese Datei immer mitzuaktualisieren.
