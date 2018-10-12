---
layout: page
title: UserSync
permalink: "install/de/sync-overview/"
language: de
---

```xml
<?xml version="1.0" encoding="utf-8"?>
<UserSyncConfig batchSize="1" syncTimeoutInSeconds="" syncIntervalInSeconds="86400">

    <!-- List of various sync sources available, e.g. LdapSyncSource -->
    <LdapSyncSource name="OneOffixx AD" queryKey="OneOffixxIdentifier" isOptional="false">
        <QueryKeyRegex group="0" match="0">([a-z0-9])*</QueryKeyRegex>
        [...]

        <!-- Any sync source has claims -->
        <Claims>	
            <Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/uid" property="uid" />
            <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenName" property="givenName" />
            <Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sn" property="sn" /> 
        </Claims>

  </LdapSyncSource>
</UserSyncConfig>
```

## Attribute

* **batchSize** Wert zwischen 1 und 100, *default 10*
* **syncTimeoutInSeconds** Wert zwischen 10 und 3600, *default 60*
* **syncIntervalInSeconds** Wert grösser als 60, *default 86400 (= 1 day)*

## SyncSources

Zur Synchronisierung stehen aktuell folgende Adapter zur Verfügung:

* [LdapSyncSource]({{ site.baseurl }}/install/de/sync/sync-ldap) 
* [StaticSyncSource]({{ site.baseurl }}/install/de/sync/sync-static) 
* [UserFieldMappingSyncSource]({{ site.baseurl }}/install/de/sync/sync-userfield) 
* [MicrosoftGraphSyncSource]({{ site.baseurl }}/install/de/sync/sync-graph) 
* [HttpSyncSource]({{ site.baseurl }}/install/de/sync/sync-http)

Alle SyncSources haben folgende Attribute und Elemente gemeinsam:

* **name** 
* **queryKey** Feldname, der als Parameter für die Abfrage verwendet werden soll. Verfügbar sind:
    * OneOffixxIdentifier
    * User.SID
    * User.LoginName
    * User.Title
* **isOptional**
* **QueryKeyRegex** *(optional)* Falls nur ein Teil des Wertes des QueryKeys verwendet werden soll, kann dies hier spezifiziert werden.
* **Claims** siehe nächster Abschnitt

## Claims

```xml
<Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/uid" property="uid" />
```

* **type** Beschreibt den Claim-Pfad. Muss ein gültiges URI-Format aufweisen, muss aber nicht existieren - solange es nur in OneOffixx verwendet wird. Falls nicht, ist es vorteilhaft, sich an die [Claims von Microsoft](https://msdn.microsoft.com/en-us/library/microsoft.identitymodel.claims.claimtypes_members.aspx) zu halten.
* **property** Ist das Gegenstück zum Property, das in der SyncSource definiert wird. Muss jeweils identisch sein.

Claims unterstützen zudem Regex, sodass z.B. auf Teile von Werten zugegriffen werden kann.

```xml
<!-- Wert für Property 'uid' ist 'hans.gseh@oneoffixx.com' -->
<Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/uid" property="uid">
    <Regex match="0" group="2">([a-z\\.]*)@([a-z\\.]*)</Regex> <!-- Liefert 'oneoffixx.com' -->
</Claim>
```

* **match** Index des Matches, meistens 0
* **group** Index der Gruppe
    * **Achtung** Die Gruppenzahl kann um 1 erhöht sein, da in Gruppe 0 gegebenenfalls der Fullmatch liegen kann.
* ***Wert*** Gültiger Regex-Ausdruck
