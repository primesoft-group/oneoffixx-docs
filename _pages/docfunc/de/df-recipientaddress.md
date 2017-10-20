---
layout: page
title: RecipientAddresses / Empfängeradresse
permalink: "docfunc/de/df/recipientaddress"
language: de
---

Die Dokumentfunktion "Empfängeradresse" muss einer Vorlage angehängt werden, wenn der Empfängerdialog angezeigt werden soll. Im Konfiguratonsfenster kann der Empfängerdialog auf verschiedene Weisen auf die Lösung massgeschneidert werden. In der Konfiguration verweisen mehrere Links auf den globalen Konfigurationsprovider, wo die Konfiguration der verschiedenen Gruss- und Abschiedsformeln hinterlegt sind. Der genaue Wortlaut und Übersetzungen der Formeln können im globalen Übersetzungsprovider angepasst werden.

Im folgenden Abschnitt wird zuerst auf die _OneOffixx-Adressprovider_ eingegangen.<br>
Für allgemeine Informationen zur Dokument-Funktion siehe [Konfiguration des Empfängerdialogs](#konfiguration-des-empfängerdialogs) weiter unten.

## OneOffixx-Adressprovider

{:.table .table-striped}
| Id  | Name |
| --- | ---- |
| 833075BF-DDE5-4E9B-83B9-E9803C96E391 | [AbacusAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/abacus)
| F3D23EE5-F722-4082-842C-1168F7FDF1B8 | [CobraAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/cobra)
| 328E6C4E-549B-4108-8ED2-D76B7E422F6B | [CreativAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/creativ)
| 121CE113-143E-4125-980A-20B6341F9FC9 | [DynamicsCRMAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/msdynamicscrm) <span class="label label-info">NEU ab 3.2.1</span>
| 739DEC43-D4F0-47F6-ADDD-C6AC73A93B02 | [DynamicsNavisionAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/msdynamics)
| C6445223-DEBE-4817-9E50-E843F507C1BC | [EGDVAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/ruf)
| 3FD89D27-37FD-4B70-8E0F-A4BD93B220A5 | [ExchangeAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/msexc)
| 8C51B042-81EA-46E3-A429-821641E19A6A | [GenericSqlAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/gernericsql)
| 5CF8E2B1-D722-4CA1-8160-75914B915843 | [GoogleMapsAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/google)
| 00BA9804-2430-4585-AE60-FCCA29909781 | [LDAPAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/ldap)
| 6EA5E6E3-1329-4B02-8779-0952C1119A15 | [LotusNotesAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/lotusnotes)
| B16EC67C-444E-46DC-A659-93E95BB4EB4D | [NestAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/nest)
| A244D5EF-93F6-4A2C-9B62-F6DA64590B8C | [OutlookAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/outlook)
| 6A3354D7-6423-48C0-A3F0-F636E606196D | [SAPPulsAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/sappuls)
| 96078EBE-4A8F-4D53-883E-9E9D0F07BC2A | [SharepointAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/sharepoint)
| D66AA3D8-B184-4AED-BE93-6AA86FA1867E | [TelSearchCHAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/telsearch)
| 5f4865d3-9d7e-47bd-846d-546f7f7dd0ad | [UserDefinedAddressProvider z.Bsp. für Excel]({{ site.baseurl }}/docfunc/de/df/ap/userdefined)
| 0861976E-318F-41A1-AE45-6D894A7E7292 | [VertecAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/vertec)
| AAA2E7F3-9E1E-4F1D-963F-C49C4886EAFD | [ZefixAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/zefix)

Addressprovider sind Plugins, die eine Schnittstelle zu einer Adressquelle implementieren. Auf Wunsch werden Addressprovider kundenspezifisch implementiert. Die Verwendung der Addressprovider kann mit Lizenzkosten verbunden sein.

![]({{ site.baseurl }}/assets/content-images/docfunc/de/recipientdialog.png)

Folgende Parameter können in allen Providern angewandt werden:

```xml
<AddressProvider id="nguid" order="0" active="true" hiddenIfNotAvailable="true">
  <Debug>false</Debug>
  <Uri></Uri>
  <Timeout></Timeout>
  <EnableProxyCredentials>false</EnableProxyCredentials>
  <ProxyCredentialsName></ProxyCredentialsName>
  <ProxyCredentialsPassword></ProxyCredentialsPassword>
  <DetailsColumnMapping>//AddressProviderData/@Id</DetailsColumnMapping>
</AddressProvider>
```
### Attribute
* __id__ GUID des Adressproviders
* __order__ Reihenfolge in der Dialog-Übersicht
* __active__ true = der Dialog wird angezigt
* __hiddenIfNotAvailable__ Der Dialog wird nicht angezeigt, wenn die Adressquelle nicht erreichbar ist.

### Elemente
* __Debug__ Erweiterte Ausgabe im Log. 
* __Uri__  (Optional) URL auf WS Adresssen.
* __Timeout__ (Optional) Maximale Wartezeit bis Ergebnisse vom Webservice geliefert werden.
* __EnableProxyCredentials__ (Optional) Falls ein Proxy im LAN betrieben wird können Logindaten im Proxy überschrieben werden. Andernfalls werden diese vom IE übernommen.
* __ProxyCredentialsName__ (Optional) Proxy Loginname.
* __ProxyCredentialsPassword__ (Optional) Proxy Password.
* __DetailsColumnMapping__ (Optional) Mappt Daten in der Trefferliste in die Datailspalte. Muss ein XPath innerhalb des generierten Contacts sein. Zum Beispiel: //Person/LastName für den Nachname oder //AddressProviderData/@Id für den Addressprovider ./ExtendentFields/Item @Key='Dynamic.Detail'] für ein ExtendedField ('Detail').

### ContactMapping
Verschiedene Provider unterstützen ein zusätzliches ContactMapping. Zum Beispiel, um SQL Spalten in OneOffixx Adressfelder zu mappen.
```xml
<ContactMapping>
    <ContactItemXPath>Contact</ContactItemXPath>  Standard-Einstellung 
    <ContactElement id="Person_PostOfficeBoxCityZipCode">PERSON_ZIPCODE</ContactElement> Mapping vom Key "PERSON_ZIPCODE" 
    <ContactElement id="Person_PostOfficeBoxCityZipCode">"FESTER WERT"</ContactElement> Mapping mit definierten Wert "FESTER WERT" 
    <ContactElement id="Company_Street" when="TYPE = 'Interne Adresse'">STREET</ContactElement>
</ContactMapping>
```

Es gibt eine Reihe von definierten "Prefixes" um das Mapping genauer zu spezifizieren, zum Beispiel: __Person__, __Company__, __Options__, __ExtendedField__ (Achtung – Mappings auf ExtendedFields bekommen den Prefix "Dynamic")

Mapping: `<ContactElement id="ExtendedField_Detail">"Provider-Value"</ContactElement>`
Nutzung für das DetailColumnMapping: `<DetailsColumnMapping>./ExtendentFields/Item[@Key='Dynamic.Detail']</DetailsColumnMapping> `
                
Dazu gibt es folgene Felder, die man mappen kann (passend zu dem jeweiligen Contact-Element, mit oder ohne Präfix, also z.B. Person_Name oder Name):

{:.table .table-striped}                 
Type | Mögliche Werte
---------|----------
Person-related | Name, LastName, FirstName, Title, SecondName, NickName, Initials, BirthDate, Profession, Position, SalutationShort, LetterSalutation, Greeting
Company-related | Name, CompanyName, Supplement, Department
Address-related (sowohl Company als auch Person) | Street, CareOf, Apartment, Floor, City, PostOfficeBox, PostOfficeBoxCityZipCode, Country 
Communication-related (sowohl Company als auch Person) | Language, Phone, Email, Fax, Mobile, Homepage, PhoneDirect, PhoneCentral, EmailDirect, EmailCentral, FaxDirect, FaxCentral
Option-related | SelectedAddress, AddressingType, AddressLabel, PersonOverFirm, CountryView, CountryCodeView, CapitalizedCity, CompanyView, SalutationView, SalutationSeparatetLine, SecondNameView, PositionView, InterneAddress

__Conditions:__ Beim Mapping werden auch Conditions unterstützt, zum Beispiel:
```xml 
<ContactElement id="Company_Street" when="TYPE = 'Interne Adresse'">STREET</ContactElement>
```

### Icon
Einige Adressprovider können mit einem Icon versehen werden, welches dann im Empfänger-Dialog angezeigt wird.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/recipientAddressesProviderWithIcon.png)

