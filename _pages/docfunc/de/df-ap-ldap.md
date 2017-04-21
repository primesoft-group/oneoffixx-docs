---
layout: page
title: LDAPAddressProvider
permalink: "docfunc/de/df/ap/ldap"
language: de
---

Adressprovider für die Suche im lokalen Active Directory. Der LDAP besteht aus zwei Abragen. In der ersten Abfage wird das Adressbuch aufgebaut. Das Resultat aus dem Adressbuch (AddressBookId) wird (optional) im SearchFilter in der zweiten Abfrage angwendet .

```xml
<AddressProvider id="00BA9804-2430-4585-AE60-FCCA29909781" order="1" active="false" hiddenIfNotAvailable="true">
    <DisplayName>LDAP-Suche</DisplayName>
    <Icon></Icon>
    <LDAP>LDAP://SERVER/DC=domain,DC=ch</LDAP>
    <AuthenticationType>Secure</AuthenticationType>
    <LDAPUserName></LDAPUserName>
    <LDAPPassword></LDAPPassword>
    <ContactMapping>
        <ContactItemXPath>Contact</ContactItemXPath>
        <ContactElement id="ID">distinguishedName</ContactElement>
        <ContactElement id="Person_Title">title</ContactElement>
        <ContactElement id="Person_LastName">sn</ContactElement>
        <ContactElement id="Person_FirstName">givenname</ContactElement>
        <ContactElement id="Person_SecondName"></ContactElement>
        <ContactElement id="Person_NickName"></ContactElement>
        <ContactElement id="Person_BirthDate"></ContactElement>
        <ContactElement id="Person_Profession"></ContactElement>
                <ContactElement id="Person_CareOf"></ContactElement>
        <ContactElement id="Person_Position"></ContactElement>
        <ContactElement id="Person_Street"></ContactElement>
        <ContactElement id="Person_City"></ContactElement>
        <ContactElement id="Person_ZipCode"></ContactElement>
        <ContactElement id="Person_PostOfficeBox"></ContactElement>
                <ContactElement id="Person_PostOfficeBoxCityZipCode"></ContactElement>
        <ContactElement id="Person_PostOfficeBoxCity"></ContactElement>
        <ContactElement id="Person_CountryShortCode"></ContactElement>
        <ContactElement id="Person_Country"></ContactElement>
        <ContactElement id="Person_Phone"></ContactElement>
        <ContactElement id="Person_Email"></ContactElement>
        <ContactElement id="Person_Fax"></ContactElement>
        <ContactElement id="Person_Mobile"></ContactElement>
        <ContactElement id="Person_Homepage"></ContactElement>
        <ContactElement id="Person_Initials"></ContactElement>
        <ContactElement id="Company_Name">company</ContactElement>
        <ContactElement id="Company_Supplement"></ContactElement>
        <ContactElement id="Company_Department">department</ContactElement>
        <ContactElement id="Company_Street">streetaddress</ContactElement>
        <ContactElement id="Company_City">l</ContactElement>
        <ContactElement id="Company_ZipCode"></ContactElement>
        <ContactElement id="Company_PostOfficeBox"></ContactElement>
                <ContactElement id="Company_PostOfficeBoxCityZipCode"></ContactElement>
        <ContactElement id="Company_PostOfficeBoxCity"></ContactElement>
                <ContactElement id="Company_CareOf"></ContactElement>
        <ContactElement id="Company_CountryShortCode">c</ContactElement>
        <ContactElement id="Company_Country">co</ContactElement>
        <ContactElement id="Company_PhoneDirect">telephonenumber</ContactElement>
        <ContactElement id="Company_PhoneCentral"></ContactElement>
        <ContactElement id="Company_EmailDirect">mail</ContactElement>
        <ContactElement id="Company_EmailCentral"></ContactElement>
        <ContactElement id="Company_FaxDirect"></ContactElement>
        <ContactElement id="Company_FaxCentral"></ContactElement>
        <ContactElement id="Company_Mobile"></ContactElement>
        <ContactElement id="Company_Homepage">wwwhomepage</ContactElement>
        <ContactElement id="SalutationShort"></ContactElement>
        <ContactElement id="Salutation"></ContactElement>
        <ContactElement id="Greeting"></ContactElement>
        <ContactElement id="Language"></ContactElement>
        <ContactElement id="Provider_ID"></ContactElement>
        <ContactElement id="Provider_Name"></ContactElement>
        <ContactElement id="Provider_Updated"></ContactElement>
        <ContactElement id="Provider_Published">whencreated</ContactElement>
        <ContactElement id="Provider_AddressLabel"></ContactElement>
        <ContactElement id="Provider_URL"></ContactElement>
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
    <!-- Felder {0-n} entsprechen den Eingabefelder in der Suchmaske. Wird ein {} weggelassen, wird das entsprechende Feld in der Suchmaske deaktiviert -->
    <SearchFilter>(&amp;(objectClass=person)(memberOf={0})(|(!(company=*))(company={1}*))(|(!(givenName=*))(givenName={2}*))(|(!(sn=*))(sn={3}*))(|(!(streetAddress=*))(streetAddress={4}*))(|(!(postalCode=*))(postalCode={5}*))(|(!(l=*))(l={6}*))(|(!(userPrincipalName=*))(userPrincipalName={7}*)))</SearchFilter>
    <MaxResults>1000</MaxResults>
    <LoadParentData>false</LoadParentData>            
    <AddressBookFilter>(&amp;(objectClass=group)(member=*))</AddressBookFilter>
    <AddressBookId>distinguishedName</AddressBookId>
    <AddressBookDisplayName>cn</AddressBookDisplayName>
    <AddressBookAddGlobal>true</AddressBookAddGlobal>
    <AddressBookGlobalName>Alle</AddressBookGlobalName>
    <DefaultSelectedAddressBookName></DefaultSelectedAddressBookName>
    
</AddressProvider>
```

