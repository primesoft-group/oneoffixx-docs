---
layout: page
title: MicrosoftGraphSyncSource
permalink: "install/de/sync/sync-graph"
language: de
---

## MicrosoftGraphSyncSource

MicrosoftGraph / Office365 Connector - can only be used in combination with our IdS & the Microsoft Graph IdentityProvider

Available properties are based on the Graph API User-Object.

```xml
<MicrosoftGraphSyncSource name="AzureAD" queryKey="OneOffixxIdentifier">
    <Claims>
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" property="preferredName" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/displayName" property="displayName" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname" property="givenName" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname" property="surname" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress" property="mail" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/webpage" property="mySite" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/phone" property="mobilePhone" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/streetaddress" property="streetAddress" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/postalcode" property="postalCode" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country" property="country" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/locality" property="city" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/mobilephone" property="mobilePhone" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/department" property="department" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/company" property="companyName" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" property="userPrincipalName" />
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/stateorprovince" property="state" />
    </Claims>
</MicrosoftGraphSyncSource>
```