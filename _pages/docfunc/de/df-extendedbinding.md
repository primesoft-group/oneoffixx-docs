---
layout: page
title: Extended Binding
permalink: "docfunc/de/df/extendedbinding"
language: de
---

Die Dokumentfunktion Extended Binding ermöglicht es über XSLT den Dokumentaufbau zu beeinflussen. Verglichen mit der Dokumentfunktion Skripts ist das Extended Binding in der Lage nebst dem Textinhalt<br/>
noch weitere Attribute, wie Textfarbe, Grösse angwenadter Style etc. zu verändern.

## Übersicht

- [Übersicht](#übersicht)
- [Beispiele](#beispiele)
- [Tags](#tags)
- [Zugriff auf Daten](#zugriffaufdaten)
- [Operatoren](#operatoren)

#### Beispiele

__Empfänger mit Versandart:__

Die Versandart und der Empfänger haben unterschiedliche Style-Informationen, zudemm ist die Versandart eine optionale Eingabe. Wird gewünscht, dass der Empfänger eine Zeile nachrückt wenn die Versandart nicht ausgefüllt ist muss dies mit Extended Binding gelöst werden. Die üblichen Skripts können nicht verschiedene Style-Informationen in einem Skript verwenden.

| ![x]({{ site.baseurl }}/assets/content-images/docfunc/de/ExtendedBindingTransmission.PNG) |![x]({{ site.baseurl }}/assets/content-images/docfunc/de/ExtendedBindingTransmission.PNG)
|:--:|
|*Verwendung von Extended Binding*|
__Dynamische Tabellen__

Tabellen mit variabler Anzahl von Zeilen sind ein weiteres Beispiel für den Einsatz von Extended Bindings. Erstellt man eine Tabelle mit Skripts muss die Anzahl Zeilen und Spalten bekannt sein. Bei der Verwendung von Extended Bindings kann das Ausgeben einer Zeile oder einer Spalte von Bedingungen abhängig gemacht werden, somit wird die Tabelle dynamisch.