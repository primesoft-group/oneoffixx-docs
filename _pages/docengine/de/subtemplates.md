---
layout: page
title: Untervorlagen
permalink: "docengine/de/subtemplates/"
language: de
---

{% include new-badge.html version="3.3.1" %}

## Einstieg {% include anchor.html name="intro" %}

In OneOffixx können eine Vielzahl von unterschiedlichen Dateitypen als "Vorlage" hinterlegt werden. Eine der Hauptstärken von OneOffixx liegt im Verwalten von Microsoft Office Dateiformaten und insbesondere dem Microsoft Word bzw. dem Open XML for Word-Processing Format.

Erstellt man im OneOffixx eine Vorlage und generiert man daraus ein Dokument wird der komplette Inhalt samt Kopf- und Fusszeile als ein einziger Abschnitt eingefügt. 
Hinweis: Über das [OneOffixx Vererbungssystem]({{ site.baseurl }}/docengine/de/inheritance/) ist es möglich über eine Word-Format-Vorlage den kompletten Kopf- bzw. Fussbereich zu steuern, sodass man die ensprechenden Angaben jeweils zentral in den dafür vorgesehenen Vorlagentypen verwalten kann.

Möchte man nun aber unterschiedliche Abschnitte einfügen, z.B. um unterschiedlichen Hoch-/Quer-Formaten oder unterschiedlichen Kopf- und Fussangaben zu realisieren, kann man auf das Feature der __Untervorlagen__ zurückgreifen.

## Aufbau {% include anchor.html name="structure" %}

Eine Untervorlage entspricht vom Aufbau her einer normalen Vorlage und verwendet denselben Vererbungsmechanismus, allerdings kann man einer Untervorlage __keine eigenen Dokumentfunktionen anhängen__. 
Benötigte Dokumentfunktionendaten, z.B. Profildaten, müssen über die entsprechende Hauptvorlage hinzugefügt werden. 

Die Verknüpfung zwischen Untervorlagen und Hauptvorlagen erfolgt über den OneOffixx Vorlageneditor: 

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-subtemplate-overview-templaterelations.png "Document-Engine - Vorlageneditor")

__Verknüpfungsarten:__

OneOffixx kennt zwei verschiedene Verknüpfungsarten für Untervorlagen:

* "Dokumenterzeugung": Diese Untervorlagen werden in der entsprechenden Reihenfolge automatisch bei der Dokumentgenerierung eingefügt. Es kann zusätzlich eine Bedingung angegeben werden, sodass man z.B. je nach Option im Dokumentparameter eine Untervorlage hinzufügen kann oder nicht. 
* "Optionale Untervorlage": Diese Untervorlagen stehen als "Weitere Inhalte" im OneOffixx Word Addin zur Verfügung.

Jede Hauptvorlage kann mit mehreren Untervorlagen verküpft werden, wobei eine Untervorlage stets einen eigenen Abschnitt entspricht.

Um eine Untervorlage zu erstellen muss man eine normale Word-Vorlage erstellen und diese als "Untervorlage" markieren. 

__Wichtig:__ Ist eine Vorlage einmal als "Untervorlage" markiert ist dies nicht mehr änderbar! 

## Untervorlagen & Dokumentfunktionen {% include anchor.html name="documentfunctiondata" %}

Um Dokumentfunktiondaten zu nutzen, wie z.B. Profildaten, muss man sicherstellen, dass die Profil-Dokumentfunktion an der Hauptvorlage definiert ist. Öffnet man danach den Vorlageneditor der Untervorlage kann man den Editor im Kontext der jeweiligen Hauptvorlage aufrufen:

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-subtemplate-overview-templaterelations_as_subtemplate.png "Document-Engine - Vorlageneditor für Untervorlagen")

## Bedingungen {% include anchor.html name="conditions" %}

Über den Vorlageneditor kann man auch Untervorlagen verknüpfen, welche nur integriert werden, falls eine entsprechende Bedingung erfüllt ist. Hierfür ist es erforderlich die Bedingung in Javascript zu formulieren. Daten aus dem Dokumentparameter können über eine API abgefragt werden, sodass man z.B. eine Checkbox im Dokumentparameter platzieren kann und nur wenn diese aktiv ist, wird ein bestimmtes Unterdokument eingefügt. 
 
## Dokumentgenerierungsprozess {% include anchor.html name="flow" %}

Das Untervorlagen-System ergänzt die bestehende [OneOffixx Dokumentpipeline]({{ site.baseurl }}/docengine/de/pipeline/):

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-subtemplate-overview.png "Document-Engine - Prozess")


 