Konfiguration:<br>
```xml
<Icon>iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAMAUExURQAAAOIaAOIbAeMbAuMcAuMdA+MeBeMfBuMgB+MiCeQjCuQkC+QkDOQnD+UqEuUrE+UsFOUvF+UxGeY0G+Y0HOY4IOc7JOc+J+hBKuhBK+hFL+hFMOhJM+lJNOlPOupUQOtVQetWQutaRutdSuteS+xiT+xnVe1rWe1tXO1vXu5zYu50ZO51Ze93Z+54aO95ae96ae98be+Cc/CBcfCDdPCFd/CGePGJevGKfPGLffGMf/GNgPGOgfKShPKUh/OYjPOZjfOckPSjmPSnnPWsovato/aupvayqfa0q/e4r/e4sPe5sfe6svi9tvjCuvjFvvnIwfnLw/nOyPrQyvrTzvrUzvvc1/ve2vzf2/zh3v3o5f3o5v3r6P3s6v7v7f7w7/7y8f708v729f739v/49//6+v/8+//8/P/9/f/+/v///wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAOq7jwsAAAEAdFJOU////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////wBT9wclAAAACXBIWXMAAA7DAAAOwwHHb6hkAAAAGXRFWHRTb2Z0d2FyZQBwYWludC5uZXQgNC4wLjE3M26fYwAAATdJREFUOE+d0VdTwkAUBWAXsYCiiL33riiKFTt2sWIDxIItOf//fd0WEpgNmfE8JHfv/SabTaqoR/4DiLrLlAIiohYyRSBnIqojI4AaWCnZRAvq+EVFC95Pppr5vQyEY4AoKIDfm3inqG0wlGV9UdHejbTJFk+7fQ4QN1hLgdEAicylPoGUAyT53NqicDbTQoKXmHeAxWMbtMeuvs27tRxaHSBAbDDZREITh6+4ZwexX9IBjJ/r5Q6SQMINhKdPP/CYAzuEHiy0kfqRI2Sr2UwLvvCw1R/FAf+WWtAwnnyBgTFXsNrt8w+jEHQFb8jsb+KCz/WgdnDvGZh1BzsDNf68GSkHoaXtqCjY786fIy3mTlAMzfCHrVcAvq6VW6OnAuCNRjmXgEWOZFRLxgIinkDGE5TGA1D6B0+SGX0LZzDfAAAAAElFTkSuQmCC</Icon>
```

