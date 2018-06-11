---
layout: page
title: Address Service
permalink: "docfunc/de/df/ap/addressservice/"
language: de
---
**Hinweis** Ohne konfigurierten Security-Key funktioniert der Address-Service nicht.

Die neue Generation der OnOffixx-Addressprovider führt die Suche auf dem OneOffixx-Server aus und nicht mehr auf den Client. 

__Konfiguration:__

Alle neuen Addressprovider, werden in einem Provider umschlossen, welcher als Schnittstelle zwischen der neuen und alten Welt dient. Beispiel:

    <AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
        <!-- Konfiguration des eigentlichen Providers -->
    </AddressProvider>

__Parameter:__

* __id__ Guid, die den Wrapper identifiziert. Immer **E10A8313-A92D-4CB2-A12B-9AEB58F39207**
* __order__ Gibt die Sortierung mit anderen Addressprovidern im Empfängerdialog an
* __active__ Gibt an, ob der Addressprovider verfügbar ist.
* __ServiceUrl__ Die Url des Addressservices, auf welchem der Addressprovider läuft. Wird keine Url angegeben, muss der Addressprovider lokal verfügbar sein.
* __EnforceDiscovery__ Standardwert: False. Wenn auf True gesetzt, wird auch die Benutzeroberfläche für den Provider immer vom Server geladen. Wenn False, wird, falls der Provider lokal verfügbar ist, dieser für die Oberfläche gefragt und eine Abfrage an den Service gespart.

# Verfügbare neue AddressProvider

## File - Excel und CSV Dateien  {% include anchor.html name="providers-file" %}

__Konfiguration:__

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

__Parameter:__

* __id__ 62C19ADA-826B-4EBC-848D-B32E957D78C6
* __SearchParameter__ Liste mit allen Eingabemöglichkeiten.
    * *Name* Eindeutige Id für den Parameter. Entspricht den **Spaltenüberschriften** für CSV oder für Excel Dateien in welchen gesucht werden soll
    * *Label* Angezeigter Text vor dem Eingabefeld
    * *Typ* Eingabetyp: String(Text), Long(Zahl), Boolean (Ja/Nein) oder Date (Datum)
    * *Length* Maximale Länge für Strings
    * *Sort* Sortierungswert gegenüber den anderen Parametern
* __Mapping__ Mapping auf OneOffixx Kontaktfelder. Siehe [Mapping]({{ site.baseurl }}/concepts/de/uomf).
* __Provider__ Provider, entweder CSV oder EXCEL. Angegeben im Attribut *Name*.
* __Title__ Der Titel, welcher dem Benutzer angezeigt wird.
* __Icon__ Base64 Icon, welches dem Benutzer im Empfängeridalog angezeigt wird.

### File: CSV Provider

__Konfiguration:__

    <Provider Name="CSV">
        <HasHeaders>True<HasHeaders>
        <Delimeter>,</Delimeter>
    </Provider>

* __HasHeaders__ Standardwert: True, falls die CSV-Datei überschriften besitzt. Anderseits False. Wenn keine Header vorhanden sind, werden die Spalten nummeriert. (SearchParameter und Mapping entsprechend anpassen)
* __Delimeter__ Trennzeichen. Standardwert: `";"` 

### File: Excel Provider

__Konfiguration:__

    <Provider Name="EXCEL">
        <HasHeaders>True<HasHeaders>
        <Sheet>Blatt 2</Sheet>
    </Provider>

* __HasHeaders__ Standardwert: True, falls die Excel-Datei überschriften besitzt. Anderseits False. Wenn keine Header vorhanden sind, werden die Spalten wie im Excel nummeriert (A, B...). (SearchParameter und Mapping entsprechend anpassen)
* __Sheet__ Das zu verwendende Excel-Blatt. Wird kein Wert angegeben, wird das erste Blatt verwendet.

## GenericSqlProvider {% include anchor.html name="providers-sql" %}

