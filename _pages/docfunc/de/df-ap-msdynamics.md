---
layout: page
title: DynamicsNavisionAddressProvider
permalink: "docfunc/de/df/ap/msdynamics"
language: de
---

Adressprovider für Microsoft Dynamics oder Microsoft Navision. Der WebService muss jeweils auf Dynamics oder Navision eingerichtet werden.

```xml
<AddressProvider id="739DEC43-D4F0-47F6-ADDD-C6AC73A93B02" order="16" active="false">
  <Uri>http://{HOST:PORT}/PROD/OData</Uri>
  <CompanyName>***TEST COMPANY***</CompanyName>
  <UserName></UserName>
  <Password></Password>
  <Domain></Domain>
  <MaxResults>100</MaxResults>
  <SearchParameters>
    <SearchParameter Name="Name" Label="Name" Type="String">
      <Field Name="Name" />
      <Field Name="Name_2" />
    </SearchParameter>
    <SearchParameter Name="First_Name" Label="Vorname" Type="String" />
    <SearchParameter Name="Address" Label="Strasse" Type="String">
      <Field Name="Address" />
      <Field Name="Address_2" />
    </SearchParameter>
    <SearchParameter Name="Post_Code" Label="PLZ" Type="String" />
    <SearchParameter Name="City" Label="Ort" Type="String" />
    <SearchParameter Name="E-Mail" Label="E-Mail" Type="String" />
    <SearchParameter Name="Phone" Label="Telefon" Type="String">
      <Field Name="Phone_No" />
      <Field Name="Mobile_Phone_No" />
    </SearchParameter>
  </SearchParameters>
</AddressProvider>
```