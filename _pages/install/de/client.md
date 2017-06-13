---
layout: page
title: Client Installation
permalink: "install/de/client/"
language: de
---

Sie finden hier die Systemvoraussetzungen und eine Anleitung für die Installation der OneOffixx Client Komponenten.

## <i class="fa fa-wrench" aria-hidden="true"></i> Systemvoraussetzung {% include anchor.html name="system-requirements" %}

__Betriebssystem__

Sie können den OneOffixx Client auf folgenden Betriebssystemen installieren:

* Windows Vista SP2 oder höher (sowohl 32bit oder 64bit) 
* Windows Server 2008 oder höher (sowohl 32bit oder 64bit)
* [Citrix XenApp/TS oder Windows Terminal Server (Versionskompatibel ab Vista SP2 32bit und 64bit)]({{ site.baseurl }}/install/de/client-citrix-ts)

__Unterstützte Microsoft Office Versionen__

OneOffixx unterstützt alle Microsoft Office Versionen __ab Office 2007__, sowohl in der 32bit als auch 64bit Variante. __[OneOffixx unterstützt die früheren Versionen von Microsoft Windows und von Microsoft Office für Windows bis zu deren Lebensende, d.h. bis zum Ende der „Erweiterten Supportdauer" von Microsoft zu den jeweiligen Produkten.](http://oneoffixx.com/lifecycle/)__

__.NET Framework__

Für den OneOffixx Client in der Version 3 wird mindestens das __[.NET Framework 4.5.2](https://www.microsoft.com/en-US/download/details.aspx?id=42642)__ vorausgesetzt. {% include new-badge.html version="3" %}

Für ältere OneOffixx Clients (Version 2) muss mindestens das __[.NET Framework 4.0 (Client Profile)](https://www.microsoft.com/en-US/download/details.aspx?id=17113)__ installiert sein.

__Festplattenspeicher__

Die Software selbst benötigt etwa 200 MB Festplattenspeicher. 

Der OneOffixx Client speichert zudem (für Fehlerbehandlung) Log-Dateien und Einstellungen und legt zusätzlich einen lokalen Cache für die Offline-Nutzung an.
Die Grösse des Caches ist abhängig von der Anzahl und Grösse der Vorlagen. 

__Active Directory__

Für den Betrieb ist es erforderlich, dass der OneOffixx Client und Server sich in der gleichen bzw. über Vertrauensstellung authorisierten Domäne befinden.

## <i class="fa fa-power-off" aria-hidden="true"></i> 32bit oder 64bit Installation {% include anchor.html name="bitness" %}

Den OneOffixx Installer gibt es in einer 32- oder 64bit Variante. Die benötigte Version ist __abhängig von der verwendeten Microsoft Office Version__.

Wird ein 64bit Microsoft Office verwendet, __muss__ die 64bit OneOffixx Version installiert werden. 

## <i class="fa fa-plug" aria-hidden="true"></i> Ports & Server-Verbindung {% include anchor.html name="ports" %}

Der OneOffixx Client kommuniziert __ausschliesslich über HTTP/HTTPS__ mit dem OneOffixx Server, damit wird in der Standard-Konfiguration nur Port 80 bzw. 443 benötigt.

## <i class="fa fa-windows" aria-hidden="true"></i> MSI Parameter {% include anchor.html name="msi" %}

Das OneOffixx MSI-Paket enthält den OneOffixx Client und die diversen Microsoft Office Addins. 

__OneOffixx-Spezifische Parameter:__

* APPLICATIONFOLDER = install folder (default C:\Program Files (x86)\OneOffixx)
* INSTALLDESKTOPSHORTCUT = 1 / 0 for yes or no
* AUTOSTART = 1 / 0 for yes or no
* SERVICEENDPOINTURL = Service Endpoint (*can be overwritten via registry)
* ADDLOCAL = Features
     * WordAddInFeature = Word Add-In
     * OutlookAddInFeature = Outlook Add-In
     * ExcelAddInFeature = Excel Add-In
     * PowerPointAddInFeature = PowerPoint Add-In
     * OfferOfEvidenceAddInFeature = OneOffixx Law Add-In
     * RegulationsAddInFeature = OneOffixx Booklet Add-In

Diese Parameter hier werden nur in bestimmten Installationsvarianten (z.B. Installation auf Terminal-Servern) benötigt und sind optional: 

* DATAINLOCALAPPDATAFOLDER = False/True (must be True on Network Share)
* CACHEFOLDER = Path e.g. //Share/... (with Placeholders like %username% from environment-variables etc.)
* SETTINGFOLDER = Path e.g. //Share/... (with Placeholders like %username% from environment-variables etc.)
* SHUTDOWNONDISCONNECT = true / false (Allows to configure OneOffixx to shutdown when a disconnect happens (such as disconnecting from an RDP Session) )
* LOGFOLDER = Path for storing logfiles e.g. //Share/... (with Placeholders supported by [NLog](https://github.com/NLog/NLog/wiki/Layout-Renderers))

Es gelten ansonsten die normalen __[MSIEXEC Command-Line Options](https://msdn.microsoft.com/en-us/library/windows/desktop/aa367988%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)__.

Beispiel: 

    msiexec /qb /i "OneOffixx.Install(x86).msi" APPLICATIONFOLDER="C:\Program Files (x86)\OneOffixx" SERVICEENDPOINTURL="http://appurl/OneOffixxService.svc" INSTALLDESKTOPSHORTCUT=1 AUTOSTART=1 /l*v OneOffixxInstall.log AddLocal=WordAddInFeature,OutlookAddInFeature

__ServiceEndpointUrl via Registry:__

OneOffixx sucht in der Registry nach einem String-Value "ServiceAddress" unter diesem Schlüsseln (HKCU & HKLM):

    [HKEY_CURRENT_USER\Software\Sevitec Informatik AG\OneOffixx]
    "ServiceAddress"="http..."

bzw. 

    [HKEY_LOCAL_MACHINE\Software\Sevitec Informatik AG\OneOffixx]
    "ServiceAddress"="http..."

bzw. (für __Group-Policies__ geeignet)

    [HKEY_CURRENT_USER\Software\Policies\Sevitec Informatik AG\OneOffixx]
    "ServiceAddress"="http..."
  
Findet der Client diesen Wert, wird dieser anstelle der ServiceAddress aus der OneOffixx.exe.config genommen. 

Um diese Einstellungen via Gruppenrichtlinien steuern zu können, stehen __[ OneOffixx ADMX Vorlagen]({{ site.baseurl }}/assets/content-files/OneOffixxGroupPoliciesTemplate.zip)__ zur Verfügung.

## <i class="fa fa-cogs" aria-hidden="true"></i> Installationsszenarien {% include anchor.html name="install" %}

Die Standardeinstellungen des OneOffixx Installers zielen auf eine "normale" Installation auf einem System ab, welches von einem oder mehreren Windows-Nutzern gestartet werden kann. 
Hierbei werden sowohl der Cache als auch die Einstellungen unter *%AppData%* gespeichert.

Jede OneOffixx Client Instanz muss für die vollständige Funktionalität exklusiven Zugriff auf den Cache bekommen - ist dies nicht der Fall (z.B. für einige Citrix/Terminal-Server Konfiguration) muss der Speicherort des Caches angegeben werden. 

### <i class="fa fa-cog" aria-hidden="true"></i> OneOffixx Client: Standard Installation

Es werden keine weiteren Parameter benötigt, hierbei werden Cache & Einstellungen unter *%AppData%* gespeichert.

__Empfohlen für:__

☑ Keine serverseitig gespeicherten Roaming Profile

### <i class="fa fa-cog" aria-hidden="true"></i> OneOffixx Client: Cache & Einstellungen lokal

Sowohl der Cache als auch die Einstellungen können unter *%AppDataLocal%* gespeichert werden, wenn dieser Parameter gesetzt wird:

    DATAINLOCALAPPDATAFOLDER = True

__Empfohlen für:__

☑ Serverseitig gespeicherten Roaming Profile

☑ *%AppDataLocal%* Ordner wird nicht gelöscht

☑ Benutzer ist immer auf derselben Maschine eingeloggt

### <i class="fa fa-cog" aria-hidden="true"></i> OneOffixx Client: Cache in spezifischen Ordner

Sollte sowohl *%AppData%* als auch *%AppDataLocal%* nicht in Frage kommen oder es passieren kann, dass mehrere OneOffixx Instanzen pro Nutzer offen sein könnten, kann über diese Einstellung der Cache Speicherort spezifiziert werden:

    CACHEFOLDER = Path e.g. //Share/... (with Placeholders like %username% etc.)

__Empfohlen für:__

☑ Terminal-Server Installation mit mehrere offenen Sessions pro Benutzer

__Voraussetzung:__

☑ Angegebenes Netzwerk-Laufwerk ist vorhanden und immer erreichbar

### <i class="fa fa-cog" aria-hidden="true"></i> OneOffixx Client: Einstellungen in spezifischen Ordner

Die Einstellungen können ebenfalls wie der Cache in einen eigenen Ordner gespeichert werden. 

    SETTINGFOLDER = Path e.g. //Share/... (with Placeholders like %username% etc.)

## <i class="fa fa-life-ring" aria-hidden="true"></i> Troubleshooting {% include anchor.html name="troubleshooting" %}

__OneOffixx Addins in Microsoft Office starten nicht {% include anchor.html name="troubleshooting-vcredist" %}__

Falls sich die OneOffixx Addins nicht starten lassen, d.h. es ist kein OneOffixx Icon im Office Ribbon zu sehen, kann es verschiedene Ursachen haben:

* Das OneOffixx Addin ist nicht installiert: 
    * Sollte das OneOffixx Addin unter "Datei - Optionen - Addins" unter den COM Addins nicht auftauchen, ist es evtl. nicht installiert. Prüfen Sie ob das entsprechende Addin bei der Installation ausgewählt wurde.
* Office ist in der 64bit Variante installiert, aber es wurde der 32bit OneOffixx Installer benutzt.
    * Sollte eine 64bit Office Installation benutzt sein, muss auch der 64bit Installer von OneOffixx genutzt werden.
* Für OneOffixx Version 2: Visual C++ Redistributable 2015 Package fehlt oder ist nicht richtig installiert 
    * Ab OneOffixx Version 2.3.40140 ist das VC++ Redistributable 2015 Package im OneOffixx enthalten, allerdings kann es passieren dass eine "korrupte" System Installation des Package die Ausführung unseres Addins unterbindet. In dem Fall sollte nochmals die Installation des [VC++ Redistributable 2015 Package](https://www.microsoft.com/de-ch/download/details.aspx?id=48145) vorgenommen werden.

__Das Starten von Microsoft Office ist seit der OneOffixx Addin Installation stark verzögert {% include anchor.html name="troubleshooting-ngen" %}__

Falls Office langsam starten sollte, kann es daran liegen, dass der "Native Image Generator (ngen)" Prozess noch nicht vollständig durchgelaufen ist. Dieser Prozess wird nach der Installation automatisch angesteuert und ist ein Bestandteil des .NET Frameworks.

Ausführung "Native Image Generator" (ngen):

Der Prozess ngen.exe befindet sich unter diesem Pfad: c:\windows\microsoft.net\framework\v4.0.30319\ngen.exe

Über "display" kann der Status geprüft werden, dies sollte so aussehen:

    C:\Windows\Microsoft.NET\Framework\v4.0.30319\ngen.exe display "C:\Program Files (x86)\OneOffixx\OneOffixx.exe"
    Microsoft (R) CLR Native Image Generator - Version 4.6.1087.0
    Copyright (c) Microsoft Corporation.  All rights reserved.

    NGEN Roots:

    C:\Program Files (x86)\OneOffixx\OneOffixx.exe

    NGEN Roots that depend on "c:\Program Files (x86)\OneOffixx\OneOffixx.exe

    C:\Program Files (x86)\OneOffixx\OneOffixx.exe

    Native Images:

    OneOffixx, Version=2.3.40190.0, Culture=neutral, PublicKeyToken=null

Sollte OneOffixx als "pending" aufgeführt werden, sollte der Kompilierungsvorgang über "update" nochmals gestartet werden:

    c:\Windows\Microsoft.NET\Framework\v4.0.30319\ngen.exe update

Dies sollte das Laden des Addins wesentlich beschleunigen. 

{% include alert.html type="warning" text="Bei Fragen oder Problemen helfen wir Ihnen natürlich gern weiter - melden Sie sich einfach bei unserem Support." %}