Empfohlene Grösse: 16x16 oder 32x32 Pixel<br>
Empfohlenes Bild-Format: PNG (auch JPG ist möglich)

Zwischen `<Icon>` und `</Icon>` muss ein Base64-String eingefügt werden.<br>
Für das Konvertieren von PNG- oder JPG-Dateien zu Base64-Strings kann ein beliebiges Programm verwendet werden oder im Internet nach einem Online-Konverter gesucht werden (Suchbegriff z. B. "online image to base64 converter").

__Beispiel-Resultat aus einer Konvertierung__<br>
~~data:image/png;base64,~~ _→ Diesen Teil weglassen, nur die folgenden Zeichen verwenden_
iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAMAUExURQAAAOIaAOIbAeMbAuMcAuMdA+MeBeMfBuMgB+MiCeQjCuQkC+QkDOQnD+UqEuUrE+UsFOUvF+UxGeY0G+Y0HOY4IOc7JOc+J+hBKuhBK+hFL+hFMOhJM+lJNOlPOupUQOtVQetWQutaRutdSuteS+xiT+xnVe1rWe1tXO1vXu5zYu50ZO51Ze93Z+54aO95ae96ae98be+Cc/CBcfCDdPCFd/CGePGJevGKfPGLffGMf/GNgPGOgfKShPKUh/OYjPOZjfOckPSjmPSnnPWsovato/aupvayqfa0q/e4r/e4sPe5sfe6svi9tvjCuvjFvvnIwfnLw/nOyPrQyvrTzvrUzvvc1/ve2vzf2/zh3v3o5f3o5v3r6P3s6v7v7f7w7/7y8f708v729f739v/49//6+v/8+//8/P/9/f/+/v///wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAOq7jwsAAAEAdFJOU////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////wBT9wclAAAACXBIWXMAAA7DAAAOwwHHb6hkAAAAGXRFWHRTb2Z0d2FyZQBwYWludC5uZXQgNC4wLjE3M26fYwAAATdJREFUOE+d0VdTwkAUBWAXsYCiiL33riiKFTt2sWIDxIItOf//fd0WEpgNmfE8JHfv/SabTaqoR/4DiLrLlAIiohYyRSBnIqojI4AaWCnZRAvq+EVFC95Pppr5vQyEY4AoKIDfm3inqG0wlGV9UdHejbTJFk+7fQ4QN1hLgdEAicylPoGUAyT53NqicDbTQoKXmHeAxWMbtMeuvs27tRxaHSBAbDDZREITh6+4ZwexX9IBjJ/r5Q6SQMINhKdPP/CYAzuEHiy0kfqRI2Sr2UwLvvCw1R/FAf+WWtAwnnyBgTFXsNrt8w+jEHQFb8jsb+KCz/WgdnDvGZh1BzsDNf68GSkHoaXtqCjY786fIy3mTlAMzfCHrVcAvq6VW6OnAuCNRjmXgEWOZFRLxgIinkDGE5TGA1D6B0+SGX0LZzDfAAAAAElFTkSuQmCC


