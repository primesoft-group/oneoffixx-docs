---
layout: page
title: Releasenotes
permalink: "install/de/releasenotes/"
language: de
---

Benötigen Sie die neuste OneOffixx Version wenden Sie sich bitte an unseren [Support](http://oneoffixx.com/services/support/).

<!-- TOC -->

- [OneOffixx V 3.1.10110 <span class="label label-success">Released</span>](#oneoffixx-v-3110110-span-classlabel-label-successreleasedspan)
    - [Client](#client)
    - [Server](#server)
    - [Office Add-In](#office-add-in)
    - [Setup](#setup)
- [OneOffixx V 3.1.10060](#oneoffixx-v-3110060)
- [OneOffixx 2.3.50090](#oneoffixx-2350090)
    - [Client](#client-1)
    - [Server](#server-1)
    - [Office Add-In](#office-add-in-1)
    - [Setup](#setup-1)
- [OneOffixx 2.3.50060](#oneoffixx-2350060)
    - [Client](#client-2)
    - [Server](#server-2)
    - [Office Add-In](#office-add-in-2)
    - [Setup](#setup-2)
- [OneOffixx 2.3.50030](#oneoffixx-2350030)
    - [Client](#client-3)
    - [Server](#server-3)
    - [Office Add-In](#office-add-in-3)
    - [Setup](#setup-3)
- [OneOffixx 2.3.40270](#oneoffixx-2340270)
    - [Client](#client-4)
    - [Server](#server-4)
    - [Office Add-In](#office-add-in-4)

<!-- /TOC -->

# OneOffixx V 3.1.10110 <span class="label label-success">Released</span>

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

# OneOffixx 2.3.50090

In dieser Version wurde das Ladeverhalten der Add-Ins optimiert. Outlook dürfte nicht mehr versuchen das Add-In wegen langsamen startens zu deaktivieren.

## Client
* <span class="label label-danger">Fixed</span> Fehlgeschlagenes Cleanup bei der Verteilung externer Dateien wird nur protokolliert anstatt einen Fehler zu verursachen. 

## Server
* <span class="label label-danger">Fixed</span> Ein Fehler beim Snippet-Import wurden behoben - der Fehler bewirkte, dass der gesamte Import Vorgang abgebrochen ist.
* <span class="label label-success">New</span> Der Magic String [empty] (bedeutet, dass das User-Feld geleert werden muss) greift nun auch, wenn der Abgleich durch eine Synchronisation eines Users ausgelöst wurde

## Office Add-In
* <span class="label label-danger">Fixed</span> Neues Ladeverhalten der Addins - Outlook sollte keine/seltener eine Warnung über einen ggf. zu langen Ladevorgang bringen.
* <span class="label label-success">New</span> ToolTip bei langen Textbausteinbeschreibung wird nun mehrzeilig dargestellt.
* <span class="label label-success">New</span> Beschreibungs-Feld bei Textbausteinen etwas vergrössert
* <span class="label label-success">New</span> LAW: Beim Öffnen von Dokumenten kommt eine Meldung vom LAW Modul, dass das Dokument möglicherweise beschädigt ist.

## Setup 
Keine Änderungen

# OneOffixx 2.3.50060
Branch von Release 2.3.4 - Es wurde ein Fehler beim "komplett überschreiben" von Snippets gefunden der dazu führte, dass Textbausteine verloren gehen (nur in Mehrsprachigen Umgebungen). Funktionalität wurde angepasst, sodass kein Snippet mehr gelöscht wird. Neu wird der Content der entsprechenden Sprachen einfach überschrieben. 
Der Text wurde entsprechend auch angepasst, da es unterschiedliche Interpretationen davon gab. Neuer "Default" ist nun auch übersetzen und nicht mehr komplett überschreiben. Da die Serverschnittstelle angepasst werden musste, sollte die Serversoftware auf die gleiche Version angehoben werden.

## Client
* <span class="label label-success">New</span> User Sync: mit "[empty]" kann bewirkt werden, dass das entsprechende Feld geleert wird. Dadurch ist ein Feld dreiwertig. Null/Value/Empty.
* <span class="label label-danger">Fixed</span> Bei Multiline-Textfelder ist der Content nach oben hin geordnet und nicht zentriert 
* <span class="label label-success">New</span> Defaultbeschreibung in Dokumentfunktion Formatierung angepasst. Das LCID des Elementes Labels zeigt neu auf Deutsch DE und CH.
* <span class="label label-danger">Fixed</span> Performance-Verbesserungen beim Laden der Addressbücher vorgenommen.
* <span class="label label-danger">Fixed</span> ClientVersion wird nun mitgeliefert in jedem Request.
* <span class="label label-danger">Fixed</span> <span class="label label-warning">Urgent</span> Es wurde ein Fehler entdeckt, der dazu führen konnte, dass evtl. mehrere Textbaustein-Favoriten erstellt wurden, welche auf denselben Textbaustein zeigen. Dies führte dazu, dass der gesamte Textbaustein-Katalog im Client nicht mehr erstellt werden konnte. Neue Textbaustein Favoriten können nun nur noch mit v2.3.5 bzw. v3 erstellt werden!

## Server
* <span class="label label-danger">Fixed</span> TemplateSave: Logging & ein potenzieller Null-Ref Fehler bei Template Permissions wurde gefixt.

## Office Add-In
* <span class="label label-success">New</span> LAW: Altes Lizenzierungsystem entfernt. Es ist nicht mehr notwendig einen Lizenzschlüssel zu hinterlegen.

## Setup
* <span class="label label-danger">Fixed</span> Wird der Client im Autostart gestartet, wird zusätzlich das Flag /Silent verwendet. Damit wird verhindert, dass der Splash Screen angezeigt wird

# OneOffixx 2.3.50030

## Client
* <span class="label label-success">New</span> Outlook Adressprivider unterstützt neu GAL Suche & Adressbuch Selektion & "Whitelists"
* <span class="label label-danger">Fixed</span> Copyright-Hinweise auf Jahr 2017 angepasst und teilweise vereinheitlicht
* <span class="label label-danger">Fixed</span> Begriffe "Textbaustein" und "text module" vereinheitlicht, englische Admin-Labels angepasst (z. B. "User Administrator"), Textbaustein-übersetzen-Fenster breiter gemacht
* <span class="label label-danger">Fixed</span> Themes-DF: Für Berechtigung der Themes eine Scrollbar hinzugefügt
* <span class="label label-danger">Fixed</span> DefaultConfig von Scripting-Dokument-Funktion aktualisiert: Fehler korrigiert, Beispiele verschoben, Verknüpfungen zum glob. Konf.-prov. entfernt, "depth"-Beschreibung hinzugefügt, Skript-Typen beschrieben (text, snippet, image)
* <span class="label label-danger">Fixed</span> Richtige Schreibweise von fFormattingNumber und fFormattingDate wird neu auch unterstützt. (Test hinzugefügt, DefaultConfig von Scripting-DF und glob. Konf.-prov. angepasst)
* <span class="label label-danger">Fixed</span> Wording im Admin beim Löschen von Usern entschärft - es wird nun von einem OneOffixx account gesprochen und es wird darauf hingewiesen, dass der AD account nicht geändert wird.
* <span class="label label-danger">Fixed</span> Excel: Bild-Binding im Header funktioniert nun auch wenn sich eine Checkbox (oder ein anderes Control) in der Arbeitsmappe befindet
* <span class="label label-danger">Fixed</span> Suchbox in der Unterschriftsprofil wird beim Anzeigen geleert (vorher wurde der Text immer wieder verwendet, was zu verwirrenden Ergebnissen geführt hat)
* <span class="label label-danger">Fixed</span> Profiladministration zeigt nun die Berechtigungsstufe an (Unterschrift / Vektorisierte Unterschrift) - es sollte sich zumindest gleich verhalten wie ein eigenes Profil
* <span class="label label-danger">Fixed</span> Beim Klick auf "Benutzer- / Profiladministration" wird automatisch das Eingefeld markiert.
* <span class="label label-success">New</span> Ctrl+S/Esc unter Organisations-Tab als Schnellzugriff für Save/Cancel
* <span class="label label-danger">Fixed</span> Profil-Management: Wenn man alle Profile bis auf eins gelöscht hatte, gab es den Fall das es so aussah als hätte man zwei "Standard-Email" Profile. Der Fehler wurden behoben.
* <span class="label label-danger">Fixed</span> Neuer UserFavoriteSnippet Endpoint in Service, welcher nur Fav-Einstellungen synchronisiert ohne die eigentlichen Snippets zu ändern
* <span class="label label-danger">Fixed</span> "Zuletzt verwendete Textbausteine" werden nun nicht mehr synchronisiert, sondern nur lokal gehalten
* <span class="label label-danger">Fixed</span> UseEnglish bzw. LCID 9 sollte nun immer greifen
* <span class="label label-danger">Fixed</span> "Leere" RegEx Text-Felder werden nur noch als Invalid markiert wenn sie als "Required" gekennzeichnet sind
* <span class="label label-success">New</span> Die MetaData Dokumentfunktion unterstützt neu int, date, double
* <span class="label label-success">New</span> Scripts:Anpassungen an fFormatingNumber: Ländervorwahl kann neu gesetzt werden (Verhalten bei existierenden Konfigurationen bleibt)
* <span class="label label-danger">Fixed</span> Unterschriftsprofil hinzufügen für einen anderen Benutzer konnte crashen falls ein freigegebenes Profil keine OE hat

## Server
* <span class="label label-danger">Fixed</span> Permissions werden nun bei der Profiladministration mitgegeben, Gruppen-Mitgliedschaften werden nun bei der Profiladministration aufgelöst
* <span class="label label-danger">Fixed</span> StopWatch Log-Einträge für Service-Performance nun auf Info (vorher Debug) gestellt
* <span class="label label-success">New</span> Um die Gruppen-Mitgliedschaften aufzulisten benötigt die AD-Komponente evtl. zumindest eine Domäne, Username und Password - dies kann nun in den Einstellungen gesetzt werden.
* <span class="label label-success">New</span> Einstellungen mit Hilfe hinterlegt 
* <span class="label label-success">New</span> Unter Security kann man nun neue User anlegen (war der einfachste und "sinnvollste" Test um festzustellen ob die AuthActiveDirectory* funktionieren.
* <span class="label label-danger">Fixed</span> App -> Download Logs as .zip hatte irrtürmlich als Beschreibung ".txt" anstelle von ".oolog" verwendet. Geändert auf ".oolog".
* <span class="label label-danger">Fixed</span> UserMigrator zeigt nun eine Warnung an falls mehrere User ein Matching-Kriterium erfüllen - vorher ist es komplett gecrasht.
* <span class="label label-success">New</span> SyncFusion PDF update - ist nun gleich mit "OneOffixx"/V3 Branch

## Office Add-In
* <span class="label label-success">New</span> Ab Outlook 2016 verwenden wir die von Outlook bereitgestellte "neuen" "Datei anfügen" (SplitButton mit zuletzt benutzten Dateien) auch im OneOffixx Ribbon.
* <span class="label label-danger">Fixed</span>  Formatierung sollte nun auch in Tabellen "richtig" funktionieren und nicht mehr versehentlich die gesamte Tabellenzelle markieren
* <span class="label label-danger">Fixed</span> Excel HeaderFooter: Durch Binding von OneOffixx-Texten entsteht neu keine Überlänge mehr (Excel akzeptiert nur 255 Zeichen)
* Fixed Changing Break Textbausteine. Textbausteine gehen in Mehrsprachigen Umgebungen verloren
* StopWatch Log-Einträge für Service-Performance nun auf Info (vorher Debug) gestellt

## Setup
* <span class="label label-success">New</span> Setup registriert Outlook-AddIn immer unter DoNotDisableAddinList, so dass das AddInauch auf langsamen Umgebungen nicht deaktiviert werden sollte.


# OneOffixx 2.3.40270

## Client
* <span class="label label-danger">Fixed</span> Der Lizenz-Endpunkt wird nun bei einer validen Lizenz nur einmal pro "Session" aufgerufen
* <span class="label label-success">New</span> Option für Software-Rendering: Bei Darstellungsproblemen kann die Hardware-Beschleunigung deaktiviert werden.
* <span class="label label-danger">Fixed</span> Fix für NullRefException beim ViewButton falls kein Type="Submit" und kein TargetView angegeben wurde.
* <span class="label label-success">New</span> Beim Importieren von Templates werden GlobalFunctionen jetzt standardmässig nicht mit importiert.
* <span class="label label-danger">Fixed</span> Unterstützung mehrzeiliger Firmen-Namen mit CR, neues Content Control "Company.Name" hinzugefügt
* <span class="label label-danger">Fixed</span> Fix für Save path Definition: Beim Öffnen eines zuvor gespeicherten Dokuments wird nochmals gespeichert - bei schreibgeschützten Dateien öffnete sich der "Speichern unter"-Dialog
* <span class="label label-danger">Fixed</span> Funktion wird nun richtig unterhalb des Namens angezeigt und nicht mehr unterhalb der Firma
* <span class="label label-danger">Fixed</span> Bilder-Id-Randomizer hat nicht immer 100% eine eindeutig zufällige Zahl generiert, da new Random() in einer Schleife aufgerufen wurde und dies ein Zeitbasierten Seed zur folge hat der gleich sein kann. Auswirkungen waren beim Snippet+Bilder einfügen zu beobachten.
* <span class="label label-success">New</span> CR RUF GeSOFT Adressprovider. Der RUF Schnittselle wurde insofern geändert, dass die Wildcardsuche nicht mehr via dem Zeichen "]" durchgeführt wird, sondern durch den Like Operator. Neu kann mit den Zeichen ">" "<" "*"(like) und "?"(contains) gesucht werden.
* <span class="label label-danger">Fixed</span> Dokumentation über imageURL angepasst, wegen der Outlook 2013/2016 & Bilder Thematik
* <span class="label label-success">New</span> Win7 Classic Desktop Textboxen in Organisation erhalten einen Rand
* <span class="label label-success">New</span> Images in Views können nun über "alignment" (center/left/right) positioniert werden (default ist center) 
* <span class="label label-danger">Fixed</span> DocFunc Recipient:Clipboard-Adressen werden nun wieder geparst & sie sind editierbar

## Server
* <span class="label label-success">New</span> ServiceAddress kann neu via Global Policies ausgerollt werden. ADMX bereitgestellt. (Siehe [Docs]({{site.baseurl}}/install/de/client/#msi)) 
* <span class="label label-success">New</span> ExtendedBinding: Command 'ConnectUpdate' now handled
* <span class="label label-success">New</span> Admin:"Gelöschte" TemplateGroups werden im Template-Tab jetzt gesondert markiert
* <span class="label label-success">New</span> TemplateActive & TemplateGroupActive added in Template -> CSV Export/Import & Editor
* <span class="label label-danger">Fixed</span> SnippetResolver - HTML Parser: Es wird nun kein zusätzliches Body-Element mehr erzeugt. Die konvertierten Elemente werden direkt an die entsprechende Stelle gesetzt - dies sollte nun "valide" docx Dateien erstellen.
* <span class="label label-danger">Fixed</span> Connect - Html2Word Converter: <li>-Kindelemente werden bei Bedarf nun immer in ein <p> gesteckt, sodass es pro <li> nur ein "top-level" numbering element gibt.
* <span class="label label-success">New</span> Die Farbe des Clients kann neu über den Server festgelegt werden, auch Farben ausserhalb der Standardpalette
* <span class="label label-success">New</span> DocFunction - CustomInterfaceConnector:Image-Loader nutzt nun DefaultAuth für Intranet Szenarien
* <span class="label label-danger">Fixed</span> SyncFusion dll fix - gedrehter Text in ContentControls wird nun im PDF ebenfalls rotiert gerendert
* <span class="label label-danger">Fixed</span> ContentControls in Header/Footer werden nun ebenfalls mit dem richtigen ContentControl Wert befüllt (vor der PDF Konvertierung)
* <span class="label label-success">New</span> Admin:Help-Link zu MSIEXEC aktualisiert (vorher führte er zu einer Windows Server 2003 Installation im TechNet)
* <span class="label label-success">New</span> MetaData DF nun serverseitig erreichbar
* <span class="label label-danger">Fixed</span> ConvertToPDf Command ändert die FileExtension 
* <span class="label label-success">New</span> Connect:HTML > Word Converter - Special Chars with & < > "
* <span class="label label-success">New</span> Connect:HTML > Word Converter - Html Encoded Chars werden umgewandelt
* <span class="label label-success">New</span> Connect:HTML > Word Converter - mehr Tags (html\body\div\br\a\inputs\textarea\time\code\quote)
* <span class="label label-success">New</span> Connect:HTML > Word Converter - Tabellen
* <span class="label label-success">New</span> Connect:OrganizationId via <Profile>-Tag

## Office Add-In
* <span class="label label-danger">Fixed</span> Standard-Button bei der Formatierung nimmt nun wieder den konfigurierten Wert.
* <span class="label label-danger">Fixed</span> Bislang hat Outlook versehentlich den TaskPanel Host von Powerpoint mit genutzt, da diese die gleiche ID hatten. Dies ist nun korrigiert und Powerpoint hat nun eine eigene ID.
* <span class="label label-danger">Fixed</span> Unsichtbares Zeichen in Mailsignature entfernen - es wird nun ein Field eingefügt
* <span class="label label-danger">Fixed</span> Outlook: Wenn die im Mail vorhandene ProfileId nicht verfügbar ist, wird versucht das Standardprofil zu verwenden.
* <span class="label label-danger">Fixed</span> Gewähltes Profil/Sprache nun nicht mehr über Outlook UserProperties gelöst, sondern über den Mailheader. Fixt das "signierte-Email" Problem
* <span class="label label-danger">Fixed</span> Fix für "OpenMainWindow" bereitgestellt - bei einigen Maschinen konnte man vorher nicht aus dem Addin das Hauptfenster aufrufen.
* <span class="label label-danger">Fixed</span> Outlook: Kampagne und Signature Buttons werden richtig 'getoggled'.
* <span class="label label-danger">Fixed</span> Outlook: Mailsprache wird nun nur auf dem neuen Text gesetzt, so wird die Rechtschreibung auf dem Orignal bei Antworten/Weiterleiten-Mails nicht neufalsch geprüft.
* <span class="label label-danger">Fixed</span> Outlook: Mailsprache wird nun nur auf dem neuen Text gesetzt, so wird die Rechtschreibung auf dem Orignal bei Antworten/Weiterleiten-Mails nicht neufalsch geprüft.
* <span class="label label-danger">Fixed</span> Outlook: Text-Signaturen wird bei Intern/Extern wechsel nun anders behandelt, da es bei einem Kunden zu Encoding-Problemen kam.
* <span class="label label-success">New</span> ContactMapping Beschreibung hinzugefügt
* <span class="label label-success">New</span> Abacus Adressprovider unterstützt neu einen gemeinsamen Service User. Dieser benötigt in der Globalen Konfig zusätzlich die Parametern <User/>,<Password/> und <Mandant/>. _Es wird dringend empfohlen die Abacus-Schnittstelle mit dem GenericAdressProvider umzusetzen, da die Suche wesentlich besser ist._
