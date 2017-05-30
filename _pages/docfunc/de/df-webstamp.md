---
layout: page
title: Webstamp
permalink: "docfunc/de/df/webstamp"
language: de
---

### Konfiguration

Die Dokumentfunktion lässt folgende Konfigurationen zu:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Configuration>	
	<UseAddressDefault> <!-- festlegen, ob die Adresse standardmässig genutzt werden soll --> </UseAddressDefault>
	<Authorization>
		<!-- Nutzer oder Nutzergruppen festlegen, die berechtigt sind, WebStamps zu bestellen -->
	</Authorization>

	<AccessData>
		<!-- Zugangsdaten zur WebStamp API der schweizerischen Post festlegen -->
	</AccessData>

	<WebStampProducts>
		<!-- WebStamp-Eigenschaften festlegen, die im Dialog dem Nutzer zur Auswahl stehen sollen -->
	</WebStampProducts>
</Configuration>
```

### Empfängeradressdaten standardmässig einbinden

Mit `true` oder `false` in `<UseAddressDefault>` kann festgelegt werden, ob die Checkbox für das Einfügen der Empfängeradressdaten im Dialog standardmässig angewählt sein soll oder nicht. 

Beispiel: die Checkbox für das Einfügen der Empfängeradressdaten wird standardmässig angewählt

```xml
<UseAddressDefault>true</UseAddressDefault>
```

### Berechtigungen

Werden keine Nutzer oder Gruppen festgelegt, sind alle Berechtigt, WebStamps zu bestellen.

Beispiel:

```xml
<Authorization>
</Authorization>
```

Wenn nur ein gewisser Nutzerkreis berechtigt sein soll kann dieser hier festgelegt werden. Es können Windows-Benutzernamen oder Windows Active Directory Benutzergruppen festgelegt werden.

Einzelne Windows-Benutzernamen können in `<WindowsUsers>` mit `,` getrennt aufgelistet werden.

Windows Active Directory Benutzergruppen können in `<WindowsGroups>` mit `,` getrennt aufgelistet werden.

Beispiel: Die Windows-Benutzer `user` und `anotherUser` und alle Benutzer in den Active Directory Gruppen `group` und `anotherGroup` sind berechtigt, WebStamps zu bestellen

```xml
<Authorization>
	<WindowsUsers>user,anotherUser</WindowsUsers>
	<WindowsGroups>group,anotherGroup</WindowsGroups>
</Authorization>
```

### Zugangsdaten

Hier müssen die Zugangsdaten zur WebStamp Schnittstelle (API) der schweizerischen Post AG festgelegt werden.

Die Zugangsdaten bestehen aus `ApplicationKey`, `UserId`, `Password` und `ServiceUrl`.

Die Konfiguration könnte so aussehen:

```xml
<AccessData>
	<ApplicationKey>a0000aa0000a0aa0aaa0a0000000a000</ApplicationKey>
	<UserId>00000000</UserId>
	<Password>00000000</Password>
	<ServiceUrl>https://subdomain.domain.ch/path</ServiceUrl>
