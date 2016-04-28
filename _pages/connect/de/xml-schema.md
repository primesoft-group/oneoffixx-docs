---
layout: page
title: XML Schema
permalink: "connect/de/xml-schema/"
---

## Namespace

Der Namespace für OneOffixx Connect lautet 

    http://schema.oneoffixx.com/OneOffixxConnectBatch/1

Wobei die hinterste Nummer der Major-Version entspricht. Die Minor Version steht in Global Settings (Key="Version" Value ="XXX")

## Validierung

Um eine OneOffixx Connect zu validieren resp. zu prüfen, kann dies via Prozessaufruf mit dem Parameter /ValidateConnector erzielt werden.
Beispielaufruf:

    c:\\program…\OneOffixx.exe /KeepConnector /ValidateConnector /connect XYZDatei.xml

Es ist zu beachten, dass hierbei das Connect-File nicht verarbeitet, sondern geprüft wird. Im produktiven Betrieb, empfielt sich eine ständige Validierung aus Performancegründen nicht.

## OneOffixx Connect Batch

![x]({{ site.baseurl }}/assets/content-images/connect/de/schema.png "Schema")

Enthält eine Batch Liste mit OneOffixx Connect Strukturen. Ein OneOffixx Connect entspricht einem OneOffixx Dokument.

## Global Settings

Diese Struktur enthält eine Key Value Liste mit Globalen Settings. Diese Settings werden während der Verarbeitung in die OneOffixx Connect Struktur kopiert.

![x]({{ site.baseurl }}/assets/content-images/connect/de/schema-globalsettings.png "Global Settings")

Bemerkung: Minor Versionen der Schnittstelle werden über globale Settings abgegrenzt. 

OneOffixx kennt die folgenden Settings:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Settings>
        <Add key="KeepConnector">true</Add>
        <Add key="CreateConnectorResult">false</Add>
        <Add key="CreateConnectorResultOnError">true</Add>
      </Settings>
      <Entries>
      …
      </Entries>
    </OneOffixxConnectBatch>
```

Diese Settings haben die gleiche Funktion wie die [entsprechenden Kommandozeilenparameter]({{ site.baseurl }}/connect/de/connect/#aufruf). Falls angegeben überschreiben sie die Kommandozeilenparameter.

__Hinweis:__ Nur bei der Angabe einer TemplateId wird ein Result-File __nach__ der Generierung erstellt. Wenn das Result_File auch bei Tag angaben gesichert erstellt werden soll, gäbe es die Möglichkeit über den "CreateConnectorResult"-Command zu gehen.

## Global Commands

Diese Struktur enthält Kommandos, welche die ganze Dokumentliste betreffen. (Bsp Merge Document). 

![x]({{ site.baseurl }}/assets/content-images/connect/de/schema-globalcommands.png "Global Commands")

## Entries

Entries entspricht einer Liste mit Dokumenten bzw. Connect aufrufen.

![x]({{ site.baseurl }}/assets/content-images/connect/de/schema-entries.png "Connect Entries")

## OneOffixx Connect

Die OneOffixxConnect Struktur entspricht einem Dokument. Jedes Dokument kann mit Argumenten, Kommandos und Dokumentfunktionen ausgestattet werden. 

![x]({{ site.baseurl }}/assets/content-images/connect/de/schema-connect.png "Connect")

Dokummentenfunktionen ("Function" im XML) reichen das Dokument mit Daten an und sind optional. Jede Funktion wird über ihre eindeutige ID identifiziert.
 
Über "Commands" kann man das generierte Dokument weiterverarbeiten und so z.B. an einem bestimmten Speicherort ablegen.
