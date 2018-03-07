---
layout: page
title: LdapSyncSource
permalink: "install/de/sync/sync-ldap"
language: de
---

## LdapSyncSource

Connect to the local AD - smallest config possible with all default claims from OneOffixx (incl. user image from AD's thumbnailPhoto-attribute): Be aware, that the query might only return properties that are applied to this user. Use the "useValueIfEmpty"-rule to ensure that all values have a correct default or use "ignoreClaimIfEmpty" to omit empty claims.

Note: LdapPropertiesToLoad can be leave blank if you want to see all available properties, but should be limited because of performance reasons.

```xml
<LdapSyncSource name="Custom LDAP" queryKey="OneOffixxIdentifier">
    <LdapPropertiesToLoad>
        cn,displayName,givenName,initials,sn,mail,wWWHomePage,telephoneNumber,otherTelephoneNumber,description,physicalDeliveryOfficeName,streetAddress,postalCode,co,l,st,postOfficeBox,homePhone,otherHomePhone,mobile,facsimileTelephoneNumber,otherFacsimileTelephoneNumber,organization,department,company,manager,userPrincipalName,title,thumbnailPhoto,userAccountControl
    </LdapPropertiesToLoad>
    <Claims>
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" property="cn" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/displayName" property="displayName" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/title" property="title" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/userImage" property="thumbnailPhoto" />
    </Claims>
</LdapSyncSource>
```