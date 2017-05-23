---
layout: page
title: Aktenverzeichnis
permalink: "docfunc/de/df/fileindex"
language: de
---

Mit dieser Dokumentfunktion können Titelblätter für Aktenmappen erstellt werden. In der Konfiguration wird ein Fenster konfiguriert, das beim Öffnen des Dokuments erscheint. Das gesamte Dokument besteht aus einem extended Binding, das anhand der im Dialog eingegebenen Informationen das gesamte Dokument erstellt.

So sieht der Aufbau der Konfiguration aus:

```xml
<Folders>
    <Folder DisplayName="Mappe weiss" Description="Beilagen zum Antrag an den Regierungsrat" />
    <Folder DisplayName="Mappe rot" Description="Geheime Dokumente" />
    <Folder DisplayName="Mappe gelb" Description="Antrag an den Stadtpräsidenten" />
    <Folder DisplayName="Benutzerdefiniert" IsDescriptionChangeable="true" />
  </Folders>
  <FolderProperties>
    <Property DisplayName="Geschäftsbezeichnung" />
    <Property DisplayName="Sachverhalt/Vorhaben/Titel" />
    <Property DisplayName="Geschäftsnummern" />
  </FolderProperties>
  <DefaultFileNames>
    <FileName DisplayText="Baugesuch - Grundriss" />
    <FileName DisplayText="Grundstücksschätzung" />
    <FileName DisplayText="Report Brandschutzkontrolle" />
  </DefaultFileNames>
```

Diese Konfiguration resultiert in folgendem Fenster:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/FileIndex_Window.png )

In den extended Bindings kann mit Hilfe der "for-each" Tags für jede Auswahl ein eigenes Titelblatt erstellt werden. 