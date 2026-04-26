# Übungen – Kapselung, Getter und Setter

## Basis

### Aufgabe 1 – Problem erkennen

Gegeben ist folgende Klasse:

```java
class Produkt {
    String name;
    double preis;
}
```

Beantworte:

- Welcher ungültige Wert könnte bei `preis` gespeichert werden?
- Warum ist direkter Zugriff auf `preis` problematisch?
- Wie kann `private` helfen?

---

### Aufgabe 2 – Attribute schützen

Passe die Klasse `Produkt` an.

Vorgaben:

- `name` ist `private`
- `preis` ist `private`
- Der Konstruktor setzt beide Werte

---

### Aufgabe 3 – Getter schreiben

Ergänze Getter für beide Attribute.

Vorgaben:

- `getName()`
- `getPreis()`

Teste in `main`, dass beide Werte gelesen werden können.

---

## Aufbau

### Aufgabe 4 – Setter mit Prüfung

Schreibe einen Setter `setPreis`.

Vorgaben:

- Parameter: `double preis`
- Der Preis darf nur geändert werden, wenn er `>= 0` ist.
- Teste einen gültigen und einen ungültigen Wert.

---

### Aufgabe 5 – Konstruktor absichern

Passe den Konstruktor so an, dass auch beim Erstellen kein negativer Preis gespeichert wird.

Vorgabe:

- Verwende im Konstruktor `setPreis(preis)`.

---

### Aufgabe 6 – Kein Setter für Name

Entscheide bewusst:

- `name` soll nach dem Erstellen nicht geändert werden.
- Entferne oder vermeide deshalb `setName`.

Beantworte kurz:

- Warum ist hier kein Setter sinnvoll?

---

## Vertiefung

### Aufgabe 7 – Bankkonto

Schreibe eine Klasse `Bankkonto`.

Attribute:

- `private String inhaber`
- `private double saldo`

Vorgaben:

- Konstruktor mit Inhaber und Startsaldo
- Getter für beide Attribute
- Methode `einzahlen(double betrag)`
- Methode `abheben(double betrag)`

Regeln:

- Einzahlen ist nur erlaubt, wenn der Betrag positiv ist.
- Abheben ist nur erlaubt, wenn der Betrag positiv ist und genug Saldo vorhanden ist.

---

### Aufgabe 8 – Rückgabewert für Erfolg

Passe `abheben` so an, dass die Methode `boolean` zurückgibt.

Vorgaben:

- `true`, wenn das Abheben erfolgreich war
- `false`, wenn das Abheben abgelehnt wurde

---

## Transfer

### Aufgabe 9 – Produktarray mit gekapselten Attributen

Erstelle ein Array mit drei Produkten.

Schreibe eine Methode `findeTeuerstesProdukt`.

Wichtig:

- Greife nicht direkt auf `preis` zu.
- Verwende `getPreis()`.

---

### Aufgabe 10 – Reflexionsauftrag im Code

Ergänze bei einer Klasse einen kurzen Kommentar:

- Warum ist ein Attribut `private`?
- Warum gibt es für ein Attribut keinen Setter?

---

## Reflexion

- Welche Attribute sollen von aussen lesbar sein?
- Welche Attribute sollen von aussen änderbar sein?
- Welche Regeln gehören in Setter oder Methoden?
- Was wird durch Kapselung einfacher zu testen?
