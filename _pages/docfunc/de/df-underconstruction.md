---
layout: page
title: Debugger
permalink: "docfunc/de/df/underconstruction"
language: de
---

Der Debugger gibt einen Einblick in die OpenXML Struktur des Dokuments und zeigt dazugehörige OneOffixx
Informationen an. Diese Funktion sollte nur während der Entwicklung genutzt werden oder zur Unterstützung beim
Scripting bzw. Extended Binding

## Übersicht
<!-- TOC -->
- [Übersicht](#übersicht)
- [Overview](#overview)
- [DocumentPart](#documentpart)
- [DocData](#docdata)
<!-- /TOC -->

### Overview

Im Overview-Ribbon werden folgende Daten des Dokuments aufegführt:
 
-  Template Id
-  Internal Template Id
-  Document Id
-  Document LCID
-  UI LCID
-  Profile Id
-  Creation Mode
-  Pipeline Version

### DocumentPart

Im DocumentPart-Ribbon wird der Inhalt vom Custom XML Part `OneOffixxDocumentPart` aufegführt.<br />

Im `OneOffixxDocumentPart` Custom XML Part befinden sich alle OneOffixx-Text-Element. Die Anzeige des OneOffixxDocumentParts im Debugger wird dazu verwenden, um sicherzustellen, dass die OneOffixx-Text-Elemente dem Dokument für die weitere Verarbeitung übergeben werden.

Nachfolgend eine Liste der gängigsten OneOffixx-Text-Elemente, die im Debugger unter DocumentPart eingesehen werden können:

-  Dokument-Parameter
-  Profilinformationen
-  Empfängerinformationen
-  Interfaces
-  Skripts

Wichtig: Die Position der Dokument-Funktion "Debugger" beeinflusst, welche Daten sich zu der Zeit im DocumentPart befinden. Wenn sich z. B. der Debugger vor dem Dokument-Parameter befindet, werden im DocumentPart keine Dokument-Parameter-Informationen angezeigt.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/debugger_position.png)

Die Informationen der grün umrandeten Dokumentfunktionen werden im DocumentPart-Ribbon angezeigt, die roten nicht, da Sie nach dem Debugger deifniert sind.

Der Inhalt vom Custom XML Part `OneOffixxDocumentPart` wird wie folgt angezeigt:

```xml
<DataModel xmlns="">
      <Parameter windowwidth="750" windowheight="450" minwindowwidth="0" maxwindowwidth="0" minwindowheight="0" maxwindowheight="0">
        [...]
        <Text id="DocParam.Subject" [...]><![CDATA[OneOffixx-Dokumentation]]></Text>
        <DateTime id="DocParam.Date" [...]><![CDATA[2018-10-31T00:00:00Z]]></DateTime>
        <Text id="DocParam.Enclosures" [...]><![CDATA[Dokument]]></Text>
        <Text id="DocParam.CopyTo" [...]><![CDATA[Kunden]]></Text>
        [...]
      </Parameter>
      <Profile windowwidth="0" windowheight="0" minwindowwidth="0" maxwindowwidth="0" minwindowheight="0" maxwindowheight="0">
        [...]
        <Text id="Profile.Org.Title"  [...]><![CDATA[OneOffixx]]></Text>
        <Text id="Profile.Org.Web"  [...]><![CDATA[oneoffixx.com]]></Text>
        <Text id="Profile.User.FirstName" [...]><![CDATA[Max]]></Text>
        <Text id="Profile.User.LastName"  [...]><![CDATA[Muster]]></Text>
        [...]
      </Profile>
      <Interfaces windowwidth="0" windowheight="0" minwindowwidth="0" maxwindowwidth="0" minwindowheight="0" maxwindowheight="0">
        <NodeGroup id="InterfaceDemo"  [...]>
          <Text id="ErstesFeld"  [...]><![CDATA[1]]></Text>
          <Text id="ZweitesFeld"  [...]><![CDATA[2]]></Text>
          <Text id="DrittesFeld"  [...]><![CDATA[3]]></Text>
        </NodeGroup>
      </Interfaces>
      [...]
</DataModel>
```

### DocData

Im DocData-Ribbon wird das gesamte Word-File in XML-Form angezeigt. Dabei werden die Files, die sich jeweils im gezippten Word-File befinden, als einzelne Packages aufgeführt.

Das File 'document.xml' im Verzeichnis 'Word' wird wie folgt angezeigt:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<?mso-application progid="Word.Document"?>
<pkg:package xmlns:pkg="http://schemas.microsoft.com/office/2006/xmlPackage">
  [...]
  <pkg:part pkg:name="/word/document.xml" pkg:contentType="application/vnd.openxmlformats-officedocument.wordprocessingml.document.main+xml">
    <pkg:xmlData>
      <w:document [...]>
        <w:body>
          <w:p>
            <w:r>
              <w:t>Inhalt vom ersten und einzigen Absatz...</w:t>
            </w:r>
          </w:p>
          <w:sectPr w:rsidR="002C66A7" w:rsidRPr="002C66A7">
            <w:pgSz w:w="11906" w:h="16838" />
            <w:pgMar w:top="1417" w:right="1417" w:bottom="1134" w:left="1417" w:header="708" w:footer="708" w:gutter="0" />
            <w:cols w:space="708" />
            <w:docGrid w:linePitch="360" />
          </w:sectPr>
        </w:body>
      </w:document>
    </pkg:xmlData>
  </pkg:part>
  [...]
</pkg:package>
```

Somit können in DocData die Inhalte von allen Files des gezippten Word-Dokuments angeschaut werden.

Dieses XML-Dokument entsteht auch, wenn ein Word-Dokument abgespeichert wird mit Dateityp «Word XML-Dokument (*.xml)».
