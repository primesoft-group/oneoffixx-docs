---
layout: page
title: Debugger
permalink: "docfunc/de/df/underconstruction"
language: de
---

Der Debugger gibt ein Einblick in die OpenXML Struktur des Dokuments und zeigt dazugehörige OneOffixx
Informationen an. Diese Funktion sollte nur wwährend der Entwicklung genutzt werden oder zur Unterstützung beim
Scripting bzw. Extended Binding

## Übersicht
<!-- TOC -->
- [Übersicht](#übersicht)
- [Overview](#overview)
- [DocumentPart](#documentpart)
- [DocData](#docdata)
<!-- /TOC -->

### Overview
In der Overview sind folgende Daten des Dokuments abgespeichert:
 
-  Template Id
-  Internal Template Id
-  Document Id
-  Document LCID
-  UI LCID
-  Profile Id
-  Creation Mode
-  Pipeline Version

### DocumentPart
Zeigt den Inhalt vom Custom XML Part `OneOffixxDocumentPart`.<br />
Der `OneOffixxDocumentPart` ist derjenige Custom XML Part, in dem sich alle OneOffixx-Text-Elemente befinden. Die Anzeige des OneOffixxDocumentParts im Debugger kann also dazu verwendet werden, um sicherzustellen, dass gewisse OneOffixx-Text-Elemente "angekommen" sind (bzw. in Word mit Content Controls gebindet werden können).

Nachfolgend eine Liste der gängigsten OneOffixx-Text-Elemente, die im Debugger unter DocumentPart eingesehen werden können:

-  Dokument-Parameter
-  Profilinformationen
-  Empfängerinformationen
-  Interfaces
-  Skripts

Wichtig: Die Position der Dokument-Funktion "Debugger" beeinflusst, welche Daten sich zu der Zeit im DocumentPart befinden. Wenn sich z. B. der Debugger vor dem Dokument-Parameter befindet, werden im DocumentPart keine Dokument-Parameter-Informationen angezeigt.

Der Inhalt vom Custom XML Part `OneOffixxDocumentPart` wird wie folgt angezeigt:

```xml
<DataModel xmlns="">
      <Parameter windowwidth="750" windowheight="450" minwindowwidth="0" maxwindowwidth="0" minwindowheight="0" maxwindowheight="0">
        [...]
        <Text id="DocParam.Subject" row="0" column="0" columnspan="0" multiline="False" multilinerows="0" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[ ]]></Text>
        <DateTime id="DocParam.Date" lid="Deutsch (Schweiz)" format="d. MMMM yyyy" calendar="Gregor" row="0" column="0" columnspan="0" locked="False" label="" readonly="False" visible="True" tooltip="" tracked="False">2018-10-31T00:00:00Z</DateTime>
        <Text id="DocParam.Enclosures" row="0" column="0" columnspan="0" multiline="False" multilinerows="0" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[ ]]></Text>
        <Text id="DocParam.CopyTo" row="0" column="0" columnspan="0" multiline="False" multilinerows="0" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[ ]]></Text>
        [...]
      </Parameter>
      <Profile windowwidth="0" windowheight="0" minwindowwidth="0" maxwindowwidth="0" minwindowheight="0" maxwindowheight="0">
        [...]
        <Text id="Profile.Org.Title" row="0" column="0" columnspan="0" multiline="False" multilinerows="0" locked="False" label="Profile.Org.Title" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Basis-FirmaTest 1]]></Text>
        <Text id="Profile.Org.Web" row="0" column="0" columnspan="0" multiline="False" multilinerows="0" locked="False" label="Profile.Org.Web" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[basis.chTest 1]]></Text>
        <Text id="Profile.User.FirstName" row="0" column="0" columnspan="0" multiline="False" multilinerows="0" locked="False" label="Profile.User.FirstName" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Max]]></Text>
        <Text id="Profile.User.LastName" row="0" column="0" columnspan="0" multiline="False" multilinerows="0" locked="False" label="Profile.User.LastName" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Muster]]></Text>
        [...]
      </Profile>
      <Interfaces windowwidth="0" windowheight="0" minwindowwidth="0" maxwindowwidth="0" minwindowheight="0" maxwindowheight="0">
        <NodeGroup id="InterfaceDemo" row="0" column="0" columnspan="0" label="InterfaceDemo" visible="True">
          <Text id="ErstesFeld" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="ErstesFeld" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[1]]></Text>
          <Text id="ZweitesFeld" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="ZweitesFeld" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[2]]></Text>
          <Text id="DrittesFeld" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="DrittesFeld" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[3]]></Text>
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

