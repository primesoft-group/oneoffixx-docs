---
layout: page
title: Global Configuration Provider
permalink: "docfunc/de/df/globalconfig"
language: de
---

Die **Globalen" Provider gehören nicht zur Klasse der Dokumentfunktionen sondern sind Globale Container die ihre Daten allen anderen Dokumentfunktionen zur Verfügung stellen. Deshalb kann ein Globaler Provider nie direkt einer Vorlage zugeordnet werden.

Im GlobalConfigurationProvider werden alle Informationen/Konfigurationen (unterteilt in Gruppen wie Config, Scripts, SnippetScripts, Formatting, Adressproviderkonfigurationen, etc.) abgelegt, die z.B. in mehreren Vorlagen verwendet werden. 
Der Vorteil liegt darin, dass die genannten Informationen bei Bedarf nur an einem Ort geändert werden müssen. Würde z.B. die Adressproviderkonfiguration in jede Vorlage eingebaut, müsste bei einer Anpassung jede Vorlage einzeln bearbeitet werden.
Die Möglichkeiten der Anwendung ist sehr umfangreich und vielfältig.

In den Beispielen ist zudem sichtbar, dass die Bezeichnungen in den globalen Übersetzungsprovider ausgelagert wurde. Damit kann bei mehrsprachigen Umgebungen sichergestellt werden, dass die Konfiguration in jeder Sprache identisch ist.
