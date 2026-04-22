# Tag 5 – StringBuilder

## Grafiken

![Konzept](./grafiken/tag5_konzept_immutability_string.svg)
![Prozess](./grafiken/tag5_prozess_string_verketten_plus.svg)
![Vergleich](./grafiken/tag5_vergleich_string_vs_stringbuilder.svg)

## Theorie

String ist immutable → Änderungen erzeugen neue Objekte.

StringBuilder ist veränderbar → effizient bei vielen Operationen.

## Übung

Refactore folgenden Code:

```java
String s = "";
for(int i=0;i<1000;i++){
  s += i;
}
```

→ Verwende StringBuilder
