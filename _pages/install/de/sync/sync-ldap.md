---
layout: page
title: LdapSyncSource
permalink: "install/de/sync/sync-ldap"
language: de
---

## LdapSyncSource

Connects to the local AD. Be aware that the query might only return properties that are applied to this user. Use the "useValueIfEmpty"-rule to ensure that all values have a correct default or use "ignoreClaimIfEmpty" to omit empty claims.

Note: LdapPropertiesToLoad can be left blank if you want to see all available properties, but should be limited due to performance impacts.

```xml
<LdapSyncSource name="Custom LDAP" queryKey="OneOffixxIdentifier">
    <LdapServer>server</LdapServer>
    <LdapIsSsl>false</LdapIsSsl>
    <LdapOverwriteSslVerificationAndReturnTrue>false</LdapOverwriteSslVerificationAndReturnTrue>
    <LdapBaseDnPath>dnpath</LdapBaseDnPath>
    <LdapUser>username</LdapUser>
    <LdapPassword>password</LdapPassword>
    <LdapAuthType>Basic</LdapAuthType>
    <LdapFilter>filtervalue</LdapFilter>
    <LdapEncodingCodePage>65001</LdapEncodingCodePage>
    <LdapUseV3ProtocolVersion>false</LdapUseV3ProtocolVersion>
    <LdapPropertiesToLoad>cn,displayName,title,thumbnailPhoto</LdapPropertiesToLoad>
    <Claims>
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" property="cn" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/displayName" property="displayName" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/title" property="title" />
        <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/userImage" property="thumbnailPhoto" />
    </Claims>
</LdapSyncSource>
```

### Options ###

* **LdapServer** If nothing is set, the current Active Directory will be used. Default port: 389.
* **LdapIsSsl** Default: false, *optional*
* **LdapOverwriteSslVerificationAndReturnTrue** Default: false, *optional* 
* **LdapBaseDnPath** If nothing is set, the current Active Directory DN Path will be used.
* **LdapUser** Default: Current user, *optional*
* **LdapPassword** Default: Current user, *optional*
* **LdapAuthType** Default: 'Basic', *optional*
    * **Anonymous**: No authentication
    * **Basic**: Basic authentication
    * **Negotiate**: Microsoft Negotiate authentication
    * **Ntlm**: Windows NT Challenge/Response (NTLM) authentication
    * **Digest**:  Digest Access authentication
    * **Sicily**: Negotiation mechanism (Sicily) will be used to choose MSN, DPA or NTLM. This should be used for LDAPv2 servers only
    * **Dpa**: Distributed Password authentication
    * **Msn**: Microsoft Network Authentication Service
    * **External**: external method will be used to authenticate
    * **Kerberos**: Kerberos authentication
* **LdapFilter** If nothing is set and queryKey is OneOffixx, the objectSid-Filter will be used.
* **LdapEncodingCodePage** Default: '65001', *optional*, [possible values](https://msdn.microsoft.com/en-us/library/windows/desktop/dd317756(v=vs.85).aspx)
* **LdapUseV3ProtocolVersion** Default: false, *optional*
* **LdapPropertiesToLoad** Properties to load, comma separated