</AccessData>
```

Die schweizerische Post bietet mehrere Schnittstellen. Eine Test-Schnittstelle und eine produktive Schnittstelle.

Ist die Test-Schnittstelle konfiguriert, können nur Test-WebStamps bestellt werden, die keine Kosten verursachen, ein Wasserzeichen über dem Stamp-Bild haben und nicht für den Versand benutzt werden können. Die Dokumentfunktion erkennt, wenn die Test-Schnittstelle konfiguriert ist und teilt dem Nutzer mit einem Hinweis mit, dass keine Kosten für bestellte WebStamps auftreten.

Ist die produktive Schnittstelle konfiguriert, können normale WebStamps bestellt werden. Die Kosten werden verrechnet und der bestellte WebStamp kann für den Versand benutzt werden.

### WebStamp-Eigenschaften

Hier lassen sich die WebStamp-Eigenschaften festlegen, die dann dem Nutzer im WebStamp-Dialog zur Auswahl stehen.

In der DefaultConfiguration sind die gängigsten Produkte bereits konfiguriert. Dies sieht dann so aus:

```xml
<WebStampProducts>
	<WebStampProduct Number="15220">A-Post Standard (A5) bis 100g</WebStampProduct>
	<WebStampProduct Number="4839">A-Post Midi (A5) 100-250g</WebStampProduct>
	<WebStampProduct Number="699358">A-Post Grossbrief (A4) bis 500g</WebStampProduct>
	<WebStampProduct Number="630">A-Post Grossbrief (A4) bis 501-1000g</WebStampProduct>
	<WebStampProduct Number="15242">B-Post Standard (A5) bis 100g</WebStampProduct>
	<WebStampProduct Number="13657">B-Post Midi (A5) 100-250g</WebStampProduct>
	<WebStampProduct Number="699735">B-Post Grossbrief (A4) bis 500g</WebStampProduct>
	<WebStampProduct Number="11838">B-Post Grossbrief (A4) bis 501-1000g</WebStampProduct>
	<WebStampProduct Number="1307915">Einschreiben B4 1kg 2cm, B5 250g 5cm</WebStampProduct>
	<WebStampProduct Number="348756">PRIO Mail Std 20g Z1 (Europa)</WebStampProduct>
	<WebStampProduct Number="348757">PRIO Mail Std 50g Z1 (Europa)</WebStampProduct>
	<WebStampProduct Number="348787">PRIO Mail Std 100g Z1 (Europa)</WebStampProduct>
	<WebStampProduct Number="348920">PRIO Mail Std 20g Z2 (Andere Kontinente)</WebStampProduct>
	<WebStampProduct Number="348921">PRIO Mail Std 50g Z2 (Andere Kontinente)</WebStampProduct>
	<WebStampProduct Number="348922">PRIO Mail Std 100g Z2 (Andere Kontinente)</WebStampProduct>
</WebStampProducts>
```

Für eine WebStamp-Eigenschaft ist die `Number` als Attribut und der Name in `<WebStampProduct>` anzugeben. 

Die `Number` muss der `post_product_number` eines `wsws_product` Objekts entsprechen, die von der WebStamp-Schnittstelle abgefragt werden können.

Der Name in `<WebStampProduct>` kann selbst gewählt werden, er sollte jedoch möglichst passend das entsprechende Produkt der WebStamp Schnittstelle beschreiben.

### Templating

Dem Templater stehen folgende Inhaltssteuerelemente zur Verfügung

* `ContainsAddress` – boolean – gibt an, ob eine Adresse im WebStamp vorhanden ist
* `ImageStampOnly` – image – beinhaltet ein Bild, sofern ein WebStamp ohne Adresse generiert wurde
    * darf nicht in skripts benutzt werden
* `ImageWithAddress` – image – beinhaltet ein Bild, sofern ein WebStamp mit Adresse generiert wurde
    * darf nicht in skripts benutzt werden
* `IsSet` – boolean – gibt an, ob ein WebStamp generiert wurde

### Dialog

Der Dialog besteht aus den folgenden Einstellungsmöglichkeiten

## Empfängeradressdaten in WebStamp einfügen

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/webstampbestelldialog01adresse.png) 

Wenn in der Empfänger-Dokumentfunktion ein oder mehr Empfänger ausgewählt wurden, hat man die Möglichkeit, diese Checkbox anzukreuzen. Hat man keinen Empfänger ausgewählt, wird die Box und der Text grau und deaktiviert.

Wird die Checkbox angekreuzt, fügt die Dokumentfunktion die ersten aller ausgewählten Empfängeradressdaten in den WebStamp ein.

## WebStamp-Eigenschaften auswählen

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/webstampbestelldialog02eigenschaften.png) 

Hier kann mit einer Dropdown-Liste eine der in der Konfiguration vorgegebenen WebStamp-Eigenschaften ausgewählt werden. Entsprechend dieser Auswahl wird der Preis auf dem Bestell-Knopf aktualisiert.

## Hinweis zur Test-Schnittstelle

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/webstampbestelldialog03hinweis.png)

Dieser Hinweis wird nur angezeigt, wenn die Test-Schnittstelle konfiguriert wurde. Andernfalls bleibt dieser Platz leer. 

Der Hinweis teilt dem Nutzer mit, dass mit einer Bestellung über die Test-Schnittstelle keine Kosten auftreten, aber der WebStamp auch nicht gültig ist. 

Auch mit der Test-Schnittstelle werden weiterhin auf dem Bestell-Knopf die Kosten angezeigt, die für die gewählten WebStamp-Eigenschaften auftreten würden. Mit dem angezeigten Hinweis treten diese bei der Bestellung nicht auf.
