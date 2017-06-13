---
layout: page
title: Formatierung
permalink: "docfunc/de/df/formatting"
language: de
---

Die Formatierung ist normalerweise nur der Stylevorlage angehängt. Hier werden die Knöpfe unter ‘Formatierung’ im OneOffixx-Word-Ribbon konfiguriert. Jedem Knopf kann ein Style zugeordnet werden. Zusätzlich zu den vordefinierten Knöpfen kann man eine beliebige Anzahl weiterer Styles hinterlegen, die über ein Dropdown ausgewählt werden können (CustomStyles).


![x]({{ site.baseurl }}/assets/content-images/docfunc/de/ribbonformatting.png)

Die Knöpfe sind im Ribbon aktiviert, sobald die Dokumentfunktion der Vorlage angehängt wird.


## Genereller Aufbau der Konfiguration

```xml
<DocumentFunction>
  
  <Group name="{Gruppenname}">
    <Definition type="{Typ}" style="{Style}" />
    <Definition type="{Typ}" style="{Style}" />
  </Group>

</DocumentFunction>
```

## Gruppen

{:.table .table-striped}
Group name="{Gruppename}" | Beschreibung
------- | -------
Headings | Kapitelüberschriften
Indents | Einrückungen / Tabulatoren
NumberingStyles  |  Aufzählungen Numerisch, Alphanumerisch und Bullet
NumberingBehaviors | Verhalten bei Numerischer Aufzählung. 
Styles | Setzen von Styleinformationen. Wenn kein Style angegeben ist, werden die Inlinestyle verwendet.
CustomStyles | Kundenspezifische Auflistung von Styles


## Attribute

* __level__ definiert die Überschrifts-Ebene (1 bis 4)
* __maxListLevels__ definiert ab wieviele Ebenen wieder zur 1. Ebene gesprungen werden soll
* __style__ entspricht dem Style-Namen in Word
* __type__ gibt den Typ der Definition an (siehe Beispiel-Konfiguration für mögliche Typen)


In den CustomStyles können Beschriftungen in alle Sprachen übersetzt werden. Dafür wird das XML-Element __Label__ verwendet. Die LCID gibt die Lokalisierungs-ID an. Wenn die UI z. B. in der deutschen Sprache angezeigt wird, muss die LCID in der Label-Konfiguration der deutschen Sprache entsprechen. Eine Auflistung von allen möglichen LCIDs finden Sie [__hier__](https://msdn.microsoft.com/de-ch/goglobal/bb964664.aspx).


## Beispiel-Konfiguration

```xml
<DocumentFunction>

  <!-- Defines whether OneOffixx overwrites Hotkeys -->
  <EnableHotkeys>false</EnableHotkeys>

  <!-- Headings -->
  <Group name="Headings">
    <Definition type="Heading" level="1" style="Überschrift 1" />
    <Definition type="Heading" level="2" style="Überschrift 2" />
    <Definition type="Heading" level="3" style="Überschrift 3" />
    <Definition type="Heading" level="4" style="Überschrift 4" />
  </Group>

  <!-- Indents -->
  <Group name="Indents" maxListLevels="4" />

  <!-- Lists and numberings -->
  <Group name="NumberingStyles">
    <Definition type="Numeric" style="ListNumeric" />
    <Definition type="Alphabetic" style="ListAlphabetic" />
    <Definition type="Bullet" style="ListBullet" />
    <Definition type="Line" style="ListLine" />
  </Group>

  <!-- Numbering settings -->
  <Group name="NumberingBehaviors">
    <Definition type="Increment" style="ListNumeric" />
    <Definition type="Decrement" />
    <!--
    <Definition type="RestartMain"/>
    <Definition type="RestartSub"/>
    -->
    <Definition type="ResetChapter" style="Überschrift 1" />
    <Definition type="ResetList" style="ListNumeric" />
  </Group>

  <!-- Other style settings -->
  <Group name="Styles">
    <Definition type="Standard" style="Standard" />
    <Definition type="Bold" style="Fett" />
    <Definition type="Italic" style="" />
    <Definition type="Underline" style="" />
  </Group>

  <!-- Custom Styles -->
  <Group name="CustomStyles">
    <Category id="Headings">
      <Label lcid="2055">Überschriften</Label>
      <Definition type="Title" style="Titel">
        <Label lcid="2055">Titel</Label>
      </Definition>
      <Definition type="Subtitle" style="Untertitel">
        <Label lcid="2055">Untertitel</Label>
      </Definition>
    </Category>
    <Category id="Various">
      <Label lcid="2055">Diverses</Label>
      <Definition type="Emphasis" style="Hervorhebung">
        <Label lcid="2055">Hervorhebung</Label>
      </Definition>
    </Category>
  </Group>

</DocumentFunction>
```

## Buttons disablen / ausgrauen

<span class="label label-info">NEU ab 3.1.1</span> Die einzelnen Buttons können über die Konfiguration deaktiviert werden.<br />
Hierfür kann das Attribut `disabled="true"` an verschiedene Elemente angehängt werden.<br />
Beispiel, bei dem alle Buttons ausgegraut sind:
```xml
<DocumentFunction>

  <!-- Defines whether OneOffixx overwrites Hotkeys -->
  <EnableHotkeys>false</EnableHotkeys>

  <!-- Headings -->
  <Group name="Headings">
    <Definition type="Heading" level="1" style="Überschrift 1" disabled="true" />
    <Definition type="Heading" level="2" style="Überschrift 2" disabled="true" />
    <Definition type="Heading" level="3" style="Überschrift 3" disabled="true" />
    <Definition type="Heading" level="4" style="Überschrift 4" disabled="true" />
  </Group>

  <!-- Indents -->
  <Group name="Indents" maxListLevels="4" disabled="true" />

  <!-- Lists and numberings -->
  <Group name="NumberingStyles">
    <!-- none -->
  </Group>

  <!-- Numbering settings -->
  <Group name="NumberingBehaviors">
    <!-- none -->
  </Group>

  <!-- Other style settings -->
  <Group name="Styles">
    <Definition type="Standard" style="Standard" disabled="true" />
    <Definition type="Bold" style="Fett" disabled="true" />
    <Definition type="Italic" style="" disabled="true" />
    <Definition type="Underline" style="" disabled="true" />
  </Group>

  <!-- Custom Styles -->
  <Group name="CustomStyles">
    <!-- none -->
  </Group>

</DocumentFunction>
```

