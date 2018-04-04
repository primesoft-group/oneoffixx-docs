---
layout: page
title: Unified OneOffixx Mapping Format
permalink: "install/de/sync/uomf"
language: de
---

## **U**nified **O**neOffixx **M**apping **F**ormat

Mit diesem standardisierten Format lassen sich Mapping durch OneOffixx hindurch einheitlich verwenden.

Beispiele:
```xml
<Mapping>
	<Map Source="fname" Target="Forname" />
	<Map SourceValue="Hans" Target="Forname" />
	<Map SourceValue="Gseh" Target="LastName" When="source('test')=='someValue'" />
	<Map SourceExpression="25*78" Target="Calculator" When="target('LastName')==='Gseh'" />

	<Map>
		<Map.Source>fname</Map.Source>
		<Map.Target>Forname</Map.Target>
	</Map>
	<Map>
		<Map.SourceValue>Hans</Map.SourceValue>
		<Map.Target>Forname</Map.Target>
	</Map>
	<Map>
		<Map.SourceValue>Gseh</Map.SourceValue>
		<Map.Target>LastName</Map.Target>
		<Map.When><![CDATA[source('test') < 12]]></Map.When>
	</Map>
	<If Condition="source('test')=='someValue'">
		<Map>
			<Map.SourceExpression>25*78</Map.SourceExpression>
			<Map.Target>Calculator</Map.Target>
		</Map>
	</If>
</Mapping>
```
## Map-Element

Ein Map Element stellt eine einzelne Zuordnungsoperation dar. Jede Eigenschaft kann wie im obigen Beispiel gezeigt, sowohl als Attribut oder als Element gesetzt werden. Z.B. `Condition` als Attribut oder `If.Condition` als Element, dabei ist der Name mit einem Punkt der Präfix für den Eigenschaftsnamen.

Dabei muss genau eine Source-Eigenschaft und das Target gesetzt sein.

{:.table .table-striped}
| Eigenschaft | Beschreibung |
| --- | --- |
| Source | Der Name, der den Wert identifiziert. Z.b. Spaltenname der Datenbank im Generic Sql Provider. Wird der Wert nicht gefunden, wird `null` weitergegeben. Siehe Mapping-Datenquelle. |
| SourceValue | Der konstante Wert, welcher verwendet werden soll. |
|  SourceExpression | Eine OneOffixx Javascript-Expression, die für jedes gemapte Element ausgewertet wird. 
| Target | Die Zieleigenschaft für das Mapping. Bei Adressprovidern handelt es sich hierbei um die Kontaktfelder.
| When | Eine OneOffixx Javascript-Expression, welche es erlaubt, das Mapping bedingt auszuführen. Wenn der Wert auf wahr ausgewertet wird, wird das Mapping ausgeführt.

## If-Element

Das If-Element erlaubt es, Bedingungen für ganze Blöcke von Mappings zu definieren. If-Blöcke können beliebig kombiniert und verschachtelt werden.

{:.table .table-striped}
| Eigenschaft | Beschreibung |
| --- | --- |
| Condition | Javascript-Bedingung - Resultat wird auf [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)-Wert geprüft. |

## JavaScript-Expressions: Bedingungen und Ausdrücke

### Escaping

Im Xml haben gewisse Zeichen wie &amp; oder &lt; eine besondere Bezeichnung. Diese können daher nicht direkt verwendet werden. Escapen Sie diese: `&` kann z.B. als `&amp;` geschrieben werden:
```xml
<Mapping>
	<Map Source="Value" Target="Target" When="source('val1') == 'test1' &amp;&amp; source('val2')=='test2'" />
</Mapping>
```

Alternativ kann dies mittels `CDATA` und Element-Schreibweise gemacht werden:
```xml
<Mapping>
	<Map Source="Value" Target="Target">
		<Map.When><![CDATA[source('val1') == 'test1' && source('val2')=='test2']]></Map.When>
	</Map>
</Mapping>
```

### Source

Via `source`-Api-Objekt kann vom JavaScript aus analog der Source-Eigenschaft auf die Quellwerte zugegriffen werden, ist der Wert nicht verfügbar, wird `undefined` zurückgegeben. Mit Javascript zwischen kann also zwischen `null` und `undefined` unterschieden werden. Folgendes Beispiel nimmt die letzte verfügbare Telefonnummer:
```XML
<Mapping>
	<Map Source="Arbeitsplatz" Target="Phone" When="source('Arbeitsplatz') != undefined" />
	<Map Source="Mobile" Target="Phone" When="source('Mobile') != undefined" />
</Mapping>
```

Aus Kompatibilitätsgründen kann auch mittels `oo` oder `OO` auf die Source zugegriffen werden.

### Target
Via `target`-Api-Objekt kann vom JavaScript aus auf zuvor gemappte Werte zugegriffen werden, ist der Wert nicht verfügbar, wird `undefined` zurückgegeben. Folgendes Beispiel setzt eine Adresse zusammen:
```XML
<Mapping>
	<Map SourceExpression="source('street')+' ' +source('hausnr')" Target="Street" />
	<Map SourceExpression="target('street') + '\r\n' + source('OrtUndPLZ')" Target="CompleteAddress"/>
</Mapping>
```
Ergibt folgendes Resultat:
```
Source
----------
street              Teststrasse
hausnr              42
OrtUndPLZ           4242 Testhausen

Resultat
----------
Street              Teststrasse 42
CompleteAddress     Teststrasse 42
                    4242 Testhausen
```

### Main-Funktion

