---
layout: page
title: GlobalTranslationProvider / Globaler Übersetzungsprovider
permalink: "docfunc/de/df/globaltranslationprovider"
language: de
---

Im globalen Übersetzungsprovider werden alle Texte hinterlegt, die in XML-Konfigurationen sprachabhängig verknüpft werden.


## Beispiel

```xml
  <group name="Texts">
    <data name="Enclosures">
      <value lcid="07">Beilagen</value>
      <value lcid="09">Enclosures</value>
      <value lcid="12">Annexes</value>
      <value lcid="16">Allegato</value>
    </data>
  </group>
```

Dieser übersetzte Text kann nun in allen XML-Konfigurationen von OneOffixx-Dokument-Funktionen verknüpft werden.
So z. B. in einem Beilagen-Skript wie folgt:
```xml
    <CustomDataNode id="Enclosures">
      <Line>
        <Text>{D[Texts.Enclosures]}:</Text>
      </Line>
      <Line>
        <Element id="DocParam.Enclosures" linePrefix="&#8211;&#009;" />
      </Line>
    </CustomDataNode>
```
`{D[Texts.Enclosures]}` wird nun jeweils abhängig von der Dokument-Sprache mit "Beilagen", "Enclosures", "Annexes" oder "Allegato" ersetzt.


## Verknüpfung durch Platzhalter

Die Übersetzungen werden mit Platzhalter nach folgendem Muster verknüpft:<br />
`{D/U[GroupName.DataName]}`

Die Sprache kann abhängig sein von:
* Dokument-Sprache → "D" → `{D[GroupName.DataName]}`
* GUI-Sprache → "U" → `{U[GroupName.DataName]}`


## Einige Übersetzungen

* [Gebräuchliche Texte (de, en, fr, it)]({{ site.baseurl }}/assets/content-files/docfunc/de/globaltranslationprovider_Translated_Texts_(de_en_fr_it).xml)
* [Texte für OneOffixx LAW (de)]({{ site.baseurl }}/assets/content-files/docfunc/de/globaltranslationprovider_OO-LAW-Group_Translated_Texts_(de).xml)





