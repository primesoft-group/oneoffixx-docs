---
layout: page
title: Roadmap and Changelog
permalink: "install/de/releasenotes/"
---

Benötigen Sie die neuste OneOffixx Version wenden Sie sich bitte an unseren [Support](http://oneoffixx.com/services/support/).

<!-- TOC -->

- [OneOffixx 3.1 (Preview)](#oneoffixx-31-preview)
- [OneOffixx 2.3.50030](#oneoffixx-2350030)
    - [Client](#client)
    - [Server](#server)
    - [Office Add-In](#office-add-in)
    - [Setup](#setup)
- [OneOffixx 2.3.40270](#oneoffixx-2340270)
    - [Client](#client-1)
    - [Server](#server-1)
    - [Office Add-In](#office-add-in-1)

<!-- /TOC -->

# OneOffixx 3.1 (Preview)

Die Version 3.1 befindet sich in der Testphase und beihaltet folgende Hauptfeatures

* Untertstützung der Vorlagenversionierung für Layouter.
* Neues Fensterkonzept im Layouter-Admin Modus
* Nebst AD-Gruppen und AD-Usern werden neu auch OneOffixx-Gruppen und OneOffixx-User unterstützt.
* Alle Serverkonfigurationen in den Dateien OneOffixx.config wurden zu einer zentralen Datei zusammengefasst.


# OneOffixx 2.3.50030

Branch von Release 2.3.4 - Es wurde ein Fehler beim "komplett überschreiben" von Snippets gefunden der dazu führte, dass Textbausteine verloren gehen (nur in Mehrsprachigen Umgebungen). Funktionalität wurde angepasst, sodass kein Snippet mehr gelöscht wird. Neu wird der Content der entsprechenden Sprachen einfach überschrieben. 
Der Text wurde entsprechend auch angepasst, da es unterschiedliche Interpretationen davon gab. Neuer "Default" ist nun auch übersetzen und nicht mehr komplett überschreiben. Da die Serverschnittstelle angepasst werden musste, sollte die Serversoftware auf die gleiche Version angehoben werden.

## Client
* **New** Outlook Adressprivider unterstützt neu GAL Suche & Adressbuch Selektion & "Whitelists"
* **Fixed** Copyright-Hinweise auf Jahr 2017 angepasst und teilweise vereinheitlicht
* **Fixed** Begriffe "Textbaustein" und "text module" vereinheitlicht, englische Admin-Labels angepasst (z. B. "User Administrator"), Textbaustein-übersetzen-Fenster breiter gemacht
* **Fixed** Themes-DF: Für Berechtigung der Themes eine Scrollbar hinzugefügt
* **Fixed** DefaultConfig von Scripting-Dokument-Funktion aktualisiert: Fehler korrigiert, Beispiele verschoben, Verknüpfungen zum glob. Konf.-prov. entfernt, "depth"-Beschreibung hinzugefügt, Skript-Typen beschrieben (text, snippet, image)
* **Fixed** Richtige Schreibweise von fFormattingNumber und fFormattingDate wird neu auch unterstützt. (Test hinzugefügt, DefaultConfig von Scripting-DF und glob. Konf.-prov. angepasst)
* **Fixed** Wording im Admin beim Löschen von Usern entschärft - es wird nun von einem OneOffixx account gesprochen und es wird darauf hingewiesen, dass der AD account nicht geändert wird.
* **Fixed** Excel: Bild-Binding im Header funktioniert nun auch wenn sich eine Checkbox (oder ein anderes Control) in der Arbeitsmappe befindet
* **Fixed** Suchbox in der Unterschriftsprofil wird beim Anzeigen geleert (vorher wurde der Text immer wieder verwendet, was zu verwirrenden Ergebnissen geführt hat)
* **Fixed** Profiladministration zeigt nun die Berechtigungsstufe an (Unterschrift / Vektorisierte Unterschrift) - es sollte sich zumindest gleich verhalten wie ein eigenes Profil
* **Fixed** Beim Klick auf "Benutzer- / Profiladministration" wird automatisch das Eingefeld markiert.
* **New** Ctrl+S/Esc unter Organisations-Tab als Schnellzugriff für Save/Cancel
* **Fixed** Profil-Management: Wenn man alle Profile bis auf eins gelöscht hatte, gab es den Fall das es so aussah als hätte man zwei "Standard-Email" Profile. Der Fehler wurden behoben.
* **Fixed** Neuer UserFavoriteSnippet Endpoint in Service, welcher nur Fav-Einstellungen synchronisiert ohne die eigentlichen Snippets zu ändern
* **Fixed** "Zuletzt verwendete Textbausteine" werden nun nicht mehr synchronisiert, sondern nur lokal gehalten
* **Fixed** UseEnglish bzw. LCID 9 sollte nun immer greifen
* **Fixed** "Leere" RegEx Text-Felder werden nur noch als Invalid markiert wenn sie als "Required" gekennzeichnet sind
* **New** Die MetaData Dokumentfunktion unterstützt neu int, date, double
* **New** Scripts:Anpassungen an fFormatingNumber: Ländervorwahl kann neu gesetzt werden (Verhalten bei existierenden Konfigurationen bleibt)
* **Fixed** Unterschriftsprofil hinzufügen für einen anderen Benutzer konnte crashen falls ein freigegebenes Profil keine OE hat

## Server
* **Fixed** Permissions werden nun bei der Profiladministration mitgegeben, Gruppen-Mitgliedschaften werden nun bei der Profiladministration aufgelöst
* **Fixed** StopWatch Log-Einträge für Service-Performance nun auf Info (vorher Debug) gestellt
* **New** Um die Gruppen-Mitgliedschaften aufzulisten benötigt die AD-Komponente evtl. zumindest eine Domäne, Username und Password - dies kann nun in den Einstellungen gesetzt werden.
* **New** Einstellungen mit Hilfe hinterlegt 
* **New** Unter Security kann man nun neue User anlegen (war der einfachste und "sinnvollste" Test um festzustellen ob die AuthActiveDirectory* funktionieren.
* **Fixed** App -> Download Logs as .zip hatte irrtürmlich als Beschreibung ".txt" anstelle von ".oolog" verwendet. Geändert auf ".oolog".
* **Fixed** UserMigrator zeigt nun eine Warnung an falls mehrere User ein Matching-Kriterium erfüllen - vorher ist es komplett gecrasht.
* **New** SyncFusion PDF update - ist nun gleich mit "OneOffixx"/V3 Branch


## Office Add-In
* **New** Ab Outlook 2016 verwenden wir die von Outlook bereitgestellte "neuen" "Datei anfügen" (SplitButton mit zuletzt benutzten Dateien) auch im OneOffixx Ribbon.
* **Fixed**  Formatierung sollte nun auch in Tabellen "richtig" funktionieren und nicht mehr versehentlich die gesamte Tabellenzelle markieren
* **Fixed** Excel HeaderFooter: Durch Binding von OneOffixx-Texten entsteht neu keine Überlänge mehr (Excel akzeptiert nur 255 Zeichen)
* Fixed Changing Break Textbausteine. Textbausteine gehen in Mehrsprachigen Umgebungen verloren
* StopWatch Log-Einträge für Service-Performance nun auf Info (vorher Debug) gestellt

## Setup
* **New** Setup registriert Outlook-AddIn immer unter DoNotDisableAddinList, so dass das AddInauch auf langsamen Umgebungen nicht deaktiviert werden sollte.


# OneOffixx 2.3.40270

## Client
* **Fixed** Der Lizenz-Endpunkt wird nun bei einer validen Lizenz nur einmal pro "Session" aufgerufen
* **New** Option für Software-Rendering: Bei Darstellungsproblemen kann die Hardware-Beschleunigung deaktiviert werden.
* **Fixed** Fix für NullRefException beim ViewButton falls kein Type="Submit" und kein TargetView angegeben wurde.
* **New** Beim Importieren von Templates werden GlobalFunctionen jetzt standardmässig nicht mit importiert.
* **Fixed** Unterstützung mehrzeiliger Firmen-Namen mit CR, neues Content Control "Company.Name" hinzugefügt
* **Fixed** Fix für Save path Definition: Beim Öffnen eines zuvor gespeicherten Dokuments wird nochmals gespeichert - bei schreibgeschützten Dateien öffnete sich der "Speichern unter"-Dialog
* **Fixed** Funktion wird nun richtig unterhalb des Namens angezeigt und nicht mehr unterhalb der Firma
* **Fixed** Bilder-Id-Randomizer hat nicht immer 100% eine eindeutig zufällige Zahl generiert, da new Random() in einer Schleife aufgerufen wurde und dies ein Zeitbasierten Seed zur folge hat der gleich sein kann. Auswirkungen waren beim Snippet+Bilder einfügen zu beobachten.
* **New** CR RUF GeSOFT Adressprovider. Der RUF Schnittselle wurde insofern geändert, dass die Wildcardsuche nicht mehr via dem Zeichen "]" durchgeführt wird, sondern durch den Like Operator. Neu kann mit den Zeichen ">" "<" "*"(like) und "?"(contains) gesucht werden.
* **Fixed** Dokumentation über imageURL angepasst, wegen der Outlook 2013/2016 & Bilder Thematik
* **New** Win7 Classic Desktop Textboxen in Organisation erhalten einen Rand
* **New** Images in Views können nun über "alignment" (center/left/right) positioniert werden (default ist center) 
* **Fixed** DocFunc Recipient:Clipboard-Adressen werden nun wieder geparst & sie sind editierbar

## Server
* **New** ServiceAddress kann neu via Global Policies ausgerollt werden. ADMX bereitgestellt. (Siehe [Docs]({{site.baseurl}}/install/de/client/#msi)) 
* **New** ExtendedBinding: Command 'ConnectUpdate' now handled
* **New** Admin:"Gelöschte" TemplateGroups werden im Template-Tab jetzt gesondert markiert
* **New** TemplateActive & TemplateGroupActive added in Template -> CSV Export/Import & Editor
* **Fixed** SnippetResolver - HTML Parser: Es wird nun kein zusätzliches Body-Element mehr erzeugt. Die konvertierten Elemente werden direkt an die entsprechende Stelle gesetzt - dies sollte nun "valide" docx Dateien erstellen.
* **Fixed** Connect - Html2Word Converter: <li>-Kindelemente werden bei Bedarf nun immer in ein <p> gesteckt, sodass es pro <li> nur ein "top-level" numbering element gibt.
* **New** Die Farbe des Clients kann neu über den Server festgelegt werden, auch Farben ausserhalb der Standardpalette
* **New** DocFunction - CustomInterfaceConnector:Image-Loader nutzt nun DefaultAuth für Intranet Szenarien
* **Fixed** SyncFusion dll fix - gedrehter Text in ContentControls wird nun im PDF ebenfalls rotiert gerendert
* **Fixed** ContentControls in Header/Footer werden nun ebenfalls mit dem richtigen ContentControl Wert befüllt (vor der PDF Konvertierung)
* **New** Admin:Help-Link zu MSIEXEC aktualisiert (vorher führte er zu einer Windows Server 2003 Installation im TechNet)
* **New** MetaData DF nun serverseitig erreichbar
* **Fixed** ConvertToPDf Command ändert die FileExtension 
* **New** Connect:HTML > Word Converter - Special Chars with & < > "
* **New** Connect:HTML > Word Converter - Html Encoded Chars werden umgewandelt
* **New** Connect:HTML > Word Converter - mehr Tags (html\body\div\br\a\inputs\textarea\time\code\quote)
* **New** Connect:HTML > Word Converter - Tabellen
* **New** Connect:OrganizationId via <Profile>-Tag

## Office Add-In
* **Fixed** Standard-Button bei der Formatierung nimmt nun wieder den konfigurierten Wert.
* **Fixed** Bislang hat Outlook versehentlich den TaskPanel Host von Powerpoint mit genutzt, da diese die gleiche ID hatten. Dies ist nun korrigiert und Powerpoint hat nun eine eigene ID.
* **Fixed** Unsichtbares Zeichen in Mailsignature entfernen - es wird nun ein Field eingefügt
* **Fixed** Outlook: Wenn die im Mail vorhandene ProfileId nicht verfügbar ist, wird versucht das Standardprofil zu verwenden.
* **Fixed** Gewähltes Profil/Sprache nun nicht mehr über Outlook UserProperties gelöst, sondern über den Mailheader. Fixt das "signierte-Email" Problem
* **Fixed** Fix für "OpenMainWindow" bereitgestellt - bei einigen Maschinen konnte man vorher nicht aus dem Addin das Hauptfenster aufrufen.
* **Fixed** Outlook: Kampagne und Signature Buttons werden richtig 'getoggled'.
* **Fixed** Outlook: Mailsprache wird nun nur auf dem neuen Text gesetzt, so wird die Rechtschreibung auf dem Orignal bei Antworten/Weiterleiten-Mails nicht neufalsch geprüft.
* **Fixed** Outlook: Mailsprache wird nun nur auf dem neuen Text gesetzt, so wird die Rechtschreibung auf dem Orignal bei Antworten/Weiterleiten-Mails nicht neufalsch geprüft.
* **Fixed** Outlook: Text-Signaturen wird bei Intern/Extern wechsel nun anders behandelt, da es bei einem Kunden zu Encoding-Problemen kam.
* **New** ContactMapping Beschreibung hinzugefügt
* **New** Abacus Adressprovider unterstützt neu einen gemeinsamen Service User. Dieser benötigt in der Globalen Konfig zusätzlich die Parametern <User/>,<Password/> und <Mandant/>. _Es wird dringend empfohlen die Abacus-Schnittstelle mit dem GenericAdressProvider umzusetzen, da die Suche wesentlich besser ist._
