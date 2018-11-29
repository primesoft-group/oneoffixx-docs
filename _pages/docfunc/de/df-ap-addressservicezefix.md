---
layout: page
title: Zefix Address Provider (ADS)
permalink: "docfunc/de/df/ap/addressservicezefix/"
language: de
---

__Konfiguration:__

```xml
    <AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
        <AddressProvider id="F6CA6CC9-B201-4556-886E-C6AF5F9460E4" >
            <!-- User/password for Zefix web service-->
            <ServiceUser>info@oneoffixx.com</ServiceUser>
            <ServicePassword>{password}</ServicePassword>
            <EnableProxyCredentials>true</EnableProxyCredentials>
        </AddressProvider>
    </AddressProvider>
```

__Parameter:__

* __id__ F6CA6CC9-B201-4556-886E-C6AF5F9460E4
* __ServiceUser__ Der User, mit welchem sich der Provider beim Zefix-Dienst anmeldet
* __ServicePassword__ Das Passwort, mit welchem sich der Provider beim Zefix-Dienst anmeldet. Kann verschlüsselt sein.
* __Uri__ Optionale Service Url. Default: http://www.e-service.admin.ch/ws-zefix-1.6/ZefixService?wsdl