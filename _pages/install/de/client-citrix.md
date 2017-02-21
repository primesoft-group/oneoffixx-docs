/msi---
layout: page
title: OneOffixx Citrix/Terminalserver Installation
permalink: "install/de/client-citrix/"
---

Terminalserver sind für einen __durchschnittlichen Workload__ ausgelegt und sind darauf angewiesen, dass die Applikationen ihre belegten Ressourcen bei Trennung der RDP Session möglichst schnell wieder freigeben. Da der Client gleichzeitig als Server für die Add-Ins dient, würde er bei einer normalen Installation im Speicher verbleiben und somit verhindern, dass die Session komplett beendet werden kann.


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

Zusätzlich oder Alternativ kann im Terminalserver der OneOffixx Client von der __Active State__ Überwachung ausgeschlossen werden. 

## Citrix XenApp und Terminal Server {% include anchor.html name="Citrix" %}
Weitere Informationen finden Sie unter folgenden Artikel:

http://support.citrix.com/article/CTX891671 </br>
http://support.citrix.com/article/CTX137340 </br>
http://www.browsium.com/faqs/configuring-xenapp-close-ion-catalyst-processes/</br>

__Beispiel Registry Einstellung Citrix__
{HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Citrix\wfshell\TWI
Value Name:LogoffCheckSysModules
Type:REG_SZ
String:OneOffixx.exe}


## Microsoft Terminal Server {% include anchor.html name="MSTS" %}
Weitere Informationen finden Sie unter folgenden Artikel:

https://support.microsoft.com/en-us/kb/2513330

__Bspiel Registry Terminal Server__
{HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\Terminal Server\Sysprocs
 Value name: OneOffixx.exe
Data type: REG_DWORD 
Base: Hex}