__Konfiguration:__

    <AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
        <AddressProvider id="7E50AA46-A035-4F11-B44F-BBCBAB4780B7" Title="My DB Soure">
            <SearchParameters>
                <SearchParameter Name="firstName" Label="Vorname/Name" Type="String" Length="100" Sort="1" />
            </SearchParameters>
            <ConnectionString>{ConnectionString}</ConnectionString>
            <ConnectionProvider>System.Data.SqlClient</ConnectionProvider>

            <Query>
                SELECT * FROM Users WHERE FirstName Like '%' + @firstName + '%'
            </Query>

            <Mapping>
                  <Map Source="CompanyName" Target="Company_Name" />
                  <Map Source="Title" Target="Person_Title" />
                  <Map Source="FirstName" Target="Person_FirstName" />
                  <Map Source="LastName" Target="Person_LastName" />
                  <Map Source="Birthday" Target="Person_BirthDate" />
                  <Map Source="Street" Target="Company_Street" />          
                  <Map Source="Zip" Target="Company_ZipCode" />
                  <Map Source="City" Target="Company_City" />
                  <Map Source="FaxBusinessDirect" Target="FaxDirect" />
                  <Map Source="EmailBusinessDirect" Target="EmailDirect" />
                  <Map Target="Company_CountryShortCode">
                    <Map.SourceExpression>
                        function main()
                        {
						switch(source('Country')) {
							case 'Albanien': return 'AL';
							case 'Andorra': return 'AD';
							case 'Aserbaidschan': return 'AZ';
							case 'Belgien': return 'BE';
							case 'Bosnien und Herzegowina': return 'BA';
							case 'Bulgarien': return 'BG';
							case 'Dänemark': return 'DK';
							case 'Deutschland': return 'DE';
							case 'Estland': return 'EE';
							case 'Finnland': return 'FI';
							case 'Frankreich': return 'FR';
							case 'Georgien': return 'GE';
							case 'Griechenland': return 'GR';
							case 'Irland': return 'IE';
							case 'Island': return 'IS';
							case 'Italien': return 'IT';
							case 'Kasachstan': return 'KZ';
							case 'Kosovo': return 'XK';
							case 'Kroatien': return 'HR';
							case 'Lettland': return 'LV';
							case 'Liechtenstein': return 'LI';
							case 'Litauen': return 'LT';
							case 'Luxemburg': return 'LU';
							case 'Malta': return 'MT';
							case 'Mazedonien': return 'MK';
							case 'Republik Moldau': return 'MD';
							case 'Monaco': return 'MC';
							case 'Montenegro': return 'ME';
							case 'Niederlande': return 'NL';
							case 'Norwegen': return 'NO';
							case 'Österreich': return 'AT';
							case 'Polen': return 'PL';
							case 'Portugal': return 'PT';
							case 'Rumänien': return 'RO';
							case 'Russland': return 'RU';
							case 'San Marino': return 'SM';
							case 'Schweden': return 'SE';
							case 'Schweiz': return 'CH';
							case 'Serbien': return 'RS';
							case 'Slowakei': return 'SK';
							case 'Slowenien': return 'SV';
							case 'Spanien': return 'ES';
							case 'Tschechien': return 'CZ';
							case 'Türkei': return 'TR';
							case 'Ukraine': return 'UA';
							case 'Ungarn': return 'HU';
							case 'Vatikanstadt': return 'VA';
							case 'Vereinigtes Königreich': return 'GB';
							case 'Weißrussland': return 'BY';
							
							default: return 'CH';
							}
							
							return '';
						}  
				    </Map.SourceExpression>
				 </Map>
            </Mapping>
        </AddressProvider>
    </AddressProvider>

__Parameter:__

* __id__ 7E50AA46-A035-4F11-B44F-BBCBAB4780B7
* __SearchParameter__ Liste mit allen Eingabemöglichkeiten.
    * *Name* Eindeutige Id für den Parameter. Entspricht den Named Parameter für den Sql Query
    * *Label* Angezeigter Text vor dem Eingabefeld
    * *Type* Eingabetyp: String(Text), Long(Zahl), Boolean (Ja/Nein) oder Date (Datum)
    * *Length* Maximale Länge für Strings
    * *Sort* Sortierungswert gegenüber den anderen Parametern
* __Mapping__ Mapping auf OneOffixx Kontaktfelder. Siehe [Mapping]({{ site.baseurl }}/concepts/de/uomf).
* __ConnectionString__ [ConnectionString](https://www.connectionstrings.com/). Kann verschlüsselt sein.
* __ConnectionProvider__ System.Data.Odbc, System.Data.OleDb, System.Data.OracleClient, System.Data.SqlClient, MySql.Data.MySqlClient, Oracle.ManagedDataAccess.Client 
* __Title__ Der Titel, welcher dem Benutzer angezeigt wird.
* __Icon__ Base64 Icon, welches dem Benutzer im Empfängeridalog angezeigt wird.

__Query:__

Der SQL Query muss in dem Format für die jeweilige Zieldatenbank sein. Da alle Suchparameter als SQL Parameter behandelt werden, muss der jeweilige SQL Parameter Syntax des Zielsystems eingehalten werden.

_Beispiel: MS SQL_

    Select FirstName, LastName FROM Users 
    WHERE FirstName LIKE '%' + @firstName + '%' AND LastName LIKE '%' + @lastName + '%'

_Beispiel: MySQL_

    Select FirstName, LastName FROM Users 
    WHERE FirstName LIKE Concat('%', @firstName, '%') AND LastName LIKE Concat('%', @lastName, '%')

_Beispiel: Oracle_

    Select FirstName, LastName from Users 
    WHERE UPPER(FirstName) Like UPPER('%' || :firstName || '%') AND UPPER(LastName) Like UPPER('%' || :lastName || '%')


## Zefix Address Provider {% include anchor.html name="providers-zefix" %}

__Konfiguration:__

    <AddressProvider id="E10A8313-A92D-4CB2-A12B-9AEB58F39207" order="1" active="true" ServiceUrl="http://localhost:41380/api/v1/Address" EnforceDiscovery="true">
        <AddressProvider id="F6CA6CC9-B201-4556-886E-C6AF5F9460E4" >
            <!-- User/password for Zefix web service-->
            <ServiceUser>info@oneoffixx.com</ServiceUser>
            <ServicePassword>{password}</ServicePassword>
            <EnableProxyCredentials>true</EnableProxyCredentials>
        </AddressProvider
    </AddressProvider>

__Parameter:__

* __id__ F6CA6CC9-B201-4556-886E-C6AF5F9460E4
* __ServiceUser__ Der User, mit welchem sich der Provider beim Zefix-Dienst anmeldet
* __ServicePassword__ Das Passwort, mit welchem sich der Provider beim Zefix-Dienst anmeldet. Kann verschlüsselt sein.
* __Uri__ Optionale Service Url. Default: http://www.e-service.admin.ch/ws-zefix-1.6/ZefixService?wsdl


    
