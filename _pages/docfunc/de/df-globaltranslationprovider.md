---
layout: page
title: GlobalTranslationProvider / Globaler Übersetzungsprovider
permalink: "docfunc/de/df/globaltranslationprovider"
language: de
---

Im globalen Übersetzungsprovider werden alle Texte hinterlegt, die in XML-Konfigurationen sprachabhängig verknüpft werden.


## Verknüpfung durch Platzhalter

Die Übersetzungen werden mit Platzhalter nach folgendem Muster verknüpft:<br />
`{D/U[GroupName.DataName]}`

Die Sprache kann abhängig sein von:
* Dokument-Sprache → "D" → `{D[GroupName.DataName]}`
* GUI-Sprache → "U" → `{U[GroupName.DataName]}`


## Beispiel

```xml
<TranslationMap>
  
  <group name="Texts">
    <data name="Enclosures">
      <value lcid="07">Beilagen</value>
      <value lcid="09">Enclosures</value>
      <value lcid="12">Annexes</value>
      <value lcid="16">Allegato</value>
    </data>
    [...]
  </group>

  [...]

</TranslationMap>
```

Dieser übersetzte Text "Texts.Enclosures" kann nun in allen XML-Konfigurationen von OneOffixx-Dokument-Funktionen verknüpft werden.
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

Übersetzte Texte können _nicht direkt_ in (z. B. Word-) Vorlagen eingefügt werden.<br />
Damit die Texte in der Vorlage verwendet werden können, muss immer über ein Skript mit Platzhalter auf den Text zugegriffen werden.<br />
Beispiel für ein Skript, das den übersetzten Text "Texts.Enclosures" zur Verfügung stellt:
```xml
    <CustomDataNode id="Texts.Enclosures">
      <Text>{D[Texts.Enclosures]}:</Text>
    </CustomDataNode>
```


## Einige Übersetzungen

* [Gebräuchliche Texte (de, en, fr, it)]({{ site.baseurl }}/assets/content-files/docfunc/de/globaltranslationprovider_Translated_Texts_(de_en_fr_it).txt)
* [Texte für OneOffixx LAW (de)]({{ site.baseurl }}/assets/content-files/docfunc/de/globaltranslationprovider_OO-LAW-Group_Translated_Texts_(de).txt)





