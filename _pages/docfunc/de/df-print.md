---
layout: page
title: Print
permalink: "docfunc/de/df/print"
language: de
---

Die Druck-Funktion definiert in einer Vorlage, welches Papier beim Drucken des Dokumentes für welche Seite verwendet werden soll. Der User kann zudem im Dokument verschiedene Optionen wählen, welche z.B. Für Logo ein/aus, Entwurf ein/aus oder ob es sich um einen Mehrfachbrief handelt.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/print.png)

Mit hilfe der Konfiguration können die Einstellungen aus dem Druckerdialog ausgelesen und angewendet werden.

**Konfiguration:**
```xml
<?xml version="1.0"?>
<Configuration>
  <Logo>FromDocument</Logo>
  <Draft>FromDocument</Draft>
  <VectorSignature>FromDocument</VectorSignature>
  <Fax>FromDocument</Fax>
  <Campaign>FromDocument</Campaign>
  <Color>FromDocument</Color>
  <!-- Each section in the document corresponds to one section within this configuration. Id is actually a DisplayName and can be translated -->
  <Section Id="Dokument">
    <PaperFirstPage>Normal</PaperFirstPage>
    <Paper>Normal</Paper>
  </Section>
</Configuration>
```

Mögliche Werte in den Elementen sind FromDocument/True/False. Dies bedeutet, im Falle von FromDocument werden die Einstellungen vom Dialog übernommen. True bedeutet diese Option ist eingeschaltet, False die Option ist ausgeschaltet.

**Erste Seite Logopapier oder normales verwenden**
`<PaperFirstPage>Logo</PaperFirstPage>`
Folgeseiten: welche Papierart, Logo oder weisses Papier
`<Paper>Normal</Paper>`			
