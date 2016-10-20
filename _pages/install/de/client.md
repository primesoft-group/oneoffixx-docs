---
layout: page
title: Client Installation
permalink: "install/de/client/"
---

Sie finden hier die Systemvoraussetzungen und eine Schritt-für-Schritt Anleitung für die Installation der OneOffixx Client Komponenten.

## <i class="fa fa-wrench" aria-hidden="true"></i> Systemvoraussetzung {% include anchor.html name="system-requirements" %}

__Betriebssystem__

Sie können den OneOffixx Client auf folgenden Betriebssystemen installieren:

* Windows Vista SP2 oder höher (sowohl 32bit oder 64bit) 
* Windows Server 2008 oder höher (sowohl 32bit oder 64bit)

__Unterstützte Microsoft Office Versionen__

OneOffixx unterstützt alle Microsoft Office Versionen ab __Office 2007__, sowohl in der 32bit als auch 64bit Variante.

__.NET Framework__

Für den OneOffixx Client wird mindestens das .NET Framework 4.0 (Client Profile) vorausgesetzt.

__Visual C++ Redistributable für Visual Studio 2015__

Für die OneOffixx Addins wird das [Visual C++ Redistributable 2015 Package](https://www.microsoft.com/de-ch/download/details.aspx?id=48145) vorrausgesetzt.

__Festplattenspeicher__

Die Software selbst benötigt etwa 200 MB Festplattenspeicher. 

Der OneOffixx Client speichert zudem (für Fehlerbehandlung) Log-Dateien und Einstellungen und legt zusätzlich einen lokalen Cache für die Offline-Nutzung an.
Die Grösse des Caches ist abhängig von der Anzahl und Grösse der Vorlagen.


__Hinweis: 32bit oder 64bit Installation__

Den OneOffixx Installer gibt es in einer 32- oder 64bit Variante. Die benötigte Version ist __abhängig von der verwendeten Microsoft Office Version__.

Wird ein 64bit Microsoft Office verwendet, __muss__ die 64bit OneOffixx Version installiert werden. 




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

## <i class="fa fa-cogs" aria-hidden="true"></i> Installationsszenarien {% include anchor.html name="install" %}

__OneOffixx Server & Datenbank auf einem neuen Server installieren__

![x]({{ site.baseurl }}/assets/content-images/install/de/server-install-overview-single.png "Neuer Windows Server für IIS & SQL Server")

{:.table .table-striped}
|     | Installations- und Konfigurationsschritt  
|:---:| ---
| 1.  | Microsoft Windows Server bereitstellen 
| 2.  | [SQL Server installieren]({{ site.baseurl }}/install/de/server-sql-install) 
| 3.  | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/install/de/server-sql-user) 
| 4.  | [Basis-Installation über Powershell ausführen und Anleitung befolgen]({{ site.baseurl }}/install/de/server-install) 
| 5.  | [Konfigurations-Wizard auf Administrations-Seite befolgen]({{ site.baseurl }}/install/de/server-config) 
| 6.  | [Funktionstest]({{ site.baseurl }}/install/de/server-test) 

__OneOffixx Server auf einem neuen Server installieren. Die Datenbank soll auf einen bestehenden Server installiert werden__

![x]({{ site.baseurl }}/assets/content-images/install/de/server-install-overview-externalsql.png "Neuer Windows Server für IIS & bestehender SQL Server")

{:.table .table-striped}
|     | Installations- und Konfigurationsschritt  
|:---:| ---
| 1.  | Microsoft Windows Server bereitstellen 
| 2.  | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/install/de/server-sql-user) 
| 3.  | [Basis-Installation über Powershell ausführen und Anleitung befolgen]({{ site.baseurl }}/install/de/server-install) 
| 4.  | [Konfigurations-Wizard auf Administrations-Seite befolgen]({{ site.baseurl }}/install/de/server-config) 
| 5.  | [Funktionstest]({{ site.baseurl }}/install/de/server-test) 

__IIS und SQL Server existieren schon. OneOffixx Server und Datenbank installieren.__

![x]({{ site.baseurl }}/assets/content-images/install/de/server-install-overview-existinginfra.png "Bestehender Windows Server für IIS & bestehender SQL Server")

{:.table .table-striped}
|     | Installations- und Konfigurationsschritt  
|:---:| ---
| 1.  | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/install/de/server-sql-user) 
| 2.  | [Basis-Installation über Powershell ausführen und Anleitung befolgen]({{ site.baseurl }}/install/de/server-install) 
| 3.  | [Konfigurations-Wizard auf Administrations-Seite befolgen]({{ site.baseurl }}/install/de/server-config) 
| 4.  | [Funktionstest]({{ site.baseurl }}/install/de/server-test) 

## <i class="fa fa-refresh" aria-hidden="true"></i> Aktualisierung der Server Anwendungen {% include anchor.html name="update" %}

Bei einem Update können Sie das Powershell Installationsscript wieder aufrufen. Es empfiehlt sich vorher ein Backup anzufertigen. Bei der Installation sollte nun darauf
geachtet werden, dass die bestehenden "web.config"/"OneOffixx.config"/"OneOffixxAdmin.config" beibehalten wird. Das Script sollte dies für Sie übernehmen.

Ausnahme: Im Falle von Änderungen die auch die Struktur der "web.config" betreffen werden wir Ihnen eine separate Anleitung liefern.

Falls ein Update Änderungen an der Datenbank erforderlich macht, wird Ihnen dies im OneOffixx Admin angezeigt und Sie können die Datenbank Änderung direkt über die Admin Webanwendung ausführen.

{% include alert.html type="warning" text="Bei Fragen oder Problemen helfen wir Ihnen natürlich gern weiter - melden Sie sich einfach bei unserem Support." %}
