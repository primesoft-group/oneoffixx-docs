---
layout: page
title: NEST/is-e
permalink: "docfunc/de/df/nestise"
language: de
---

{% include new-badge.html version="3.3" %} 

Nest-Adressprovider von [Innosolv](https://www.nest.ch).

Die OneOffixx-Nest-Adressschnittstelle spricht vom «BasisService» den Endpunkt «FindSubjektKontaktperson» an.

## Vor NEST-Release 2018

Beispiel-Konfiguration:

```xml
<AddressProvider id="B16EC67C-444E-46DC-A659-93E95BB4EB4D" order="8" active="false" hiddenIfNotAvailable="true">
  <Uri>http://services.example.com:12345/BasisService</Uri>
  <UserName>myUserName</UserName>
  <Password>myPassword</Password>
</AddressProvider>
```

## Ab NEST-Release 2018

Beispiel-Konfiguration 1 (minimal):
```xml
<!-- Nest Address-Provider -->
<AddressProvider id="B16EC67C-444E-46DC-A659-93E95BB4EB4D" order="1" active="true" hiddenIfNotAvailable="false">
  <NestVersion>2018</NestVersion>
  <Uri>http://services.example.com:12345/BasisService</Uri>
  <UserName>myUserName</UserName>
  <Password>myPassword</Password>
</AddressProvider>
```

Beispiel-Konfiguration 2 (ausführlich):
```xml
<!-- Nest Address-Provider -->
<AddressProvider id="B16EC67C-444E-46DC-A659-93E95BB4EB4D" order="1" active="true" hiddenIfNotAvailable="false">
  <Title>NEST Kontaktperson</Title>
  <NestVersion>2018</NestVersion>
  <Uri>http://services.example.com:12345/BasisService</Uri>
  <UserName>myUserName</UserName>
  <Password>myPassword</Password>
  <Debug>false</Debug>
  <AlleAdressartenDefault>false</AlleAdressartenDefault>
  <DetailsColumnMapping>./ExtendentFields/Item[@Key='Dynamic.Adressart']</DetailsColumnMapping>
  <SearchParameters>
    <SearchParameter Name="Vorname" Label="Vorname" Type="String" Length="100" Sort="1" />
    <SearchParameter Name="Name" Label="Nachname" Type="String" Length="100" Sort="2" />
    <SearchParameter Name="Geburtsdatum" Label="Geburtstag" Type="Date" Length="100" Sort="3" />
    <SearchParameter Name="StrasseHaus" Label="Strasse/Haus" Type="String" Length="100" Sort="4" />
    <SearchParameter Name="PLZ" Label="PLZ/Ort" Type="String" Length="6" Sort="5" />
    <SearchParameter Name="Ortsname" Label="" Type="String" Length="100" Width="130" Sort="5" />
    <SearchParameter Name="ID_Subjekt" Label="Subjekt-ID" Type="Long" Length="100" Sort="6" />
    <SearchParameter Name="AlleAdressarten" Label="AlleAdressarten" Type="Boolean" Length="100" Sort="7" />
  </SearchParameters>
</AddressProvider>
```

Mit übersetzten Beschriftungen:
```xml
[...]
<Title>NEST Kontaktperson</Title>
[...]
<SearchParameters>
  <SearchParameter Name="Vorname" Label="{U[Recipients.NestAddressProvider.SearchParameterLabel.FirstName]}" Type="String" Length="100" Sort="1" />
  <SearchParameter Name="Name" Label="{U[Recipients.NestAddressProvider.SearchParameterLabel.LastName]}" Type="String" Length="100" Sort="2" />
  <SearchParameter Name="Geburtsdatum" Label="{U[Recipients.NestAddressProvider.SearchParameterLabel.Birthday]}" Type="Date" Length="100" Sort="3" />
  <SearchParameter Name="StrasseHaus" Label="{U[Recipients.NestAddressProvider.SearchParameterLabel.StreetHouse]}" Type="String" Length="100" Sort="4" />
  <SearchParameter Name="PLZ" Label="{U[Recipients.NestAddressProvider.SearchParameterLabel.ZipCodeCity]}" Type="String" Length="6" Sort="5" />
  <SearchParameter Name="Ortsname" Label="" Type="String" Length="100" Width="130" Sort="5" />
  <SearchParameter Name="ID_Subjekt" Label="{U[Recipients.NestAddressProvider.SearchParameterLabel.SubjectID]}" Type="Long" Length="100" Sort="6" />
  <SearchParameter Name="AlleAdressarten" Label="{U[Recipients.NestAddressProvider.SearchParameterLabel.AllAddressTypes]}" Type="Boolean" Length="100" Sort="7" />
</SearchParameters>
[...]
```

Einträge für den globalen Übersetzungsprovider:
```xml
  <group name="Recipients">
    [...]
    <data name="NestAddressProvider.Title">
      <value lcid="07">NEST Kontaktperson</value>
      <value lcid="09">NEST contact person</value>
      <value lcid="12">Personne de contact de NEST</value>
      <value lcid="16">Persona di contatto NEST</value>
    </data>
    <data name="NestAddressProvider.SearchParameterLabel.FirstName">
      <value lcid="07">Vorname</value>
      <value lcid="09">First name</value>
      <value lcid="12">Prénom</value>
      <value lcid="16">Nome</value>
    </data>
    <data name="NestAddressProvider.SearchParameterLabel.LastName">
      <value lcid="07">Nachname</value>
      <value lcid="09">Last name</value>
      <value lcid="12">Nom de famille</value>
      <value lcid="16">Cognome</value>
    </data>
    <data name="NestAddressProvider.SearchParameterLabel.StreetHouse">
      <value lcid="07">Strasse/Haus</value>
      <value lcid="09">Street/House</value>
      <value lcid="12">Rue/maison</value>
      <value lcid="16">strada / casa</value>
    </data>
    <data name="NestAddressProvider.SearchParameterLabel.ZipCodeCity">
      <value lcid="07">PLZ/Ort</value>
      <value lcid="09">Zip code/town</value>
      <value lcid="12">Zip/Ville</value>
      <value lcid="16">Zip / Città</value>
    </data>
    <data name="NestAddressProvider.SearchParameterLabel.Birthday">
      <value lcid="07">Geburtstag</value>
      <value lcid="09">Birthday</value>
      <value lcid="12">Date de naissance</value>
      <value lcid="16">Data di nascita</value>
    </data>
    <data name="NestAddressProvider.SearchParameterLabel.SubjectID">
      <value lcid="07">Subjekt-ID</value>
      <value lcid="09">Subject id</value>
      <value lcid="12">Id du sujet</value>
      <value lcid="16">Id dell'oggetto</value>
    </data>
    <data name="NestAddressProvider.SearchParameterLabel.AllAddressTypes">
      <value lcid="07">Alle Adressarten</value>
      <value lcid="09">All address types</value>
      <value lcid="12">Tous les types d'adresse</value>
      <value lcid="16">Tutti i tipi di indirizzo</value>
    </data>
  </group>
```


### Aufbau

* **Title** Titel des Adressproviders (wird so in Tab angezeigt). Default: «NEST Kontaktperson» (bei UI-Sprache Deutsch)
* **NestVersion** Version vom Nest-Service. `2018`, falls der Nest-Release 2018 (oder neuer) installiert ist.
* **Uri** Uri des Nest-Service-Endpunkts
* **UserName** Benutzername für Authentifizierung beim Nest-Service-Endpunkt
* **Password** Password für Authentifizierung beim Nest-Service-Endpunkt
* **Debug** `true` falls zusätzliche Informationen geloggt werden sollen (Request und Response)
* **AlleAdressartenDefault** `false`, falls «AlleAdressarten»-Suchparameter deaktiviert sein soll. Durch den SearchParameter «AlleAdressarten» (falls konfiguriert) kann der Benutzer diese Option für die aktuelle Suche ändern.
* **DetailsColumnMapping** bestimmt, welche Daten in der Details-Spalte angezeigt werden. Default: `./ExtendentFields/Item[@Key='Dynamic.Adressart']`
* **SearchParameters** Hier kann die Such-Maske konfiguriert werden (siehe Beispiel-Konfiguration). Wenn dieses Element nicht konfiguriert wird, wird eine Standard-Suchmaske angezeigt (verfügbar in DE, EN, FR, IT; CheckBox «AlleAdressarten» wird nicht angezeigt). Bei der Nest-Suche können folgende Parameter verwendet werden:
  * Vorname
  * Name
  * Geburtsdatum (Date)
  * StrasseHaus
  * PLZ
  * Ortsname
  * ID_Subjekt (Long)
  * AlleAdressarten (Boolean