## Konfiguration des Empfängerdialogs

### Beispiel

```xml
<?xml version="1.0"?>
<RecipientAddressesConfiguration>
  
  <!-- Flag indicating if the document is a multi letter or not -->
  <IsMultiLetter>true</IsMultiLetter>
  <!-- Maximum contacts allowed (0: no restriction) -->
  <MaxContacts>0</MaxContacts>
  <!-- Flag indicating if the RecipientDialog is in FullDetail mode-->
  <FullDetailMode>true</FullDetailMode>
  <!-- Override the standard addressing types. To;CC;BCC -->
  <AddressingTypes>An;Cc;Bcc</AddressingTypes>
  <!-- Always use english country names (default: false) -->
  <UseEnglishCountryNames>false</UseEnglishCountryNames>
  <!-- Automatic selection of Id for recipients coming from connect -->
  <PreferredRecipientId>Kunde1</PreferredRecipientId>
  
  <!-- Cities as default in capital letters -->
  <CapitalizedCities>false</CapitalizedCities>
  <DefaultLanguageCode>DE</DefaultLanguageCode>
  <DefaultCountryCode>CH</DefaultCountryCode>
  
  <!-- CustomCountries can be added via this registration: -->
  <CustomCountries>
    <CustomCountry Name="Amerikanische Jungferninseln" EnglishName="United States Virgin Islands" ISO="VI" />
    <CustomCountry Name="Republik Zypern" EnglishName="Cyprus" ISO="CY" />
    <CustomCountry Name="Kosovo" EnglishName="Kosovo" ISO="XK" />
  </CustomCountries>
  
  <!-- Address provider configurations -->
  {[Recipients.ProviderConfiguration]}
  
  <!-- Salutation configuration -->
  {[Recipients.SalutationConfiguration]}
  
  <!-- Letter salutation configuration -->
  {[Recipients.LetterSalutationConfiguration]}
  
  <!-- Greeting formula configuration -->
  {[Recipients.GreetingFormulaConfiguration]}
  
  <!-- Shipping method configuration -->
  {[Recipients.ShippingMethodConfiguration]}
  
</RecipientAddressesConfiguration>
```

### Konfig.-Elemente

* `IsMultiLetter`<br>
  Kann `true`oder `false` enthalten. Bestimmt, ob es sich bei der Vorlage um einen Multibrief handelt oder nicht.<br>
  _Speziell bei Multibriefen:_ Es wird jeweils nur ein Empfänger angezeigt und es kann zwischen den Empfängern hin- und hergewechselt werden.<br>
  _Typischer Nicht-Multibrief:_ Ein Protokoll, bei dem alle Empfänger eines Typs in Listenform unter «anwesend» aufgeführt werden.
* `MaxContacts`<br>
  Bestimmt, wieviele Empfänger maximal hinzugefügt werden können.<br>
  `0` bedeutet, dass es keine Obergrenze gibt.
* `FullDetailMode`<br>
   Kann `true`oder `false` enthalten. Bestimmt, ob die folgenden Details im Dialog angezeigt werden.<br>
   ![x]({{ site.baseurl }}/assets/content-images/docfunc/de/recipientAddressesDetailsInDialog.png)
* `AddressingTypes`<br>
  Hier können Anzeigenamen für die 3 Adresstypen konfiguriert werden.<br>
  Zum Beispiel: `An;Cc;Bcc` oder `Anwesend;Abgemeldet;Verteiler`, je nach Verwendungszweck der Adresstypen.
* `UseEnglishCountryNames`<br>
  Kann `true`oder `false` enthalten. Bestimmt, ob Ländernamen immer Englisch sind (true) oder ob sie in der jeweiligen Dokument-Sprache ausgegeben werden (false).
* `PreferredRecipientId`<br>
  Falls die Vorlage über "Connect" aufgerufen wird und falls im Connect-Aufruf-XML Empfänger definiert sind: Hier wird anhand der ID bestimmt, welcher Empfänger ausgewählt sein soll.
