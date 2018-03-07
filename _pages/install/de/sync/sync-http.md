---
layout: page
title: HttpSyncSource
permalink: "install/de/sync/sync-http"
language: de
---

## HttpSyncSource

```xml
<HttpSyncSource name="Custom HTTP" queryKey="OneOffixxIdentifier">
	<Endpoint method="GET" url="http://127.0.0.1:8080/test/{queryKey}" />
	<Authentication type="Basic">
		<Username>Username</Username>
		<Password>Password</Password>
		<Domain>Domain</Domain>
	 </Authentication>   
	<ResultMapping>
		<Mapping Type="xml">
			<Map Source="//Identifikation[@Name='ID']" Target="PropertyX" />
			<If Condition="'1'=='1'">
				<Map SourceValue="Hans" Target="PropertyY" />
			</If>
			<Map Source="//Email" Target="PropertyZ" />
		</Mapping>
	</ResultMapping>
	<Claims>
		<Claim type="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" property="PropertyX" />
		<Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/displayName" property="PropertyY" />
		<Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/title" property="PropertyZ">
			<Regex match="0" group="0">(?:[\.a-z]+)</Regex>
		</Claim>
		<Claim type="http://schema.oneoffixx.com/ws/2011/01/identity/claims/domain" property="PropertyZ">
			<Regex match="1" group="0">(?:[\.a-z]+)</Regex>
		</Claim>
	</Claims>
</HttpSyncSource>
```

### Endpoint

Der Endpunkt muss eine gültige Uri sein, kann aber den Platzhalter {queryKey} enthalten. Dieser wird vor dem Aufruf durch den Wert des Parameters "queryKey" aus der SyncSource ersetzt.

### Authentication

* **Type** Authentifizierungsart. Möglich sind
	* **Basic** Basic authentication
	* **Windows** Windows authentication
* **Username** Benutzername, immer ohne Domain
* **Password** Passwort, kann in verschlüsselter Form oder Klartext sein
* **Domain** Domain des Benutzers, optional *(nur möglich für Type **Windows**)*


### ResultMapping

Das neue UOMF (Unified Object Mapping Format) von OneOffixx. Als Type werden aktuell sowohl XML als auch JSON unterstützt. Als Target wird ein Wert angegeben, der mit dem Property-Parameter eines Claims korrelieren muss.