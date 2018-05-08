---
layout: page
title: Address Service
permalink: "install/de/addressservice/"
language: de
---
**Nicht vergessen** Ohne konfigurierten Security-Key funktioniert der Address-Service nicht.

Die neue Generation der OnOffixx-Addressprovider kann sowohl lokal als auch auf dem OneOffixx-Server ausgeführt werden. Normalfall ist dabei das Ausführen auf dem Server.

# Konfiguration

Alle neuen Addressprovider, werden in einem Provider umschlossen, welcher als Schnittstelle zwischen der neuen und alten Welt dient. Beispiel:

    <AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
        <!-- Konfiguration des eigentlichen Providers -->
    </AddressProvider>

### Parameter

* __id__ Guid, die den Wrapper identifiziert. Immer **E10A8313-A92D-4CB2-A12B-9AEB58F39207**
* __order__ Gibt die Sortierung mit anderen Addressprovidern im Empfängerdialog an
* __active__ Gibt an, ob der Addressprovider verfügbar ist.
* __ServiceUrl__ Die Url des Addressservices, auf welchem der Addressprovider läuft. Wird keine Url angegeben, muss der Addressprovider lokal verfügbar sein.
* __EnforceDiscovery__ Standardwert: False. Wenn auf True gesetzt, wird auch die Benutzeroberfläche für den Provider immer vom Server geladen. Wenn False, wird, falls der Provider lokal verfügbar ist, dieser für die Oberfläche gefragt und eine Abfrage an den Service gespart.

# Verfügbare neue AddressProvider

## File - Excel und CSV Dateien

# Konfiguration

     <AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
        <AddressProvider id="62C19ADA-826B-4EBC-848D-B32E957D78C6" Title="myCSVFile.csv">
            <SearchParameters>
                <SearchParameter Name="firstName" Label="Vorname/Name" Type="String" Length="100" Sort="1" />
            <SearchParameters>
            <FilePath>myCSVFile.csv</FilePath>
            <Provider Name="CSV">

            </Provider>
            <Icon>

            </Icon>
            <Mapping>
             <!-- -->
            </Mapping>
        </AddressProvider
    </AddressProvider>

### Parameter

* __id__ 62C19ADA-826B-4EBC-848D-B32E957D78C6
* __SearchParameter__ Liste mit allen Eingabemöglichkeiten.
    * *Name* Eindeutige Id für den Parameter. Entspricht den **Spaltenüberschriften** für CSV oder für Excel Dateien in welchen gesucht werden soll
    * *Label* Angezeigter Text vor dem Eingabefeld
    * *Typ* Eingabetyp: String(Text), Long(Zahl), Boolean (Ja/Nein) oder Date (Datum)
    * *Length* Maximale Länge für Strings
    * *Sort* Sortierungswert gegenüber den anderen Parametern
* __Mapping__ Mapping auf OneOffixx Kontaktfelder. Siehe Mapping.
* __Provider__ Provider, entweder CSV oder EXCEL. Angegeben im Attribut *Name*.
* __Title__ Der Titel, welcher dem Benutzer angezeigt wird.
* __Icon__ Base64 Icon, welches dem Benutzer im Empfängeridalog angezeigt wird.

### CSV Provider

Beispielskonfiguration:

    <Provider Name="CSV">
        <HasHeaders>True<HasHeaders>
        <Delimeter>,</Delimeter>
    </Provider>

* __HasHeaders__ Standardwert: True, falls die CSV-Datei überschriften besitzt. Anderseits False. Wenn keine Header vorhanden sind, werden die Spalten nummeriert. (SearchParameter und Mapping entsprechend anpassen)
* __Delimeter__ Trennzeichen. Standardwert: `";"` 

### Excel Provider

Beispielskonfiguration:

    <Provider Name="EXCEL">
        <HasHeaders>True<HasHeaders>
        <Sheet>Blatt 2</Sheet>
    </Provider>

* __HasHeaders__ Standardwert: True, falls die Excel-Datei überschriften besitzt. Anderseits False. Wenn keine Header vorhanden sind, werden die Spalten wie im Excel nummeriert (A, B...). (SearchParameter und Mapping entsprechend anpassen)
* __Sheet__ Das zu verwendende Excel-Blatt. Wird kein Wert angegeben, wird das erste Blatt verwendet.

## GenericSqlProvider

Beispielskonfiguration:

    <AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
        <AddressProvider id="7E50AA46-A035-4F11-B44F-BBCBAB4780B7" Title="My DB Soure">
            <SearchParameters>
                <SearchParameter Name="firstName" Label="Vorname/Name" Type="String" Length="100" Sort="1" />
            <SearchParameters>
            <ConnectionString>{ConnectionString}</ConnectionString>
            <ConnectionProvider>System.Data.SqlClient</ConnectionProvider>

            <Query>
                SELECT * FROM Table WHERE UCase(Vorname) Like @firstName
            </Query>

            <Mapping>
             <!-- -->
            </Mapping>
        </AddressProvider
    </AddressProvider>

### Parameter

* __id__ 7E50AA46-A035-4F11-B44F-BBCBAB4780B7
* __SearchParameter__ Liste mit allen Eingabemöglichkeiten.
    * *Name* Eindeutige Id für den Parameter. Entspricht den Named Parameter für den Sql Query
    * *Label* Angezeigter Text vor dem Eingabefeld
    * *Typ* Eingabetyp: String(Text), Long(Zahl), Boolean (Ja/Nein) oder Date (Datum)
    * *Length* Maximale Länge für Strings
    * *Sort* Sortierungswert gegenüber den anderen Parametern
* __Mapping__ Mapping auf OneOffixx KKontaktfelder. Siehe Mapping.
* __ConnectionString__ [ConnectionString](https://www.connectionstrings.com/). Kann verschlüsselt sein.
* __ConnectionProvider__ System.Data.Odbc, System.Data.OleDb, System.Data.OracleClient, System.Data.SqlClient
* __Title__ Der Titel, welcher dem Benutzer angezeigt wird.
* __Icon__ Base64 Icon, welches dem Benutzer im Empfängeridalog angezeigt wird.

## Zefix Address Provider

Beispielskonfiguration:

    <AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
        <AddressProvider id="F6CA6CC9-B201-4556-886E-C6AF5F9460E4" >
            <!-- User/password for Zefix web service-->
            <ServiceUser>info@oneoffixx.com</ServiceUser>
            <ServicePassword>{password}</ServicePassword>
            <EnableProxyCredentials>true</EnableProxyCredentials>
        </AddressProvider
    </AddressProvider>

### Parameter

* __id__ F6CA6CC9-B201-4556-886E-C6AF5F9460E4
* __ServiceUser__ Der User, mit welchem sich der Provider beim Zefix-Dienst anmeldet
* __ServicePassword__ Das Passwort, mit welchem sich der Provider beim Zefix-Dienst anmeldet. Kann verschlüsselt sein.
* __Uri__ Optionale Service Url. Default: http://www.e-service.admin.ch/ws-zefix-1.6/ZefixService?wsdl


    