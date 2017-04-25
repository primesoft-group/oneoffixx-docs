---
layout: page
title: LotusNotesAddressProvider
permalink: "docfunc/de/df/ap/lotusnotes"
language: de
---
Aus den Lotus Notes Datenbanken werden die Adressen via Ategra oder Magermann-Webservice als Adressprovider in OneOffixx zu Verfügung gestellt. Für jede Datenbank wird von Ategra ein Webservice eingerichtet auf welchen zugegriffen werden kann.

Es ist der Adressprovider in der globalen Konfiguration einzurichten, wobei die URL des Webservice bekannt sein muss und bei gewünschten speziellen Suchparametern diese konfiguriert werden können.

```xml
<AddressProvider id="6EA5E6E3-1329-4B02-8779-0952C1119A15" order="8" active="true" hiddenIfNotAvailable="true">
    <Uri>http://{host}/appl/KAI/KAI_DEV.nsf/KAIaddressProvider?OpenWebService</Uri>
    <Namespace>urn:oneoffixinterface.ategra.com</Namespace>
    <UserName>{username}</UserName>
    <Password>{password}</Password>
    <!--
    <WindowsUser>{WindowsServiceUser}</WindowsUser>
	-->
    <Title>KAI Adressen TEST</Title>
    <SearchParameters>
      <SearchParameter Name="companyName" Label="Firma" Type="String" />
      <SearchParameter Name="LastName" Label="Name" Type="String" />
      <SearchParameter Name="FirstName" Label="Vorname" Type="String" />
      <SearchParameter Name="Street" Label="Strasse" Type="String" />
      <SearchParameter Name="ZipCode" Label="PLZ" Type="String" />
      <SearchParameter Name="City" Label="Ort" Type="String" />
    </SearchParameters>
</AddressProvider>
```

Der Adressprovider unterstützt sowohl Windows Auth alsauch Basic Auth.