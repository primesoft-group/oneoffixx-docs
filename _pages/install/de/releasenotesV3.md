---
layout: page
title: Releasenotes V3
permalink: "install/de/releasenotesv3/"
language: de
---

Benötigen Sie die neuste OneOffixx Version? Wenden Sie sich an unseren [Support](http://oneoffixx.com/services/support/).

- [OneOffixx V 3.4.10050](#oneoffixx-v-3410050)
    - [Client](#client-1)
    - [Admin](#admin-0)
- [OneOffixx V 3.4.10040](#oneoffixx-v-3410040)
    - [Client](#client-2)
    - [DF – Dokument-Parameter](#df-–-dokument-parameter)
    - [DF – Debugger](#df-–-debugger-1)
    - [Client / Service](#client/service)
    - [OneOffixx.config / IdS / AddressService](#oneoffixxconfig-/-ids-/-addressservice)
- [OneOffixx V 3.4.10030](#oneoffixx-v-3410030)
    - [Client](#client-3)
    - [Word](#word-1)
    - [DF – LAW](#df-–-law)
- [OneOffixx V 3.4.10020](#oneoffixx-v-3410020)
    - [Client](#client-4)
    - [DF – Empfängerdialog](#df-–-empfängerdialog-1)
    - [Word](#word-2)
    - [Admin](#admin-1)
    - [Misc](#misc)
    - [Server](#server-1)
- [OneOffixx V 3.4.10010](#oneoffixx-v-3410010)
    - [Features](#features)
    - [Client](#client-6)
    - [Client – Admin](#df-–-admin)
    - [OneOffixx.config](#oneoffixxconfig)
    - [Datenbank](#datenbank)
    - [Server](#server-2)
    - [Connect](#connect-1)
    - [Wichtig](#wichtig)
- [OneOffixx V 3.3.10380](#oneoffixx-v-3310380)
    - [Client](#client-7)
    - [Admin](#admin-2)
    - [Connect](#connect-2)
    - [WebAPI](#webapi)
- [OneOffixx V 3.3.10370](#oneoffixx-v-3310370)
    - [Client](#client-8)
    - [Admin](#admin-3]
    - [Connect](#connect-3)
    - [IdS](#ids)
- [OneOffixx V 3.3.10330 - 3.3.10360](#oneoffixx-v-3310330---3310360)
    - [Client](#client-9)
    - [Installer](#installier)
    - [Service](#service)
- [OneOffixx V 3.3.10320](#oneoffixx-v-3310320)
    - [Client](#client-10)
    - [DF – Dokument-Parameter](#df-–-dokument-parameter)
    - [Übersetzungen](#übersetzungen)
    - [IdentityServer](#identityserver)
- [OneOffixx V 3.3.10310](#oneoffixx-v-3310310)
    - [Client](#client-12)
    - [Client – Outlook Signaturen/Kampagnen/Disclaimer](#client-–-outlook-signaturen/kampagnen/disclaimer)
    - [DF – Dokument-Parameter](#df-–-dokument-parameter)
    - [DF – Empfängerdialog](#df-–-empfängerdialog-2)
    - [Word](#word-3)
    - [Admin](#admin-4)
    - [Custom](#custom)
    - [Server-Performance](#server-performance)
    - [Pipeline](#pipeline)
    - [Connect](#connect-4)
- [OneOffixx V 3.3.10300](#oneoffixx-v-3310300)
    - [Client](#client-13)
    - [Client & Outlook](#client&outlook)
    - [Build](#build)
- [OneOffixx V 3.3.10290](#oneoffixx-v-3310290)
    - [Client](#client-14)
    - [Client – AddIn](#client-–-addin)
    - [DF – Dokument-Parameter](#df-–-dokument-parameter)
    - [DF – Debugger](#df-–-debugger-1)
    - [Admin](#admin-5)
    - [Document Engine](#document-engine-1)
    - [Server](#server-4)
    - [AddressService](#addressservice)
- [OneOffixx V 3.3.10280](#oneoffixx-v-3310280)
    - [Client](#client-15)
- [OneOffixx V 3.3.10270](#oneoffixx-v-3310270)
    - [Client](#client-16)
    - [Admin](#admin-6)
    - [Server](#server-5)
    - [Document Engine](#document-engine-2)
    - [Build/Package](#build/package)
- [OneOffixx V 3.3.10260](#oneoffixx-v-3310260)
    - [Client](#client-17)
    - [Admin](#admin-7)
- [OneOffixx V 3.3.10253](#oneoffixx-v-3310253)
    - [Client](#client-18)
    - [UserSync](#usersync-2)
- [OneOffixx V 3.3.10252](#oneoffixx-v-3310252)
    - [Client – Document Engine](#client-–-document-engine)
    - [Server](#server-6)
    - [Office Add-In](#office-add-in)
    - [Setup](#setup)
    - [Connect](#connect-5)


# OneOffixx V 3.4.10050

## Client
* <span class="label label-danger">Fixed</span>Bei neuen Profilen kann nicht mehr in (gesperrte) Felder der OE reingeschrieben werden.
* <span class="label label-danger">Fixed</span>Beim Anpassen von Vorlagenberechtigungen haben die OEs wieder die richtige Reihenfolge.
* <span class="label label-danger">Fixed</span>Verwendung der Tags beziehungsweise Zähler funktioniert wieder korrekt.
* <span class="label label-danger">Fixed</span>Dynamics-CRM-Adressprovider: Unterstützt neu auch Dynamics-On-Premises

## Admin
* Smuggler "ChunkSize" von 0.01 MB auf 1MB erhöht –  sorgt für einen deutlich schnelleren Upload.
* Fusszeile ist in Statistiken nicht mehr doppelt vorhanden.


# 3.4.10040

## Client
* <span class="label label-danger">Fixed</span>OE-Auswahl ist bei vielen OEs in Themes-Konfiguration nicht mehr abgeschnitten

## DF – Dokument-Parameter
* <span class="label label-danger">Fixed</span><span class="label label-success">New</span>"Views" haben ein neues Attribut bekommen: "IsVisible", darüber kann man "QuickCheck-Only" Dokument-Parameter umsetzen.
* <span class="label label-danger">Fixed</span><span class="label label-success">New</span>"IsDefault" auf Buttons bewirkt nun, dass die Standard-Aktion getriggert wird und der Fokus pro View beim Navigieren entsprechend immer auf dem ersten Control ist.

## DF – Debugger
* <span class="label label-success">New</span>Debugger bricht nun bei [ESC] ab.

## Client / Service
* <span class="label label-danger">Fixed</span>Profil zeigt nicht mehr auf gelöschte OE.

## OneOffixx.config / IdS / AddressService
* <span class="label label-danger">Fixed</span>AddressService & IdS: http 500 ist nun lowerCase URL konfiguriert. 


# OneOffixx V 3.4.10030

## Client
* <span class="label label-danger">Fixed</span>Splash Screen hat nun in diversen Sprachen die richtige Bezeichnung (Splash Screen mit "v2019" entfernt).
* <span class="label label-danger">Fixed</span>Optionen werden nicht mehr in der Dokumentsprache angezeigt. (Dokumentsprache wurde für UI Teile genutzt).
* <span class="label label-danger">Fixed</span>Profilverwaltung: OE-Zuweisung ist auch bei neuen, noch nicht gespeicherten Profilen sichtbar (eigene Profile & Fremdprofile).

## Word
* <span class="label label-danger">Fixed</span>Speichern-Button in der italienischen Version in Nicht-OneOffixx-Dokumenten funktioniert jetzt wieder.

## DF – LAW
* <span class="label label-danger">Fixed</span>LAW zeigt Übersetzungen wieder an (LAW-Lokalisation).


# OneOffixx V 3.4.10020

## Client
* <span class="label label-danger">Fixed</span>Unterschriftsprofile via Adminbereich im Client können wieder hinzugefügt werden.
* <span class="label label-danger">Fixed</span>Farbmodus wird nun beim Einfügen von optionalen Untervorlagen beachtet.

## DF – Empfängerdialog
* <span class="label label-danger">Fixed</span>Bei importierten Outlook-Kontakten aus OneOffixx konnten Anrede- oder Grussdaten falsch übernommen werden, was schlussendlich in einen Absturz endete.
* <span class="label label-danger">Fixed</span>Der "To"/"Bcc"/"Cc" Button-Bereich überlappt sich mit dem Ergebnisfeld und daher konnte der untere Bereich des Buttons nicht geklickt werden.
* <span class="label label-danger">Fixed</span>Das Einfügen von Adressen aus dem Clipboard zeigt nun Adressen mit zwei Namen korrekt an.
* <span class="label label-danger">Fixed</span>Fehlerbehebungen für mögliche Abstürze bei der Verwendung von "aus Clipboard einfügen"
* <span class="label label-danger">Fixed</span>Neues Tag "SalutationSeparatedLine"

## Word
* <span class="label label-danger">Fixed</span>Kopfzeile/Fusszeile Felder im Word werden nun nach dem Einfügen von einem Unterdokument korrekt aktualisiert.

## Admin
* <span class="label label-danger">Fixed</span>Vorlagenimport: Es kam zu einem Fehler bei (fälschlicher) Vergabe von derselben SID. Der Importer hat abgesprochen ohne konkrete Meldung im Log.

## Misc
* <span class="label label-danger">Fixed</span>DF Booklet funktioniert wieder korrekt und kann den CXMLPart wieder einfügen.

## Server
* <span class="label label-danger">Fixed</span>Behebung für "null-refs" im Service nach der Installation von .NET Framework 4.7.2 bzw. 4.6.1
* <span class="label label-danger">Fixed</span>Bilder-Snippets können wieder eingefügt werden.
* <span class="label label-danger">Fixed</span>Behebung für AutoText Sync (wurde nicht richtig übertragen)


# OneOffixx V 3.4.10010

## Features
* Trial-Variante hinzugefügt
* AutoText für Textbausteine
* Brandic-Vorlagen für PowerPoint/Excel können verteilt und wieder entfernt werden
* DocParam bei Mails mit Binding
* Server/Client können nun eine Mindest-ClientVersion aushandeln – ältere Clients können so später vom Service getrennt werden (wird durch den Client gemacht).
* Lizenzierung wieder entfernt

## Client
* <span class="label label-success">New</span>[!] Client, Empfänger, Anreden und Grussformeln: Die Konfiguration wurde vereinfacht. 
* <span class="label label-success">New</span>In Mailvorlagen kann in den Mailfeldern (Subject, To, CC, BCC) neu, zum Beispiel via Dokument-Parameter, konfiguriert werden.
* <span class="label label-success">New</span>Debugger kann für Mailvorlagen verwendet werden.
* <span class="label label-success">New</span>Dokument-Parameter: Verwirrende Anzeige der CheckBoxen im Details-Dialog behoben.
* <span class="label label-success">New</span>Neustart wegen UI-Sprach-Änderung geschieht nicht mehr im Hauptfenster (abrupt für Benutzer) sondern im Splashscreen.
* <span class="label label-success">New</span>OneOffixx PowerPoint Dokumentfunktion erstellt
* <span class="label label-success">New</span>Textbausteine unterstützen nun das Word AutoText-Feature.
* <span class="label label-success">New</span>Template Distribution unterstützt nun Scriptable Configs – so kann die Verteilung mit Bedinungen an das Zielsystem angepasst werden. Ausserdem kann beim Deinstallieren aufgeräumt werden.
* ActPlus MetaTemplate gelöscht
* Leere Dropdown im Vorlagen-Editor sind nun deaktiviert.
* Tags im Vorlageneditor werden nun aktualisiert, wenn Tags erstellt oder gelöscht werden und Fehlermeldung bei fehlenden Tags in Vorlagen behoben.
* <span class="label label-danger">Fixed</span>AddIn: Nummerierungsstufe erhöhen / verkleinern: Problem behoben, dass das Resultat erst nach erneutem Tippen sichtbar wurde.
* <span class="label label-danger">Fixed</span>Auto-Vervollständigung (IntelliSense) von DocParam: Fehler bei Checkbox korrigiert – IsChecked-Attribut entfernt
* <span class="label label-danger">Fixed</span>Empfängerdetails: Felder etwas vergrössert
* <span class="label label-danger">Fixed</span>Neuer Address-Parser für das Einfügen aus der Zwischenablage
* <span class="label label-danger">Fixed</span>Dokument-Parameter: Tooltips, die bei den DataNodes definiert wurden, funktionieren nun
* <span class="label label-danger">Fixed</span>Fehler, die im STA-Thread-ausgeführten Dokumentfunktionen werden nun korrekt weitergegeben.
* <span class="label label-danger">Fixed</span>Snippet-Skript: Wenn ein einzelner Textbaustein nicht gefunden wurde, werden die restlichen Textbausteine nun doch abgefüllt.

## Client – Admin
* UI-Sprachen: diverse Änderungen im Client und im Admin (Details siehe WorkItem)
* <span class="label label-danger">Fixed</span>Ein im Client erstellter Benutzer erhält neu automatisch eine SID. Im Admin wird eine SID nach demselben Schema vorgeschlagen. (oouser-[new guid]).
* <span class="label label-danger">Fixed</span>Datasource Management generiert den ConnectionString nun korrekt.

## OneOffixx.config
* <span class="label label-success">New</span>Readonly / Trial Mode: Datenbank kann als schreibgeschützt markiert werden.
* <span class="label label-success">New</span>Pfade zu Logverzeichnisse anderer Applikationen (logFilePath) können neu auch relative Pfade sein.

## Datenbank
* Schema optimiert, um nvarchar(max) Spalten zu minimieren
* AutoText Spalte hinzugefügt bei Snippets

## Server
* OperationContext flowed mit Async-Calls (Verhindert potenzielle NullRef-Exceptions im Service)

## Connect
* <span class="label label-danger">Fixed</span>TemplatePicker: Vorlagenliste wird neu aktualisiert, wenn das Profil gewechselt wird.
* <span class="label label-danger">Fixed</span>Connect Batches für den Connect Service funktionieren wieder korrekt. Es konnte zu Fehlern bei mehreren Dokumenten kommen.

## Wichtig
* [!] .NET 4.7.2 wird nun server- und clientseitig benötigt!
* Es wurden im Grunde fast alle NuGet Packages aktualisiert, das fängt beim UI Package an und zieht sich auch über die Dokumentenerstellung hinweg. 


# OneOffixx V 3.3.10380

## Client
* <span class="label label-danger">Fixed</span>Diverse Fehlerbehebungen bei Briefumschlag- und Etikettengenerierung.
* <span class="label label-danger">Fixed</span>Beim Speichern einer OE wird eine Fehlermeldung angezeigt, wenn im Hintergrund die Berechtigung zum Ändern dieser entzogen wurde.
* <span class="label label-danger">Fixed</span>Dokument-Parameter: ComboBox-Elemente: leere Elemente können konfiguriert werden (werden mit Leerzeichen ersetzt), Aktualisierung der Elemente verbessert
* <span class="label label-danger">Fixed</span>Empfängerdialog: Labels werden nicht mehr abgeschnitten (betrifft v. A. italienisch)

## Admin
* <span class="label label-danger">Fixed</span>Benutzer-Editor: Fehler beim Aufruf tritt nicht mehr auf (fehlendes «using»-Statement für 'Logger')

## Connect
* <span class="label label-danger">Fixed</span>Top-Level Connect Commands werden wieder richtig eingelesen.

## WebAPI
* <span class="label label-danger">Fixed</span>Proxy-Settings können nun in der appsettings.json übersteuert werden - dies ist für .NET Core + IIS Deployments wichtig


# OneOffixx V 3.3.10370

## Client
* <span class="label label-danger">Fixed</span>Profildaten- & Benutzeradministration: Beim zweiten Speichern ohne weg zu navigieren, konnten neu eingegebene Daten verloren gehen.

## Admin
* <span class="label label-danger">Fixed</span>Vorlagen-Import: Tag-Verknüpfungen werden nun auch bei existierenden Vorlagen mitimportiert.
* <span class="label label-danger">Fixed</span>CSRF-Attacke bei Aktivierung von Dokumentfunktionen verhindert mit Anti-Forgery Token

## Connect
* <span class="label label-danger">Fixed</span>DefaultProcess Connect-Befehl wird korrekt nur genau dann eingefügt, wenn kein anderer existiert (auch wenn der Befehl in Filter-Commands drin ist)

## IdS
* <span class="label label-danger">Fixed</span>DelayMeta auf «true» gestellt, ist auch die Standardeinstellung im IdS


# OneOffixx V 3.3.10330 - 3.3.10360

## Client
* <span class="label label-success">New</span>Sync Cache Version eingeführt – Client löscht nun nicht mehr immer den Cache, sondern nur bei "Cache-Struktur"-Änderungen
* <span class="label label-danger">Fixed</span>Cache wird beim Wechsel der Datenbank nur noch neu erstellt, wenn nötig.
* <span class="label label-danger">Fixed</span>Dokument-Parameter-Vererbung funktioniert wieder korrekt.

## Installer
* <span class="label label-danger">Fixed</span>Versionsnummer nicht mehr im Produktnamen bei der Installationsliste im Windows enthalten

## Service
* <span class="label label-danger">Fixed</span>Der Service hatte beim Abrufen eines einzelnen Tags zu früh die DB-Verbindung gekappt.


# OneOffixx V 3.3.10320

## Client
* <span class="label label-danger">Fixed</span>Behebung für NullRef bei Zuweisung einer OE zu einem nicht gespeichertem Profil
* <span class="label label-danger">Fixed</span>Dokument-Parameter, ComboBox: In Views gesetzter Wert (Vorauswahl) funktioniert nun.
* <span class="label label-danger">Fixed</span>Dokument-Parameter, Script: Auto-Vervollständigung verbessert (XSD, IntelliSense)
* <span class="label label-danger">Fixed</span>Validierung von Checkboxen funktioniert nun initial korrekt.
* <span class="label label-success">New</span>RadioButtons können nun als Required markiert werden.
* <span class="label label-danger">Fixed</span>Behebung für Leerschlag zwischen Datei und Dateiendung – Zusätzlicher Leerschlag zwischen Punkt und Dateiextension beim PDF-Speichern in der italienischen Sprache

## DF – Dokument-Parameter
* <span class="label label-success">New</span>«Required» bei RadioButtons hinzugefügt
* <span class="label label-danger">Fixed</span>Null-Ref Behebung für fehlenden ShippingProvider

## Übersetzungen
* <span class="label label-danger">Fixed</span>Fehlende FR/IT Übersetzungen sind nun enthalten.

## IdentityServer
* <span class="label label-danger">Fixed</span>Impersonate-Grant wurde doppelt verschlüsselt


# OneOffixx V 3.3.10310

## Client
* <span class="label label-danger">Fixed</span>Wenn eine Vorlage einen nicht mehr existierenden Tag zugewiesen hatte, führte dies zu einer Fehlermeldung beim Anzeigen der Vorlagenkategorie.
* <span class="label label-danger">Fixed</span>Wenn einem Profil eine neue OE zugewiesen wurde, verschwanden alle Felder aus der Oberfläche.
* <span class="label label-danger">Fixed</span>Synchronisation: Ladebalken macht nun auch Fortschritte, wenn Elemente nach dem Upload wieder heruntergeladen werden (re-get; Log wird ebenfalls geschrieben)
* <span class="label label-danger">Fixed</span>LanguageLcid im Connect-Aufruf wird nun beim TemplatePicker respektiert
* <span class="label label-danger">Fixed</span>Behebung für Snippet-Script mit Fixtext
* <span class="label label-danger">Fixed</span>Versionierung für Outlookmails wird nun korrekt respektiert.
* <span class="label label-danger">Fixed</span>Sync: Sync-Intervall wird nun clientseitig gespeichert (Bug) und es wurde verhindert, dass doppelte Syncs ausgeführt werden. Zudem verteilt das Intervall nun per Zufall die Anfragen besser.

## Client – Outlook Signaturen/Kampagnen/Disclaimer
* <span class="label label-danger">Fixed</span>[!] Die Signaturen samt Disclaimer- und Kampagnenauswahl berücksichtigen nun den "Admin"-Modus im Client, damit können Vorlagenbearbeiter auch in einen normalen Benutzermodus wechseln. z.%nbsp;B. nicht berechtigte Kampagnen tauchen in dem Fall nicht auf.

## DF – Dokument-Parameter
* <span class="label label-danger">Fixed</span>CheckBoxes können als «Required» markiert werden und müssen dann vom Benutzer ausgewählt werden.
* <span class="label label-danger">Fixed</span>Ist bei der ComboBox der Wert als «Invalid» markiert, wird ein rotes Dreieck angezeigt.
* <span class="label label-danger">Fixed</span>PowerPoint oder Excelvorlagen mit Dokument-Parameter konnten nicht mehr erstellt werden.
* <span class="label label-danger">Fixed</span>Wir erkennen nun im Falle von RadioButtons "ungültige" Konfigurationen (mehrere RadioButtons mit derselben Id und Value) und zeigen eine Fehlermeldung an Bug

## DF – Empfängerdialog
* <span class="label label-danger">Fixed</span>Anrede wird nun wieder korrekt zusammengebaut

## Word
* <span class="label label-danger">Fixed</span>Verhalten beim Einrücken und Ausrücken von Listen and das Verhalten von Word angeglichen. Buttons sind nun so wie die Wordbuttons angeordnet.

## Admin
* <span class="label label-success">New</span>Snippets: Snippet Ordner können nun verschoben werden; Reihenfolge gleich wie im Client (wenn 'Sort' gesetzt); Baum-Elemente können eingeklappt werden

## Custom
* <span class="label label-success">New</span>AXA CRM Suche via PolicyNummer verbessert

## Server-Performance
* <span class="label label-danger">Fixed</span>Sync-API ist nun fast vollständig auf Async umgebaut und Behebungen für hohe CPU Auslastung / bzw. "teure" Queries

## Pipeline
* <span class="label label-danger">Fixed</span>Bestehende V1 (Pipelineversion) Dokumente konnten einen Absturz verursachen.

## Connect
* <span class="label label-danger">Fixed</span><span class="label label-success">New</span>[!] Neu wird das Resultat von Connect-Operationen richtig ausgegeben, z.&nbsp;B. bei Abbruch. Dies hat die Möglichkeit zur Folge, das Connect-Befehle je nach Status ausgeführt werden können.


# OneOffixx V 3.3.10300

## Client
* <span class="label label-danger">Fixed</span>Navigation zwischen Vorlagenkategorien schlug teilweise fehl.
* <span class="label label-success">New</span>"Testmodus"/Healthcheck für Dokumente (nur über Feature Flag erreichbar)

## Client & Outlook
* <span class="label label-danger">Fixed</span><span class="label label-success">New</span>Manuelle Kampagnenauswahl implementiert
Custom AddressProvider
* <span class="label label-danger">Fixed</span>Diverse Behebungen

## Build
* Migration von TFVC auf GIT vollzogen
* "Docs" auf DocFX im Repo und im Build


# OneOffixx V 3.3.10290

## Client
* <span class="label label-danger">Fixed</span>Behebung leere Field-Labels bei neuen OEs
* <span class="label label-danger">Fixed</span>Behebung für leere Fields bei OEs/Benutzern, falls keine Daten hinterlegt wurden
* <span class="label label-success">New</span>Möglichkeit, über die Registry die RibbonPosition im Word/Outlook zu übersteuern
* <span class="label label-danger">Fixed</span>Behebung ImageBinding
* <span class="label label-danger">Fixed</span>Behebung, dass falsche Vorlagen-Id gespeichert wurde
* <span class="label label-danger">Fixed</span>Verscriptete Vektorsignaturen aus dem AddIn heraus behoben (Update von Bildern in verscripten Snippets)
* <span class="label label-danger">Fixed</span>UI + Wording auf Help-Tab angepasst
* [!] Word-Styles können nicht mehr bei Outlook-Vorlagen als "Basierend auf" verlinkt werden. Dies funktionierte ohnehin nicht und hat nur Fragen aufgeworfen.
* <span class="label label-danger">Fixed</span>Umbenannte Tags wurden in der Vorlagensuche nicht richtig berücksichtigt.
* <span class="label label-danger">Fixed</span>Bild-Export: Die Dateinamenserweiterung (z.&nbsp;B. png) ging verloren, wenn ein Dateiname mit Punkt eingegeben wurde (z. &nbsp;B. "abc.def").
* <span class="label label-danger">Fixed</span>OE-, Benutzer-, Profil-Bearbeitungs-Ansicht: Gesperrte CheckBoxen sind nun als solche ersichtlich (analog gesperrten TextBoxen).
* <span class="label label-danger">Fixed</span>Tag-Administration lädt Verwendungsdaten um ein Vielfaches schneller und stoppt, wenn von der Administration weg navigiert wird.
* <span class="label label-success">New</span>nest-Adressprovider: Aktualisierung auf nest-Release 2018 (Suchparameter hinzugekommen) – Konfiguration muss angepasst werden, Suchmaske neu konfigurierbar, weitere Verbesserungen.
* <span class="label label-danger">Fixed</span>Der TemplatePicker zeigt die Vorlagen nun in der gleichen Sortierung wie in der normalen Client-Liste an.
* <span class="label label-success">New</span>Im Backstage kann nun der lokale Cache zurückgesetzt werden.

## Client – AddIn
* <span class="label label-danger">Fixed</span>DF Adressdeckblatt lässt sich wieder aus dem Word heraus aufrufen ("Ursache:" Fehler beim DF-Interface Change).
* <span class="label label-success">New</span>Word-Felder aktualisieren: Das AddIn aktualisiert alle Word-Felder im Dokument bei OneOffixx-Fertigstellen-Aktionen (Drucken, Senden, Vorschau, PDF speichern) und beim Öffnen und Speichern (spezielles Custom Document Property muss «true» sein).

## DF – Dokument-Parameter
* <span class="label label-danger">Fixed</span>Behebung für Collection Binding mit SQL Sources – Key wurde nicht mit "ToLower..." im entsprechenden Dictionary hinterlegt (Bug von der Perf-Operation).
* <span class="label label-danger">Fixed</span>Behebung für ComboBox "IsInvalidWhenValue": Bei initialem Rendering wurde nicht richtig ausgewertet.

## DF – Debugger
* <span class="label label-danger">Fixed</span>Fix DocumentData Anzeige (falsches Property gebunden)

## Admin
* <span class="label label-danger">Fixed</span>FieldDef Admin-UI hat die Reihenfolge der Felder bislang ignoriert
* <span class="label label-danger">Fixed</span>FieldDef ADmin-UI berücksichtigt nun die DefaultUI Sprache für die Feld Labels (DefaultUI Sprache wird nun standardmässig genommen)
* <span class="label label-danger">Fixed</span>Organisation/Benutzer/Profil Editor: CheckBox-Werte (true, false, nicht gesetzt) werden nun korrekt angezeigt.
* <span class="label label-success">New</span>Seite, auf welcher der Adress-Service getestet werden kann
* Hinweis für Rollenänderungen + Cache im Security-Register hinzugefügt

## Document Engine
* <span class="label label-danger">Fixed</span>Behebung ImageHelper bei korrupten ImagePart (Ids waren dupliziert in der Vorlage hinterlegt)

## Server
* Sync-Performance bei GetChanges für Snippets/DocFunctions/OEs/Tags verbessert

## AddressService
* <span class="label label-danger">Fixed</span>Zefix AddressProvider – Label nun ohne ":" (ansonsten wird es im Client mit "::" angegeben)


# OneOffixx V 3.3.10280

## Client
* <span class="label label-danger">Fixed</span>Mehrere Benutzer/Profilfelder, die inkorrekt die gleiche Id haben, verhinderten das Generieren von Dokumenten wenn das Themes-Modul angehängt ist.
* <span class="label label-danger">Fixed</span>Scripts werden beim Aktualisieren (z.&nbsp;B. Profilwechsel) korrekt ausgeführt.
* <span class="label label-danger">Fixed</span>Fehlerhafte Warnung für MetaTemplate Policies werden nicht mehr ins Log geschrieben.
* <span class="label label-danger">Fixed</span>Server – Connect: SaveAs-Befehl in Zusammenhang mit dem "Autoconvert" und ConvertToPdf Command behoben (Der AutoConvert von einem .dotx zu .docx ist immer angesprungen, auch wenn die Daten bereits ins PDF Format konvertiert wurden).
* <span class="label label-danger">Fixed</span>Web: Behebung für "leere" Localizations


# OneOffixx V 3.3.10270

## Client
* <span class="label label-danger">Fixed</span>SendEmail-DF: Performance-Optimierung – beim Klick auf "Senden" in Word erscheint der Dialog nun deutlich schneller.
* <span class="label label-success">New</span>Nur für Entwickler (Berechtigung): Performance Charts im Backstage
* <span class="label label-danger">Fixed</span>oneoffixx:hidden funktioniert wieder
* <span class="label label-danger">Fixed</span>Outlook-AddIn: ermöglichen, Formatierungsbuttons im Ribbon auszugrauen / zu disablen (analog Word)
* <span class="label label-success">New</span>Connect URL Bezug: Connect kann über eine URL geladen werden
* <span class="label label-danger">Fixed</span>[!] Empfängerdialog: Probleme bzgl. Anrede / Briefanrede behoben ("Breaking": im Details-Dialog wird beim Anpassen des AddressTypes (wird automatisch ausgewertet) die Briefanrede neu nicht zurückgesetzt)
* <span class="label label-success">New</span>[!] Performance des Dokument-Parameter-Dialoges optimiert
* <span class="label label-danger">Fixed</span>Bug behoben, der verhinderte das OEs in der Profiladministration richtig angezeigt wurden.

## Admin
* <span class="label label-danger">Fixed</span>Field-Tab: Naming geändert von "Name" auf "FieldId" in der Fields-Tabelle (der Name ist lokalisiert und wird da nicht ausgegeben)
* <span class="label label-danger">Fixed</span>Löschen von Vorlagen ermöglicht, wenn mehrere Versionen veröffentlicht sind (dieser Zustand sollte eigentlich nie entstehen)
* <span class="label label-success">New</span>[UI] Connect URL Bezug: URLPolicies können im Admin gepflegt werden
* <span class="label label-danger">Fixed</span><span class="label label-success">New</span>AddressService: Globales Error-Handling hinzugefügt
* <span class="label label-danger">Fixed</span>Mapping mappt nun auch "BirthDate" (zusätzlich zu Birthday – wir verwenden im Spec BirthDate, das Property heisst aber BirthDay)
* <span class="label label-danger">Fixed</span>Namespace Refactoring im Mapping → AddressProvider müssen neu ausgeliefert werden beim Deployment!
* <span class="label label-danger">Fixed</span><span class="label label-success">New</span>MySQL & Oracle Provider hinzugefügt und Datenbank Parameter Syntax für MySQL/Oracle/MSSQL Syntax angepasst
* <span class="label label-danger">Fixed</span>ContactMapping kommt nun mit Null-Werten klar – vorher gab es eine Exception
* <span class="label label-danger">Fixed</span>Behebung für .NET Core SDK 2.1 Issue mit ASP.NET  Core 1.1 Apps
* <span class="label label-danger">Fixed</span>Install.ps1: Der Installer sollte nun das .NET Core 2.0.7 Bundle mit IIS Integration runterladen
* <span class="label label-danger">Fixed</span>Es werden nun "Well-known SIDs" anstelle von Benutzerkonten (IUSR) etc. verwendet, um etwaige Lokalisierungsprobleme zu umgehen
* Docker: "Admin" Nutzer im Docker File wieder entfernt

## Server
* <span class="label label-success">New</span>Performance Updates für Synchronisation
* <span class="label label-danger">Fixed</span>Sync-Perf Update für Textbausteine und Vorlagen

## Document Engine
* <span class="label label-success">New</span>[!] Alle Dokumentfunktionen sind nun auf dem neuen DocumentEngine-Interface mit intelligenterer Speicherverwaltung.
* <span class="label label-success">New</span>Script-Transformation: Performance verbessert, indem das Entfernen von Skripts aus dem vorherigen Durchgang verschnellert wurde.
* <span class="label label-success">New</span>Performance verbessert: Binding von Images ist 6x-7x schneller.
* <span class="label label-success">New</span>Auswirkungen der Performance Messungen verkleinert
* <span class="label label-success">New</span>[!] Performance von FieldContainer verbessert (OE, Profile und Benutzer)
* <span class="label label-success">New</span>Themes Dokumentfunktion ist einiges schneller.
* <span class="label label-success">New</span>Word Layout MetaTemplate ist schneller.

## Build/Package
* <span class="label label-success">New</span>Im Build wird nun unter _Clients/ ein .zip abgelegt, in dem nur der "FatClient" enthalten ist. Dies kann für XCopy Deployments (zum Testen) verwendet werden.


# OneOffixx V 3.3.10260

## Client
* <span class="label label-danger">Fixed</span>Bookmarks, die ganze Sections umfassen, führten dazu, dass Unterdokumente nicht eingefügt wurden; das funktioniert jetzt wieder.
* <span class="label label-danger">Fixed</span>Behebung für Userdefined AP
* <span class="label label-danger">Fixed</span>Tls 1.1 und Tls 1.2 Support (viele neuere Services verweigern SSL3/TSl1.0, da verschiedene Sicherheitslücken bekannt sind)

## Admin
* <span class="label label-success">New</span>Link beim MouseOver auf der Datasource-Seite hinzugefügt
* <span class="label label-danger">Fixed</span>AddNestIseDF MigrationStep behoben: Je nach Konfiguration des Systems konnte es zu einem SQL Fehler kommen, da der MigrationStep nicht explizit das "Active"-Flag mitgibt. Im ersten Schritt gibt nun der MigrationStep explizit das Active-Flag mit.


# OneOffixx V 3.3.10253

## Client
* <span class="label label-danger">Fixed</span>Absturz Behebung, falls beim Verbinden von einem Benutzer und einem AD-Account ein Fehler passiert in der Benutzerverwaltung.

## UserSync
* <span class="label label-danger">Fixed</span>RegEx kann nun mit null-Werten umgehen und WhatIf kann für die Client-Interaktion auch auf Title/LoginName zugreifen


# OneOffixx V 3.3.10252

WICHTIG BEIM DEPLOYMENT: Windows Auth muss nun im IIS beim Service aktiviert sein! 
Hinweis zur Auth-Änderung: Alte Clients sollte auf den "alten" TemplateDocumentWebService ausweichen können.

## Client – Document Engine
* <span class="label label-danger">Fixed</span> Neu werden leere Sub-Templats (d.h. gar kein Content vorhanden) ignoriert 
* <span class="label label-danger">Fixed</span> Themes laden nun im Profil überschriebene Bilder richtig. 
* <span class="label label-danger">Fixed</span> Crash verhindert, falls man eine Vorlage mit angehangenen Unterdokumenten im TemplateEditor offen hatte und beim Unterdokument die Vorschau aktualisiert hatte. 
* <span class="label label-danger">Fixed</span> DocParam, Calc: Das Calc-Binding beachtet beim Parsen die Nummernformat-Einstellungen des PCs zur Dokument-Sprache (vorher wurde Framework-Standard von Dokument-Sprache verwendet) 
* <span class="label label-danger">Fixed</span> Im "CalcBinding" wurde in der Vergangenheit "," mit "." ausgetauscht, dies hatte in nicht -ch Regionen (z.&nbsp;B. en-uk) Fehlerhafte Auswirkungen: aus 99,99 wurde 99.99, welches in der Region nicht in eine Zahl umzuwandeln ist. Da das Feature eher eine "Bequemlichkeit" war, wurde das Verhalten geändert - Zahlen müssen immer in der jeweiligen Regionsvariante angegeben werden. 
* <span class="label label-danger">Fixed</span> ListItems im "falschen" Format werden nun ignoriert. Der neue ListItem Stil, welcher im XSD vorgegeben ist, muss beachtet werden 
* <span class="label label-success">New</span> Das Dokumentparameter-Fenster im neuen Design ist nun von der Grösse her variabel (CanResize / Resizable). Die Angabe bei WindowHeight/WindowWith wird als Initialwert genommen. Der Empfänger-Dialog verhält sich im Grunde genauso. 
* <span class="label label-success">New</span> Neue Script-Funktion zum Formatieren von Zahlen hinzugefügt: fFormattingNumeric - damit kann man eine Dezimalzahl über die normalen .NET Formatierungsoptionen formatieren.
* <span class="label label-success">New</span> Performance-Optimierung bei Skripts: Skript-Durchläufe werden abgebrochen, sobald der Output 2-mal derselbe ist ("Depth" gibt neu nur noch die maximale Anzahl Durchläufe an) 
* <span class="label label-success">New</span> Startseite der Datasource-Wahl modernisiert und mit einem Healtcheck ausgestattet 
* <span class="label label-success">New</span> Datasource Management hinzugefügt für grosse Templating Umgebungen 
* <span class="label label-danger">Fixed</span> Wording Änderung beim Rampup bezüglich primaryDatasource 
* <span class="label label-danger">Fixed</span> Falls bei einem Snippet-Script alle Bedingungen nicht erfüllt sind, wird der Inhalt des Bookmarks geleert. Bislang war es so, dass in dem Fall der Text aus dem Entwurfsmodus stehen blieb. 
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
* <span class="label label-danger">Fixed</span> Custom Xml-Parts werden richtig zusammengeführt: Betrifft sowohl Unterdokumente als auch die direkte Vererbung. Dadurch funktionieren ExtendedBinding, Bilder und Snippets, welche in der Untervorlage oder einer Abhängigkeit (z.&nbsp;B. der Formatvorlage der Untervorlage) definiert sind, richtig. 
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

## Office AddIn
* <span class="label label-danger">Fixed</span> Excel: Das Logging wurde am Startup noch erweitert um die Absturzursachen einzugrenzen. Zudem wurde ein Unterschied zwischen den Excel Addin und den anderen Addins gefunden, welcher evtl. zum Absturz führen konnte  
* <span class="label label-success">New</span> Felddefinitionen grafisch überarbeitet 
* <span class="label label-danger">Fixed</span> Möglicher fix für Fehlermeldung falls "LoadBasicData" zu langsam ist und man das Dokument schliesst 
* <span class="label label-danger">Fixed</span> Ein Fehler bricht nun nicht mehr den gesamten Sync ab und die HttpSyncSource nutzt nun auch den SyncReport 

## Setup
* <span class="label label-danger">Fixed</span> Trotz Leerzeichen im Installationspfad sollte nun der Kopiervorgang erfolgreich abgeschlossen werden 
* <span class="label label-danger">Fixed</span> Basic Auth wird nun automatisch mit installiert 
* <span class="label label-danger">Fixed</span> Es werden jetzt nur noch die Haupt-Assemblies für NGEN vorgesehen (d. h. AddIn.dlls und OneOffixx.exe) - dieser werden als Prio 1 NGen übergeben. 

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
* <span class="label label-success">New</span> Dynamicy CRM Address Provider: Support für Fetch XML: Erweiterte Queries wie z.&nbsp;B. ein Join von Entities sind nun unterstützt User Story
* <span class="label label-danger">Fixed</span> Fix AdressDailog: Eingabe werden nicht angenommen in "einfacher Ansicht" 
* <span class="label label-danger">Fixed</span> Fix für Empfängerbox - Adresse aus Zwischenablage 
* <span class="label label-danger">Fixed</span> Fix für Adressfeld-Vorschau im Adressprovider wird nicht aktualisiert (Software-Fehler) 

## Server
* <span class="label label-danger">Fixed</span> Der Smuggler hatte OneOffixxGroups ignoriert, welches dann zu einem Fehler beim Import/Export geführt hat - "beschädigte" Exports müssen neu erzeugt werden, da die Info direkt im Export ebenfalls fehlt!  

##Client:
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
* <span class="label label-danger">Fixed</span> Template-Versions Selektion hat bei Interaktionen vom Ribbon (z.&nbsp;B. Dokument Parameter) nicht zuverlässig die richtige Config ausgewählt 
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


# OneOffixx V 3.1.10060

Die Version 3.1 wurde offiziell freigegeben und beinhaltet folgende Hauptfeatures:

* Unterstützung der Vorlagenversionierung für Layouter.
* Neues Fensterkonzept im Layouter-Admin Modus
* Neben AD-Gruppen und AD-Usern werden neu auch OneOffixx-Gruppen und OneOffixx-User unterstützt.
* Alle Serverkonfigurationen in den Dateien OneOffixx.config wurden zu einer zentralen Datei zusammengefasst.