* `CapitalizedCities`<br>
  Kann `true`oder `false` enthalten. Bestimmt, ob die Städte-Namen im Adressblock in GROSSBUCHSTABEN geschrieben werden sollen (true) oder nicht (false).
* `DefaultLanguageCode`<br>
  Hat momentan keinen Effekt.
* `DefaultCountryCode`<br>
  Hier kann der Länder-Code des Standard-Landes gesetzt werden. Das Standard-Land ist jeweils zu Beginn ausgewählt.
* `CustomCountries`<br>
  Hier können mit folgendem Muster, Länder hinzugefügt werden, welche im Dialog standardmässig nicht vorhanden sind:<br>
  `<CustomCountry Name="Amerikanische Jungferninseln" EnglishName="United States Virgin Islands" ISO="VI" />`

#### Adressprovider

Die Konfiguration der Adressprovider wird in fast allen Fällen in den globalen Konfigurationsprovider ausgelagert.<br>
Daher sieht die Konfiguration in der Dokument-Funktion praktisch immer so aus:
```xml
  <!-- Address provider configurations -->
  {[Recipients.ProviderConfiguration]}
```

Siehe [OneOffixx-Adressprovider](#oneoffixx-adressprovider).

#### Anrede, Briefanrede, Grussformel, Versandart (Salutation, LetterSalutation, GreetingFormula, ShippingMehod)

Die Konfiguration von Anrede, Briefanrede, Grussformel und Versandart wird auch in fast allen Fällen in den globalen Konfigurationsprovider ausgelagert.
Daher sieht die Konfiguration in der Dokument-Funktion praktisch immer so aus:
```xml
  <!-- Salutation configuration -->
  {[Recipients.SalutationConfiguration]}
  
  <!-- Letter salutation configuration -->
  {[Recipients.LetterSalutationConfiguration]}
  
  <!-- Greeting formula configuration -->
  {[Recipients.GreetingFormulaConfiguration]}
  
  <!-- Shipping method configuration -->
  {[Recipients.ShippingMethodConfiguration]}
```

Die Konfiguration im globalen Konfigurationsprovider sieht wie folgt aus:
```xml
        <!-- SalutationConfiguration -->
        <SalutationConfiguration>
          <ArrayOfSalutation xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
            <Salutation>
              <DisplayName>{D[Salutation.Default]}</DisplayName>
              <IsDefault>true</IsDefault>
              <Qualification>
                <Id>Label</Id>
                <IsPlural>false</IsPlural>
                <Gender>Undefined</Gender>
                <IsDefault>false</IsDefault>
              </Qualification>
            </Salutation>
            [...]
          </ArrayOfSalutation>
        </SalutationConfiguration>
```
```xml
        <!-- LetterSalutationConfiguration -->
        <LetterSalutationConfiguration>
          <ArrayOfSalutation xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
            <Salutation>
              <DisplayName>{D[LetterSalutation.Default]}</DisplayName>
              <IsDefault>true</IsDefault>
              <Qualification>
                <Id>Label</Id>
                <IsPlural>false</IsPlural>
                <Gender>Undefined</Gender>
                <IsDefault>false</IsDefault>
              </Qualification>
            </Salutation>
            [...]
          </ArrayOfSalutation>
        </LetterSalutationConfiguration>
```
```xml
        <!-- GreetingFormulaConfiguration -->
        <GreetingFormulaConfiguration>
          <ArrayOfGreetingFormula xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
            <GreetingFormula>
              <DisplayName>{D[Greetings.Default]}</DisplayName>
              <IsDefault>true</IsDefault>
              <Qualification>
                <Id>Label</Id>
                <IsPlural>false</IsPlural>
                <Gender>Undefined</Gender>
                <IsDefault>false</IsDefault>
              </Qualification>
            </GreetingFormula>
            [...]
          </ArrayOfGreetingFormula>
        </GreetingFormulaConfiguration>
```
```xml
        <!-- ShippingMethodConfiguration -->
        <ShippingMethodConfiguration>
          <ArrayOfShippingMethod xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
            <ShippingMethod>
              <DisplayName>{D[ShippingMethod.Default]}</DisplayName>
              <IsDefault>true</IsDefault>
              <TypeOfDistribution>DefaultText</TypeOfDistribution>
            </ShippingMethod>
            [...]
          </ArrayOfShippingMethod>
        </ShippingMethodConfiguration>
```


