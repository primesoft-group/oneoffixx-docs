---
layout: page
title: RecipientAddresses / Empfängeradresse
permalink: "docfunc/de/df/recipientaddress"
language: de
---

Die Dokumentfunktion "Empfängeradresse" muss einer Vorlage angehängt werden, wenn der Empfängerdialog angezeigt werden soll. Im Konfiguratonsfenster kann der Empfängerdialog auf verschiedene Weisen auf die Lösung massgeschneidert werden. In der Konfiguration verweisen mehrere Links auf den globalen Konfigurationsprovider, wo die Konfiguration der verschiedenen Gruss- und Abschiedsformeln hinterlegt sind. Der genaue Wortlaut und Übersetzungen der Formeln können im globalen Übersetzungsprovider angepasst werden.

Im folgenden Abschnitt wird zuerst auf die _OneOffixx-Adressprovider_ eingegangen.
Für allgemeine Informationen zur Dokument-Funktion siehe [Konfiguration des Empfängerdialogs]((#konfiguration-des-empfängerdialogs)) weiter unten.

## OneOffixx-Adressprovider
- [AbacusAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/abacus)
- [CobraAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/cobra)
- [CreativAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/creativ)
- [DynamicsNavisionAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/msdynamics)
- [EGDVAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/ruf)
- [ExchangeAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/msexc)
- [GenericSqlAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/gernericsql)
- [GoogleMapsAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/google)
- [LDAPAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/ldap)
- [LotusNotesAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/lotusnotes)
- [NestAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/nest)
- [OutlookAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/outlook)
- [SAPPulsAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/sappuls)
- [SharepointAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/sharepoint)
- [TelSearchCHAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/telsearch)
- [UserDefinedAddressProvider z.Bsp. für Excel]({{ site.baseurl }}/docfunc/de/df/ap/userdefined/)
- [VertecAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/vertec)
- [ZefixAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/zefix)

Addressprovider sind Plugins welche eine Schnittstelle zu einer Adressquelle implementieren. Auf Wunsch werden Addressprovider kundenspezifisch implementiert. Die Verwendung der Addressprovider kann mit Lizenzkosten verbunden sein.

![]({{ site.baseurl }}/assets/content-images/docfunc/de/recipientdialog.png)

Folgende Parameter können in allen Providern angewandt werden. 

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

_**Attribute**_
* __id__ GUID des Adressproviders
* __order__ Reihenfolge in der Dialog-Übersicht
* __active__ true = der Dialog wird angezigt
* __hiddenIfNotAvailable__ Der Dialog wird nicht angezeigt, wenn die Adressquelle nicht erreichbar ist.

_**Elemente**_
* __Debug__ Erweiterte Ausgabe im Log. 
* __Uri__  (Optional) URL auf WS Adresssen.
* __Timeout__ (Optional) Maximale Wartezeit bis Ergebnisse vom Webservice geliefert werden.
* __EnableProxyCredentials__ (Optional) Falls ein Proxy im LAN betrieben wird können Logindaten im Proxy überschrieben werden. Andernfalls werden diese vom IE übernommen.
* __ProxyCredentialsName__ (Optional) Proxy Loginname.
* __ProxyCredentialsPassword__ (Optional) Proxy Password.
* __DetailsColumnMapping__ (Optional) Mappt Daten in der Trefferliste in die Datailspalte. Muss ein XPath innerhalb des generierten Contacts sein. Zum Beispiel: //Person/LastName für den Nachname oder //AddressProviderData/@Id für den Addressprovider ./ExtendentFields/Item @Key='Dynamic.Detail'] für ein ExtendedField ('Detail').

Verschiedene Provider unterstützen ein zusätzliches ContactMapping. Zum Beispiel um SQL Spalten in OneOffixx Adressfelder zu mappen.
```xml
<ContactMapping>
    <ContactItemXPath>Contact</ContactItemXPath>  Standard-Einstellung 
    <ContactElement id="Person_PostOfficeBoxCityZipCode">PERSON_ZIPCODE</ContactElement> Mapping vom Key "PERSON_ZIPCODE" 
    <ContactElement id="Person_PostOfficeBoxCityZipCode">"FESTER WERT"</ContactElement> Mapping mit definierten Wert "FESTER WERT" 
    <ContactElement id="Company_Street" when="TYPE = 'Interne Adresse'">STREET</ContactElement>
</ContactMapping>
```

Es gibt eine Reihe von definierten "Prefixes" um das Mapping genauer zu spezifizieren: __Person__, __Company__, __Options__, __ExtendedField__ (Achtung – Mappings auf ExtendedFields bekommen den Prefix "Dynamic"), z. B.

Mapping: <ContactElement id="ExtendedField_Detail">"Provider-Value"</ContactElement>
Nutzung für das DetailColumnMapping: <DetailsColumnMapping>./ExtendentFields/Item[@Key='Dynamic.Detail']</DetailsColumnMapping> 
                
Dazu gibt es folgene Felder die man mappen kann (passend zu dem jeweiligen Contact-Element): (mit oder ohne Prefix, also z.B. Person_Name oder Name)

{:.table .table-striped}                 
Type | Mögliche Werte
---------|----------
Person-related | Name, LastName, FirstName, Title, SecondName, NickName, Initials, BirthDate, Profession, Position, SalutationShort, LetterSalutation, Greeting
Company-related | Name, CompanyName, Supplement, Department
Address-related (sowohl Company als auch Person) | Street, CareOf, Apartment, Floor, City, PostOfficeBox, PostOfficeBoxCityZipCode, Country 
Communication-related (sowohl Company als auch Person) | Language, Phone, Email, Fax, Mobile, Homepage, PhoneDirect, PhoneCentral, EmailDirect, EmailCentral, FaxDirect, FaxCentral
Option-related | SelectedAddress, AddressingType, AddressLabel, PersonOverFirm, CountryView, CountryCodeView, CapitalizedCity, CompanyView, SalutationView, SalutationSeparatetLine, SecondNameView, PositionView, InterneAddress

__Conditions:__ Beim Mapping werden auch Conditions unterstützt, z.B.
```xml 
ContactElement id="Company_Street" when="TYPE = 'Interne Adresse'">STREET</ContactElement>
```

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
   Kann `true`oder `false` enthalten. Bestimmt, ob die folgenden Details im Dialog angezeigt werden.
   ![x]({{ site.baseurl }}/assets/content-images/docfunc/de/recipientAddressesDetailsInDialog.png)
* `AddressingTypes`<br>
  Hier können Anzeigenamen für die 3 Adresstypen konfiguriert werden.<br>
  Z. B. `An;Cc;Bcc` oder `Anwesend;Abgemeldet;Verteiler`, je nach Verwendungszweck der Adresstypen.
* `UseEnglishCountryNames`<br>
  Kann `true`oder `false` enthalten. Bestimmt, ob Ländernamen immer englisch sind (true) oder ob sie in der jeweiligen Dokument-Sprache ausgegeben werden (false).
* `PreferredRecipientId`<br>
  Falls die Voralge über Conenct aufgerufen und falls im Connect-Aufruf-XML Empfänger definiert sind: Hier wird anhand der ID bestimmt, welcher Empfänger ausgewählt sein soll.
* `CapitalizedCities`<br>
  Kann `true`oder `false` enthalten. Bestimmt, ob die Städte-Namen im Adressblock in GROSSBUCHSTABEN geschrieben werden sollen (true) oder nicht (false).
* `DefaultLanguageCode`<br>
  Hat momentan keinen Effekt.
* `DefaultCountryCode`<br>
  Hier kann der Länder-Code des Standard-Landes gesetzt werden. Das Standard-Land ist jeweils zu Beginn ausgewählt.
* `CustomCountries`<br>
  Hier können mit folgendem Muster Länder hinzugefügt werden, welche im dialog standardmässig nicht vorhanden sind:<br>
  `<CustomCountry Name="Amerikanische Jungferninseln" EnglishName="United States Virgin Islands" ISO="VI" />`

#### Adressprovider

Die Konfiguration der Adressprovider wird in fast allen Fällen in den globalen Konfigurationsprovider ausgelagert.
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


