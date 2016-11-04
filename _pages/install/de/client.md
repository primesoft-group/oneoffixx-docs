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

Für den OneOffixx Client wird mindestens das [.NET Framework 4.0 (Client Profile)](https://www.microsoft.com/en-US/download/details.aspx?id=17113) vorausgesetzt.

__Visual C++ Redistributable für Visual Studio 2015__

Für die OneOffixx Addins wird das [Visual C++ Redistributable 2015 Package](https://www.microsoft.com/de-ch/download/details.aspx?id=48145) vorrausgesetzt.

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

Der OneOffixx Client kommuniziert __ausschliesslich über HTTP/HTTPS__ mit dem OneOffixx Server, es werden keine weiteren Ports benutzt.

{% include alert.html type="warning" text="Bei Fragen oder Problemen helfen wir Ihnen natürlich gern weiter - melden Sie sich einfach bei unserem Support." %}
