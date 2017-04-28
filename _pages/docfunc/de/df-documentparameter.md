---
layout: page
title: Dokumentenparameter
permalink: "docfunc/de/df/documentparameter"
language: de
---

In der Dokumentfunktion ‘Dokument Parameter’ kann die Eingabemaske konfiguriert werden, die beim Anwählen einer Vorlage erscheint. Die Konfiguration kann grob in zwei Teile unterteilt werden: oben bei den ‘DataNodes’ werden die Nodes definiert, auf die in der ‘View’ im unteren Teil zugegriffen wird. In der View wird das Aussehen des Dokumentparameters festgelegt.

Eine der ersten Zeilen ist die CustomContentSection. Darin können die Grösse und Name des Dokument Parameters festgelegt werden. Über das 'Name' Attribut kann der Fenstername gewählt werden. Mit 'WindowWidth' und 'WindowHeight' können die Breite, resp. die Höhe des Fensters angepasst werden.

Beispiel:
`<CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">`