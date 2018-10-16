---
layout: page
title: Anwendungsfälle
subtitle: Dokument an einen definierten Ort speichern
permalink: "connect/de/usecases/create-document-on-location/"
language: de
---

Das erzeugte Dokument wird an einen definierten Ort gespeichert. Der Befehl „SaveAs" speichert das Dokument unverändert.

```xml
<?xml version="1.0" encoding="utf-8"?>
<OneOffixxConnectBatch xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1">
  <Entries>
    <OneOffixxConnect>
      <Arguments>
        <TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
        <LanguageLcid>2055</LanguageLcid>
      </Arguments>
      <Commands>
        <Command Name="SaveAs">
          <Parameters>
            <Add key="Filename">\\e205\share\organization\...\documentxyz.dotx</Add>
            <Add key="Overwrite">true</Add>
            <Add key="CreateFolder">true</Add>
          </Parameters>
        </Command>
        <Command Name="DefaultProcess">
          <Parameters>
            <Add key="Start">False</Add>
          </Parameters>
        </Command>
      </Commands>
    </OneOffixxConnect>
  </Entries>
</OneOffixxConnectBatch>
```

Soll daraus ein Dokument erstellt werden, muss vorgängig das Kommando „ConvertToDocument" aufgerufen werden. Hinweis: Der Befehl "DefaultProcess" der deaktiviert ist, bewirkt, dass das generierte Dokument nicht geöffnet wird. Das Dokument wird also generiert, gespeichert und dabei nicht im Word geöffnet.

```xml
<?xml version="1.0" encoding="utf-8"?>
<OneOffixxConnectBatch xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1">
  <Entries>
    <OneOffixxConnect>
      <Arguments>
        <TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
        <LanguageLcid>2055</LanguageLcid>
      </Arguments>
      <Commands>
        <Command Name="ConvertToDocument" />
        <Command Name="SaveAs">
          <Parameters>
            <Add key="Filename">\\e205\share\organization\...\documentxyz.docx</Add>
            <Add key="Overwrite">true</Add>
            <Add key="CreateFolder">true</Add>
          </Parameters>
        </Command>
        <Command Name="DefaultProcess">
          <Parameters>
            <Add key="Start">False</Add>
          </Parameters>
        </Command>
      </Commands>
    </OneOffixxConnect>
  </Entries>
</OneOffixxConnectBatch>
```