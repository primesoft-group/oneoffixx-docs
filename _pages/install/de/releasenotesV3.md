---
layout: page
title: Releasenotes V3
permalink: "install/de/releasenotesv3/"
language: de
---

Benötigen Sie die neuste OneOffixx Version wenden Sie sich bitte an unseren [Support](http://oneoffixx.com/services/support/).

<!-- TOC -->

- [OneOffixx V 3.3.10252](#oneoffixx-v-3310252)
    - [Client / Document Engine](#client--document-engine)
    - [Server](#server)
    - [Office Add-In](#office-add-in)
    - [Setup](#setup)
    - [Connect](#connect)
- [OneOffixx V 3.1.10170](#oneoffixx-v-3110170)
    - [Client](#client)
- [OneOffixx V 3.1.10160](#oneoffixx-v-3110160)
    - [Client](#client-1)
- [OneOffixx V 3.1.10150](#oneoffixx-v-3110150)
    - [Client](#client-2)
    - [Server](#server-1)
- [OneOffixx V 3.1.10140](#oneoffixx-v-3110140)
    - [Client](#client-3)
    - [Server](#server-2)
    - [Office Add-In](#office-add-in-1)
    - [Setup](#setup-1)
- [OneOffixx V 3.1.10110](#oneoffixx-v-3110110)
    - [Client](#client-4)
    - [Server](#server-3)
    - [Office Add-In](#office-add-in-2)
    - [Setup](#setup-2)
- [OneOffixx V 3.1.10060](#oneoffixx-v-3110060)

<!-- /TOC -->
# OneOffixx V 3.3.10252

WICHTIG BEIM DEPLOYMENT: Windows Auth muss nun im IIS beim Service aktiviert sein!
Hinweis zur Auth-Änderung: Alte Clients sollte auf den "alten" TemplateDocumentWebService ausweichen können. Zumindest ein Test mit einer 2.3.5 und 3.1 Version war so erfolgreich und konnte synchronisiert werden.

##  Client / Document Engine
* <span class="label label-danger">Fixed</span> Neu werden leere Sub-Templats (d.h. gar kein Content vorhanden) ignoriert 
* <span class="label label-danger">Fixed</span> Themes laden nun im Profil überschriebene Bilder richtig. 
* <span class="label label-danger">Fixed</span> Crash verhindert falls man ein Template mit angehangenen Unterdokumenten im TemplateEditor offen hatte und beim Unterdokument die Previe aktualisiert hatte 
* <span class="label label-danger">Fixed</span> DocParam, Calc: Das Calc-Binding beachtet beim Parsen die Nummernformat-Einstellungen des PCs zur Dokument-Sprache (vorher wurde Framework-Standard von Dokument-Sprache verwendet) 
* <span class="label label-danger">Fixed</span> Im "CalcBinding" wurde in der Vergangenheit "," mit "." ausgetauscht, dies hatte in nicht -ch Regionen (z.B. en-uk) Fehlerhafte Auswirkungen: aus 99,99 wurde 99.99, welches in der Region nicht in eine Zahl umzuwandeln ist. Da das Feature eher eine "Bequemlichkeit" war, wurde das Verhalten geändert - Zahlen müssen immer in der jeweiligen Regionsvariante angegeben werden. 
* <span class="label label-danger">Fixed</span> ListItems im "falschen" Format werden nun ignoriert. Der neue ListItem Stil, welcher im XSD vorgegeben ist, muss beachtet werden 
* <span class="label label-success">New</span> Das Dokumentparameter-Fenster im neuen Design ist nun von der Grösse her variabel (CanResize / Resizable). Die Angabe bei WindowHeight/WindowWith wird als Initialwert genommen. Der Empfänger-Dialog verhält sich im Grunde genauso. 
* <span class="label label-success">New</span> Neue Script-Funktion zum Formatieren von Zahlen hinzugefügt: fFormattingNumeric - damit kann man eine Dezimalzahl über die normalen .NET Formatierungsoptionen formatieren.
* <span class="label label-success">New</span> Performance-Optimierung bei Skripts: Skript-Durchläufe werden abgebrochen, sobald der Output 2-mal derselbe ist ("Depth" gibt neu nur noch die maximale Anzahl Durchläufe an) 
* <span class="label label-success">New</span> Startseite der Datasource-Wahl modernisiert und mit einem Healtcheck ausgestattet 
* <span class="label label-success">New</span> Datasource Management hinzugefügt für grosse Templating Umgebungen 
* <span class="label label-danger">Fixed</span> Wording Änderung beim Rampup bezüglich primaryDatasource 
* <span class="label label-danger">Fixed</span> Falls bei einem Snippet-Script alle Bedingungen nicht erfüllt sind, wird der Inhalt des Bookmarks geleert. Bislang war es so, dass in dem Fall der Text aus dem Entwurfsmodus stehen blib. 
* <span class="label label-success">New</span> SyncFusion (ConvertToPdf) aktualisiert auf Version 16.1.0.24 
* <span class="label label-success">New</span> nest/is-e added UserStory
* <span class="label label-danger">Fixed</span> SubTemplates, welche vor dem MainTemplate eingefügt werden, löschen nun nicht mehr den Content vom MainTemplate 
* <span class="label label-warning">Fixed</span> WPF Software Rendering ist nun der Default. Das Flag "ForceSoftwareRendering" in der config wurde auch wieder entfernt, da nun der neue Default direkt das SoftwareRendering ist. 
* <span class="label label-danger">Fixed</span> Im der "Eigenschaften" Ansicht im TemplateEditor wurde das "Active" Flag bei einer Dokumentfunktion nicht ausgewertet. "Aktive" Dokumentfunktion ist zwar vom Wording her etwas blöd, aber das Feature kam er vor kurzem rein. Man kann DFs auch auf Template-Ebene deaktivieren. Dies wird jetzt auch im Eigenschafts-Tab visualisiert 
* <span class="label label-danger">Fixed</span> Führende WhiteSpaces im CustomHelpLink konnten den Client zum Absturz bringen. Der Link wird nun geloggt und führende/abschliessende Leerzeichen entfernt und Process.Start fehler werden abgefangen. 
* <span class="label label-success">New</span> Diverse Performanceverbessserungen beim Öffnen von Dokumentparameter 
* <span class="label label-success">New</span> Performance Verbesserung beim Aufruf des TemplateEditor (das Laden der TemplateRelations (SubTemplates etc.)) wurde beschleunigt 
* <span class="label label-danger">Fixed</span> Verschachtelte Span-Elemente mit Formatierungsoptionen sollten nun richtig konvertiert werden 
* <span class="label label-danger">Fixed</span> Es konnte auftreten, dass leere Field Localizations in der DB gespeichert wurden. Dies führte dazu, dass im Client ein leeres Label gezeigt wurde. Zudem wird nun nur noch in derselben Sprachfamilie nach einem Label gesucht (also bei einem DE System werden nur DE Localizations gesucht (DE-CH/DE-AT/DE-DE). Falls nichts gefunden wird, wird die FieldId zurückgegeben. 
* <span class="label label-danger">Fixed</span> Performance Improvement für UserFavorites 
* <span class="label label-success">New</span> XML Editor verbessert: XML Region support und "Standard" XML Autocomple-Einträge hinzugefügt 
* <span class="label label-danger">Fixed</span> Lokalisierung vom SubTemplate Editor Knopf im TemplateEditor fehlte 
* <span class="label label-danger">Fixed</span> Falls kein SubTemplate die Bedingungen erfüllt, wird auch nicht mehr versucht diese einzufügen #13125
* <span class="label label-danger">Fixed</span> Unterdokumente erzeugen nun keine unvorhergesehenen Leerzeilen bei Snippets 
* <span class="label label-success">New</span> XML Transformation hinzugefügt (aus dem MergeConfig Dev-Branch). Damit ist es möglich XML Konfigurationen zu transformieren. Zusätzlich wurde ein Button "Config testen" eingebaut, welcher die Engine anstösst, sodass man sieht wie die Config als 
* <span class="label label-danger">Fixed</span> Fix falls man Snippet-Scripts in Unterdokumenten einsetzt und dieses Mehrfach einfügt. Vorher wurde nur das erste Snippet-Script beachtet, nun werden alle richtig abgefüllt. 
* <span class="label label-danger">Fixed</span> Lizenzendpunkt wird nun mit Auth-Informationen aufgerufen 
* <span class="label label-danger">Fixed</span> ExtendedBinding wird beim Mergen wieder beachtet 
* <span class="label label-danger">Fixed</span> Custom Xml-Parts werden richtig zusammengeführt: Betrifft sowohl Unterdokumente als auch die direkte Vererbung. Dadurch funktionieren ExtendedBinding, Bilder und Snippets, welche in der Untervorlage oder einer Abhängigkeit (z.B. der Formatvorlage der Untervorlage) definiert sind, richtig. 
* <span class="label label-danger">Fixed</span> Der Template-Picker lädt nun Kategorien und Templatenamen in der richtigen UI-Sprache und nicht in der OS-Sprache. 
* <span class="label label-success">New</span> Es ist nun möglich im TemplateEditor nach den englischen "nativen" DF Namen zu suchen - unabhängig welche UI Sprache gerade gewählt ist 
* <span class="label label-danger">Fixed</span> Besseres Fehlerhandling für DB Size Calc 
* <span class="label label-success">New</span> Verfügbarer Disc Space wird im Dashboard angezeigt 
* <span class="label label-success">New</span> SyncSources können Identifier via Regex verarbeiten. Ausserdem stehen neue Identifier zur Verfügung.
* <span class="label label-success">New</span> RegexTester in Dashboard implementiert. Dadurch verringert sich hoffentlich der Aufwand bei zukünftigen SyncSource-Konfigurationen. 

## Server
* <span class="label label-danger">Fixed</span> Der UserSync konnte einen Fehler und damit ein Absturz des Clients provozieren, falls ein bestimmter Wert nicht gefunden wurde. Dabei wurde "null" in ein Claim gepackt, welcher an der Stelle nicht valide ist. 
* <span class="label label-danger">Fixed</span> Fix für die Profil-Administration: Felder sollten wieder von anderen Benutzern lokalisiert werden können. Zudem gab es einen seltsamen Fehler, dass die LCID für die Felder nicht richtig gesetzt wurde und dadurch die Client-Anzeige die Felder falsch darstellte. 
* <span class="label label-danger">Fixed</span> Admin:Im Profilviewer konnte man die Sprache bei Organisationsfelder nicht umstellen 
* <span class="label label-danger">Fixed</span> Claims können überschrieben werden, wenn sie mehrfach von einem Mapping-Target gesetzt werden. 
* <span class="label label-success">New</span> Felddefinitionen grafisch überarbeitet 
* <span class="label label-danger">Fixed</span> [UI] Die Berechtigungsprüfung wird nun im TemplateEditor vorgenommen - jeder Templater kann nun jedes Template im Editor öffnen, aber schreibende Aktionen werden unterbunden. 
* <span class="label label-danger">Fixed</span> Wenn keine Salutation konfiguriert wurde, stürzte der Recipient-Dialog ab. 
* <span class="label label-danger">Fixed</span> Custome Interfaces mit dem Typ Data werden nun auch akzeptiert, wenn die Config leer ist. 
* <span class="label label-danger">Fixed</span> Problem behoben, dass das editieren von Outlook-Vorlagen verhinderte. 
* <span class="label label-success">New</span> Mappings unterstützen das Referenzieren vorher gemappter Werte via JS: <Map SourceExpression="target('Targetname')" Target="AnotherTarget" /> 
* <span class="label label-success">New</span> Mappings beherrschen neu Selbstreferenzierung (d.h. können Daten aus früheren Mappings mit JavaScript referenzieren) 
* <span class="label label-danger">Fixed</span> Refresh bei 'Sync now' liefert geordnete Resultate
* <span class="label label-danger">Fixed</span> Überlange Felder bei Sync werden auf Maximallänge von 250 Zeigen beschnitten
* <span class="label label-danger">Fixed</span> 'Sort'-Eintrag bei Felddefinition funktioniert wieder (und sieht schöner aus)
* <span class="label label-danger">Fixed</span> Fix für Cloud Auth und WebApi Authorization 
* <span class="label label-danger">Fixed</span> Fix für Windows Auth WebApi Authorization & OneOffixx Groups 
* <span class="label label-danger">Fixed</span> Fix Auth Bug für TemplateDocument API 
* <span class="label label-success">New</span> RegexTester in Dashboard implementiert. Dadurch verringert sich hoffentlich der Aufwand bei zukünftigen SyncSource-Konfigurationen.
* <span class="label label-warning">New</span> Authentication für integrierte Streaming Web Api (Service.Host-Project), Authorization für Template Streaming Api. Breaking Change: Für alle Datenbanken mit grossen Dateien - die zwingend die Streaming-Api benötigen - müssen Client und Server zusammen geupdated werden. , UserStory
* <span class="label label-success">New</span> Dokumentfunktionen können via Dashboard global deaktiviert werden. UserStory
* <span class="label label-success">New</span> DBHost/DBName wird nun nicht mehr dem Client bekannt gegeben wenn explizit ein "Name" gesetzt wurde für die Datasource 
* <span class="label label-danger">Fixed</span> Falls von einem Fremdsystem / CRM eine Anrede und/oder Briefanrede kommt (aber keine Grussformel!), dann wurde vorher die Daten initial wieder zurückgesetzt. Neu wird zumindest initial alles erhalten und Briefanrede/Anrede wird direkt übernommen. Bei einer nachträglichen Änderung am Namen wird allerdings wieder die OneOffixx Logik aktiv 
* <span class="label label-danger">Fixed</span> "GetRoles"-DB Query Performance verbessert 10x schneller 
* <span class="label label-success">New</span> HttpSyncSource implementiert für den UserSync 
* <span class="label label-danger">Fixed</span> OpenXML Snippets in AltChunks konnten nicht mehr eingefügt werden, da (warum auch immer es jemals ging), weil XDocument.Parse und ein späterer ToString() die XML Deklaration entfernen. Ein OpenXML AltChunk ohne XML Deklaration wird von Office nicht geöffnet und die Word Datei wird als beschädigt gemeldet. Der Bug selbst bescheibt einen komplexeren UseCase, aber es hatte zugereift ein Profil-Bild in ein OpenXML Snippet zu packen und im Dokument zu verlinken, danach wurde das Dokument korrupt.  

## Office Add-In
* <span class="label label-danger">Fixed</span> Excel: Das Logging wurde am Startup noch erweitert um die Absturzursachen einzugrenzen. Zudem wurde ein Unterschied zwischen den Excel Addin und den anderen Addins gefunden, welcher evtl. zum Absturz führen konnte  
* <span class="label label-success">New</span> Felddefinitionen grafisch überarbeitet 
* <span class="label label-danger">Fixed</span> Möglicher fix für Fehlermeldung falls "LoadBasicData" zu langsam ist und man das Dokument schliesst 
* <span class="label label-danger">Fixed</span> Ein Fehler bricht nun nicht mehr den gesamten Sync ab und die HttpSyncSource nutzt nun auch den SyncReport 

## Setup
* <span class="label label-danger">Fixed</span> Trotz Leerzeichen im Installationspfad sollte nun der Kopiervorgang erfolgreich abgeschlossen werden 
* <span class="label label-danger">Fixed</span> Basic Auth wird nun automatisch mit installiert 
* <span class="label label-danger">Fixed</span> Es werden jetzt nur noch die Haupt-Assemblies für NGEN vorgesehen (d.h. Addin.dlls und OneOffixx.exe) - dieser werden als Prio 1 NGen übergeben. 

## Connect
* <span class="label label-success">New</span> SaveAs mit "CopyOnly" in Client UserStory
* <span class="label label-success">New</span> SaveAs mit autoconvert bei dotx -> docx wenn die Dateiendung im Pfad angegeben ist UserStory


# OneOffixx V 3.1.10170

##  Client
* <span class="label label-danger">Fixed</span> Absturz wenn Dokument keine Dokumentparameter besitzt behoben 
* <span class="label label-danger">Fixed</span> Fix damit der Client bei einem "invalidem" Dokument nicht abstürzt
* <span class="label label-danger">Fixed</span> Ensure window position is set even on silent/hidden 

# OneOffixx V 3.1.10160

## Client
* <span class="label label-danger">Fixed</span> Es kann nun die TemplateId genutzt werden anstelle der internen ID  
* <span class="label label-danger">Fixed</span> TemplatePicker & CreateConnectorResult: (von v3.3.1x) Connector-Input Pfad wird nun wieder richtig an das CreateConnectorResult-Command weitergeben auch wenn der TemplatePicker Dialog aufgerufen wurde.

# OneOffixx V 3.1.10150

## Client
* <span class="label label-danger">Fixed</span> Bei einem gespeicherten Dokument konnte ein Absturz beim "OO-Senden" auftreten, wenn keine Konfiguration für "Text saved=true" hinterlegt war  
* <span class="label label-danger">Fixed</span> Im Template Editor löste Ctrl+T oft den "Silent"-Modus aus. Dies führte dazu das initial beim Testen der Vorlage die Dokumentfunktionen nicht ausgeführt wurden. 
* <span class="label label-success">New</span> Dynamicy CRM Address Provider: Support für Fetch XML: Erweiterte Queries wie z.B. ein Join von Entities sind nun unterstützt User Story
* <span class="label label-danger">Fixed</span> Fix AdressDailog: Eingabe werden nicht angenommen in "einfacher Ansicht" 
* <span class="label label-danger">Fixed</span> Fix für Empfängerbox - Adresse aus Zwischenablage 
* <span class="label label-danger">Fixed</span> Fix für Adressfeld-Vorschau im Adressprovider wird nicht aktualisiert (Software-Fehler) 

## Server
* <span class="label label-danger">Fixed</span> Der Smuggler hatte OneOffixxGroups ignoriert, welches dann zu einem Fehler beim Import/Export geführt hat - "beschädigte" Exports müssen neu erzeugt werden, da die Info direkt im Export ebenfalls fehlt!  
Client:
* <span class="label label-danger">Fixed</span> "Alter" TemplateDocumentService konnte keine "TemplateDocuments" den richtigen Templates zuordnen, tritt nur auf bei deaktivierter WebApi - ist bereits als Hotfix in 3.1.10013 drin 
* <span class="label label-danger">Fixed</span> [Vom Hotfix 3.1.10113] "Alter" TemplateDocumentService konnte keine "TemplateDocuments" den richtigen Templates zuordnen, tritt nur auf bei deaktivierter WebApi  ist bereits als Hotfix in 3.1.10013 drin

# OneOffixx V 3.1.10140

## Client
* <span class="label label-success">New</span> Empfänger, Connect: ContactItem.ContactViewOptions.SelectedAddress (Private/Business) wird angepasst, wenn ansonsten keine Adresse erscheinen würde
* <span class="label label-success">New</span> Empfänger: Ländername wird aufgrund von Länderkurzzeichen ermittelt (bei Erhalt durch Provider oder Connect)
* <span class="label label-success">New</span> Ausbau Adressprovider MS Dynamics CRM
* <span class="label label-success">New</span> Dokument-Parameter-TextBoxen: TextBoxen können mit Masken versehen werden, die die Eingabe erleichtern
* <span class="label label-danger">Fixed</span> Excel-Adressprovider: leere Zeilen (auch solche mit Leerzeichen) werden beim einlesen ignoriert
* <span class="label label-danger">Fixed</span> Es wurde ein "Null-Ref" Fehler im Zusammenhang mit alten Server und neueren Client-Versionen behoben (GroupSids waren null)
* <span class="label label-danger">Fixed</span> Connect-Command BindCustomXML: Mehrzeilige Texte werden nun korrekt gebinded (betrifft auch Connect-Command ConvertToPdf) 
* <span class="label label-danger">Fixed</span> Connect-Aufruf über Tags: Und/Oder-Logik funktioniert wieder wie im Docs beschrieben 
* <span class="label label-danger">Fixed</span> Potentielles Sync-Problem behoben ('MaxItemsInObjectGraph' wird clientseitig explizit gesetzt)
* <span class="label label-danger">Fixed</span> OOP-Export via Client: Vorschauen und Vorlagen-Dokumente werden wieder korrekt exportiert

## Server
* <span class="label label-danger">Fixed</span> OOP-Export via Client: Vorschauen und Vorlagen-Dokumente werden wieder korrekt exportiert
* <span class="label label-danger">Fixed</span> License-Endpoint bei mehreren isPrimary Datasources wirft keinen Fehler mehr solange überall das gleiche Lizenzfile hinterlegt ist. 
* <span class="label label-danger">Fixed</span> ClaimsAuth fix bei mehreren isPrimary Datasources 
* <span class="label label-danger">Fixed</span> LicenseJobCheck -> LicenseUpdate mode wird nicht mehr als gegeben angesehen -> führte zu Fehlern.
* <span class="label label-danger">Fixed</span> Evtl. fix & logging code für verschwindende OrgPermissions
* <span class="label label-danger">Fixed</span> In V3 gab es das Problem, dass nicht freigebene Styles & Formatvorlagen für normale User nicht synchronisiert wurden - dies kann zu recht heftigen Fehlern führen. Neu werden Styles / Formatvorlagen und SubDocuments immer synchronisiert.
* <span class="label label-danger">Fixed</span> Lizenzierungsregeln angepasst (Range 2.3 - 3 => Invalid bei Version 3.1). Range 2.3 - 3 wird jetzt als 2.3 - 3.MAXVERSION verstanden)
* <span class="label label-danger">Fixed</span> Connect: "Default-Size" auf 32MB erhöht
* <span class="label label-danger">Fixed</span> Connect - Html2Word:Fix für Span mit verschiedenen Formatierungsoptionen
* <span class="label label-danger">Fixed</span> Connect - Html2Word:Fix für Span mit verschiedenen Formatierungsoptionen #12227


## Office Add-In
* <span class="label label-danger">Fixed</span> Null Ref im FormattingController behoben (tritt nur auf, wenn keine Formatierung hinterlegt ist)
* <span class="label label-danger">Fixed</span> In selten Fällen, wurde auf gewissen Computern der Ribbon in einem neuen Mail nicht angezeigt sofern man offline war.


## Setup
* <span class="label label-success">New</span> PowerShell Skript für update "cleverer" gemacht 

# OneOffixx V 3.1.10110

## Client
* <span class="label label-danger">Fixed</span> Potentielles Sync-Problem behoben ('MaxItemsInObjectGraph' wird clientseitig explizit gesetzt)
* <span class="label label-danger">Fixed</span> Empfängerdialog: Briefanrede-Auswahl geht nicht mehr verloren, wenn im Details-Dialog der Name verändert wird
* <span class="label label-danger">Fixed</span> Nach Import: Concurrency-Problem erzeugte Exception nach Sync
* <span class="label label-danger">Fixed</span> Snippets: Fix beim Verschieben von Kategorien aus Vorlagen-Textbausteinen (Usage von Objekten wird angepasst)
* <span class="label label-danger">Fixed</span> DF-DocParam: Views ohne "id" hatten eine Null-Ref erzeugt
* <span class="label label-danger">Fixed</span> Parmeter wurden doppelt in CXML abgelegt 
* <span class="label label-danger">Fixed</span> Absturz wenn von einer neuen Version das Dokument geöffnet wurde
* <span class="label label-success">New</span> Italienische Ressourcen vervollständigt
* <span class="label label-danger">Fixed</span> Template-Versions Selektion hat bei Interaktionen vom Ribbon (z.B. Dokument Parameter) nicht zuverlässig die richtige Config ausgewählt 
* <span class="label label-danger">Fixed</span> Unterdokumente wurden nicht korrekt ausgewählt, wenn die Versions-ID nicht mit der Gesamt-ID der Vorlage übereinstimmte.
* <span class="label label-success">New</span> Zuletzt geklicktes Template wird sich nun (in Memory) pro TemplateGroup gemerkt.
* <span class="label label-success">New</span> Performanceverbesserung bei der Template-Auswahl
* <span class="label label-danger">Fixed</span> Fix Logging/ErrorMessaging in SignalR Handler
* <span class="label label-danger">Fixed</span> Fix Logging/ErrorMessaging in SignalR Handler
* <span class="label label-success">New</span> RecipientAddresses / Empfängeradressen: "Frau und Herr" als Anrede neu konfigurierbar 
* <span class="label label-danger">Fixed</span> RecipientAddresses - Outlook Adressbücher Zugriff "stabilisiert" 


## Server
* <span class="label label-danger">Fixed</span> Import Table SecurityGroupSecurityAccount wird nun korrekt gelöscht. Vorher schlug der Import fehl, wenn eine OneOffixxGruppe mit exportiert wurde.
* <span class="label label-danger">Fixed</span> Exception bei Vorlagen-Import tritt nicht mehr auf. Ursache war das asynchrone Laden der Bilder, was Performanceverbesserungen gebracht hatte, aber durch diese Fehler wieder rückgängig gemacht wurde.
* <span class="label label-danger">Fixed</span> Typo fix in Admin ("remove" => "remote active directory")
* <span class="label label-success">New</span> Unter "Fields" - "Field-Viewer" werden nun synchronisierte Felder direkt mit einem Icon markiert

## Office Add-In
* <span class="label label-danger">Fixed</span> Problem behoben, dass Textbausteine im Root nicht sichtbar sind (Snippets, die bereits unsichtbar sind, bleiben unsichtbar → Snippet verschieben behebt das Problem)
* <span class="label label-danger">Fixed</span> «Rechtsklick, Klick» bewirkt nicht mehr, dass der Snippet verschoben wird
* <span class="label label-danger">Fixed</span> Wenn OneOffixx noch nie gestartet wurde, haben die AddIns einen Fehler beim starten.
* <span class="label label-success">New</span> AddIn-Ribbon & Formatierung-DF: Formatierungs-Buttons wie "T1" können nun durch Konfiguration ausgegraut werden; lcid aus Konfiguration entfernt; Autovervollständigung hinzugefügt; DefaultConfig angepasst 
* <span class="label label-success">New</span> AddIn-Ribbon: "Unterschrift ändern"-Button ist deaktiviert, wenn kein Signer gesetzt werden kann

## Setup
Keine Änderungen


# OneOffixx V 3.1.10060

Die Version 3.1 wurde offiziell released und beinhaltet folgende Hauptfeatures.

* Unterstützung der Vorlagenversionierung für Layouter.
* Neues Fensterkonzept im Layouter-Admin Modus
* Neben AD-Gruppen und AD-Usern werden neu auch OneOffixx-Gruppen und OneOffixx-User unterstützt.
* Alle Serverkonfigurationen in den Dateien OneOffixx.config wurden zu einer zentralen Datei zusammengefasst.

