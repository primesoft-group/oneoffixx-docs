---
layout: page
title: Citrix XenApp / Terminalserver Installation
permalink: "install/de/client-citrix-ts/"
language: de
---

Terminalserver sind für einen __durchschnittlichen Workload__ ausgelegt und sind darauf angewiesen das die Applikationen ihre Ressourcen bei Trennung der RDP Session möglichst schnell wieder freigeben. Da der Client gleichzeitig als Server für die Add-Ins dient, würde er mit normaler Konfiguration im Speicher verbleiben und verhindern, dass die Session komplett beendet werden kann.

Durch die Einstellung __ShutdownOnDisconnect__ in der OneOffixx.exe.config wird der Client dazu angewiesen, dass er den Client automatisch beendet, sobald das __Session Disconnect__ vom Terminalserver erhält. Für den Anwender macht sich dies so bemerkbar, dass OneOffixx nach jedem __Session Start__ neu im Hintergrund gestartet wird.

```xml
  <configuration>
    <configSections>
    <appSettings>
      <!-- Allows to configure OneOffixx to shutdown 
           when a disconnect happens (such as disconnecting from an RDP Session) -->
      <add key="ShutdownOnDisconnect" value="true" />
    </appSettings>
  </configuration>
```

<span class="label label-info">NEU ab 3.0</span>
Diese Einstellung kann im [Setup]({{ site.baseurl }}/install/de/client/#msi) entweder über die UI oder über ein Parameter eingestellt werden.

Bei __Load Balanced__ Terminal Server Umgebung muss sichergestellt werden, dass jeder OneOffixx Client exklusiven Zugriff auf den Cache hat. Dies kann durch die richtige Bereitstellung des [Cacheordners]({{ site.baseurl }}/install/de/client/#install) sichergestellt werden.

Optional kann im Terminalserver der OneOffixx Client von der __Active State__ Überwachung ausgeschlossen werden. 

## Citrix XenApp und Terminal Server {% include anchor.html name="Citrix" %}
Weitere Informationen finden Sie unter folgenden Artikel:

* [http://support.citrix.com/article/CTX891671](http://support.citrix.com/article/CTX891671)
* [http://support.citrix.com/article/CTX137340](http://support.citrix.com/article/CTX137340)
* [http://www.browsium.com/faqs/configuring-xenapp-close-ion-catalyst-processes/](http://www.browsium.com/faqs/configuring-xenapp-close-ion-catalyst-processes/)

__Beispiel Registry: Citrix__

```
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Citrix\wfshell\TWI
   Value Name:LogoffCheckSysModules
   Type:REG_SZ
   String:OneOffixx.exe
```
## Microsoft Terminal Server {% include anchor.html name="MSTS" %}
Weitere Informationen finden Sie unter folgenden Artikel:

* [https://support.microsoft.com/en-us/kb/2513330](https://support.microsoft.com/en-us/kb/2513330)

__Beispiel Registry: Terminal Server__

```
   HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\Terminal Server\Sysprocs
   Value name: OneOffixx.exe
   Data type: REG_DWORD 
   Base: Hex
```   
Achtung: Der Terminalserver muss nach der Einstellung neu gestartet werden.

