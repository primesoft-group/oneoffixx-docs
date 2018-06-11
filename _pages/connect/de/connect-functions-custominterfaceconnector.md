---
layout: page
title: "Function: CustomInterfaceConnector"
subtitle: Daten aus einer Fachapplikation übergeben
permalink: "connect/de/functions/custominterface/"
language: de
---

## CustomInterface

Wird OneOffixx aus einer Fachapplikationen heraus aufgerufen können fachapplikationsspezifische Daten an OneOffixx übergeben werden.

Element- und Attributnamen sind frei wählbar bzw. können von Fachapplikation definiert und angepasst werden. 

Pro Schnittstelle muss __ein eindeutiger Schnittstellename__ definiert werden. Dadurch ist OneOffixx in der Lage die Daten intern zu transformieren und für die Dokumentgenerierung aufzubereiten.

```xml
<Interface Name="SchnittstelleXY" />
```
Standard-Format-Aufruf:

```xml
 <Function name="CustomInterfaceConnector" id="70E94788-CE84-4460-9698-5663878A295B">
    <Arguments>
      <Interface Name="SchnittstelleXY">
         <Node Id="KeyA">ValueA</Node>
         <Node Id="KeyB">ValueB</Node>
         <Node Id="KeyC">ValueC</Node>
      </Interface>
    </Arguments>
  </Function>
```

Beispiel-Aufruf, wobei eine Transformation konfiguriert werden muss:

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
          <PictureFilePath>http://www.mycompany.com/files/pics/Bild_1234.jpg</PictureFilePath>
          <Picture>iVBORw0KGgoAAAANSUhEUgAAAF8AAAB4CAIAAAAbh7ksAAAAAXNSR0IArs4c6QAAAARnQU1BAACx
jwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAAZdEVYdFNvZnR3YXJlAHBhaW50Lm5ldCA0LjAu
MTHaDTpWAAAA8UlEQVR4Xu3QQQ0AIAwAMfz/UIS0oWCnoEkV9Nw3bOwUO8VOsVPsFDvFTrFT7BQ7
xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvF
TrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VO
sVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6x
U+wUO8VOsVPsFDvFTrFT7BQ7xc7uzQeYsdPzpHNxAAAAAABJRU5ErkJggg==</Picture>
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

## Transformation
OneOffixx transformiert das XML der Fachapplikation in ein internes Format. Die Konfiguration dafür wird entweder global oder auf der Vorlage definiert. Dazu muss in der Vorlage die Dokumentfunktion __Connect Konverter (CustomInterfaceConnector)__  angezogen und konfiguriert werden. 

Es ist möglich Bilder in Form einer Url oder im Base64 Format zu übergeben. Dafür muss im Node Element das Attribute _Type="Image"_ zusätzlich angeben wird. Sofern eine URL übergeben wird muss der Client und/oder der Server Lesezugriff auf die Bilder haben.

Beispiel einer Transformationsdatei. Die Elementinhalte werden als Beispielcontent während der Designphase verwendet.
```xml
  <InterfaceDescription Name="CollectionDemo">
    <Node Id="SimpleBindingOne" XPath="//SimpleBindingOne">SimpleBindingOneText</Node>
    <Node Id="SimpleBindingTwo" XPath="//SimpleBindingTwo">SimpleBindingTwoText</Node>
    <Node Id="SimpleBindingThree" XPath="//SimpleBindingThree">SimpleBindingThreeText</Node>
    <NodeCollection Id="ListBinding" XPath="//List/EachElement">
      <Node Id="Firstname" XPath="./FirstName" /> // these Elements are beneth <EachElement>
      <Node Id="Surname" XPath="./Surname" /> // these Elements are beneth <EachElement>
      <NodeCollection Id="Orders" XPath="./Orders/Order"> // even Collection in Collections are supported
        <Node Id="OrderId" XPath="./Id" />
        <Node Id="OrderProduct" XPath="./Product" />
      </NodeCollection>
    </NodeCollection>
    <!-- Bild wird im Base64 Format übergeben -->
    <Node Id="PictureSample" Type="Image" XPath="//PictureSample" >iVBORw0KGgoAAAANSUhEUgAAAF8AAAB4CAIAAAAbh7ksAAAAAXNSR0IArs4c6QAAAARnQU1BAACx
jwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAAZdEVYdFNvZnR3YXJlAHBhaW50Lm5ldCA0LjAu
MTHaDTpWAAAA8UlEQVR4Xu3QQQ0AIAwAMfz/UIS0oWCnoEkV9Nw3bOwUO8VOsVPsFDvFTrFT7BQ7
xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvF
TrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VO
sVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6xU+wUO8VOsVPsFDvFTrFT7BQ7xU6x
U+wUO8VOsVPsFDvFTrFT7BQ7xc7uzQeYsdPzpHNxAAAAAABJRU5ErkJggg==</Node>

    <!-- Bild als URL übergeben -->
    <Node Id="PictureFilePathSample" Type="Image" XPath="//PictureFilePathSample" />
  </InterfaceDescription>
```



## CustomInterface: type="Data"

{% include new-badge.html version="3.3" %} 

Wird das Interface mit __type='Data'__ mitgegeben, muss kein konfiguriertes Interface in der Konfiguration hinterlegt sein. Die Daten werden als CustomXmlNodes interpretiert und sind sowohl im Editor als auch im Dokument verfügbar. 

Beispiel:

```xml
<Function name="InterfaceConnector" id="70E94788-CE84-4460-9698-5663878A295B" xmlns="">
    <Arguments>
      <Interface Name="ReportAusFachapplikation" type="Data">
        <Text Id="ID">42</Text>
        <Text Id="Vorname">Max</Text>
        <Text Id="Ort">Eschlikon TG</Text>
        <Text Id="Nachname">Mustermann</Text>
        <Text Id="Zivilstand">verheiratet</Text>
        <DateTime Id="Geburtsdatum">1998-09-01</DateTime>
        <Collection Id="Telefonnummern">
            <Element>
                <Text Id="Mobil">012 345 67 89</Text>
                <Text Id="Festnetz">012 345 67 89</Text>
            </Element>
        </Collection>
      </Interface>
    </Arguments>
</Function>
```
