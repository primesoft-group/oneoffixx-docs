---
layout: page
title: Vererbungskonzept
permalink: "docengine/de/inheritance/"
language: de
---

## Document Engine - Vererbungssystem {% include anchor.html name="docengine-inheritance" %}

Jede Vorlage bzw. Vorlagentyp bringt einen Teil der spezifischen Merkmale des Enddokumentes mit. Zum Beispiel liefert das "Style" Dokument alle Style Merkmale des Hauptdokumentes mit. Die verschiedenen Vorlagentypen können so beliebig kombiniert und jederzeit ausgetauscht oder aktualisiert werden. Dadurch können Redundanzen im Vorlagenbau vermieden werden. Die Dokumente werden immer zur Laufzeit neu generiert.

Diese Grafik zeigt die __maximale__ Vererbungsstufe - jede Ebene ist optional.

![x]({{ site.baseurl }}/assets/content-images/concepts/de/docengine-inheritance.png "Document-Engine - Vererbungssystem")

Die Dokumentenpipeline enthält ein vorlagenspezifische Liste von Funktionen, die als PlugIns realisiert sind und beim Starten von OneOffixx geladen werden. 

Welche Dokumentfunktionen in welcher Reihenfolge in einer Vorlage verwendet werden, wird in OneOffixx im Vorlagenbearbeitungsmodus vom Vorlagenbauer festgelegt. 

Dokumentfunktionen enthalten für sich geschlossene Prozeduren, die auf das Dokument, Schnittstellen etc. angewendet werden.

## Vererbung von Dokumentfunktionen {% include anchor.html name="docengine-docfunction-inheritance" %}

Es werden alle Dokumentfunktionen, welche im Vorlagenvererbungssystem auf den verschiedenen Ebenen angehangen sind, in eine Kette zusammengefasst. Dabei wird jede Dokumentfunktion nur einmalig hinzugefügt.

Fügt man z.B. in einer virtuellen Vorlage eine Dokumentfunktion hinzu wird diese am Ende der Ausführungsreihenfolge ausgeführt.

Hierbei gibt es allerdings Ausnahmen: Systembedingt werden manche Dokumentfunktionen automatisch ans Ende der Kette verschoben (wie z.B. die "Script"-Funktion). 

__Aktive bzw. deaktivierte Funktionen:__

{% include new-badge.html version="3.3" %} 

Definiert man die "Dokumentparamter"-Funktion auf der Style-Ebene, haben alle davon erbenden Vorlagen ebenfalls diese Funktion automatisch mit ausgeführt. Bislang konnte man die Konfiguration überschreiben (siehe nächstes Kapitel), jedoch bis Version 3.3 nicht mehr vollständig deaktivieren.
Ab Version 3.3 kann man nun Dokumentfunktionen einer Vorlage anhängen und "deaktivieren". Dies sorgt dafür, dass diese Dokumentfunktion für die Vorlage nicht mehr ausgeführt wird, auch wenn diese auf einer höheren Ebene definiert wurde.

## Vererbung von Dokumentfunktionkonfiguration {% include anchor.html name="docengine-docfunction-config" %}

Definiert man eine Dokumentfunktion auf __verschiedenen__ Ebenen, greift für die meisten Dokumentfunktion folgende Regel:

Die Konfiguration, welche __näher__ am eigentlichen Dokument konfiguriert wurde, wird in der Document Engine genommen. 

Ausnahmen dieser Regel ist z.B. die "Script"-Funktion: Hierbei werden die verschiedenen DataNodes von jeder Stufe zusammengesetzt, sodass am Ende alle Scripte von allen Ebenen durchgelaufen werden können.

__Transformation:__ 

{% include new-badge.html version="3.3" %} 

