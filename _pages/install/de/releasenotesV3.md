---
layout: page
title: Releasenotes V3
permalink: "install/de/releasenotesv3/"
language: de
---

Benötigen Sie die neuste OneOffixx Version wenden Sie sich bitte an unseren [Support](http://oneoffixx.com/services/support/).

<!-- TOC -->

- [OneOffixx V 3.1.10170](#oneoffixx-v-3110170)
    - [Client](#client)
- [OneOffixx V 3.1.10160](#oneoffixx-v-3110160)
    - [Client](#client-1)
- [OneOffixx V 3.1.10150](#oneoffixx-v-3110150)
    - [Client](#client-2)
    - [Server](#server)
- [OneOffixx V 3.1.10140](#oneoffixx-v-3110140)
    - [Client](#client-3)
    - [Server](#server-1)
    - [Office Add-In](#office-add-in)
    - [Setup](#setup)
- [OneOffixx V 3.1.10110](#oneoffixx-v-3110110)
    - [Client](#client-4)
    - [Server](#server-2)
    - [Office Add-In](#office-add-in-1)
    - [Setup](#setup-1)
- [OneOffixx V 3.1.10060](#oneoffixx-v-3110060)

<!-- /TOC -->


# OneOffixx V 3.1.10170

##  Client
* <span class="label label-danger">Fixed</span> Absturz wenn Dokument keine Dokumentparameter besitzt behoben 
* <span class="label label-danger">Fixed</span> Fix damit der Client bei einem "invalidem" Dokument nicht abstürzt
* <span class="label label-danger">Fixed</span> Ensure window position is set even on silent/hidden 

# OneOffixx V 3.1.10160

## Client
* <span class="label label-danger">Fixed</span> Es kann nun die TemplateId genutzt werden anstelle der internen ID Bug 
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
* <span class="label label-success">New</span> PowerShell Skript für update "cleverer" gemacht Changeset

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

