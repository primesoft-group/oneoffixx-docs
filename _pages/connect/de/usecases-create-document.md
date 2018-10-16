---
layout: page
title: Anwendungsfälle
subtitle: Dokument erstellen
permalink: "connect/de/usecases/create-document/"
language: de
---

In diesem Beispiel soll aus einer Vorlage ein neues Dokument in einer spezifischen Dokumentensprache erstellt werden.

 {% include new-badge.html version="3.3" %}
 Ab Version 3.3 kann das Argument "Editor" verwendet werden, wenn anstelle eines Dokumentes (.docx) sich die Vorlage im Editor (.dotx) öffnen soll.

```xml
<?xml version="1.0" encoding="utf-8"?>
<OneOffixxConnectBatch xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1">
  <Entries>
    <OneOffixxConnect>
      <Arguments>
        <TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
        <LanguageLcid>2055</LanguageLcid>
        <Editor>true</Editor>
      </Arguments>
    </OneOffixxConnect>
  </Entries>
</OneOffixxConnectBatch>
```