Es ist nun möglich von einer "niedrigeren" bzw. näher am Dokument befindlichen Ebene (z.B. auf Hauptvorlagen) gezielt Konfigurationseinträge von einer höheren Ebene (z.B. Formatvorlage) zu überschreiben. Diese Art der Konfiguration erlaubt es sehr genaue Änderungen an einer bestehenden Konfiguration zu machen, jedoch erfordert es eine Einarbeitung in ["XDT"-Transformationen](https://msdn.microsoft.com/en-us/library/dd465326(v=vs.110).aspx).

__Szenario:__

Formatvorlage mit Formatting-DF:

```
<DocumentFunction>

    <!-- Sollen die Hotkeys von OneOffixx überschrieben werden? -->
    <EnableHotkeys>false</EnableHotkeys>

    <!-- Parametrierung der Überschriften -->
    <Group name="Headings">
        <Definition type="Heading" level="1" style="Überschrift 1"/>
        <Definition type="Heading" level="2" style="Überschrift 2"/>
        <Definition type="Heading" level="3" style="Überschrift 3"/>
        <Definition type="Heading" level="4" style="Überschrift 4"/>
    </Group>

    <!-- Parametrierung der Tabulatoren -->
    <Group name="Indents" maxListLevels="4">
    </Group>

    <!-- Parametrierung der Listen, Aufzählungen und Nummerierungen -->
    <Group name="NumberingStyles">
        <Definition type="Numeric" tabPosition="1" style="NumericListStyle" />
        <Definition type="Alphabetic" tabPosition="1" style="AlphabeticListStyle" />
        <Definition type="Bullet" tabPosition="1" style="BulletListStyle" />
        <Definition type="Line" tabPosition="1" style="LineListStyle" />
    </Group>

    <!-- Parametrierung der Nummerierungs-Optionen -->
    <Group name="NumberingBehaviors">
        <Definition type="Increment" style="NumericListStyle"/>
        <Definition type="Decrement"/>
        <!--<Definition type="RestartMain"/>
        <Definition type="RestartSub"/>-->
        <Definition type="ResetChapter" style="Überschrift 1"/>
        <Definition type="ResetList" style="NumericListStyle"/>
    </Group>

    <!-- Parametrierung der weiteren Formatierungs-Optionen -->
    <Group name="Styles">
        <Definition type="Standard" style="Standard"/>
        <Definition type="Bold" style="Fett"/>
        <Definition type="Italic" style=""/>
        <Definition type="Underline" style=""/>
    </Group>

   
</DocumentFunction>
```

Nun soll in einer bestimmten Word-Vorlage andere Überschriften eingesetzt werden. Ohne Transformation müsste man alles ersetzen, mit Transformation kann man folgende Konfiguration definieren:

```
<DocumentFunction xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
         
   <Group name="Headings" xdt:Transform="Replace" xdt:Locator="Match(name)">
        <Definition type="Heading" level="1" style="Überschrift A"/>
        <Definition type="Heading" level="2" style="Überschrift B"/>
        <Definition type="Heading" level="3" style="Überschrift C"/>
        <Definition type="Heading" level="4" style="Überschrift D"/>
   </Group>
     
</DocumentFunction>
```

Man kann auch mehrere Transformationen hintereinander verketten, sodass z.B. eine virtuelle Vorlage die bestehende Konfiguration nochmals transformiert.

```
<DocumentFunction xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <Group name="NumberingBehaviors">
        <Definition type="Increment" style="NumericListStyleOther" xdt:Transform="Replace" xdt:Locator="Match(type)" />
    </Group>   
</DocumentFunction>
```

Eine Transformation wird nur gestartet, wenn man den folgenden XML Namespace importiert:

    xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform"

Ohne diesen XML-Namespace wird der normale Merge-Mechanismus genutzt, welches meist die Konfiguration insgesamt mit dem höher liegenden ersetzt.

Eine vollständige Dokumentation über alle XDT-Aktionen befindet sich in der [MSDN](https://msdn.microsoft.com/en-us/library/dd465326(v=vs.110).aspx).