---
layout: page
title: XML-Daten Injektor
permalink: "docfunc/de/df/customxmlpartsinjector"
language: de
---

Über den XML-Daten Injektor kann statisches XML definiert werden, das einem Dokument im Hintergrund mitgegeben wird. Dies wird vorallem gebraucht, um externen Schnittstellen das Identifizieren von Vorlagen zu ermöglichen.

Der Aufbau sieht folgendermassen aus:

```xml
<Parts>
  <Part>
    <MyCustomXmlPart1>Part 1</MyCustomXmlPart1>
  </Part>
  <Part>
    <MyCustomXmlPart2>
      <CanHostNestedElements>
        Sample Content
      </CanHostNestedElements>
    </MyCustomXmlPart2>
  </Part>
</Parts>
```