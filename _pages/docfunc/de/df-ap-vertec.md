---
layout: page
title: VertecAddressProvider
permalink: "docfunc/de/df/ap/vertec"
language: de
---
Der Vertec AddressProvider kann neu auch über Token angesporchen werden. Dazu muess die Konfiguration wie folgt geändert werden:<br>
(Ab der Vertec Version 6.2.0.8 ist nur noch das Ansprechen per Token möglich.)

```xml
<!-- Alte Konfiguration -->
        <BasicAuth>
          <Name></Name>
          <Password></Password>
        </BasicAuth>

<!-- Neue Konfiguration -->
        <BasicAuth>
          <Token></Token>
        </BasicAuth>
```

Beim ersten Aufruf des Empfängerdialogs öffnet sich das Anmeldefenster, in welchem man die Anmeldedaten vom Vertec eingibt. Das wird nur beim ersten Mal verlangt, die Anmdeldedaten werden gespeichert.
Zudem besteht die Möglichkeit den Benutzer zu wechseln.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/VertecTokenLogin.PNG)

```xml
<!-- Vertec address provider -->
<AddressProvider id="0861976E-318F-41A1-AE45-6D894A7E7292" order="12" active="false" hiddenIfNotAvailable="true">
  <Uri>http://{host}/xml</Uri>
  <Timeout>10000</Timeout>
  <ContactMapping>
    <ContactItemXPath>//Kontakt</ContactItemXPath>
    <ContactItemXPath>//Firma</ContactItemXPath>
    <ContactItemXPath>//Person</ContactItemXPath>
    <Namespaces />
    <ContactElement id="Company_City">Firma/standardOrt</ContactElement>
    <ContactElement id="Company_City">Kontakt/standardOrt</ContactElement>
    <ContactElement id="Company_Country">Firma/standardLand</ContactElement>
    <ContactElement id="Company_Country">Kontakt/standardLand</ContactElement>
    <ContactElement id="Company_CountryShortCode"></ContactElement>
    <ContactElement id="Company_Department">Kontakt/Abteilung</ContactElement>
    <ContactElement id="Company_EmailCentral">Firma/standardEMail</ContactElement>
    <ContactElement id="Company_EmailDirect">Kontakt/standardEMail</ContactElement>
    <ContactElement id="Company_FaxCentral">Firma/standardFax</ContactElement>
    <ContactElement id="Company_FaxDirect">Kontakt/standardFax</ContactElement>
    <ContactElement id="Company_Homepage">Firma/standardHomepage</ContactElement>
    <ContactElement id="Company_Homepage">Kontakt/standardHomepage</ContactElement>
    <ContactElement id="Company_Mobile"></ContactElement>
    <ContactElement id="Company_Name">firmenname</ContactElement>
    <ContactElement id="Company_PhoneCentral">Firma/standardTelefon</ContactElement>
    <ContactElement id="Company_PhoneDirect">Kontakt/standardTelefon</ContactElement>
    <ContactElement id="Company_PostOfficeBox" fReplace="Postfach,PostfachPostfach" fSubstringAfter="Postfach"></ContactElement>
    <ContactElement id="Company_PostOfficeBox" fReplace="Postfach,PostfachPostfach" fSubstringAfter="Postfach"></ContactElement>
    <ContactElement id="Company_PostOfficeBoxCity"></ContactElement>
    <ContactElement id="Company_Street">Firma/standardAdresse</ContactElement>
    <ContactElement id="Company_Street">Kontakt/standardAdresse</ContactElement>
    <ContactElement id="Company_Supplement"></ContactElement>
    <ContactElement id="Company_ZipCode">Firma/standardPLZ</ContactElement>
    <ContactElement id="Company_ZipCode">Kontakt/standardPLZ</ContactElement>
    <ContactElement id="Greeting">grussformel</ContactElement>
    <ContactElement id="ID">objid</ContactElement>
    <ContactElement id="Language"></ContactElement>
    <ContactElement id="Person_BirthDate">Kontakt/geburtsdatum</ContactElement>
    <ContactElement id="Person_BirthDate">Person/geburtsdatum</ContactElement>
    <ContactElement id="Person_Country">Person/standardLand</ContactElement>
    <ContactElement id="Person_CountryShortCode"></ContactElement>
    <ContactElement id="Person_City">Person/standardOrt</ContactElement>
    <ContactElement id="Person_Email">Person/standardEMail</ContactElement>
    <ContactElement id="Person_Fax">Person/standardFax</ContactElement>
    <ContactElement id="Person_FirstName">Kontakt/kontaktvorname</ContactElement>
    <ContactElement id="Person_FirstName">Person/kontaktvorname</ContactElement>
    <ContactElement id="Person_Homepage">Person/standardHomepage</ContactElement>
    <ContactElement id="Person_LastName">Kontakt/kontaktname</ContactElement>
    <ContactElement id="Person_LastName">Person/kontaktname</ContactElement>
    <ContactElement id="Person_Mobile"></ContactElement>
    <ContactElement id="Person_NickName"></ContactElement>
    <ContactElement id="Person_Phone">Person/standardTelefon</ContactElement>
    <ContactElement id="Person_Position">Kontakt/stellung</ContactElement>
    <ContactElement id="Person_Position">Person/stellung</ContactElement>
    <ContactElement id="Person_PostOfficeBox" fReplace="Postfach,PostfachPostfach" fSubstringAfter="Postfach"></ContactElement>
    <ContactElement id="Person_PostOfficeBoxCity"></ContactElement>
    <ContactElement id="Person_Profession"></ContactElement>
    <ContactElement id="Person_SecondName"></ContactElement>
    <ContactElement id="Person_Street">Person/standardAdresse</ContactElement>
    <ContactElement id="Person_Title">Kontakt/titel</ContactElement>
    <ContactElement id="Person_Title">Person/titel</ContactElement>
    <ContactElement id="Person_ZipCode">Person/standardPLZ</ContactElement>
    <ContactElement id="Provider_AddressLabel">anschrift</ContactElement>
    <ContactElement id="Salutation">briefanrede</ContactElement>
    <ContactElement id="SalutationShort">anrede</ContactElement>
  </ContactMapping>
  <RequestConfiguration>
    <Envelope>
      <Header>
        <BasicAuth>
          <!-- ↓Alte Konfiguration↓ -->
          <Name></Name>
          <Password></Password>
          <!-- ↑Alte Konfiguration↑ -->
          <!-- ↓Neue Konfiguration↓ -->
            <Token></Token>
          <!-- ↑Neue Konfiguration↑ -->
        </BasicAuth>
      </Header>
      <Body>
        <Query>
          <Selection>
            <ocl>Adresseintrag</ocl>
            <sqlwhere>
                  aktiv = 1 
                            and
                        (
                    (alias like '%{0}%') or (standardadresse like '%{0}%') or (standardPLZ like '%{0}%') or (standardOrt like '%{0}%')
                      or
                    (firma in (select bold_id from adresseintrag where (name like '%{0}%') or (alias like '%{0}%') or (standardadresse like '%{0}%') or (standardPLZ like '%{0}%') or (standardOrt like '%{0}%')))
                  )
                    </sqlwhere>
          </Selection>
          <Resultdef>
            <member>Personenkonto</member>
            <member>Alias</member>
            <member>LieferantenNr</member>
            <member>Standardadresse</member>
            <member>Stellung</member>
            <member>Zusatz</member>
            <member>StandardKanton</member>
            <member>StandardTelefon</member>
            <member>Bankverbindung</member>
            <member>StandardMobile</member>
            <member>Geburtsdatum</member>
            <member>StandardHomepage</member>
            <member>StandardLand</member>
            <member>MWSTNR</member>
            <member>StandardFax</member>
            <member>Briefanrede</member>
            <member>IsMale</member>
            <member>Grussformel</member>
            <member>StandardEMail</member>
            <member>Titel</member>
            <member>StandardOrt</member>
            <member>Name</member>
            <member>Anrede</member>
            <member>StandardPLZ</member>
            <expression>
              <alias>Sprache</alias>
              <ocl>sprache.asstring</ocl>
            </expression>
            <member>KundenNR</member>
            <expression>
              <alias>firmenname</alias>
              <ocl>
                    if self.oclistypeof(Firma) then self.oclastype(Firma).name
                    else
                    if self.oclistypeof(Kontakt) and self.oclastype(Kontakt).firma-&gt;notempty then self.oclastype(Kontakt).firma.name
                    else ''
                    endif
                    endif
                  </ocl>
            </expression>
            <expression>
              <alias>kontaktname</alias>
              <ocl>
                    if self.oclistypeof(Person) then self.oclastype(Person).name
                    else
                    if self.oclistypeof(Kontakt) then 
                      if self.oclastype(Kontakt).person-&gt;notempty then self.oclastype(Kontakt).person.name 
                      else self.oclastype(Kontakt).name
                      endif
                    else ''
                    endif
                    endif
                  </ocl>
            </expression>
            <expression>
              <alias>kontaktvorname</alias>
              <ocl>
                    if self.oclistypeof(Person) then self.oclastype(Person).vorname
                    else
                    if self.oclistypeof(Kontakt) then
                      if self.oclastype(Kontakt).person-&gt;notempty then self.oclastype(Kontakt).person.vorname
                      else self.oclastype(Kontakt).vorname
                      endif
                    else ''
                    endif
                    endif		  
                  </ocl>
            </expression>
            <member>adresstext</member>
            <expression>
              <alias>Kuerzel</alias>
              <ocl>
                    if self.oclistypeof(Kontakt) then self.oclastype(Kontakt).abteilung else '' endif
                  </ocl>
            </expression>
            <expression>
              <alias>Abteilung</alias>
              <ocl>
                    if self.oclistypeof(Kontakt) then zusatzfeldasstring('abteilung') else '' endif
                  </ocl>
            </expression>
          </Resultdef>
        </Query>
      </Body>
    </Envelope>
  </RequestConfiguration>
</AddressProvider>
```