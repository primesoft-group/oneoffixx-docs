---
layout: default
title: XML Schema
permalink: "connect/de/xml-schema/"
---

## Namespace

Der Namespace für OneOffixx Connect lautet 

http://schema.oneoffixx.com/OneOffixxConnectBatch/1

wobei die hinterste Nummer der Major-Version entspricht. Die Minor Version steht in Global Settings (Key="Version" Value ="XXX")

## Validierung

Um eine OneOffixx Connect zu validieren resp. zu prüfen, kann dies via Prozessaufruf mit dem Parameter /ValidateConnector erzielt werden.
Beispielaufruf:

c:\\program…\OneOffixx.exe /KeepConnector /ValidateConnector /connect XYZDatei.xml

Es ist zu beachten, dass hierbei das Connect-File nicht verarbeitet, sondern geprüft wird. Im produktiven Betrieb, empfielt sich eine ständige Validierung aus Performancegründen nicht.

## OneOffixx Connect Batch

-- IMG --

Enthält eine Batch Liste mit OneOffixx Connect Strukturen. Ein OneOffixx Connect entspricht einem OneOffixx Dokument.

## Global Settings

Diese Struktur enthält eine Key Value Liste mit Globalen Settings. Diese Settings werden während der Verarbeitung in die OneOffixx Connect Struktur kopiert.

-- IMG --

Bemerkung: Minor Versionen der Schnittstelle werden über globale Settings abgegrenzt. 

OneOffixx kennt die folgenden Settings:

    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Settings>
        <Add key="KeepConnector">true</Add>
        <Add key="CreateConnectorResult">false</Add>
        <Add key="CreateConnectorResultOnError">true</Add>
      </Settings>
      <Entries>
      …
      </Entries>
    </OneOffixxConnectBatch>
	
Diese Settings haben die gleiche Funktion wie die entsprechenden Kommandozeilenparameter (s. Kapitel 2.3.1 und 2.3.1.2). Falls angegeben überschreiben sie die Kommandozeilenparameter.

## Global Commands

Diese Struktur enthält Kommandos, welche die ganze Dokumentliste betreffen. (Bsp Merge Document). 

-- IMG --

## Entries

Entries entspricht einer Liste mit Dokumenten.

-- IMG --

## OneOffixx Connect

Die OneOffixxConnect Struktur entspricht einem Dokument. Jedes Dokument kann mit Argumenten, Kommandos und Dokumentfunktionen ausgestattet werden. 

-- IMG --

Mit Dokumentfunktionen kann das Verhalten gesteuert werden, wie ein Dokument geöffnet bzw. verarbeitet wird. Funktionen sind optional. Jede Funktion hat eine eindeutige Id bzw. diese ist konstant. Die Elemente innerhalb einer Dokumentfunktion sind abhängig von der Dokumentfunktion.