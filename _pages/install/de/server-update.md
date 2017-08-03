---
layout: page
title: Server Update Hinweise
permalink: "install/de/server-update/"
language: de
---

## V2.X auf V3.x {% include anchor.html name="v2-v3" %}

Mit Version 3 wurde ein einheitliche Konfiguration für alle Server-Applikationen eingeführt. In Version 2 gab es pro Applikation eine eigene "OneOffixx.config"-Datei und der Admin hatte eine eigene "OneOffixxAdmin.config".

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

Die Änderung auf die zentrale Konfiguration ist die grösste Änderung bei dem Update.
		
### Anleitung - V3 Installation & kopieren der .config

Die Anleitung beschreibt den "einfachsten" Weg, allerdings sind die Web-Applikationen in der Zeit __nicht__ erreichbar, wobei der OneOffixx Client Offline-fähig ist und ohnehin keine ständige Verbindung zum Server benötigt.

1. Benennen Sie den "OneOffixx"-Ordner um oder verschieben Sie ihn in einen anderen Ordner.
2. Führen Sie das "Install.ps1"-Script von den Installationsdateien aus.

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

3. Kopieren Sie aus dem __V2-Service__ Ordner die alte OneOffixx.config in das neue "OneOffixx" Verzeichnis und überschreiben Sie die aktuell leere OneOffixx.config. 
4. Öffnen Sie die OneOffixx.config und tauschen Sie

```
<oneoffixxConfig>...</oneoffixxConfig>
```

durch 

```
<oneoffixx>...</oneoffixx>
```

aus.

Das Hauptelement wurde umbenannt und heisst neu nur noch "oneoffixx".
5. Kopieren Sie aus dem __V2-Admin web.config__ den kompletten Bereich: 

```
<authorization>...</authorization>
```
 
... und fügen Sie diesen ebenfalls in der web.config des Admins (innerhalb des system.web-Eintrags) hinzu.

6. Führen Sie die Datenbank Migrationen im Admin-Dashboard aus. 
7. In Version 3 wird eine valide Lizenz für einige Features vorausgesetzt, dieses Lizenzfile sollte parallel zur OneOffixx.config liegen und bei der jeweiligen Datasource konfiguriert werden:

```
<datasources><add ...  licenseLocation="..." /></datasources>
```

8. Der JobHost sollte ebenfalls unter den "<apps>" hinzugefügt werden:

```
<add id="aaad1092-db97-4fe6-a048-70b4ba8a3025" name="JobHost" logFilePath="C:\inetpub\wwwroot\OneOffixx\JobHost" type="JobHost" />
```    

Eine komplette Beispiel Konfiguraiton können Sie über /Admin/RampUp einsehen.

Die OneOffixx Installation ist nun damit auf dem neusten Stand gebracht.

### Anleitung - Manuell

Falls das Powershell-Script nicht ausgeführt werden kann, können die Schritte auch manuell vollzogen werden.

Hierfür müssen die Admin/Hub/JobHost/Service/Web-Ordner manuell in das bestehende OneOffixx-Installationsverzeichnis kopiert werden. Vorher sollten die alten Dateien ebenfalls verschoben werden, damit keine alten Dateien im Verzeichnis übrig sind.
Nach dem Kopiervorgang sollten die Schritte ab Punkt 3. von der script-gesteuerten Installation nachvollzogen werden.

### Neue Applikation: JobHost 

In Version 3 gibt es eine neue Anwendung, welche Prozesse im Hintergrund (z.B. den UserSync) durchführt: Den JobHost. 
Das Powershell Script sollte dafür sorgen, dass der JobHost als __Scheduled Task__ einmal täglich aufgerufen wird. Falls das Script nicht genommen wurde, sollte sichergestellt werden, dass die OneOffixx.JobHost.exe einmal täglich aufgerufen wird.

 
