---
layout: page
title: ARTS Module
permalink: "docfunc/de/df/artsmodule"
language: de
---

In der Dokumentfunktion ‘ARTS Module’ kann der Upload von Dokumenten in das Universalarchiv ARTS von Uptime konfiguriert werden. Mittels Tastenkombination '**ALT + i**' oder mit einem Klick auf die Schaltfläche '**Extras**' '**In ARTS DMS speichern**’ wird das Dokument im ARTS abgelegt.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/artsmodulesave.png)

Wie im nachfolgenden Beispiel aufgezeigt wird, können unterschiedliche nebst dem Ablageortes des ARTS – Upload Tools Argumente konfiguriert werden, welche beim Upload in das Archiv mitgegeben werden. 

```xml
<ARTSConfiguration>
    <Command type="shell">
      <Uri>N:\Arts\products\ARTSCmdTool\bin\ARTSCmdTool.app\ARTSCmdTool.exe</Uri>
      <Arguments>
        <Argument name="-archive" />
        <Argument name="-silent" />
        <Argument name="-instanceName" elementId="CustomElements.PuM.getInstanceName" connector=" "></Argument>
        <Argument name="ARCHIV" />
        <Argument name="-u" quotes="true">{file}</Argument>
        <Argument name="-a" />
        <Argument name="Name" elementId="Name" connector="=" quotes="true" />
        <Argument name="Vorname" elementId="FirstName" connector="=" quotes="true" />
        <Argument name="Geburtsdatum" elementId="GebDatum" connector="=" quotes="true" />
        <Argument name="Geschlecht" elementId="Geschlecht" connector="=" quotes="true" />
        <Argument name="Bezeichnung" elementId="ARTSDocName" connector="=" quotes="true" />
        <Argument name="Geschäfts-Nr" connector="=" quotes="true">0</Argument>
        <Argument name="Datum" connector="=" quotes="true">{date}</Argument>
        <Argument name="Klassifizierung" elementId="Classification" connector="=" quotes="true" />
        <Argument name="Dossiertyp" elementId="Dossiertyp" connector="=" quotes="true" />
      </Arguments>
    </Command>
  </ARTSConfiguration>

```