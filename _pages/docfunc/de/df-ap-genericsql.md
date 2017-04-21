---
layout: page
title: GenericSqlAddressProvider
permalink: "docfunc/de/df/ap/gernericsql"
language: de
---

Adressen werden per SQL Select Abrage in der Datenquelle abgeholt und einem Adressobjekt in OneOffixx zugewiesen. Jede DB Spalte wird mit dem Schlüsselwort "as" einem OneOffixx Feld zugewiesen. Die WHERE Clausel enthaltet die Filterparameter. Diese werden im Element SearchParameter definiert. Der Name des Parameters kann in der Query mit {} aufgerufen werden. 

```xml

 <AddressProvider id="8C51B042-81EA-46E3-A429-821641E19A6A" order="1" active="false">
  <Debug>false</Debug>
  <!-- Title for the Address Provider -->
  <Title>Generic SQL</Title>
  <!-- Connection string for generic sql provider database (driver: http://www.microsoft.com/en-us/download/details.aspx?id=13255) -->
  <ConnectionString>{ConnectionString}</ConnectionString>
  <!-- The provider which is use to open the connection and send the query -->
  <ConnectionProvider>System.Data.OleDb</ConnectionProvider>
  <Icon>{Base64 Image}</Icon>
  <!-- Query for the Search -->
  <Query>
    SELECT [SPALTENNAME] AS {Feldname OneOffixx} 
    FROM [TABLE]
    WHERE
        UCase([Vorname]) Like UCase('%{firstName}%') AND
        UCase([Name]) Like UCase('%{lastName}%') AND
        UCase([Strasse] &amp; ' ' &amp; [Hausnummer]) Like UCase('%{street}%') AND
        [Postleitzahl] Like '%{plz}%' AND
        UCase([Ort]) Like UCase('%{city}%')
  </Query>
  <!-- Search paremeters -->
  <SearchParameters>
    <SearchParameter Name="company" Label="Firma" Type="String" Length="100" Sort="1" />
    <SearchParameter Name="firstName" Label="Vorname/Name" Type="String" Length="100" Sort="2" />
    <SearchParameter Name="lastName" Label="" Type="String" Length="100" Sort="2" Width="90" />
    <SearchParameter Name="street" Label="Strasse" Type="String" Length="100" Sort="3" />
    <SearchParameter Name="plz" Label="PLZ/Ort" Type="String" Length="6" Sort="4" />
    <SearchParameter Name="city" Label="" Type="String" Length="100" Width="130" Sort="4" />
    <SearchParameter Name="country" Label="Land" Type="String" Length="100" Sort="5" />
  </SearchParameters>
</AddressProvider>

```

* __ConnectionString__ Datenbank [ConnectionString ](https://www.connectionstrings.com/).
* __ConnectionProvider__ Dataprovider -  System.Data.Odbc, System.Data.OleDb, System.Data.OracleClient, System.Data.SqlClient
* __Icon__ Base64 Image für Icon

Die Liste der Suchparameter ist für die Eingabemaske nötig. Falls keine SearchParameterliste angegeben ist, werden Suchparameter automatisch erzeugt.
```xml
<SearchParameter Name="company" Label="Firma" Type="String" Length="100" Sort="1" />
```

* __Name__ Eindeutiger Feldname. Kann in der Query verwendet werden im Format {XXX}
* __Label__ Anzeigetext im Dialog vor Control
* __Type__ Type des Controls (Mögliche Werte sind String, Long, Boolean, Date)


