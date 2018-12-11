---
layout: page
title: Address Service
permalink: "docfunc/de/df/ap/addressservice/"
language: de
---
**Hinweis** Ohne konfigurierten Security-Key funktioniert der Address-Service nicht.

Die neue Generation der OneOffixx-Addressprovider führt die Suche auf dem OneOffixx-Server aus und nicht mehr auf den Client. 

__Konfiguration:__

Alle neuen Addressprovider, werden in einem Provider umschlossen, welcher als Schnittstelle zwischen der neuen und alten Welt dient. Beispiel:

```xml
<AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
    <!-- Konfiguration des eigentlichen Providers -->
</AddressProvider>
```

__Parameter:__

* __id__ Guid, die den Wrapper identifiziert. Immer **E10A8313-A92D-4CB2-A12B-9AEB58F39207**
* __order__ Gibt die Sortierung mit anderen Addressprovidern im Empfängerdialog an
* __active__ Gibt an, ob der Addressprovider verfügbar ist.
* __ServiceUrl__ Die Url des Addressservices, auf welchem der Addressprovider läuft. Wird keine Url angegeben, muss der Addressprovider lokal verfügbar sein.
* __EnforceDiscovery__ Standardwert: False. Wenn auf True gesetzt, wird auch die Benutzeroberfläche für den Provider immer vom Server geladen. Wenn False, wird, falls der Provider lokal verfügbar ist, dieser für die Oberfläche gefragt und eine Abfrage an den Service gespart.

__Beispiel:__

```xml
<AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
    <AddressProvider id="62C19ADA-826B-4EBC-848D-B32E957D78C6" Title="myCSVFile.csv">
        <SearchParameters>
            <SearchParameter Name="firstName" Label="Vorname/Name" Type="String" Length="100" Sort="1" />
        </SearchParameters>
        <FilePath>myCSVFile.csv</FilePath>
        <Provider Name="CSV">

        </Provider>
        <Icon>

        </Icon>
        <Mapping>
            <!-- Mapping -->
        </Mapping>
    </AddressProvider>
</AddressProvider>
```


