---
layout: page
title: Anwendungsfälle
subtitle: Kontaktinformationen als Empfängeradressen hinterlegen
permalink: "connect/de/usecases/contact-information/"
---

Wird OneOffixx aus Fachapplikationen heraus aufgerufen können fachapplikationsspezifische Daten an OneOffixx übergeben werden. Elementname und Attributenamen sind frei wählbar. Pro Schnittstelle muss ein eindeutiger Schnittstellename definiert werden. Aufgrund dieses Namens wendet OneOffixx die interne Transformation.  

```xml
<Interface Name="SchnittstelleXY">
```

Beispiel:
```xml
<Function name="CustomInterfaceConnector" id="70E94788-CE84-4460-9698-5663878A295B">
  <Arguments>
    <Interface Name="SchnittstelleXY">
      <Allgemein>
        <Telefon_a>#Telefon_a#</Telefon_a>
        <Telefon_b>#Telefon_b#</Telefon_b>
        <Homepage>#Homepage#</Homepage>
        <akadTitel>#akadTitel#</akadTitel>
        <TelefonSekretariat>#TelefonSekretariat#</TelefonSekretariat>
        <ObjKeyOrgProfile>#ObjKeyOrgProfile#</ObjKeyOrgProfile>
      </Allgemein>
      <Auftrag>
        <EntscheidDatum>#EntscheidDatum#</EntscheidDatum>
        <VersandDatum>#VersandDatum#</VersandDatum>
        <SBEntscheid>#SBEntscheid#</SBEntscheid>
        <VerfuegungTitel>#VerfuegungTitel#</VerfuegungTitel>
        <verrechnungstabelle>
          <vteintrag>
            <vtperiode>@01.01.1900-01.01.2016</vtperiode>
            <vtanspruch>@11'600.00</vtanspruch>
            <vtzurueckbezahlt>@1'234.00</vtzurueckbezahlt>
            <vtoffen>@5'000.00</vtoffen>
          </vteintrag>
          <vteintrag>
            <vtperiode>@01.01.1901-01.01.2016</vtperiode>
            <vtanspruch>@11'600.01</vtanspruch>
            <vtzurueckbezahlt>@1'234.01</vtzurueckbezahlt>
            <vtoffen>@5'000.01</vtoffen>
          </vteintrag>
        </verrechnungstabelle>
        <VTtotalText>#VTtotalText#</VTtotalText>
        <VTTotal>#VTTotal#</VTTotal>
      </Auftrag>
    </Interface>
  </Arguments>
</Function>
```