* __LDAP__ Connectionstring auf das LDAP Verzeichnis
* __AuthenticationType__ AuthType auf das LDAP (Standard Secure). 


Member name | Description 
---------|----------
Anonymous | No authentication is performed. 
 Delegation | Enables Active Directory Services Interface (ADSI) to delegate the user's security context, which is necessary for moving objects across domains. 
 Encryption | Attaches a cryptographic signature to the message that both identifies the sender and ensures that the message has not been modified in transit. 
FastBind | Specifies that ADSI will not attempt to query the Active Directory Domain Services objectClass property. Therefore, only the base interfaces that are supported by all ADSI objects will be exposed. Other interfaces that the object supports will not be available. A user can use this option to boost the performance in a series of object manipulations that involve only methods of the base interfaces. However, ADSI does not verify if any of the request objects actually exist on the server. For more information, see the topic "Fast Binding Option for Batch Write/Modify Operations" in the MSDN Library at http://msdn.microsoft.com/library. For more information about the objectClass property, see the "Object-Class" topic in the MSDN Library at http://msdn.microsoft.com/library. 
None | Equates to zero, which means to use basic authentication (simple bind) in the LDAP provider. 
ReadonlyServer | For a WinNT provider, ADSI tries to connect to a domain controller. For Active Directory Domain Services, this flag indicates that a writable server is not required for a serverless binding. 
Sealing | Encrypts data using Kerberos. The Secure flag must also be set to use sealing.
Secure | Requests secure authentication. When this flag is set, the WinNT provider uses NTLM to authenticate the client. Active Directory Domain Services uses Kerberos, and possibly NTLM, to authenticate the client. When the user name and password are a null reference (Nothing in Visual Basic), ADSI binds to the object using the security context of the calling thread, which is either the security context of the user account under which the application is running or of the client user account that the calling thread is impersonating. 
SecureSocketsLayer | Attaches a cryptographic signature to the message that both identifies the sender and ensures that the message has not been modified in transit. Active Directory Domain Services requires the Certificate Server be installed to support Secure Sockets Layer (SSL) encryption. 
ServerBind | If your ADsPath includes a server name, specify this flag when using the LDAP provider. Do not use this flag for paths that include a domain name or for serverless paths. Specifying a server name without also specifying this flag results in unnecessary network traffic. 
Signing | Verifies data integrity to ensure that the data received is the same as the data sent. The Secure flag must also be set to use signing. 


























