---
layout: page
title: Empfängeradresse
permalink: "docfunc/de/df/recipientaddress"
language: de
---

Die Dokumentfunktion ‘Empfängeradresse’ muss einer Vorlage angehängt werden, wenn der Empfängerdialog angezeigt werden soll. Im Konfiguratonsfenster kann der Empfängerdialog auf verschiedene Weisen auf die Lösung massgeschneidert werden. In der Konfiguration verweisen mehrere Links auf den globalen Konfigurationsprovider, wo die Konfiguration der verschiedenen Gruss- und Abschiedsformeln hinterlegt sind. Der genaue Wortlaut und Übersetzungen der Formeln können im globalen Übersetzungsprovider angepasst werden.

Addressprovider sind Plugins welche eine Schnittstelle zu einer Adressquelle implementieren. Auf Wunsch werden Addressprovider kundenspezifisch implementiert. Die Verwendung der Addressprovider kann mit Lizenzkosten verbunden sein..

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

Es gibt eine Reihe von definierten "Prefixes" um das Mapping genauer zu spezifizieren: __Person___, __Company___, __Options___, __ExtendedField___ (Achtung - Mappings auf ExtendedFields bekommen den Prefix "Dynamic"), z.B.

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

CONDITIONS: Beim Mapping werden auch Conditions unterstützt, z.B.
```xml 
ContactElement id="Company_Street" when="TYPE = 'Interne Adresse'">STREET</ContactElement>
```

## OneOffixx Addressprovider
- [AbacusAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/abacus)
- [CobraAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/cobra)
- [CreativAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/creativ)
- [DynamicsNavisionAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/msdynamics)
- [EGDVAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/ruf)
- [ExchangeAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/msexc)
- [GenericSqlAddressProvider]({{ site.baseurl }}/docfunc/de/df/ap/gernericsql)
- [GoogleMapsAddressProvider](#googlemapsaddressprovider)
- [LDAPAddressProvider](#ldapaddressprovider)
- [LotusNotesAddressProvider](#lotusnotesaddressprovider)
- [NestAddressProvider](#nestaddressprovider)
- [OutlookAddressProvider](#outlookaddressprovider)
- [SAPPulsAddressProvider](#sappulsaddressprovider)
- [SharepointAddressProvider](#sharepointaddressprovider)
- [TelSearchCHAddressProvider](#telsearchchaddressprovider)
- [UserDefinedAddressProvider](#userdefinedaddressprovider)
- [VertecAddressProvider](#vertecaddressprovider)
- [ZefixAddressProvider](#zefixaddressprovider)


## ExchangeAddressProvider
Ermöglicht Adressabfrage direkt auf die Exchange Server API

## GoogleMapsAddressProvider

## LDAPAddressProvider

## LotusNotesAddressProvider

## NestAddressProvider

## OutlookAddressProvider

## SAPPulsAddressProvider

## SharepointAddressProvider

## TelSearchCHAddressProvider

## UserDefinedAddressProvider

## VertecAddressProvider

## ZefixAddressProvider

