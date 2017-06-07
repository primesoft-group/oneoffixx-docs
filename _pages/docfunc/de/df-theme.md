---
layout: page
title: Themes
permalink: "docfunc/de/df/theme"
language: de
---

In der Dokumentenfunktion **Themes** wird die Umschaltung zwischen farbige Darstellung und schwarz/weiss Darstellung der Logos und Schriftwelten im Dokument gesteuert.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/themeribbon.png)
 
Dazu gehörig müssen 2 Vorlagen erstellt werden, die Word Themes. 1x für Farbwahl, 1x für s/w-Wahl. Benannt werden diese standardmässig **Theme Basis farbig** und **Theme Basis SW**. Darin wird definiert, welche Schriften, Titel, Überschriften, Farbgruppen etc., im Dokument ausgegeben werden.
 
![x]({{ site.baseurl }}/assets/content-images/docfunc/de/themetemplate.png)

Beim Öffnen der Dokumentenfunktion wird zuerst die XML-Definition angezeigt. Mit Klick auf _im Fenster bearbeiten_ können Sie diese auf die Standardansicht umschalten. 

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/themeeditor.png)
 
Ab Version 3.1 kann die Konfiguration auch direkt im XML geschrieben werden.
In den 3 Reitern (Farbe/Graustufe/Schwarz/Weiss) wählen Sie aus, ob Dokumente die Standards farbig oder s/w sind, mittels anklicken der Checkbox (im XML =  `<Themes type="Color" default="true">`")

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/themeeditor2.png)
 
Wählen Sie das entsprechende «Theme» aus und setzen Sie für die entsprechenden Organisationseinheiten, für welche diese Einstellungen gelten, die Checkbox auf aktiv. 
(im XML = `<Theme id="13de0413-b312-42e7-b40b-5ce56691b042" default="true" organizationUnitId="44daf192-effd4-49dd-b5c5-9c3c5d466edd;2dfbeac9-bf6d-409c-9f96-e1501e55q953;60294b8a-ad40-41ec-bdef-c54ae4ccc8fe" />`) 
Das gleiche Vorgehen gilt für die Setzung der Informationen im s/w Modus. Die Variante «Graustufen» kann leer gelassen werden.
 
Im Bereich _Bilder_ mappen Sie das Bild welches angezeigt werden soll wenn das Dokument farbig oder s/w ist.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/thememapping.png) 

Dazu müssen in der Organisationseinheit die entsprechenden Logos (1x farbig, 1x s/w) hinterlegt sein.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/themeprofile.png)

