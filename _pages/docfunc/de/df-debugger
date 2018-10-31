---
layout: page
title: Debugger
permalink: "docfunc/de/df/underconstruction"
language: de
---

Der Debugger gibt einen Einblick in die OpenXML Struktur des Dokuments und zeigt dazugehörige OneOffixx-Informationen an. Diese Funktion sollte nur während der Entwicklung genutzt werden oder zur Unterstützung beim
Scripting bzw. Extended Binding.


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

Im DocumentPart-Ribbon wird der Inhalt vom Custom XML Part `OneOffixxDocumentPart` aufgeführt.<br />

Im `OneOffixxDocumentPart` Custom XML Part befinden sich alle OneOffixx-Text-Elemente. Die Anzeige des OneOffixxDocumentParts im Debugger wird dazu verwendet, um sicherzustellen, dass die OneOffixx-Text-Elemente dem Dokument für die weitere Verarbeitung übergeben werden.

Nachfolgend eine Liste der gängigsten OneOffixx-Text-Elemente, die im Debugger unter DocumentPart eingesehen werden können:

-  Dokument-Parameter
-  Profilinformationen
-  Empfängerinformationen
-  Interfaces
-  Skripts

Wichtig: Die Position der Dokument-Funktion "Debugger" beeinflusst, welche Daten sich zu der Zeit im DocumentPart befinden. Wenn sich z. B. der Debugger vor den Skripts befindet, werden im DocumentPart keine Skript-Informationen angezeigt.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/Debugger.png)

Die Informationen der Dokumentfunktionen, welche sich überhalb des Debuggers befinden werden im DocumentPart angezeigt, die Informationen derjenigen, welche sich unterhalb befinden werden nicht angezeigt.

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
Die <![[CDATA[]]>-Tags sorgen dafür, dass Spezialzeichen nicht als XML interpretiert werden, somit muss man sie nicht einzeln escapen.

### DocData

Im DocData-Ribbon wird das gesamte Word-File in XML-Form angezeigt. Dabei werden die einzelnen Files, die sich jeweils im  Word-File-Verzeichnis befinden, als einzelne Packages aufgeführt.

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

Somit können in DocData die Inhalte von allen Files des Word-File-Verzeichnises angeschaut werden.

Dieses XML-Dokument entsteht auch, wenn ein Word-Dokument abgespeichert wird mit Dateityp «Word XML-Dokument (*.xml)».
