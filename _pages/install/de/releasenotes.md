---
layout: page
title: Releasenotes
permalink: "install/de/releasenotes/"
language: de
---

Benötigen Sie die neuste OneOffixx Version, wenden Sie sich bitte an unseren [Support](http://oneoffixx.com/services/support/).

<!-- TOC -->

- [OneOffixx V 3.3.10252 <span class="label label-success">Released</span>](#oneoffixx-v-3310252-span-classlabel-label-successreleasedspan)
    - [Unterdokumente](#unterdokumente)
    - [Textbausteine](#textbausteine)
    - [Betriebsarten](#betriebsarten)
    - [Dokumentparameter](#dokumentparameter)
    - [Aktualisierungshinweis](#aktualisierungshinweis)
- [OneOffixx Version 3.1 - 3.2](#oneoffixx-version-31---32)
- [OneOffixx Version 2.3.4 - 2.3.5](#oneoffixx-version-234---235)

<!-- /TOC -->

# OneOffixx V 3.3.10252 <span class="label label-success">Released</span>

Willkommen zum Release 3.3.1 von OneOffixx. Der Release 3.3.1 beinhaltet wichtige Neuerungen für den Vorlagenbearbeiter und den Betrieb.

Hier einige Highlights von diesem Release:
* [Unterdokumente](#unterdokumente) - Das Konzept wurden komplett überarbeitet.
* [Textbausteine](#textbausteine) - Bessere Visualisierung und bessere Import-/ Export-Möglichkeiten
* [Betriebsarten](#betriebsarten) - Vorbereitung auf SaaS (Software as a Service)
* [Dokumentparameter](#dokumentparameter) - Neue Syntax anstelle von CustonDataNode, Collections, Images und JavaScript Support
* [Aktualisierungshinweis](#Aktualisierungshinweis) - CI/CD-Check von alten Dokumenten

## Unterdokumente
In der früheren Version von OneOffixx wurden Unterdokumente in den Vorlagen selbst verwaltet. Neu werden die Abhängigkeiten der Unterdokumente in der Datenbank verwaltet. Dadurch ist es möglich, Unterdokumente via Dokumentarameter einzublenden.
![subdocuments]({{ site.baseurl }}/assets/content-images/releasenotes/subdocuments.gif)

## Textbausteine
Die neue Visualisierung der Textbausteine zeigt in zwei Ansichten auf, wie Textbausteine in den Vorlagen zur Verwendung kommen. In der Ansicht *Snippet Perspektive* werden alle Vorlagen angezeigt die einen Textbaustein verwenden. In der Ansicht *Template Perspective* werden alle Textbausteine angezeigt die eine Vorlage verwendet. Die Nummer hinter den Textbausteinen zeigt an ob die Textbausteine wirklich verwendet werden. Durchsucht werden Scripts und Vorlagen. Die Textbausteine werden ausschliesslich via Dashboard von OneOffixx importiert und exportiert. Eine Integration im Client ist nicht vorgesehen.
![Snippet Usage]({{ site.baseurl }}/assets/content-images/releasenotes/SnippetUsage.gif)

## Betriebsarten
OneOffixx kennt jetzt zwei Betriebsarten: "OnPremise" - klassisch mit Windows Authentifizierung. "Cloud" - neu - die Authentifizierung erfolgt nur noch über den Identity-Server, der wieder ein Provider-Modell bietet, sodass man OneOffixx über Office 365, Microsoft Account oder der klassischen Windows-Anmeldung nutzen kann.

## Dokumentparameter
Für komplexe Dialoge wurde der Dokument-Parameter-Dialog massiv ausgebaut. Er kann neu aus mehreren Seiten bestehen, was eine grössere Übersicht bei grossen Formularen ermöglicht. Weiter können Validierungen gemacht werden. Die Dialoge lassen sich mit JavaScript miteinander in Abhängigkeit setzen.

## Aktualisierungshinweis
Pro Vorlage kann neu ein Ablaufdatum festgelegt werden. Wird ein altes Dokument geöffnet, prüft OneOffixx, ob das Dokumnent auf der aktuellsten Version der Vorlage basiert. Ist das nicht der Fall, wird der Benutzer mit einem Hinweis darauf aufmerksam gemacht.
![Aktualisierungshinweis]({{ site.baseurl }}/assets/content-images/releasenotes/Aktualisierungshinweis.PNG)

# OneOffixx Version 3.1 - 3.2
[Finden Sie hier die Releasenotes der OneOffixx Version 3]({{ site.baseurl }}/install/de/releasenotesv3)

# OneOffixx Version 2.3.4 - 2.3.5
[Finden Sie hier die Releasenotes der OneOffixx Version 2]({{ site.baseurl }}/install/de/releasenotesv2)