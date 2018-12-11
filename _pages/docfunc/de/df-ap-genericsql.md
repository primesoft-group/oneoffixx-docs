---
layout: page
title: GenericSqlAddressProvider
permalink: "docfunc/de/df/ap/genericsql"
language: de
---

Adressen werden per SQL Select-Abfrage an der Datenquelle abgeholt und einem Adressobjekt in OneOffixx zugewiesen. Jede Datenbank-Spalte wird mit dem Schlüsselwort "as" in ein OneOffixx Feld abgefüllt. Die WHERE-Klausel enthält die Filterparameter. Diese werden im Element ___SearchParameter___ definiert. Der Wert eines Parameters kann in der Query mit {_Parametername_} aufgerufen werden. 

```xml

 <AddressProvider id="8C51B042-81EA-46E3-A429-821641E19A6A" order="1" active="false">
  <Debug>false</Debug>
  <Title>Generic SQL Provider</Title>
  <Icon>{Base64 Image}</Icon>
  <SafeQuery>false</SafeQuery>
  <ConnectionString>{ConnectionString}</ConnectionString>
  <ConnectionProvider>System.Data.OleDb</ConnectionProvider>

  <Query>
    <!-- Example in T-SQL -->
    SELECT 
        [SPALTENNAME] AS {Feldname OneOffixx} 
    FROM [TABLE]
    WHERE
        UCase([Vorname]) Like UCase('%{firstName}%') AND
        UCase([Name]) Like UCase('%{lastName}%') AND
        UCase([Strasse] &amp; ' ' &amp; [Hausnummer]) Like UCase('%{street}%') AND
        [Postleitzahl] Like '%{plz}%' AND
        UCase([Ort]) Like UCase('%{city}%')
  </Query>

  <SearchParameters>
    <SearchParameter Name="company" Label="Firma" Type="String" Length="100" Sort="1" />
    <SearchParameter Name="firstName" Label="Vorname/Name" Type="String" Length="100" Sort="2" />
    <SearchParameter Name="lastName" Label="" Type="String" Length="100" Sort="2" Width="90" />
    <SearchParameter Name="street" Label="Strasse" Type="String" Length="100" Sort="3" />
    <SearchParameter Name="plz" Label="PLZ/Ort" Type="String" Length="6" Sort="4" />
    <SearchParameter Name="city" Label="" Type="String" Length="100" Width="130" Sort="4" />
    <SearchParameter Name="country" Label="Land" Type="String" Length="100" Sort="5" />
  </SearchParameters>

  <ContactMapping>
    <ContactItemXPath>Contact</ContactItemXPath>
    <ContactElement id="Person_LastName">Column_LastName</ContactElement>
    <ContactElement id="Person_FirstName">Column_FirstName</ContactElement>
  </ContactMapping>
</AddressProvider>

```


## Aufbau

