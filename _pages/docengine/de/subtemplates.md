---
layout: page
title: Untervorlagen
permalink: "docengine/de/subtemplates/"
language: de
---

{% include new-badge.html version="3.3" %}

## Einstieg {% include anchor.html name="intro" %}

In OneOffixx können eine Vielzahl von unterschiedlichen Dateitypen als "Vorlage" hinterlegt werden. Eine der Hauptstärken von OneOffixx liegt im Verwalten von Microsoft Office Dateiformaten und insbesondere dem Microsoft Word bzw. dem Open XML for Word-Processing Format.

Erstellt man im OneOffixx eine Vorlage und generiert man daraus ein Dokument wird der komplette Inhalt samt Kopf- und Fusszeile über einen einzigen Abschnitt eingefügt. 
Hinweis: Über das OneOffixx [Vererbungssystem]({{ site.baseurl }}/docengine/de/inheritance/) kann man z.B. über eine Word-Format-Vorlage den kompletten Kopf- bzw. Fussbereit steuern, sodass man die ensprechenden Angaben jeweils zentral in den dafür vorgesehenen Vorlagentypen steuern kann.

Möchte man nun aber unterschiedliche Abschnitte einfügen, z.B. um unterschiedlichen Hoch-/Quer-Formaten oder unterschiedlichen Kopf- und Fussangaben zu realisieren, kann man auf das Feature der __Untervorlagen__ zurückgreifen.

## Aufbau {% include anchor.html name="structure" %}

Eine Untervorlage entspricht vom Aufbau her einer normalen Vorlage und verwendet denselben Vererbungsmechanismus, allerdings kann man einer Untervorlage keine eigenen Dokumentfunktionen anhängen. 

...
