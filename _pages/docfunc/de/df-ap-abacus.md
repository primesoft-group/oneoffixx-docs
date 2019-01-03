---
layout: page
title: AbacusAddressProvider
permalink: "docfunc/de/df/ap/abacus"
language: de
---

Auf Abacus kann entweder über einen WebService oder direkt auf die Datenbank zugegriffen werden. Die Verwendung der Indices liefert nicht in allen Anwendungsfällen die optimalen Ergebnisse. Wir empfehlen die Suche per [Generic SQL](#AbacusGenericSQL) zu realsieren.

## abaconnect Schnittstelle 2014
Ruft die Abacus Webservices Schnittstelle http://www.abacus.ch/abaconnect/2007.10 auf.
Über die abaconnect Schnittstelle können Addressdaten via Indices abgerufen werden. In OneOffixx können die Anzahl Indices und die Abfrage konfiguriert werden. Allerdings ist darauf zu achten, dass in Abacus die gleichen Indices ebenfalls vorhanden sind. Andernfalls schlägt die Suchabfrage fehl.

abaconnect fordert alle Felder an. Zum Beispiel, wird im Index 4 der Name weggelassen, werden alle Einträge ab AAAA ausgegeben.

```xml
<AddressProvider id="833075BF-DDE5-4E9B-83B9-E9803C96E391" order="15" active="false">
  <Uri>http://[server]:[port]/abaconnect/services/Address_[version]_00</Uri>
  <Version>2014</Version>
  <!-- Search indexes for abacus 2014 http://www.abacus.ch/fileadmin/zipfiles/abaconnect/adre/adre_acws_parameters.html -->
  <Indexes>
    <Index Id="1">
      <SearchParams>
        <SearchParam Name="AddressNumber" Type="Long" Length="10" Sort="1" />
      </SearchParams>
    </Index>
    <Index Id="2">
      <SearchParams>
        <SearchParam Name="CodeName" Type="String" Length="16" Sort="1" />
      </SearchParams>
    </Index>
    <Index Id="3">
      <SearchParams>
        <SearchParam Name="Country" Type="String" Length="4" Sort="1" />
        <SearchParam Name="ZIP" Type="String" Length="15" Sort="2" />
        <SearchParam Name="CodeName" Type="String" Length="16" Sort="3" />
      </SearchParams>
    </Index>
    <Index Id="4">
      <SearchParams>
        <SearchParam Name="Name" Type="String" Length="100" Sort="1" />
        <SearchParam Name="FirstName" Type="String" Length="50" Sort="2" />
        <SearchParam Name="ZIP" Type="String" Length="15" Sort="3" />
        <SearchParam Name="AddressNumber" Type="Long" Length="10" Sort="4" />
      </SearchParams>
    </Index>
  </Indexes>
</AddressProvider>
```

## AbacusGenericSQL
Der [Generic SQL Provider]({{ site.baseurl }}/docfunc/de/df/ap/genericsql) versucht aufgrund des Vornamens zu erkennen ob es sich um eine private oder geschäftliche Adresse handelt.

```xml
<AddressProvider id="8C51B042-81EA-46E3-A429-821641E19A6A" order="1" active="true">
  <Title>Abacus MYCOMPANY</Title>
  <!-- Icon in BASE64 format for the Address Provider -->
  <Icon>iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAIAAACQkWg2AAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAAZdEVYdFNvZnR3YXJlAHBhaW50Lm5ldCA0LjAuMTM0A1t6AAABtUlEQVQ4T5WRyy8DURSH/SF2SKzZW4tYsWKBsCHCwo6QiDTEwkIEoZHYoBHSaGhQ8SyCKtIgrXaqqq3SmU7n0bnzuuNULzoiEt9q7r2/7+ScM0XGP/lFSE86QqXNOIvI2YxZ0HTe7hZdl8y4PT2zLt8/kfsCTIIuomhNH+841V5ZqryVGVuFG/L2ybeArkMpywJ0ImxfPtcNqjGanXU+VnbirEwSHxABbrVUBl0F5duIEowLG2fClkd0eenR5czirux/zscAImTmt5SHGMyQaBuTzv1YkqO1/bz9WEtxVFlLyrKoc9l8Midwtn0DYzVOs3NOrGrIF34bmMciEne88cZh9emVndsMV3RAC0RQH5MwJVSFD4VKQAKakTwB5A2yVqfgPOeW9pJdE1CCCABr3dBZEStqvGUUXVOwnEhVT25dNBcqaYJl5GMAEQA5EEtPOwxdzx76kt1TOsNztoNodS/MpgsSCRUK0JWw6ZHvItKFH342DMCvusGEqUjig28BgErhinZu+VBj+GBxAz2yRB4KMAmA9sLwK0ex+iF0Q32tspCfAsCvnURr+jFSyNnML8JfGMY7nTO7bRIF1AcAAAAASUVORK5CYII=</Icon>
  <ConnectionString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog={DataSource};Data Source={DB};</ConnectionString>
  <ConnectionProvider>System.Data.OleDb</ConnectionProvider>
  <Query>
SELECT TOP (1000) 
	CASE WHEN COALESCE(A.Vorname,'') = '' THEN A.Nachname  ELSE '' END as CompanyName, 
	CASE WHEN COALESCE(A.Vorname,'') = '' THEN A.Bezeichnung ELSE '' END as Department, 
	CASE WHEN COALESCE(A.Vorname,'') = '' THEN '' ELSE A.Bezeichnung END as Position, 
	CASE WHEN COALESCE(A.Vorname,'') = '' THEN K.Nachname  ELSE A.Nachname END as LastName, 
	CASE WHEN COALESCE(A.Vorname,'') = '' THEN K.Vorname ELSE A.Vorname END as FirstName, 
	CASE WHEN COALESCE(A.Vorname,'') = '' OR A.Begruessung IS NULL THEN A.Begruessung ELSE K.Begruessung END as SalutationShort, 
	CASE WHEN COALESCE(A.Vorname,'') = '' OR A.BegruessungsText IS NULL THEN A.BegruessungsText ELSE K.BegruessungsText END as Salutation, 
	CASE WHEN A.Land IS NULL THEN 'CH' ELSE A.Land END as CountryCode, 
	A.PLZ as Zip,
	A.Stadt as City,
	A.Adresse1 as Street, 
	A.Adresse2 as PostOfficeBox, 
	A.Email as EmailBusinessDirect, 
	A.Telefon1 as PhoneBusinessDirect,                      
	A.Mobil as MobileBusiness, 
	A.Fax as FaxBusinessDirect, 
	A.Webseite as HomepageBusiness, 
	K.Email AS EmailPrivat, 
	K.Telefon1 as PhonePrivat, 
	K.Mobil AS MobilePrivat, 
	K.Fax as FaxPrivat
	FROM Adresse A 
	LEFT OUTER JOIN Kontakt K ON A.ID = K.AdresseID
	WHERE        
	('{company}' = '' OR A.Nachname Like '%{company}%' OR K.Nachname like '%{company}%') AND 
	('{firstName}' = '' OR A.Vorname Like '%{firstName}%' OR K.Vorname like '%{firstName}%') AND 
	('{plz}' = '' OR A.PLZ Like '%{plz}%') AND 
	('{city}' = '' OR A.Stadt Like '%{city}%') AND
	('{addressid}' = '' OR Str(A.ID) Like '%{addressid}%' )
	</Query>
  <!-- Definition der Suchfelder (optional) -->
  <SearchParameters>
    <SearchParameter Name="company" Label="Nachname/Firma" Type="String" Length="100" Sort="1" />
    <SearchParameter Name="firstName" Label="Vorname" Type="String" Length="100" Sort="2" />
    <SearchParameter Name="plz" Label="PLZ/Ort" Type="String" Length="6" Sort="3" />
    <SearchParameter Name="city" Label="" Type="String" Length="100" Width="130" Sort="3" />
    <SearchParameter Name="addressid" Label="Address ID" Type="String" Length="100" Sort="4" />
  </SearchParameters>
</AddressProvider>

```