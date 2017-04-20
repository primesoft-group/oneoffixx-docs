---
layout: page
title: Profil Daten
permalink: "docfunc/de/df/profiledata"
language: de
---

Die Dokumentfunktion ‘Profildaten’ wird benötigt damit die Vorlage auf die Daten aus dem Profil zugreifen kann. Dazu gehören alle Daten, die in den Einstellungen unter ‘Organisationseinheit’ und ‘Benutzer’ definiert wurden. Bei Bildern ist zu beachten, dass jedes Bild in den Profildaten einzeln angegeben werden muss. Dies dient zur Performanceoptimierung, da OneOffixx so nicht jedes Mal alle Bilder laden muss. In der Dokumentfunktion hat es zuunterst einige Beispiele, die zeigen wie man die Bilder angeben muss. Die einzige Ausnahme sind Unterschriftsbilder. Diese müssen nicht einzeln angegeben werden, sondern um auf diese zuzugreifen muss in der Zeile ‘IncludeSignatures’ das Attribut ‘withImage’ auf ‘true’ gesetzt werden. In derselben Zeile kann auch definiert werden, wie viele Signaturen möglich sind.
