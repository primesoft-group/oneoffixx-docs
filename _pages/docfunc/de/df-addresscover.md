---
layout: page
title: AddressCover / Adressdeckblatt / Kuvert
permalink: "docfunc/de/df/addresscover"
language: de
---

Diese Dokument-Funktion wird benötigt, um den Umgang mit Adressdeckblättern (Vorlagen des Typs „Word Address Cover“, in der Regel Adressdeckblätter und Kuverts) zu konfigurieren.

Dabei hat die Dokument-Funktion zwei Funktionen:
* Konfiguration von Vorlagen des Typs „Word Address Cover“
* Konfiguration der Möglichkeiten, wie aus dem Dokument über den „Kuvert“-Button im Ribbon ein Adressdeckblatt erstellt werden kann (bei den restlichen Word-Vorlagen-Typen)

## Konfiguration von Vorlagen des Typs „Word Address Cover“

Bei Vorlagen des Typs „Word Address Cover“ ist das Anhängen dieser Dokument-Funktion Pflicht.

Zusätzlich muss vor dieser Dokument-Funktion unbedingt die Dokument-Funktion [RecipientAddresses]({{ site.baseurl }}/docfunc/de/df/recipientaddress) („Empfängeradressen“) angehängt sein.

In diesem Fall ist nur der Teil zwischen `<AddressCoverTemplate>` und `</AddressCoverTemplate>` relevant.

### Vorschau

Zwischen `<RecipientPreview>` und `</RecipientPreview>` kann der anzuzeigende Text für die Vorschau konfiguriert werden:

```xml
<RecipientPreview>
  <DataNode id="CustomElements.Recipient.AddressCover" />
</RecipientPreview>
```

Dabei muss die ID des Textes angegeben werden. In der Regel bleibt diese so wie oben.

### Skripts (pro Adressdeckblatt)

Zwischen `<Script>` und `</Script>` können Skripts definiert werden, welche schlussendlich pro Empfänger generiert werden.
Wenn also z. B. mit `<Element id="Contact.Recipient.Selected.Person.FirstName" />` auf den Vornamen verwiesen wird, wird beim 1. Adressdeckblatt der Vorname des 1. Empfängers und beim 2. Adressdeckblatt der Vorname des 2. Empfängers usw. verwendet.

Standardmässig steht hier nur das Vorschau-Skript:

```xml
<Script>
  <CustomDataNode id="Recipient.AddressCover" type="Text">
    <Line>
      <Element id="Contact.Recipient.Selected.Person.FirstName" />
    </Line>
    <Line>
      <Element id="Person.Anschrift" />
    </Line>
  </CustomDataNode>
</Script>
```


## Konfiguration von anderen Word-Vorlagen

Bei „normalen“ Word-Vorlagen kann mit dieser Dokument-Funktion konfiguriert werden, dass das Erstellen von Adressdeckblättern mit Übernahme der aktuellen Empfänger aus den künftigen Dokumenten möglich ist, indem der „Kuvert“-Button im OneOffixx-Ribbon gewählt wird:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/addressCoverButtonRibbon.png)

Hierbei ist nur die Konfiguration zwischen `<AddressCoverDialog>` und `</AddressCoverDialog>` relevant.

Der Dialog, der beim Klick auf den „Kuvert“-Button im Ribbon erscheint, sieht so aus:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/addressCoverDialog.png)

### Verfügbare Adressdeckblatt-Vorlagen

Diese werden zwischen `<LabelTemplates>` und `</LabelTemplates>` definiert. Hier eine Beispiel-Konfiguration:

```xml
<LabelTemplates>
  <Template id="18e4a599-3d93-41a3-a289-39fe5263eab5" /> <!-- Kuvert C5 rechts (Standard) -->
  <Template id="4049d9de-ac64-4441-bec9-f342b3dc15b6" /> <!-- Kuvert C5 links -->
  <Template id="1948dcff-288d-466a-9598-9a33c16f87de" /> <!-- Kuvert C6 -->
  <Template id="24886fd2-01a9-49a2-80e9-2a920e6392d3" /> <!-- Adressdeckblatt A4 -->
</LabelTemplates>
```

Dies bedeutet nun, dass beim Aufruf der „Kuvert“-Dialogs zwischen diesen 4 Vorlagen ausgewählt werden kann.<br>
Bei der ID handelt es sich um die Vorlagen-ID (nicht um die Versions-ID).

Im Dialog sieht dies dann unten rechts so aus:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/addressCoverDialogTemplateSelection.png)
 
### Anrede und Versandart

Zusätzlich müssen Anrede und Versandart konfiguriert sein.

Diese Konfiguration sollte identisch sein wie diejenige in der Empfängeradressen-Dokument-Funktion.

In der Regel werden hier mit den folgenden zwei Zeilen die Anrede- und Versandart-Konfiguration im globalen Konfigurationsprovider verknüpft:

```xml
{[Recipients.SalutationConfiguration]}

{[Recipients.ShippingMethodConfiguration]}
```

Falls die Konfiguration nicht wie oben aus dem globalen Konfigurationsprovider kommen soll, muss sie folgendermassen erfolgen:


```xml
<SalutationConfiguration>
  [...]
</SalutationConfiguration>

<ShippingMethodConfiguration>
  [...]
</ShippingMethodConfiguration>
```

`[...]` → Analog zur [RecipientAddresses]({{ site.baseurl }}/docfunc/de/df/recipientaddress)/Empfängeradressen-Dokument-Funktion
