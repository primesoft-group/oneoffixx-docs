---
layout: page
title: OneOffixx Basis Installation
permalink: "install/de/server-install/"
language: de
---

Im mitgelieferten OneOffixx Installationspaket ist ein Powershell Script __"Install.ps1"__ enthalten, welches die Basis-Installation übernimmt.

Das Script muss __als Administrator__ ausgeführt werden, da fehlende Windows Features aktiviert werden, und das Ausführen von Powershell Scripts muss aktiviert sein. 

__ExecutionPolicy:__

Um das Script zu starten muss die ExecutionPolicy auf "Unrestricted" stehen:

     Set-ExecutionPolicy Unrestricted

```ps
PS C:\Users\administrator> Set-ExecutionPolicy Unrestricted

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
http://go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): y
```

__Variante 1: Starten über eine neue Powershell Session"__

Eine neue Powershell Session erzeugen und im Installationspaket die "Install.ps1" aufrufen.

__Variante 2: Run with Powershell__

Über den Windows Explorer kann das "Install.ps1" gestartet werden, hierbei muss allerdings die ExecutionPolicy dies ebenfalls zulassen:

![x]({{ site.baseurl }}/assets/content-images/install/en/server-install-explorer.png "Starten via Windows Explorer")

## Script Ablauf

__1. Benötigte Windows Feature überprüfen__

Im ersten Schritt wird überprüft ob alle erforderlichen Windows Features installiert sind. Darunter zählt unter anderem der Internet Information Service mit ASP.NET sowie WCF Dienste.

__2. "OneOffixx"-Website im IIS__

Im nächsten Schritt wird überprüft ob bereits eine "OneOffixx"- Website im IIS registriert ist. Ist dies bereits der Fall wird zum nächsten Schritt gegangen.

Falls die Website nicht gefunden wird, werden Sie gefragt ob diese angelegt werden soll mit der Angabe des Installationspfades und des Port. Die Standardeinstellungen werden Ihnen im Installation-Script angezeigt.

__3. "OneOffixx"-Apps__

In diesem Schritt werden die eigentlichen Webanwendungen in der "OneOffixx"-Website hinterlegt.

Falls die Anwendungen bereits installiert sind wird der Installateur gefragt, ob die eine Aktualisierung stattfinden soll. Dabei können die "web.config" bzw. OneOffixx-Konfigurationsdateien der bestehenden Anwendungen
beibehalten werden oder nicht. 

Im Fall einer einfachen Aktualisierung empfiehlt es sich die Konfigurationsdateien beizubehalten.

__4. "OneOffixx JobHost"-Scheduled Task__ {% include new-badge.html version="3.3" %} 

Im letzten Schritt erfolgt eine Abfrage ob der "OneOffixx-JobHost" als Scheduled Task eingerichtet werden soll.

Der OneOffixx-JobHost ist ein Konsolenprogramm, welches z.B. Benutzerdaten im Hintergrund in einem bestimmten Interval aktualisiert und sollte daher mit installiert werden.

__Abschluss der Basis-Installation__

Nach der ersten Installation sollten nun sowohl der IIS als auch die Webanwendungen und der Scheduled Task installiert sein.

{% include alert.html type="info" text="In der Standard-Installation wird eine Webseite erzeugt, welche auf den Port 80 lauscht. Dies könnte mit evtl. anderen Webseiten zu Konflikten führen. <br/><b>In dem Fall wird die OneOffixx Website nicht gestartet.</b>" %}

