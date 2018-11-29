---
layout: page
title: Global Print Configuration Provider
permalink: "docfunc/de/df/globalprintconfigurationprovider"
language: de
---

Diese Dokument-Funktion regelt auf globaler Ebene die Druckerkonfiguration. Sie regelt, welche Papierarten verfügbar sind.

__Konfiguration:__
```xml
<Configuration>
  <Papers>
    <Paper Id="AECA0DBD-4C1A-4DD1-8E21-8299319167B2" Logo="false" Color="false" Format="A4" Default="true">
      <Name>Normal</Name>
      <DisplayName>Standardpapier A4</DisplayName>
      <Description>Standardpapier für überall</Description>
    </Paper>
    <Paper Id="FAC3862B-6E3F-4B04-B5BF-B45E486C08E6" Logo="true" Color="true" Format="A4" Orientation="Portrait" Lcid="2055">
      <Name>Logo</Name>
      <DisplayName>Logopapier</DisplayName>
      <Description>Logopapier (nur ohne Logo benutzen)</Description>
    </Paper>
  </Papers>
</Configuration>
```