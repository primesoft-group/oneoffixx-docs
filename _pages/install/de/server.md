---
layout: page
title: Server Installation
permalink: "install/de/server/"
---

Das Dokument beschreibt die Systemvorraussetzungen und Schritte für die Installation der OneOffixx Server Komponenten. 

## Systemvoraussetzung {% include anchor.html name="system-requirements" %}

__Betriebssystem & Komponenten__

Sie können OneOffixx Server auf folgenden Betriebssystemen installieren:

* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

Für den Betrieb der OneOffixx Server Anwendungen sind folgende Komponenten notwendig:

* Internet Information Server ab Version 7
* SQL Server ab Version 2008 (Express oder höher)
* Microsoft .NET Framework 4.5 oder höher

*Im Lieferpaket ist ein Powershell Script enthalten, welches die Installation auf dem Server vereinfachen soll. Damit das Script funktioniert muss auf dem Server die Windows Powershell 2.0 installiert sein (ab Windows Server 2008 R2 automatisch vorhanden).*

*Die Powershell "ExecutionPolicy" muss das Ausführen von Powershell Scripts zulassen. Falls das Script nicht geladen werden kann, führen Sie den Befehl "Set-ExecutionPolicy RemoteSigned" in der Powershell aus.*

__Arbeitsspeicher & CPU Cores__

OneOffixx Server wird innerhalb des Internet Information Servers betrieben. Wir empfehlen die Anforderungen von Microsoft zu berücksichtigen. 

Empfehlenswert sind jedoch mindestens 4 GB Arbeitsspeicher und 2 Cores. Läuft auf dem Webserver noch weitere Software (z.B. der SQL Server) empfiehlt sich einen stärkeren CPU bzw. mehr Arbeitsspeicher zu benutzen.

__Festplattenspeicher__

Die Software selbst benötigt etwa 100 MB Festplattenspeicher. Alle OneOffixx Server Bestandteile loggen in der Standardkonfiguration in das jeweilige Applikationsverzeichnis.

Die Logfiles werden pro Tag erstellt und je nach Last können auch einige hundert MB gross sein. Es werden maximal die letzte 7 Tage gespeichert.

__Active Directory__

Der Server auf dem OneOffixx gehostet wird muss Mitglied des Active Directory sein. Die Berechtigung der Organisationseinheiten im OneOffixx erfolgt über das Active Directory. 

Stellen Sie sicher, dass ihr Unternehmensnetzwerk im Active Directory eingebunden ist.

__DNS__

Die OneOffixx Clients kommunizieren per HTTP/HTTPS mit dem OneOffixx Server. Empfehlenswert ist, wenn der OneOffixx Server einen eigenen CNAME im lokalen DNS Server erhält. Dieser wird in der Konfiguration der Clients und dem Server
mehrfach verwendet.

Im Folgenden wird als Beispiel folgender DNS CNAME verwendet:

oneoffixx.firmamuster.ch

__Einsatz von Virenscanners auf dem Windows Server__

Falls auf dem System auf dem die OneOffixx Server Anwendungen ausgeführt werden ein Virenscanner im Einsatz ist sollte dieser so konfiguriert werden, dass die Funktionalität von OneOffixx nicht eingeschränkt ist.

Folgende Empfehlungen:

* Der Virenscanner sollte das OneOffixx Installationsverzeichnis (Standard "C:\inetpub\wwwroot\OneOffixx\") auf dem Server nicht analysieren. Da in der Standardeinstellung Logfiles generiert werden, wird in den Verzeichnissen häufig geschrieben.
* Ebenfalls sollte das Verzeichnis der IIS Logs nicht analysiert werden ("C:\inetpub\logs").
* Falls der Virenscanner HTTP\HTTPS Verbindungen analysiert sollte die Adresse des OneOffixx Service als Ausnahme hinzugefügt werden.

Falls OneOffixx ohne diese Änderungen mit einem Virenscanner auf dem Server betrieben wird kann es zu Performanceproblemen kommen.

## Installationsszenarien {% include anchor.html name="options" %}

__OneOffixx Server und Datenbank auf einem neuen Server zu installieren__

{:.table .table-striped}
|     |     | Installations- und Konfigurationsschritt  
|:---:|:---:| ---
| 1.  | &#x2610; | Microsoft Windows Server bereitstellen 
| 2.  | &#x2610; | [SQL Server installieren]({{ site.baseurl }}/connect/de/server-sql-install) 
| 3.  | &#x2610; | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/connect/de/server-sql-user) 
| 4.  | &#x2610; | Basis-Installation über Powershell ausführen und Anleitung befolgen (siehe Kapitel 6) 
| 5.  | &#x2610; | Konfigurations-Wizard auf Administrations-Seite befolgen (siehe Kapitel 7)
| 6.  | &#x2610; | Funktionstest (siehe Kapitel 9)

__OneOffixx Server auf einem neuen Server zu installieren. Die Datenbank soll auf einen bestehenden Server installiert werden__

{:.table .table-striped}
|     |     | Installations- und Konfigurationsschritt  
|:---:|:---:| ---
| 1.  | &#x2610; | Microsoft Windows Server bereitstellen 
| 2.  | &#x2610; | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/connect/de/server-sql-user) 
| 3.  | &#x2610; | Basis-Installation über Powershell ausführen und Anleitung befolgen (siehe Kapitel 6)
| 4.  | &#x2610; | Konfigurations-Wizard auf Administrations-Seite befolgen (siehe Kapitel 7)
| 5.  | &#x2610; | Funktionstest (siehe Kapitel 9)

__IIS und SQL Server existieren schon. OneOffixx Server und DB installieren__

{:.table .table-striped}
|     |     | Installations- und Konfigurationsschritt  
|:---:|:---:| ---
| 1.  | &#x2610; | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/connect/de/server-sql-user) 
| 2.  | &#x2610; | Basis-Installation über Powershell ausführen und Anleitung befolgen (siehe Kapitel 6)
| 3.  | &#x2610; | Konfigurations-Wizard auf Administrations-Seite befolgen (siehe Kapitel 7)
| 4.  | &#x2610; | Funktionstest (siehe Kapitel 9)

