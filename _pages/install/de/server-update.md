---
layout: page
title: Server Update Hinweise
permalink: "install/de/server-update/"
language: de
---

## V2.X auf V3.x {% include anchor.html name="v2-v3" %}

Mit Version 3 wurde eine einheitliche Konfiguration für alle Server-Applikationen eingeführt. In Version 2 gab es pro Applikation eine eigene "OneOffixx.config"-Datei und der Admin hatte eine eigene "OneOffixxAdmin.config".

Die __Version 2 Struktur__ war typischerweise so vorzufinden:

    C:\inetpub\wwwroot\OneOffixx\
    ├── Admin\
    │   ├── OneOffixxAdmin.config
    │   └── ...
    ├── Service\
    │   ├── OneOffixx.config
    │   └── ...
    ├── Web\
    │   ├── OneOffixx.config
    │   └── ...
    └── Hub\
        └── ...

Die Änderung auf die zentrale Konfiguration ist die grösste Änderung in diesem Update.
		
### Anleitung - V3 Installation & kopieren der .config

Die Anleitung beschreibt den "einfachsten" Weg, allerdings sind die Web-Applikationen in der Zeit __nicht__ erreichbar, wobei der OneOffixx Client offline-fähig ist und ohnehin keine ständige Verbindung zum Server benötigt.

Hinweis: Die Website wird über das Script automatisch gestoppt und am Ende wieder gestartet.

__1__: Erstellen Sie ein Backup des bestehenden "OneOffixx"-Ordners.

__2__: Öffnen Sie eine PowerShell Konsole im __Administrator__ Modus und stellen Sie sicher, dass die "ExecutionPolicy" auf "unrestricted" gesetzt ist:

    Set-ExecutionPolicy Unrestricted

__3__: Führen Sie das "Install.ps1"-Script über die PowerShell Konsole im Installationordner aus. 

__4__: Das Script wird feststellen, dass bereits eine OneOffixx Installation vorliegt und wird Sie im dritten Schritt "Step 3: Deploy OneOffixx WebApps" fragen, ob Sie die bestehende Konfiguration beibehalten wollen: __Verneinen__ Sie das, indem Sie__"n"__ eingeben. Das sollte eine "saubere" Installation über die bestehenden Installation erzwingen.

Nun sollte im Installationsverzeichnis folgendes vorzufinden sein:

    C:\inetpub\wwwroot\OneOffixx\
    ├── Admin\
    │   └── ...
    ├── Service\
    │   └── ...
    ├── Web\
    │   └── ...
    ├── JobHost\
    │   └── ...   
    ├── Hub\
    │   └── ...
    └── OneOffixx.config

{% include alert.html type="info" text="Hinweis: Das Installationsverzeichnis kann im Install.ps1-Script überschrieben werden - im Standardfall wird C:\inetpub\wwwroot\OneOffixx\ genommen." %}

__5__: Aus dem Backup Admin Ordner den Inhalt zwischen &lt;oneOffixxAdminConfig&gt; und &lt;/oneOffixxAdminConfig> kopieren und in die neue (aktuell leere) OneOffixx.config zwischen &lt;oneoffixx&gt;...&lt;/oneoffixx&gt; einfügen. 

Das Hauptelement wurde umbenannt und heisst neu nur noch "oneoffixx".

__6__: Fügen Sie folgende Attribute der Datasource hinzu: 

* isPrimary: Bestimmt die jeweilige Datenquelle als primäre Datenquelle - nur eine Datenquelle sollte mit "isPrimary=true" markiert werden.
* licenseLocation: In Version 3 wird eine valide Lizenz für einige Features vorausgesetzt, dieses Lizenzfile sollte parallel zur OneOffixx.config liegen und bei der jeweiligen Datasource konfiguriert werden.

```
<datasources><add ...  isPrimary="true" licenseLocation="LICENSEFILE-PATH" /></datasources>
```

__7__: Der JobHost sollte ebenfalls unter den "&lt;apps&gt;" hinzugefügt werden:

```
<add id="aaad1092-db97-4fe6-a048-70b4ba8a3025" name="JobHost" logFilePath="C:\inetpub\wwwroot\OneOffixx\JobHost" type="JobHost" />
```    

Hinweis: Erstellen Sie eine eindeutige, neue ID z.B. über diese [Seite](https://www.guidgenerator.com/). Die hier abgebildete Id ist nur ein Beispiel.

__8__: Kopieren Sie aus dem __V2-Admin web.config__ den kompletten Bereich: 

```
<authorization>...</authorization>
```
 
...und fügen Sie diesen ebenfalls in der web.config des Admins (innerhalb des system.web-Eintrags) hinzu.

__9__: Führen Sie die Datenbank Migrationen im Admin-Dashboard aus. 

Die OneOffixx Installation ist damit auf dem neusten Stand gebracht.

Hinweis zur OneOffixx.config: Eine komplette Beispiel Konfiguration können Sie über /Admin/RampUp einsehen.

### Anleitung - Manuell

Falls das Powershell-Script nicht ausgeführt werden kann, können die Schritte auch manuell vollzogen werden.

Hierfür müssen die Admin/Hub/JobHost/Service/Web-Ordner manuell in das bestehende OneOffixx-Installationsverzeichnis kopiert werden. Vorher sollten die alten Dateien ebenfalls verschoben werden, damit keine alten Dateien im Verzeichnis übrig sind. Nach dem Kopiervorgang sollten die Schritte ab Punkt 3 von der script-gesteuerten Installation nachvollzogen werden.

### Neue Applikation: JobHost 

In Version 3 gibt es eine neue Anwendung, welche Prozesse im Hintergrund (z.B. den UserSync) durchführt: Den JobHost. 
Das Powershell Script soll dafür sorgen, dass der JobHost als __Scheduled Task__ einmal täglich aufgerufen wird. Falls das Script nicht genommen wird, sollte sichergestellt werden, dass die OneOffixx.JobHost.exe einmal täglich aufgerufen wird.

 
