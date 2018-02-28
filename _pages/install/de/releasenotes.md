---
layout: page
title: Releasenotes
permalink: "install/de/releasenotes/"
language: de
---

Benötigen Sie die neuste OneOffixx Version wenden Sie sich bitte an unseren [Support](http://oneoffixx.com/services/support/).

<!-- TOC -->

- [OneOffixx V 3.3.10160 <span class="label label-success">Released</span>](#oneoffixx-v-3310160-span-classlabel-label-successreleasedspan)
    - [Unterdokumente](#unterdokumente)
    - [Textbausteine](#textbausteine)
    - [Betriebsarten](#betriebsarten)
    - [Dokumentparameter](#dokumentparameter)
    - [Aktualisierungshinweis](#aktualisierungshinweis)
- [OneOffixx Version 3.0 - 3.2](#oneoffixx-version-30---32)
- [OneOffixx Version 2.3.0 - 2.4](#oneoffixx-version-230---24)

<!-- /TOC -->

# OneOffixx V 3.3.10160 <span class="label label-success">Released</span>

Willkommen zum Februar Release 3.3 von OneOffixx. Der Release 3.3 beinhaltet wichtige Neuerungen für den Layouter und den Betrieb.

Hier einige Highlights von diesem Release:
* [Unterdokumente](#unterdokumente) - Das Konzept wurden komplett überarbeitet.
* [Textbausteine](#textbausteine) - Bessere Visualisierung und bessere Import / Export Möglichkeiten
* [Betriebsarten](#betriebsarten) - Vorbereitung auf SaaS 
* [Dokumentparameter](#dokumentparameter) - Neuer Syntax anstelle von CustonDataNode, Collections, Images. JavaScript Support
* [Aktualisierungshinweis](#Aktualisierungshinweis) - CI/CD Check alter Dokumente

## Unterdokumente
In der vorherigen Version von OneOffixx wurden Unterdokumente in den Vorlagen selbst verwaltet. Neu werden die Abhängigkeiten der Unterdokumente in der Datenbank verwaltet. Dadurch ist es möglich Unterdokumente via Dokumentparameter ein zu blenden.
![subdocuments]({{ site.baseurl }}/assets/content-images/releasenotes/subdocuments.gif)

## Textbausteine
Die neue Visualisierung der Textbausteine zeigt in zwei Ansichten auf, wie Textbausteine in den Vorlagen zur Verwendung kommen. In der Ansicht *Snippet Perspektive* werden alle Vorlagen angezeigt die einen Textbaustein verwenden. In der Ansicht *Template Perspective* werden alle Textbausteine angezeigt die eine Vorlage verwendet. Die Nummer hinter den Textbausteinen zeigt an ob die Textbausteine wirklich verwendet werden. Durchsucht werden Scripts und Vorlagen.
![Snippet Usage]({{ site.baseurl }}/assets/content-images/releasenotes/SnippetUsage.gif)

## Betriebsarten
OneOffixx kennt nun zwei "Betriebsarten: "OnPremise" - klassisch mit Windows Authentifierung. "Cloud" - neu - Authentifizierung erfolgt nur noch über den IdentityServer, welcher wieder ein Provider-Modell bietet, sodass man über Office 365, Microsoft Account oder klassische Windows-Anmeldungen nutzen kann.

## Dokumentparameter
Für komplexe Dialog wurde der Dokumentparameter Dialog massiv ausgebaut. Es ist nun möglich Fehlervalidierung über mehrere Felder zu machen. Weiter lassen sich mit JavaScript die Dokumentparameter miteinander in Abhängigkeit setzen.

## Aktualisierungshinweis
Pro Vorlage kann neu ein Ablaufdatum festgelegt werden. Wird ein altes Dokument geöffnet prüft OneOffixx ob das Dokumnent auf der aktuellsten Version der Vorlage basiert. Ist dies nicht der Fall, wird dem Benutzer mit einem Hinweis darauf aufmerksam gemacht.
![Aktualisierungshinweis]({{ site.baseurl }}/assets/content-images/releasenotes/Aktualisierungshinweis.PNG)

# OneOffixx Version 3.0 - 3.2
[Finden Sie hier die Releasenotes der OneOffixx Version 3]({{ site.baseurl }}/install/de/releasenotesv3)

# OneOffixx Version 2.3.0 - 2.4
[Finden Sie hier die Releasenotes der OneOffixx Version 2]({{ site.baseurl }}/install/de/releasenotesv2)