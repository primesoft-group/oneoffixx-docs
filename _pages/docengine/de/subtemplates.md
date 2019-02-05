---
layout: page
title: Untervorlagen
permalink: "docengine/de/subtemplates/"
language: de
---

{% include new-badge.html version="3.3.1" %}

## Einstieg {% include anchor.html name="intro" %}

In OneOffixx können eine Vielzahl von unterschiedlichen Dateitypen als Vorlage hinterlegt werden. Eine der Hauptstärken von OneOffixx liegt im Verwalten von Microsoft Office Dateiformaten und insbesondere dem Word bzw. dem Open XML for Word-Processing-Format.

Wird in OneOffixx eine Vorlage erstellt und wird daraus ein Dokument generiert, wird der komplette Inhalt samt Kopf- und Fusszeile als ein einziger Abschnitt eingefügt. 
Hinweis: Dank dem [OneOffixx Vererbungssystem]({{ site.baseurl }}/docengine/de/inheritance/) ist es möglich, über eine Word-Vorlage die komplette Kopf- bzw. Fusszeile zu steuern, sodass man die ensprechenden Angaben jeweils zentral in den dafür vorgesehenen Vorlagentypen verwalten kann.

Möchte man nun aber unterschiedliche Abschnitte einfügen, z.&nbsp;B. um unterschiedliche Hoch-/Quer-Formate oder unterschiedliche Kopf- und Fussangaben umzusetzen, können die __Untervorlagen__ angewendet werden.

## Aufbau {% include anchor.html name="structure" %}

Eine Untervorlage entspricht vom Aufbau her einer normalen Vorlage. Sie verwendet denselben Vererbungsmechanismus, allerdings kann man einer Untervorlage __keine eigenen Dokumentfunktionen anhängen__. 
Benötigte Daten aus Dokumentfunktionen, z.&nbsp;B. Profildaten, müssen über die entsprechende Hauptvorlage hinzugefügt werden. 

Die Verknüpfung zwischen Untervorlagen und Hauptvorlagen erfolgt über den OneOffixx Vorlageneditor: 

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-subtemplate-overview-templaterelations.png "Document-Engine - Vorlageneditor")

__Verknüpfungsarten:__

OneOffixx kennt zwei verschiedene Verknüpfungsarten für Untervorlagen:

* "Bei Generierung": Diese Untervorlagen werden in der entsprechenden Reihenfolge automatisch bei der Dokumentgenerierung eingefügt. Es kann zusätzlich eine Bedingung angegeben werden, sodass z.&nbsp;B. je nach Option im Dokument-Parameter eine Untervorlage hinzugefügt wird oder nicht. 
* "Optional": Diese Untervorlagen stehen im generierten Dokument im OneOffixx Ribbon unter "Weitere Inhalte" zur Verfügung.

Jede Hauptvorlage kann mit mehreren Untervorlagen verküpft werden, wobei eine Untervorlage stets einem eigenen Abschnitt entspricht. Um eine Untervorlage zu erstellen, muss eine normale Word-Vorlage erstellt und diese als "Untervorlage" markiert werden. 

__Wichtig:__ Ist eine Vorlage einmal als "Untervorlage" markiert, kann das nicht mehr rückgängig gemacht werden! 

## Untervorlagen & Dokumentfunktionen {% include anchor.html name="documentfunctiondata" %}

Um Daten aus Dokumentfunktionen zu nutzen, wie z.&nbsp;B. Profildaten, muss man sicherstellen, dass die Dokumentfunktion "Profildaten" an der Hauptvorlage definiert ist. Wird danach der Vorlageneditor der Untervorlage geöffnet, kann der Word-Editor der Untervorlage mittels Auswahl einer Hauptvorlage aufgerufen werden:

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-subtemplate-overview-templaterelations_as_subtemplate.png "Document-Engine - Vorlageneditor für Untervorlagen")

## Bedingungen {% include anchor.html name="conditions" %}

Über den Vorlageneditor können auch Untervorlagen verknüpft werden, die nur integriert werden, falls eine entsprechende Bedingung erfüllt ist. Dafür ist es erforderlich, die Bedingung in JavaScript zu formulieren. Daten aus dem Dokument-Parameter können über eine API abgefragt werden, sodass z.&nbsp;B. eine Checkbox im Dokument-Parameter platziert werden kann. Nur wenn diese aktiv ist, wird ein bestimmtes Unterdokument eingefügt. 
 
## Dokumentgenerierungsprozess {% include anchor.html name="flow" %}

Das System der Untervorlagen ergänzt die bestehende [OneOffixx Dokumentpipeline]({{ site.baseurl }}/docengine/de/pipeline/):

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-subtemplate-overview.png "Document-Engine - Prozess")


 