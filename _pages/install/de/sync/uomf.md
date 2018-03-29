---
layout: page
title: Unified Object Mapping Format
permalink: "install/de/sync/uomf"
language: de
---

## **U**nified **O**bject **M**apping **F**ormat

Mit diesem standardisierten Format lassen sich Mapping durch OneOffixx hindurch einheitlich verwenden.

```xml
<Mapping Type="xml">
	<Map Source="//Identifikation[@Name='ID']" Target="PropertyX" />
	<If Condition="'1'=='1'">
		<Map SourceValue="Hans" Target="PropertyY" />
	</If>
	<Map Source="//Email" Target="PropertyZ" />
</Mapping>	

<Mapping Type="xml">
	<Map Source="//Identifikation[@Name='ID']" Target="PropertyX" />
	<Map SourceExpression="function main() { return OO('PropertyX'); }" Target="PropertyY" />
</Mapping>	
```

## Typen

### Dictionary Mapping

Beim Dictionary Mapping wird als *Source* der Schlüsselname des Wertes angegeben.

```xml
<Mapping>
	<Map Source="KeyName" Target="PropertyName" />
</Mapping>	
```

### XML Mapping

Beim diesem Mapping wird als Source ein XPath-Ausdruck angegeben. Dieses kann aktuell bei den Sync-Sources verwendet werden.

```xml
<Mapping Type="xml">
	<!-- <Map Source="XPath" Target="PropertyName" /> -->
	<Map Source="//Identification[@Name='ID']" Target="PropertyName" />
</Mapping>	
```


### JSON Mapping <span class="label label-warning">inaktiv</span>

Diese Art von Mapping ist aktuell inaktiv.


## Patterns und Beispiele

### Verweis auf vorherigen Wert

**Beispiel:** Wir möchten zwei Werte via XPath extrahieren und dann zusammensetzen, in diesem Fall eine Postleitzahl und ein Ort. Mit *OO('xyz')* wird auf die Targets der vorherigen Mappings zugegriffen.

```xml
<Mapping Type="xml">
	<Map Source="//KdmKontakt/Kontaktperson/Kontaktdaten/Postleitzahl" Target="Postleitzahl" />
	<Map Source="//KdmKontakt/Kontaktperson/Kontaktdaten/Ort" Target="Ort" />
	<Map SourceExpression="function main() { return OO('Postleitzahl') + ' ' + OO('Ort'); }" Target="Location" />
</Mapping>
```

### Konditioneller Verweis

**Beispiel:** Wir möchten die Telefonnummer setzen, und zwar die Handynummer (falls vorhanden), ansonsten die Festnetznummer (falls vorhanden), sonst die Geschäftsstellennummer.

#### Variante 1

```xml
<Mapping Type="xml">
	<Map Source="//Kontakt/Kontaktperson/Kontaktdaten/Handynummer" Target="Telefonnummer" />

	<If Condition="OO('Telefonnummer') == null || OO('Telefonnummer') == ''">
		<Map Source="//Kontakt/Kontaktperson/Kontaktdaten/Festnetznummer" Target="Telefonnummer" />
	</If>

	<If Condition="OO('Telefonnummer') == null || OO('Telefonnummer') == ''">
		<Map Source="//Kontakt/Kontaktperson/Kontaktdaten/Geschaeftsnummer" Target="Telefonnummer" />
	</If>
</Mapping>
```


#### Variante 2

Bei dieser Variante ist die Logik direkt als SourceExpression angegeben. Achtung: **&**-Zeichen müssen als **&amp;amp;** angegeben werden. Ausserdem dürfen main()-Functions nur über ein Return-Statement verfügen.

```xml
<Mapping Type="xml">
	<Map Source="//Kontakt/Kontaktperson/Kontaktdaten/Handynummer" Target="Handynummer" />
	<Map Source="//Kontakt/Kontaktperson/Kontaktdaten/Festnetznummer" Target="Festnetznummer" />
	<Map Source="//Kontakt/Kontaktperson/Kontaktdaten/Geschaeftsnummer" Target="Geschaeftsnummer" />

	<Map SourceExpression="
		function main() { 
			var value = OO('Geschaeftsnummer');
			if(OO('Festnetznummer') != null &amp;&amp; OO('Festnetznummer') != '') { value = OO('Festnetznummer'); }
			if(OO('Handynummer') != null &amp;&amp; OO('Handynummer') != '') { value = OO('Handynummer'); }
			return value;	
		}" 
	Target="Telefonnummer" />
</Mapping>
```
