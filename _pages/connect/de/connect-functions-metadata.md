---
layout: page
title: "Function: MetaData"
subtitle: Daten im Dokument unter Dokumenteigenschaften setzen
permalink: "connect/de/functions/metadata/"
language: de
---

Die Fachapplikation übergibt via Schnittstelle Metadaten, die in den Dokumenteigenschaften gespeichert werden sollen.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Entries>
    <OneOffixxConnect>
      <Arguments>
        <TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
        <LanguageLcid>2055</LanguageLcid>
      </Arguments>
      <Function name="MetaData" id="c364b495-7176-4ce2-9f7c-e71f302b8096">
        <Arguments>
          <Value key="SampleKeyForThisInt" type="int">1</Value>
          <Value key="SampleKeyForThisString" type="string">Sample Text</Value>
          <Value key="SampleKeyForThisDouble" type="double">99.99</Value>
          <Value key="SampleKeyForThisBool" type="bool">true</Value>
          <Value key="SampleKeyForThisDate" type="date">2017-01-01</Value>
        </Arguments>
      </Function>
    </OneOffixxConnect>
  </Entries>
</OneOffixxConnectBatch>
```
{% include alert.html type="warning" text="Diese Funktion steht erst ab der Version 2.3.40160 auch serverseitig zur Verfügung. Ab Version 2.3.50000 wird der Datentyp "double" und "date" unterstützt." %}
