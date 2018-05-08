---
layout: page
title: Dokumentenpipeline
permalink: "docengine/de/pipeline/"
language: de
---

## Document Engine - Übersicht {% include anchor.html name="docengine-overview" %}

Die Document Engine ist das Herzstück der OneOffixx Applikation. 

Sie kommt sowohl im Server als auch im Client zum Einsatz und erstellt aus dem angeforderten "Template" und zusätzliche "Connect"-Daten das entsprechende Dokument.

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-overview.png "Document-Engine - Übersicht")

Im ersten Schritt werden die Daten und die Konfiguration geladen. Danach werden konfigurierte Dokumentfunktionen im __"Processing"-Schritt__ entsprechend aufgerufen. 
Auf der __["Connect - Functions"]({{ site.baseurl }}/connect/de/connect-functions/)__-Seite sind alle Dokumentfunktionen aufgelisted, welche über die Connect Schnittstelle parametrierbar sind.

{% include new-badge.html version="3.3" %}

Nach diesen Schritt wird das eigentliche Dokument erzeugt. Ab Version 3.3 wird zusätzlich geprüft, ob der Vorlage noch Untervorlagen angehangen sind. Sind Untervorlagen konfiguriert werden diese entsprechend der Bedingung und Reihenfolge eingefügt. Weitere Informationen zum Thema Untervorlagen sind [hier]({{ site.baseurl }}/docengine/de/subtemplates/) zu finden.

Falls __["Connect - Commands"]({{ site.baseurl }}/connect/de/connect-commands/)__ definiert wurden, werden diese nun durchlaufen. Hierdurch kann das generierte Dokument z.B. in ein PDF konvertiert werden oder auf ein Netzwerklaufwerk abgespeichert werden. Die einzelnen "Commands" werden der Reihe nach aufgerufen.

Am Ende geht das fertige Dokument wieder an den Aufrufer.
