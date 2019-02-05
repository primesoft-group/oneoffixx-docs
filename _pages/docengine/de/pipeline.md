---
layout: page
title: Dokumentenpipeline
permalink: "docengine/de/pipeline/"
language: de
---

## Document Engine - Übersicht {% include anchor.html name="docengine-overview" %}

Die Document Engine ist das Herzstück des OneOffixx Programms. Sie kommt sowohl im Server als auch im Client zum Einsatz und erstellt aus der angeforderten Vorlage und den zusätzlichen "Connect"-Daten das entsprechende Dokument.

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-overview.png "Document-Engine - Übersicht")

Im ersten Schritt werden die Daten und die Konfiguration geladen. Danach werden konfigurierten Dokumentfunktionen im __"Processing"-Schritt__ entsprechend aufgerufen. Auf der __["Connect - Functions"]({{ site.baseurl }}/connect/de/connect-functions/)__-Seite sind alle Dokumentfunktionen aufgelistet, die über die Connect Schnittstelle parametrierbar sind.

{% include new-badge.html version="3.3.1" %}

Nach diesen Schritt wird das eigentliche Dokument generiert. Ab Version 3.3.1 wird zusätzlich geprüft, ob der Vorlage noch Untervorlagen angehängt sind. Sind Untervorlagen konfiguriert, werden diese entsprechend der Bedingung und Reihenfolge eingefügt. Weitere Informationen zum Thema Untervorlagen sind [hier]({{ site.baseurl }}/docengine/de/subtemplates/) zu finden.

Falls __["Connect - Commands"]({{ site.baseurl }}/connect/de/connect-commands/)__ definiert wurden, werden diese nun durchlaufen. Dadurch kann das generierte Dokument z.&nbsp;B. in ein PDF konvertiert oder auf ein Netzwerklaufwerk abgespeichert werden. Die einzelnen Befehle (Commands) werden der Reihe nach aufgerufen.

Am Ende geht das fertiggestellte Dokument wieder an den Aufrufer.
