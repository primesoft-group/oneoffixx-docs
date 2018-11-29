---
layout: page
title: Address Service
permalink: "docfunc/de/df/ap/addressservice/"
language: de
---

# File - Excel und CSV Dateien  {% include anchor.html name="providers-file" %}

__Konfiguration:__

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
             <!-- -->
            </Mapping>
        </AddressProvider>
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
        <HasHeaders>True</HasHeaders>
        <Delimeter>,</Delimeter>
    </Provider>

* __HasHeaders__ Standardwert: True, falls die CSV-Datei überschriften besitzt. Anderseits False. Wenn keine Header vorhanden sind, werden die Spalten nummeriert. (SearchParameter und Mapping entsprechend anpassen)
* __Delimeter__ Trennzeichen. Standardwert: `";"` 

### File: Excel Provider

__Konfiguration:__

    <Provider Name="EXCEL">
        <HasHeaders>True</HasHeaders>
        <Sheet>Blatt 2</Sheet>
    </Provider>

* __HasHeaders__ Standardwert: True, falls die Excel-Datei überschriften besitzt. Anderseits False. Wenn keine Header vorhanden sind, werden die Spalten wie im Excel nummeriert (A, B...). (SearchParameter und Mapping entsprechend anpassen)
* __Sheet__ Das zu verwendende Excel-Blatt. Wird kein Wert angegeben, wird das erste Blatt verwendet.