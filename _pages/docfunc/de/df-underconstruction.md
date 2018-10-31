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

### DocData

Im DocData-Ribbon wird das gesamte Word-File in XML-Form angezeigt. Dabei werden die Files, die sich jeweils im gezippten Word-File befinden, als einzelne Packages aufgeführt.

Das File 'document.xml' im Verzeichnis 'Word' wird z. B. wie folgt angezeigt:

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

