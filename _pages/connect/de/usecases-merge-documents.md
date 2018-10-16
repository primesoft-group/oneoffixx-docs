---
layout: page
title: Anwendungsfälle
subtitle: Zusammenführen von Dokumenten
permalink: "connect/de/usecases/merge-documents/"
language: de
---

OneOffixx ist in der Lage, mithilfe des globalen Befehls „Merge" ("zusammenführen"), verschiedene Dokumente desselben Typs miteinander zu verbinden. Jedes einzelne Dokument wird als OneOffixx Connect Entry übergeben. Client-seitig können sowohl bestehende (Angeben der DocumentLocation) als auch neue Dokumente (Angeben der TemplateId) miteinander verbunden werden. Server-seitig ist nur das Verbinden von neu erstellten Dokumenten möglich.

## Verbinden von zwei bestehenden Dokumenten:

```xml
<?xml version="1.0" encoding="utf-8"?>
<OneOffixxConnectBatch xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1">
  <Commands>
    <Command Name="Merge">
      <Parameters>
        <Add key="PageNumberStart">123</Add>
      </Parameters>
    </Command>
    <Command Name="DefaultProcess">
      <Parameters>
        <Add key="Start">true</Add>
      </Parameters>
    </Command>
  </Commands>
  <Entries>
    <OneOffixxConnect>
      <Arguments>
        <DocumentLocation>c:\Temp\Dok1.docx</DocumentLocation>
      </Arguments>
    </OneOffixxConnect>
    <OneOffixxConnect>
      <Arguments>
        <DocumentLocation>c:\Temp\Dok2.docx</DocumentLocation>
      </Arguments>
    </OneOffixxConnect>
    		...
    	</Entries>
</OneOffixxConnectBatch>
```

## Verbinden von zwei zu generierenden Dokumenten:

```xml
<?xml version="1.0" encoding="utf-8"?>
<OneOffixxConnectBatch xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1">
  <Commands>
    <Command Name="Merge">
      <Parameters>
        <Add key="PageNumberStart">123</Add>
      </Parameters>
    </Command>
    <Command Name="DefaultProcess">
      <Parameters>
        <Add key="Start">true</Add>
      </Parameters>
    </Command>
  </Commands>
  <Entries>
    <OneOffixxConnect>
      <Arguments>
        <TemplateId>19d9d75d-0177-4427-a739-115a2df0842e</TemplateId>
      </Arguments>
    </OneOffixxConnect>
    <OneOffixxConnect>
      <Arguments>
        <TemplateId>19d9d75d-0177-4427-a739-115a2df0841e</TemplateId>
      </Arguments>
    </OneOffixxConnect>
    		...
    	</Entries>
</OneOffixxConnectBatch>
```

## Beide Varianten in einem Beispiel:

```xml
<?xml version="1.0" encoding="utf-8"?>
<OneOffixxConnectBatch xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1">
  <Commands>
    <Command Name="Merge">
      <Parameters>
        <Add key="PageNumberStart">123</Add>
      </Parameters>
    </Command>
    <Command Name="DefaultProcess">
      <Parameters>
        <Add key="Start">true</Add>
      </Parameters>
    </Command>
  </Commands>
  <Entries>
    <OneOffixxConnect>
      <Arguments>
        <DocumentLocation>c:\Temp\Dok1.docx</DocumentLocation>
      </Arguments>
    </OneOffixxConnect>
    <OneOffixxConnect>
      <Arguments>
        <TemplateId>19d9d75d-0177-4427-a739-115a2df0841e</TemplateId>
      </Arguments>
    </OneOffixxConnect>
    		...
    	</Entries>
</OneOffixxConnectBatch>
```