* __Debug__ *true* falls zusätzliche Informationen geloggt werden sollen
* __Title__ Titel des Adressproviders (wird so in Tab angezeigt)
* __Icon__ Bild für Icon *(als Base64-String; empfohlen: PNG, 32x32 Pixel)*
* __SafeQuery__  Fügt vor jeden Parameter im Query ein '@' ein (*true* nur möglich für *System.Data.SqlClient*)
* __ConnectionString__ Datenbank [ConnectionString ](https://www.connectionstrings.com/).
* __ConnectionProvider__ 
    * System.Data.Odbc
    * System.Data.OleDb
    * System.Data.OracleClient
    * System.Data.SqlClient

## Query

Die Abfrage in der korrekten Syntax und Sprache für den gewählten Provider. Es gilt zu beachten, dass es erhebliche Unterschiede zwischen den SQL-Dialekten gibt.

#### Beispiel für Transact-SQL 

```sql
SELECT 
    [Column1] AS OneOffixxFieldname1, 
    [Column2] AS OneOffixxFieldname2, 
FROM [TABLENAME]
WHERE
    UCase([Column1]) Like UCase('%{searchParam1}%') AND
    UCase([Column2]) Like UCase('%{searchParam2}%')
```

#### Beispiel für Oracle SQL

```sql
SELECT 
    Column1 AS "OneOffixxFieldname1",
    Column2 AS "OneOffixxFieldname2"
FROM TABLENAME
WHERE
    UPPER(Column1) Like UPPER('%{searchParam1}%') AND
    UPPER(Column2) Like UPPER('%{searchParam2}%') 
```

## SearchParameter

Die Liste der Suchparameter ist für die Eingabemaske nötig. Falls keine SearchParameterliste angegeben ist, werden Suchparameter automatisch erzeugt. Es können maximal zwei Controls auf einer Zeile plaziert werden.
```xml
<SearchParameter Name="company" Label="Firma" Type="String" Length="100" Sort="1" />
```

* __Name__ Eindeutiger Feldname. Kann in der Query verwendet werden im Format {XXX}
* __Label__ Anzeigetext im Dialog vor Control
* __Type__ Type des Controls (Mögliche Werte sind String, Long, Boolean, Date)

## ContactMapping *(optional)*

Fürs Mapping der Rückgabewerte stehen ein Vielzahl von Zielfeldern zur Verfügung. Jedes Feld wird über ein Prefix von **Person** oder **Company** angesprochen, nicht alle Felder existieren jedoch für beide Kategorien.

**Hinweis:** Wenn die Kolonnennamen der Datenbankresultate mit den Feldnamen übereinstimmen, ist kein weiteres ContactMapping nötig.  


### Mapping für *Person* und *AdditionalPerson*

**Hinweis:** die Felder für *AdditionalPerson* sind identisch, beginnen aber mit *AdditionalPerson_* anstelle *Person_*.

{:.table .table-striped}
| Kategorie | Feldname | Beschreibung |                      
| -- | -- | -- | --- | --- |
| Person | Person_Title | Titel |
| Person | Person_LastName | Nachname |
| Person | Person_FirstName |  Vorname |
| Person | Person_SecondName | Zweitname |
| Person | Person_NickName | Spitzname |
| Person | Person_Initials | Initialen |
| Person | Person_Birthday | Geburtstag *(als DateTime)* |
| Person | Person_Profession | Beruf / Funktion |
| Person | Person_Position | Position |
| Person | Person_SalutationShort | Anrede kurz |
| Person | Person_Salutation | Anrede |
| Person | Person_Greeting | Grussformel |
| Person | Person_Picture | Bild der Person *(als Byte-Array / base64-String)* |
| Adresse | Person_Street | Strasse
| Adresse | Person_CareOf | Zustellanweisung (c/o) |
| Adresse | Person_Apartment | Apartment |
| Adresse | Person_Floor | Stockwerk |
| Adresse | Person_City | Ortsname |
| Adresse | Person_City_ZipCode | Postleitzahl |
| Adresse | Person_Country | Ländername |
| Adresse | Person_Country_ShortCode | Länder ISO-Code |
| Adresse | Person_PostOfficeBoxCity | Ort von Postfach |
| Adresse | Person_PostOfficeBoxCity_ZipCode | Postleitzahl von Postfach |
| Kommunikation | Person_Language | Sprache |
| Kommunikation | Person_PhoneDirect | Telefonnummer |
| Kommunikation | Person_Mobile | Mobiltelefonnummer |
| Kommunikation | Person_FaxDirect | Faxnummer |
| Kommunikation | Person_EmailDirect | Emailadresse |
| Kommunikation | Person_Homepage | Webseite |

```xml
<ContactMapping>
	<ContactItemXPath>Contact</ContactItemXPath>	  
	<ContactElement id="Person_Title">...</ContactElement>
	<ContactElement id="Person_LastName">...</ContactElement>
	<ContactElement id="Person_FirstName">...</ContactElement>
	<ContactElement id="Person_SecondName">...</ContactElement>
	<ContactElement id="Person_NickName">...</ContactElement>
	<ContactElement id="Person_Initials">...</ContactElement>
	<ContactElement id="Person_Birthday">...</ContactElement>
	<ContactElement id="Person_Profession">...</ContactElement>
	<ContactElement id="Person_Position">...</ContactElement>
	<ContactElement id="Person_SalutationShort">...</ContactElement>
	<ContactElement id="Person_Salutation">...</ContactElement>
	<ContactElement id="Person_Greeting">...</ContactElement>
	<ContactElement id="Person_Picture">...</ContactElement>
	<ContactElement id="Person_Street">...</ContactElement>
	<ContactElement id="Person_CareOf">...</ContactElement>
	<ContactElement id="Person_Apartment">...</ContactElement>
	<ContactElement id="Person_Floor">...</ContactElement>
	<ContactElement id="Person_City">...</ContactElement>
	<ContactElement id="Person_City_ZipCode">...</ContactElement>
	<ContactElement id="Person_Country">...</ContactElement>
	<ContactElement id="Person_Country_ShortCode">...</ContactElement>
	<ContactElement id="Person_PostOfficeBoxCity">...</ContactElement>
	<ContactElement id="Person_PostOfficeBoxCity_ZipCode">...</ContactElement>
	<ContactElement id="Person_Language">...</ContactElement>
	<ContactElement id="Person_PhoneDirect">...</ContactElement>
	<ContactElement id="Person_Mobile">...</ContactElement>
	<ContactElement id="Person_FaxDirect">...</ContactElement>
	<ContactElement id="Person_EmailDirect">...</ContactElement>
	<ContactElement id="Person_Homepage">...</ContactElement>
</ContactMapping>
```


### Mapping für Firmen

{:.table .table-striped}
| Kategorie | Feldname | Beschreibung |                      
| -- | -- | -- | --- | --- |
| Firma | Company_CompanyName | Firmenname |
| Firma | Company_Supplement | Zusatz |
| Firma | Company_Department | Abteilung |
| Firma | Company_Picture | Logo der Firma *(als Byte-Array / base64-String)* |
| Adresse | Company_Street | Strasse
| Adresse | Company_CareOf | Zustellanweisung (c/o) |
| Adresse | Company_Apartment | Apartment |
| Adresse | Company_Floor | Stockwerk |
| Adresse | Company_City | Ortsname |
| Adresse | Company_City_ZipCode | Postleitzahl |
| Adresse | Company_Country | Ländername |
| Adresse | Company_Country_ShortCode | Länder ISO-Code |
| Adresse | Company_PostOfficeBoxCity | Ort von Postfach |
| Adresse | Company_PostOfficeBoxCity_ZipCode | Postleitzahl von Postfach |
| Kommunikation | Company_Language | Sprache |
| Kommunikation | Company_PhoneDirect | Telefonnummer *(direkt)* |
| Kommunikation | Company_PhoneCentral | Telefonnummer *(Zentrale)* |
| Kommunikation | Company_Mobile | Mobiltelefonnummer |
| Kommunikation | Company_FaxDirect | Faxnummer *(direct)* |
| Kommunikation | Company_FaxCentral | Faxnummer *(Zentrale)* |
| Kommunikation | Company_EmailDirect | Emailadresse *(direkt)* |
| Kommunikation | Company_EmailCentral | Emailadresse *(Zentrale)* |
| Kommunikation | Company_Homepage | Webseite |

```xml
<ContactMapping>	
	<ContactElement id="Company_CompanyName">...</ContactElement>
	<ContactElement id="Company_Supplement">...</ContactElement>
	<ContactElement id="Company_Department">...</ContactElement>
	<ContactElement id="Company_Picture">...</ContactElement>
	<ContactElement id="Company_Street">...</ContactElement>
	<ContactElement id="Company_CareOf">...</ContactElement>
	<ContactElement id="Company_Apartment">...</ContactElement>
	<ContactElement id="Company_Floor">...</ContactElement>
	<ContactElement id="Company_City">...</ContactElement>
	<ContactElement id="Company_City_ZipCode">...</ContactElement>
	<ContactElement id="Company_Country">...</ContactElement>
	<ContactElement id="Company_Country_ShortCode">...</ContactElement>
	<ContactElement id="Company_PostOfficeBoxCity">...</ContactElement>
	<ContactElement id="Company_PostOfficeBoxCity_ZipCode">...</ContactElement>
	<ContactElement id="Company_Language">...</ContactElement>
	<ContactElement id="Company_PhoneDirect">...</ContactElement>
	<ContactElement id="Company_PhoneCentral">...</ContactElement>
	<ContactElement id="Company_Mobile">...</ContactElement>
	<ContactElement id="Company_FaxDirect">...</ContactElement>
	<ContactElement id="Company_FaxCentral">...</ContactElement>
	<ContactElement id="Company_EmailDirect">...</ContactElement>
	<ContactElement id="Company_EmailCentral">...</ContactElement>
	<ContactElement id="Company_Homepage">...</ContactElement>
</ContactMapping>
```


### Mapping für Optionen

{:.table .table-striped}
| Kategorie | Feldname | Beschreibung | Werte |                     
| -- | -- | -- | --- | --- |
| Optionen | Options_SelectedAddress | Steuert ob die geschäftliche oder private Adressierung verwendet wird | *Business, Private* |
| Optionen | Options_AddressingType | Steuert ob der Empfänger das Dokument direkt oder als Kopie erhält | *An, Cc, Bcc* |
| Optionen | Options_ShowProviderLayout | Steuert ob das Layout der Adressierung von OneOffixx erstellt wird oder ob jenes des Adresslieferanten verwendet wird | *true, false* |
| Optionen | Options_PersonOverFirm | Steuert ob der Name des Ansprechpartners oberhalb der Firmenbezeichnung in der Adressierung angezeigt wird - für eine persönliche / vertrauliche Adressierung | *true, false* |
| Optionen | Options_CountryView | Steuert ob das Land in der Adressierung angezeigt wird | *true, false* |
| Optionen | Options_CountryCodeView | Steuert ob das Länderkurzzeichen in der Adressierung angezeigt wird | *true, false* |
| Optionen | Options_CompanyView | Steuert ob die Firmanansicht standardmässig angezeigt wird | *true, false* |
| Optionen | Options_CapitalizedCity | Steuert ob der Ortschaftsnamen in Grossbuchstaben geschrieben wird | *true, false* |
| Optionen | Options_SalutationView | Steuert ob die Anrede in der Adressierung angezeigt wird | *true, false* |
| Optionen | Options_SalutationSeparatetLine | Steuert ob die Anrede auf einer separaten Zeile angezeigt wird | *true, false* |
| Optionen | Options_SecondNameView | Steuert ob der Zweitname angezeigt wird | *true, false* |
| Optionen | Options_PositionView | Steuert ob die Position resp. Funktion der Person angezeigt wird | *true, false* |
| Optionen | Options_InterneAddress | Steuert ob Checkbox *interne Adresse* angewählt ist | *true, false* |
| Versand | Transmission_Text | *nicht ohne Weiteres einsetzbar* | |
| Versand | Transmission_DocumentLanguage | *nicht ohne Weiteres einsetzbar* |  |
| Versand | Transmission_TypeOfDistribution | *nicht ohne Weiteres einsetzbar* |  |
| Provider | AddressProviderData_Id | *nicht ohne Weiteres einsetzbar* |  |
| Provider | AddressProviderData_Name | *nicht ohne Weiteres einsetzbar* |  |
| Provider | AddressProviderData_Updated | *nicht ohne Weiteres einsetzbar* | *DateTime* |
| Provider | AddressProviderData_Published | *nicht ohne Weiteres einsetzbar* | *DateTime* |
| Provider | AddressProviderData_ProviderResponse | *nicht ohne Weiteres einsetzbar* |  |
| Provider | AddressProviderData_Label | *nicht ohne Weiteres einsetzbar* |  |
| Provider | AddressProviderData_Label_Type | *nicht ohne Weiteres einsetzbar* | *text, html* |
| Provider | AddressProviderData_Links | *nicht ohne Weiteres einsetzbar*  | *complex* |
| Zusatz | Extension | *nicht ohne Weiteres einsetzbar* | |
| Zusatz | Extension_Key | *nicht ohne Weiteres einsetzbar* | |

**Hinweis:** Einige müssen jeweils von Fall zu Fall mit der Entwicklung abgesprochen werden, da es dort Querabhängigkeiten geben kann.

```xml
<ContactMapping>
	<ContactElement id="Options_SelectedAddress">...</ContactElement>
	<ContactElement id="Options_AddressingType">...</ContactElement>
	<ContactElement id="Options_ShowProviderLayout">...</ContactElement>
	<ContactElement id="Options_PersonOverFirm">...</ContactElement>
	<ContactElement id="Options_CountryView">...</ContactElement>
	<ContactElement id="Options_CountryCodeView">...</ContactElement>
	<ContactElement id="Options_CompanyView">...</ContactElement>
	<ContactElement id="Options_CapitalizedCity">...</ContactElement>
	<ContactElement id="Options_SalutationView">...</ContactElement>
	<ContactElement id="Options_SalutationSeparatetLine">...</ContactElement>
	<ContactElement id="Options_SecondNameView">...</ContactElement>
	<ContactElement id="Options_PositionView">...</ContactElement>
	<ContactElement id="Options_InterneAddress">...</ContactElement>
</ContactMapping>
```