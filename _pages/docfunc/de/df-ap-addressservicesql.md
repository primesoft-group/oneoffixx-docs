---
layout: page
title: GenericSqlProvider (ADS)
permalink: "docfunc/de/df/ap/addressservicesql/"
language: de
---

# GenericSqlProvider {% include anchor.html name="providers-sql" %}

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

Hinweis bei bei Oracle: Die "SearchParameters" und die Reihenfolge innerhalb vom SQL Query muss übereinstimmen!

_Beispiel: MS SQL_

    Select FirstName, LastName FROM Users 
    WHERE FirstName LIKE '%' + @firstName + '%' AND LastName LIKE '%' + @lastName + '%'

_Beispiel: MySQL_

    Select FirstName, LastName FROM Users 
    WHERE FirstName LIKE Concat('%', @firstName, '%') AND LastName LIKE Concat('%', @lastName, '%')

_Beispiel: Oracle_

    Select FirstName, LastName from Users 
    WHERE UPPER(NVL(FirstName, ' ')) Like UPPER('%' || :firstName || '%') AND UPPER(NVL(LastName, ' ')) Like UPPER('%' || :lastName || '%')