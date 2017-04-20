---
layout: page
title: Vererbungskonzept
permalink: "docengine/de/inheritance/"
language: de
---

## Document Engine - Vererbungssystem {% include anchor.html name="docengine-inheritance" %}

Jede Vorlage bzw. Vorlagentyp bringt einen Teil der spezifischen Merkmale des Enddokumentes mit. Zum Beispiel liefert das "Style" Dokument alle Style Merkmale des Hauptdokumentes mit. Die verschiedenen Vorlagentypen können so beliebig kombiniert und jederzeit ausgetauscht oder aktualisiert werden. Dadurch können Redundanzen im Vorlagenbau vermieden werden. Die Dokumente werden immer zur Laufzeit neu generiert.

Diese Grafik zeigt die __maximale__ Vererbungsstufe - jede Ebene ist optional.

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-inheritance.png "Document-Engine - Vererbungssystem")

Die Dokumentenpipeline enthält ein vorlagenspezifisches Liste von Funktionen, die als PlugIns realisiert sind und beim Starten von OneOffixx geladen werden. 

Welche Dokumentfunktionen in welcher Reihenfolge in einer Vorlage verwendet werden, wird in OneOffixx im Vorlagenbearbeitungsmodus vom Vorlagenbauer festgelegt. 

Dokumentfunktionen enthalten für sich geschlossene Prozeduren, die auf das Dokument, Schnittstellen etc. angewendet werden.