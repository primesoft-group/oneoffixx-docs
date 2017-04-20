---
layout: page
title: Übersicht
permalink: "concepts/de/overview/"
language: de
---

# Systemübersicht {% include anchor.html name="system" %}

Folgende Systemübersicht zeigt schematisch welche Kommunikationspfade OneOffixx unterstützt. 

![x]({{ site.baseurl }}/assets/content-images/concepts/de/system-overview.png "Architektur")

Zentrale Komponenten ist die Document-Engine welche sowohl auf dem Client als auch auf dem Server implementiert ist und folgende Hauptmerkmale besitzt:

* __[Dokumenten Pipline]({{ site.baseurl }}/docengine/de/pipeline)__ und Dokumentfunktionen. 

* __[Dokument Vererbungskonzept]({{ site.baseurl }}/docengine/de/inheritance)__ zum Beispiel mit den Style-, Format- und Virtuelle Vorlagen.

*  __[Versionierung von Vorlagen]({{ site.baseurl }}/docengine/de/versioncontrol)__ für den Vorlagen-Layouter


Für die Schnittstellenbeschreibung stehen zwei Schnittstellen im Fokus:

* Die Fachapplikaton kann OneOffixx mit unterschiedlichen Methoden aufrufen: __[Connect Verarbeitung auf dem Client]({{ site.baseurl }}/connect/de/usage#client)__

* Die Fachapplikaton ruft den OneOffixx Document Creation Server auf: __[Connect Verarbeitung auf dem Server]({{ site.baseurl }}/connect/de/usage#server)__

