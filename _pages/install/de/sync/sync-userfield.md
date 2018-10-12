---
layout: page
title: UserFieldMappingSyncSource
permalink: "install/de/sync/sync-userfield"
language: de
---

## UserFieldMappingSyncSource

XSLT Tranformation for incomming fields. Output must be declared through claims (as usual).

```xml
<UserFieldMappingSyncSource name="Mapping">
    <FieldMapping>
        <MapFieldNames>*</MapFieldNames>
        <Element id="neuesFeld1" separator="#">postalcode</Element>
        <Element id="neuesFeld2" fCase="upper">mdbusedefaults</Element>
        <Element id="neuesFeld3" fCase="upper">l</Element>
    </FieldMapping>
    <Claims>
        <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/fieldmapping" property="neuesFeld1" />
    </Claims>
</UserFieldMappingSyncSource>
```