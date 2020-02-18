---
layout: page
title: Server Installation
permalink: "install/de/server/"
language: de
---

Sie finden hier die Systemvoraussetzungen und eine Schritt-für-Schritt Anleitung für die Installation der OneOffixx-Server-Komponenten.

## <i class="fa fa-wrench" aria-hidden="true"></i> Systemvoraussetzung {% include anchor.html name="system-requirements" %}

__Betriebssystem und Komponenten__

Sie können die OneOffixx Server Anwendungen auf folgenden Betriebssystemen installieren:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

Für den Betrieb sind folgende Komponenten notwendig:

* Internet Information Server ab Version 7
* SQL Server ab Version 2012 (Express oder höher). Bei vielen Benutzern empfiehlt es sich, nicht *Express* zu verwenden.
* [Microsoft .NET Framework 4.7.2 oder höher](http://go.microsoft.com/fwlink/?linkid=863265)
* [Microsoft .NET Core 3.0 Runtime & Hosting Bundle](https://dotnet.microsoft.com/download/thank-you/dotnet-runtime-3.0.0-windows-hosting-bundle-installer)

*Im Lieferpaket ist ein Powershell-Skript enthalten, das die Installation auf dem Server vereinfachen soll.*

*Die Powershell "ExecutionPolicy" muss das Ausführen von Powershell-Skripts zulassen. Falls das Skript nicht geladen werden kann, wird der Befehl "Set-ExecutionPolicy Unrestricted" in der Powershell ausgeführt.*

__Arbeitsspeicher und CPU Cores__

Die OneOffixx Server Anwendungen werden innerhalb des Internet Information Servers (IIS) betrieben. Wir empfehlen, die Anforderungen von Microsoft zu berücksichtigen. Empfehlenswert sind jedoch mindestens 4 GB Arbeitsspeicher und 2 Kerne. Läuft auf dem Webserver noch weitere Software (z.&nbsp;B. der SQL Server) empfiehlt es sich, einen stärkeren CPU bzw. mehr Arbeitsspeicher zu benutzen.

__Festplattenspeicher__

Die Software selbst benötigt etwa 500 MB Festplattenspeicher. Alle OneOffixx Server Anwendungen loggen in der Standardkonfiguration in das jeweilige Applikationsverzeichnis. Die Logfiles werden pro Tag erstellt und je nach Last können einige auch hundert MB gross sein. Es werden maximal die letzten 7 Tage gespeichert, wobei dies über eine Konfigurationsdatei angepasst werden kann.

__Active Directory__

Der Server, auf dem OneOffixx gehostet wird, muss Mitglied des Active Directory sein. Die Berechtigung der Organisationseinheiten im OneOffixx erfolgt über das Active Directory.  Stellen Sie sicher, dass ihr Unternehmensnetzwerk im Active Directory eingebunden ist.

__DNS__

Die OneOffixx Clients kommunizieren per HTTP/HTTPS mit dem OneOffixx Server. Empfehlenswert ist, wenn der OneOffixx Server einen eigenen CNAME im lokalen DNS-Server erhält. Dieser wird in der Konfiguration der Clients und dem Server mehrfach verwendet.

Im Folgenden wird als Beispiel folgender DNS CNAME verwendet:

    oneoffixx.firmamuster.ch

__Einsatz von Virenscanner auf dem Windows Server__

Falls auf dem System, auf dem die OneOffixx Server Anwendungen ausgeführt werden, ein Virenscanner im Einsatz ist, sollte dieser so konfiguriert werden, dass die Funktionalität von OneOffixx nicht eingeschränkt ist.

Folgende Empfehlungen:

* Der Virenscanner sollte das OneOffixx Installationsverzeichnis (Standard "C:\inetpub\wwwroot\OneOffixx\") auf dem Server nicht analysieren. Da in der Standardeinstellung Logfiles generiert werden, wird in den Verzeichnissen häufig geschrieben.
* Ebenfalls sollte das Verzeichnis der IIS Logs nicht analysiert werden ("C:\inetpub\logs").
* Falls der Virenscanner HTTP\HTTPS Verbindungen analysiert, sollte die Adresse des OneOffixx Service als Ausnahme hinzugefügt werden.

Falls OneOffixx ohne diese Änderungen mit einem Virenscanner auf dem Server betrieben wird, kann es zu Performance-Problemen kommen.

__Troubleshooting__

Wegen atypischer Server- oder IIS-Konfigurationen kann es gelegentlich zu Schwierigkeiten kommen. Hier finden Sie Lösungen zu den gängigsten Fragen: [Troubleshooting]({{ site.baseurl }}/install/de/server-troubleshooting)


## <i class="fa fa-cogs" aria-hidden="true"></i> Installationsszenarien {% include anchor.html name="install" %}

__OneOffixx Server und Datenbank auf einem neuen Server installieren__

![x]({{ site.baseurl }}/assets/content-images/install/en/server-install-overview-single.png "Neuer Windows Server für IIS & SQL Server")

{:.table .table-striped}
|     | Installations- und Konfigurationsschritt | 
|:---:| --- |
| 1.  | Microsoft Windows Server bereitstellen |
| 2.  | [SQL Server installieren]({{ site.baseurl }}/install/de/server-sql-install) |
| 3.  | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/install/de/server-sql-user) |
| 4.  | [Basis-Installation über Powershell ausführen und Anleitung befolgen]({{ site.baseurl }}/install/de/server-install) |
| 5.  | [Konfigurations-Wizard auf Administrations-Seite befolgen]({{ site.baseurl }}/install/de/server-config) |
| 6.  | [Funktionstest]({{ site.baseurl }}/install/de/server-test) |

__OneOffixx Server auf einem neuen Server installieren - Die Datenbank soll auf einen bestehenden Server installiert werden__

![x]({{ site.baseurl }}/assets/content-images/install/en/server-install-overview-externalsql.png "Neuer Windows Server für IIS & bestehender SQL Server")

{:.table .table-striped}
|     | Installations- und Konfigurationsschritt | 
|:---:| --- |
| 1.  | Microsoft Windows Server bereitstellen | 
| 2.  | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/install/de/server-sql-user) |
| 3.  | [Basis-Installation über Powershell ausführen und Anleitung befolgen]({{ site.baseurl }}/install/de/server-install) |
| 4.  | [Konfigurations-Wizard auf Administrations-Seite befolgen]({{ site.baseurl }}/install/de/server-config) |
| 5.  | [Funktionstest]({{ site.baseurl }}/install/de/server-test) |

__IIS und SQL Server existieren schon - OneOffixx Server und Datenbank installieren__

![x]({{ site.baseurl }}/assets/content-images/install/en/server-install-overview-existinginfra.png "Bestehender Windows Server für IIS & bestehender SQL Server")

{:.table .table-striped}
|     | Installations- und Konfigurationsschritt | 
|:---:| --- |
| 1.  | [SQL Server OneOffixx User anlegen]({{ site.baseurl }}/install/de/server-sql-user) |
| 2.  | [Basis-Installation über Powershell ausführen und Anleitung befolgen]({{ site.baseurl }}/install/de/server-install) |
| 3.  | [Konfigurations-Wizard auf Administrations-Seite befolgen]({{ site.baseurl }}/install/de/server-config) |
| 4.  | [Funktionstest]({{ site.baseurl }}/install/de/server-test) |

## <i class="fa fa-refresh" aria-hidden="true"></i> Aktualisierung der Server Anwendungen {% include anchor.html name="update" %}

{% include alert.html type="info" text="<b>Hinweis ab Version 3.0</b><br/>Mit Version 3.0 wurde eine einheitliche Konfiguration für alle Server-Applikationen eingeführt." %}

Eine Anleitung zur Migration von Version 2.0 auf 3.0 finden Sie __[hier]({{ site.baseurl }}/install/de/server-update/)__. Bei einem Update können Sie das Powershell-Installationsskript wieder aufrufen. Es empfiehlt sich, vorher ein Backup zu machen. Bei der Installation sollte nun darauf geachtet werden, dass die bestehende "OneOffixx.config" beibehalten wird. Das Skript sollte das für Sie übernehmen.

Hinweis für Version 2.0: Die Admin Applikation (Dashboard) verfügt über eine eigene Konfigurationsdatei "OneOffixxAdmin.config".  Ausnahme: Im Fall von Änderungen, die auch die Struktur der "web.config" betreffen, werden wir Ihnen eine separate Anleitung liefern.

Falls ein Update Änderungen an der Datenbank erforderlich macht, wird Ihnen das im Dashboard angezeigt und Sie können die Datenbank-Änderung direkt über das Dashboard ausführen.

{% include alert.html type="warning" text="Bei Fragen oder Problemen helfen wir Ihnen natürlich gern weiter - melden Sie sich einfach bei unserem Support." %}
