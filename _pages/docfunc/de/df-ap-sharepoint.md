---
layout: page
title: SharepointAddressProvider
permalink: "docfunc/de/df/ap/sharepoint"
language: de
---

Direkte Abfrage aus Sharepoint Listen. Die Berechtigung wird in SharePoint gesteuert.

``` xml
<AddressProvider id="96078EBE-4A8F-4D53-883E-9E9D0F07BC2A" order="17" active="true" hiddenIfNotAvailable="true">
  <ListTitle>Kontakte</ListTitle>
  <Uri>https://{host}/websites/{site}/_api/lists</Uri>
  <ContactMapping>
    <ContactItemXPath>//entry</ContactItemXPath>
    <ContactElement id="ID">content/m:properties/d:GUID</ContactElement>
    <ContactElement id="Company_Name">content/m:properties/d:Company</ContactElement>
    <ContactElement id="Company_Street">content/m:properties/d:WorkAddress</ContactElement>
    <ContactElement id="Company_ZipCode">content/m:properties/d:WorkZip</ContactElement>
    <ContactElement id="Company_City">content/m:properties/d:WorkCity</ContactElement>
    <ContactElement id="Company_Country">content/m:properties/d:WorkCountry</ContactElement>
    <ContactElement id="Company_CountryShortCode">"CH"</ContactElement>
    <ContactElement id="Company_EmailDirect">content/m:properties/d:Email</ContactElement>
    <ContactElement id="Company_FaxCentral">content/m:properties/d:WorkFax</ContactElement>
    <ContactElement id="Company_Homepage">content/m:properties/d:WebPage</ContactElement>
    <ContactElement id="Company_Mobile">content/m:properties/d:CellPhone</ContactElement>
    <ContactElement id="Company_PhoneDirect">content/m:properties/d:WorkPhone</ContactElement>
    <ContactElement id="Person_FirstName">content/m:properties/d:FirstName</ContactElement>
    <ContactElement id="Person_LastName">content/m:properties/d:Title</ContactElement>
    <ContactElement id="Person_Phone">content/m:properties/d:HomePhone</ContactElement>
    <ContactElement id="Person_Profession">content/m:properties/d:JobTitle</ContactElement>
  </ContactMapping>
  <SearchParameters>
    <SearchParameter Name="Title" Label="Titel" Type="String" />
    <SearchParameter Name="Company" Label="Firma" Type="String" />
    <!-- also supported: Binding to multiple fields, otherwise Name will be used
                  <SearchParameter Name="Title" Label="Titel" Type="String" />
                    <Field Name="Name"/>
                    <Field Name="Name_2"/>
                  </SearchParameter>
                  -->
  </SearchParameters>
</AddressProvider>
```