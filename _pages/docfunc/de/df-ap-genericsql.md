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
* __ConnectionString__ Datenbank [ConnectionString ](https://www.connectionstrings.com/).
* __ConnectionProvider__ 
    * System.Data.Odbc
    * System.Data.OleDb
    * System.Data.OracleClient
    * System.Data.SqlClient

## Query

Die Abfrage in der korrekten Syntax und Sprache für den gewählten Provider. Es gilt zu beachten, dass es erhebliche Unterschiede zwischen den SQL-Dialekten gibt.

### Transact-SQL

```sql
SELECT 
    [Column1] AS {OneOffixxFieldname1}, 
    [Column2] AS {OneOffixxFieldname2}, 
FROM [TABLENAME]
WHERE
    UCase([Column1]) Like UCase('%{searchParam1}%') AND
    UCase([Column2]) Like UCase('%{searchParam2}%')
```

### Oracle

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

Die Liste der Suchparameter ist für die Eingabemaske nötig. Falls keine SearchParameterliste angegeben ist, werden Suchparameter automatisch erzeugt.
```xml
<SearchParameter Name="company" Label="Firma" Type="String" Length="100" Sort="1" />
```

* __Name__ Eindeutiger Feldname. Kann in der Query verwendet werden im Format {XXX}
* __Label__ Anzeigetext im Dialog vor Control
* __Type__ Type des Controls (Mögliche Werte sind String, Long, Boolean, Date)

## ContactMapping (optional)

Fürs Mapping der Rückgabewerte stehen ein Vielzahl von Zielfeldern zur Verfügung. Jedes Feld wird über ein Prefix von **Person** oder **Company** angesprochen, nicht alle Felder existieren jedoch für beide Kategorien.

**Wichtig:** Wenn die Kolonnennamen der Datenbankresultate mit den Feldnamen übereinstimmen, ist kein weiteres ContactMapping nötig.  

{:.table .table-striped}
| Kategorie | Feldname | Für *Person_* | Für *Company_*  | Beschreibung |                      
| -- | -- | -- | --- | --- |
| | _Title | x | | Titel |
| | _LastName | x | | Nachname |
| | _FirstName | x | | Vorname |
| | _SecondName | x | | Zweitname |
| | _NickName | x | | Spitzname |
| | _Initials | x | | Initialen |
| | _Birthday | x | | Geburtstag *(als DateTime)* |
| | _Profession | x | | Beruf / Funktion |
| | _Position | x | | Position |
| | _SalutationShort | x | | Anrede kurz
| | _Salutation | x | | Anrede
| | _Greeting | x | | Grussformel
| | _Picture | x | | Bild der Person *(als Byte-Array)* |
| | _Name | | x | Name |
| | _CompanyName | | x | Firmenname |
| | _Supplement | | x | Zusatz |
| | _Department | | x | Abteilung |
| Adresse | _Street | x | x | Strasse
| Adresse | _CareOf | x | x | Zustellanweisung (c/o) |
| Adresse | _Apartment | x | x | Apartment |
| Adresse | _Floor | x | x | Stockwerk |
| Adresse | _City | x | x | Ortsname |
| Adresse | _Country | x | x | Ländername |
| Adresse | _CountryShortCode | x | x | Länder ISO-Code |
| Adresse | _ZipCode | x | x | Postleitzahl |
| Adresse | _PostOfficeBox | x | x | Postfach |
| Adresse | _PostOfficeBoxCityZipCode | x | x | Postleitzahl von Postfach |
| Adresse | _PostOfficeBoxCity | x | x | Ort von Postfach|
| Kommunikation | _Language | x | x | Sprache |
| Kommunikation | _Mobile | x | x | Mobiltelefonnummer |
| Kommunikation | _Homepage | x | x | Webseite |
| Kommunikation | _Phone | x | x | Telefonnummer |
| Kommunikation | _PhoneDirect | x | x | Telefonnummer *(direkt)* |
| Kommunikation | _PhoneCentral | x | x | Telefonnummer *(Zentrale)* |
| Kommunikation | _Email | x | x | Emailadresse |
| Kommunikation | _EmailDirect | x | x | Emailadresse *(direkt)* |
| Kommunikation | _EmailCentral | x | x | Emailadresse *(Zentrale)* |
| Kommunikation | _Fax | x | x | Faxnummer |
| Kommunikation | _FaxDirect | x | x | Faxnummer *(direkt)* |
| Kommunikation | _FaxCentral | x | x | Faxnummer *(Zentrale)* |


