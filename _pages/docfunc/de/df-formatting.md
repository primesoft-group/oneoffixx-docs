---
layout: page
title: Formatierung
permalink: "docfunc/de/df/formatting"
language: de
---

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/ribbonformatting.png)

Die Formatierung ist normalerweise nur der Stylevorlage angehängt. Hier konfiguriert man die Knöpfe unter ‘Formatierung’ im OneOffixx Ribbon. Jedem Knopf kann ein Style zugeordnet werden. Zusätzlich zu den vordefinierten Knöpfen kann man eine beliebige Anzahl weiterer Styles hinterlegen, die über ein Dropdown ausgewählt werden können.

```xml
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
        <Definition type="Numeric" tabPosition="1" style="List_Numeric" />
        <Definition type="Alphabetic" tabPosition="1" style="List_Alphabetic" />
        <Definition type="Bullet" tabPosition="1" style="List_Bullet" />
        <Definition type="Line" tabPosition="1" style="List_Line" />
    </Group>

    <!-- Parametrierung der Nummerierungs-Optionen -->
    <Group name="NumberingBehaviors">
        <Definition type="Increment" style="List_Numeric"/>
        <Definition type="Decrement"/>
        <!--<Definition type="RestartMain"/>
        <Definition type="RestartSub"/>-->
        <Definition type="ResetChapter" style="Überschrift 1"/>
        <Definition type="ResetList" style="List_Numeric"/>
    </Group>

    <!-- Parametrierung der weiteren Formatierungs-Optionen -->
    <Group name="Styles">
        <Definition type="Standard" style="Standard"/>
        <Definition type="Bold" style="Fett"/>
        <Definition type="Italic" style=""/>
        <Definition type="Underline" style=""/>
    </Group>

    <!-- Parametrierung der weiteren kundenspezifischen Formatierungs-Optionen -->
   
    <Group name="CustomStyles">
          <Category id="Headings">
                <Label lcid="1042">Zusätzliche Standard</Label>
                <Definition type="Standard 1" style="Standard 1">
                    <Label lcid="1042">Standard 1</Label>
                </Definition>
                <Definition type="Standard 1 klein" style="Standard 1 klein">
                    <Label lcid="1042">Standard 1 klein</Label>
                </Definition>
                <Definition type="Standard 2" style="Standard 2">
                    <Label lcid="1042">Standard 2</Label>
                </Definition>
                <Definition type="Standard 2 klein" style="Standard 2 klein">
                    <Label lcid="1042">Standard 2 klein</Label>
                </Definition>
                <Definition type="Standard 3" style="Standard 3">
                    <Label lcid="1042">Standard 3</Label>
                </Definition>
                <Definition type="Standard 3 klein" style="Standard 3 klein">
                    <Label lcid="1042">Standard 3 klein</Label>
                </Definition>
                <Definition type="Standard 4" style="Standard 4">
                    <Label lcid="1042">Standard 4</Label>
                </Definition>
                <Definition type="Standard 4 klein" style="Standard 4 klein">
                    <Label lcid="1042">Standard 4 klein</Label>
                </Definition>
                <Definition type="Titel" style="Titel">
                    <Label lcid="1042">Titel</Label>
                </Definition>
                <Definition type="Untertitel" style="Untertitel">
                    <Label lcid="1042">Untertitel</Label>
                </Definition>
          </Category>  
     <!--      <Category id="Formats">
                <Label lcid="1042">div. Formatierungen</Label>
                <Definition type="Intensiv" style="Intensiv">
                    <Label lcid="1042">Hervorgehoben</Label>
                </Definition>
                <Definition type="Bold" style="Fett">
                    <Label lcid="1042">Fett</Label>
                </Definition>
          </Category> 
          -->
    </Group>
    

</DocumentFunction>
```