---
layout: page
title: DynamicsCRMAddressProvider
permalink: "docfunc/de/df/ap/msdynamicscrm"
language: de
---

 <span class="label label-info">NEU ab 3.2.1</span>

Adressprovider für Microsoft Dynamics CRM 365.

Nutzt die [Microsoft Dynamics 365 Web API](https://msdn.microsoft.com/en-us/library/mt593051.aspx).

Siehe Beispiel-Konfiguration:

```xml
<!-- Dynamics CRM Adressprovider -->
<AddressProvider id="121CE113-143E-4125-980A-20B6341F9FC9" order="1" active="true">
  
  <!-- Debug (default: false)
       When Debug is set to 'true', log contains the requests, responses and transformed responses -->
  <Debug>false</Debug>
  <!-- Title for the Address Provider -->
  <Title>Dynamics CRM</Title>
  <!-- URI of the web service -->
  <Uri>https://my-subdomain.crm[n].dynamics.com/api/data/v8.2/contacts</Uri>
  <!-- Timeout in milliseconds (default: 3000) -->
  <Timeout>3000</Timeout>
  <!-- Icon -->
  <Icon>iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAMAUExURQAgUAEhUQMiUgYkVAcmVQgnVg4sWRAtWhs3Yh46ZB86ZShCay1Gbi1HbzBIcDpQdjtTeEZcgElegU5jhU9khlltjFtvjmBzkWN1k2Z4lX2MpX6NpoKRqY+csZunuq21xa+2x664x7G4yLe+zbi+zLzC0L7F0sXK1sbL18bM18zS3M/U3dDU3tPX4NbZ4tnd5d/i6OTn7OXo7fP09/v7/Pz8/f7+/v///wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAIpbQccAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAAZdEVYdFNvZnR3YXJlAHBhaW50Lm5ldCA0LjAuMTczbp9jAAAAeklEQVQoU42K1w6CUBAFj2Lv3Yu9AaLYWOD8/5+ZG1YSX4zzcnYmi78Z6xZsdD9UX0B9pGKZCbA0KpaLoCkG0576hFL2aeZpP/fKg7Imtxk1rEi5kSE1DJLv0Ij5jMK4CLXr/RQcdwcvOuehvRi2SvbT6br7jj1+ArwBtM4N4Dj6Dh8AAAAASUVORK5CYII=</Icon>
  
  <!-- Connection settings -->
  <AuthorityUri>https://login.windows.net/common</AuthorityUri>
  <Resource>https://my-subdomain.crm[n].dynamics.com/</Resource>
  <ClientId>11111111-1111-1111-1111-111111111111</ClientId>
  <!-- Username and Password are only required when ManualLogin is set to 'false' -->
  <Username>username@my-domain.ch</Username>
  <Password>PASSWORD</Password>
  <!-- ManualLogin (default: false)
       When set to 'true', a login window appears.
       A login via this window is required if the user has never been logged in manually with the defined client ID before. -->
  <ManualLogin>false</ManualLogin>
  <!-- Redirect URI is only required when ManualLogin is set to 'true' -->
  <RedirecUri>https://any-subdomain.my-domain.ch</RedirecUri>
  
  <!-- Search paremeters -->
  <SearchParameters>
    <SearchParameter Name="company" Label="Firma" Type="String" Length="100" Sort="1" />
    <SearchParameter Name="firstname" Label="Vorname/Name" Type="String" Length="100" Sort="2" />
    <SearchParameter Name="lastname" Label="" Type="String" Length="100" Sort="2" Width="90" />
    <SearchParameter Name="address1_line1" Label="Strasse" Type="String" Length="100" Sort="3" />
    <SearchParameter Name="address1_postalcode" Label="PLZ/Ort" Type="String" Length="6" Sort="4" />
    <SearchParameter Name="address1_city" Label="" Type="String" Length="100" Width="130" Sort="4" />
    <SearchParameter Name="address1_country" Label="Land" Type="String" Length="100" Sort="5" />
  </SearchParameters>
  
  <!-- Contact mapping -->
  <ContactMapping>
    <ContactItemXPath>Contact</ContactItemXPath>
    <ContactElement id="Person_Title"></ContactElement>
    <ContactElement id="Person_LastName">lastname</ContactElement>
    <ContactElement id="Person_FirstName">firstname</ContactElement>
    <ContactElement id="Person_SecondName"></ContactElement>
    <ContactElement id="Person_NickName">nickname</ContactElement>
    <ContactElement id="Person_BirthDate">birthdate</ContactElement>
    <ContactElement id="Person_Profession">jobtitle</ContactElement>
    <ContactElement id="Person_CareOf"></ContactElement>
    <ContactElement id="Person_Position"></ContactElement>
    <ContactElement id="Person_Street">address1_line1</ContactElement>
    <ContactElement id="Person_Apartment">address1_line2</ContactElement>
    <ContactElement id="Person_Floor">address1_line3</ContactElement>
    <ContactElement id="Person_City">address1_city</ContactElement>
    <ContactElement id="Person_ZipCode">address1_postalcode</ContactElement>
    <ContactElement id="Person_PostOfficeBox">address1_postofficebox</ContactElement>
    <ContactElement id="Person_PostOfficeBoxCityZipCode"></ContactElement>
    <ContactElement id="Person_PostOfficeBoxCity"></ContactElement>
    <ContactElement id="Person_CountryShortCode">address1_country</ContactElement>
    <ContactElement id="Person_Country"></ContactElement>
    <ContactElement id="Person_Phone">telephone1</ContactElement>
    <ContactElement id="Person_Email">emailaddress1</ContactElement>
    <ContactElement id="Person_Fax">fax</ContactElement>
    <ContactElement id="Person_Mobile">mobilephone</ContactElement>
    <ContactElement id="Person_Homepage">websiteurl</ContactElement>
    <ContactElement id="Person_Initials"></ContactElement>
    <ContactElement id="Company_Name">company</ContactElement>
    <ContactElement id="Company_Supplement"></ContactElement>
    <ContactElement id="Company_Department">department</ContactElement>
    <ContactElement id="Company_Street"></ContactElement>
    <ContactElement id="Company_Apartment"></ContactElement>
    <ContactElement id="Company_Floor"></ContactElement>
    <ContactElement id="Company_City"></ContactElement>
    <ContactElement id="Company_ZipCode"></ContactElement>
    <ContactElement id="Company_PostOfficeBox"></ContactElement>
    <ContactElement id="Company_PostOfficeBoxCityZipCode"></ContactElement>
    <ContactElement id="Company_PostOfficeBoxCity"></ContactElement>
    <ContactElement id="Company_CareOf"></ContactElement>
    <ContactElement id="Company_CountryShortCode"></ContactElement>
    <ContactElement id="Company_Country"></ContactElement>
    <ContactElement id="Company_PhoneDirect"></ContactElement>
    <ContactElement id="Company_PhoneCentral"></ContactElement>
    <ContactElement id="Company_EmailDirect"></ContactElement>
    <ContactElement id="Company_EmailCentral"></ContactElement>
    <ContactElement id="Company_FaxDirect"></ContactElement>
    <ContactElement id="Company_FaxCentral"></ContactElement>
    <ContactElement id="Company_Mobile"></ContactElement>
    <ContactElement id="Company_Homepage"></ContactElement>
    <ContactElement id="Options_AddressingType"></ContactElement>
    <ContactElement id="Options_ShowProviderLayout"></ContactElement>
    <ContactElement id="Options_PersonOverFirm"></ContactElement>
    <ContactElement id="Options_CountryView"></ContactElement>
    <ContactElement id="Options_CountryCodeView"></ContactElement>
    <ContactElement id="Options_SalutationView"></ContactElement>
    <ContactElement id="Options_SalutationSeparatetLine"></ContactElement>
    <ContactElement id="Options_SecondNameView"></ContactElement>
    <ContactElement id="Options_PositionView"></ContactElement>
  </ContactMapping>
  
</AddressProvider>
```