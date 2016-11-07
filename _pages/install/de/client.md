---
layout: page
title: Client Installation
permalink: "install/de/client/"
---

Sie finden hier die Systemvoraussetzungen und eine Anleitung für die Installation der OneOffixx Client Komponenten.

## <i class="fa fa-wrench" aria-hidden="true"></i> Systemvoraussetzung {% include anchor.html name="system-requirements" %}

__Betriebssystem__

Sie können den OneOffixx Client auf folgenden Betriebssystemen installieren:

* Windows Vista SP2 oder höher (sowohl 32bit oder 64bit) 
* Windows Server 2008 oder höher (sowohl 32bit oder 64bit)

__Unterstützte Microsoft Office Versionen__

OneOffixx unterstützt alle Microsoft Office Versionen ab __Office 2007__, sowohl in der 32bit als auch 64bit Variante.

__.NET Framework__

Für den OneOffixx Client wird mindestens das __[.NET Framework 4.0 (Client Profile)](https://www.microsoft.com/en-US/download/details.aspx?id=17113)__ vorausgesetzt.

__Visual C++ Redistributable für Visual Studio 2015__

Für die OneOffixx Addins wird das __[Visual C++ Redistributable 2015 Package](https://www.microsoft.com/de-ch/download/details.aspx?id=48145)__ vorrausgesetzt.

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
* SERVICEENDPOINTURL = Service Endpoint
* ADDLOCAL = Features
    * WordAddInFeature = Word Add-In
    * OutlookAddInFeature = Outlook Add-In
    * ExcelAddInFeature = Excel Add-In
    * PowerPointAddInFeature = PowerPoint Add-In
    * OfferOfEvidenceAddInFeature = OneOffixx Law Add-In
    * RegulationsAddInFeature = OneOffixx Booklet Add-In

Diese Parameter hier werden nur in bestimmten Installationsvarianten (z.B. Installation auf Terminal-Servern) benötigt und sind optional: 

* DATAINLOCALAPPDATAFOLDER = False/True (must be True on Network Share)
* CACHEFOLDER = Path e.g. //Share/... (with Placeholders like %username% etc.)
* SETTINGFOLDER = Path e.g. //Share/... (with Placeholders like %username% etc.)

Es gelten ansonsten die normalen __[MSIEXEC Command-Line Options]__(https://msdn.microsoft.com/en-us/library/windows/desktop/aa367988%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396).

Beispiel: 

    msiexec /qb /i "OneOffixx.Install(x86).msi" APPLICATIONFOLDER="C:\Program Files (x86)\OneOffixx" SERVICEENDPOINTURL="http://appurl/OneOffixxService.svc" INSTALLDESKTOPSHORTCUT=1 AUTOSTART=1 /l*v OneOffixxInstall.log AddLocal=WordAddInFeature,OutlookAddInFeature


	
{% include alert.html type="warning" text="Bei Fragen oder Problemen helfen wir Ihnen natürlich gern weiter - melden Sie sich einfach bei unserem Support." %}