Um komplexere JavaScript-Methoden auszuführen, kann die Funktion `main()` definiert werden. Ist eine solche definiert, wird sie aufgerufen. Folgendes Beispiel normalisiert und internationalisiert schweizer Telefonnummern:

```xml
<Mapping>
    <Map Target="Phone">
        <Map.SourceExpression>
            function main()
            {
                // normalisiert alle Telefonnummern
                // 0715110500 => +41 71 511 05 00
                // +41 71 511 05 00 => +41 71 511 05 00
                var input = source('phonenumber').replace(/ /g, '');
                var patt = /((\+|00)41|0)([0-9]+)/;
                var matchArray = patt.exec(input);
                var number = matchArray[3];
                return  "+41 " + number.substring(0,2) + " " + number.substring(2,5)
                    + " " + number.substring(5,7)+ " " + number.substring(7,9);
            }
    	</Map.SourceExpression>
	</Map>
</Mapping>
```

### Bemerkungen

* In JavaScript werden Bedingungen auf einen [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)-Wert überprüft. D.h. es können auch nicht-boolesche (Wahr oder Falsch) Werte ausgewertet werden. So werden positive Zahlen oder nicht leere Zeichenketten auch als wahr ausgewertet.
* Vergleiche: Der `==` Operator kann auch verwendet werden, um verschiedene Datentypen zu vergleichen, z.B. wird `'55'==55` als wahr ausgewertet. Praktischer Tipp: da `undefined==null` auch als wahr ausgewertet wird, kann mittels `source('Name')==null`sowohl auf leere (`null`) als auch auf nicht verfügbare (`undefined`) Werte überprüft werden. Mehr zu Vergleichen mit JavaScript finden Sie [hier](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness).

## Mapping-Datenquelle

Je nach Datenquelle ist der Zugriff auf die Daten anders, d.h. wie der Quellwert im `Source`-Attribut oder im Javascript der `source()`-Funktion übergeben wird. Es gibt folgende Quellen:

### Default - Schlüssel-Wert-Liste

Es werden einfache Schlüssel angegeben - es existiert eine direkte Zuordnung. Beispiele:

- Spaltenname für den Sql-Adress-Provider
- Spaltenname oder Spaltennummer für CSV/XLSX Adress-Provider

### XML-Quelle

Bei Xml-Quellen kann ein [XPath](https://de.wikipedia.org/wiki/XPath) (1.0) angegeben werden, um den Wert zu identifizieren.

Dabei werden folgende Rückgaben gemacht:

{:.table .table-striped}
| Resultat des XPath | Zurückgegebener Wert |
| --- | --- |
| Attribut | Wert des Attribut
| Element | Inhalt/Wert des Elements
| Text | Der Text
| CData | Ist das Resultat in CData gewrappt, wird dieses *ohne* den CData Tag zurückgegeben

#### Beispiel

XML Quelldatei:
```xml
<Kontakt>
	<Company>Sevitec Informatik AG<Company>
	<Adresse>
		<PLZ>8360</PLZ>
		<City>Eschlikon</City>
		<Street>Bahnhofsstrasse 4</Street>
	<Adresse>
	<Contact>
		<Option Type="Phone">+41 71 511 0 500</Option>
		<Option Type="Mail">info@sevitec.ch</Option>
	<Contact>
</Kontakt>
```
    
Mapping:

```xml
<Mapping Type="XML">
	<Map Source="//PLZ" Target="Postleitzahl" />
	<Map Source="/Kontakt/Adresse/City" Target="Stadt" />
	<Map Source="//Street" Target="Strasse" />
	<Map Target="KompletteAdresse">
		<Map.SourceExpression>
			source('//Company') + '\r\n' + source('//Street') + '\r\n' + source('//PLZ') + ' ' + source('//City')
		<Map.SourceExpression>
	<Map>
	<Map Source="//Contact/Option[@Type='Phone']" Target="Telefon"/>
</Mapping>
```
Resultat:

    Postleitzahl:       8360
    Stadt:              Eschlikon
    Strasse:            Bahnhofsstrasse 4
    KompletteAdresse:   Sevitec Informatik AG
                        Bahnhofsstrasse 4
                        8360 Eschlikon
    Telefon:            +41 71 511 0 500


## Verschiedene Beispiele

### If-Else

In der aktuellen Version gibt es keinen Else-Abschnitt. Für grössere Abschnitte kann die Bedingung negiert werden:
```xml
<Mapping>
	<If Condition="source('Typ') == 'Geschäftlich'">
		<!-- Map Elemente für FirmenAdresse-->
	</If>
	<If Condition="!(source('Typ') == 'Geschäftlich')">
		<!-- Map Elemente für Else-Fall-->
	</If>
<Mapping>
```
Um einen Wert aus verfügbaren Elementen auszuwählen, können mehrere Maps mit dem gleichen Target verwendet werden:
```xml
<Mapping>
	<Map Source="Privat" Target="Phone"/>
	<Map Source="Büro" Target="Phone" When="source('Privat')!=null"/>
    <Map Source="Mobile" Target="Phone" When="source('Privat')!=null"/>
</Mapping>
```
Beachten Sie die Reihenfolge: Die Maps werden der Reihenfolge nach ausgewertet, d.h. die letzte vorhandene Nummer wird verwendet.

Alternativ kann eine Javascript-Expression benutzt werden:
```xml
<Mapping>
    <Map Target="Phone">
        <Map.SourceExpression>
            function main()
            {
                if(source('Mobile') != null)
                {
                    return source('Mobile');
                }
                else if(source('Büro') != null)
                {
                    return source('Mobile');
                }
                else
                {
                    return source('Privat');
                }
            }	
        </Map.SourceExpression>
    </Map>
</Mapping>
```