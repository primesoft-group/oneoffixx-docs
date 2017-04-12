---
layout: page
title: Citrix XenApp / Terminalserver Installation
permalink: "install/en/client-citrix-ts/"
language: en
---

Terminal servers are made for __an average work load__ and are dependent on applications to release their resources as fast as possible when disconnecting from the RDP session. A client in normal configuration would stay in the memory and prevent the session from being closed completely, since the client is also serving as a server for the add-ins.

The setting __ShutdownOnDisconnect__ in OneOffixx.exe instructs the client to shut down automatically as soon as __Session Disconnect__ reaches it. This may be noticed by the user when OneOffixx starts again in the background after every __Session Start__.

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

<span class="label label-info">New since 3.0</span>
This setting can be adjusted in the [Setup]({{ site.baseurl }}/install/en/client/#msi) through the UI or a parameter.

It must be assured that every OneOffixx client has its own exclusive access to the cache in the __Load Balanced__ Terminal Server environment. This can be ensured through the correct supply of the [cache folder]({{ site.baseurl }}/install/en/client/#install).

Another option is to exclude the OneOffixx client from __Active State__ monitoring in the terminal server.

## Citrix XenApp and Terminal Server {% include anchor.html name="Citrix" %}
Further information can be found in the following articles:

* [http://support.citrix.com/article/CTX891671](http://support.citrix.com/article/CTX891671)
* [http://support.citrix.com/article/CTX137340](http://support.citrix.com/article/CTX137340)
* [http://www.browsium.com/faqs/configuring-xenapp-close-ion-catalyst-processes/](http://www.browsium.com/faqs/configuring-xenapp-close-ion-catalyst-processes/)

__Example registry: Citrix__

```
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Citrix\wfshell\TWI
   Value Name:LogoffCheckSysModules
   Type:REG_SZ
   String:OneOffixx.exe
```
## Microsoft Terminal Server {% include anchor.html name="MSTS" %}
Further information can be found in the following article:

* [https://support.microsoft.com/en-us/kb/2513330](https://support.microsoft.com/en-us/kb/2513330)

__Example registry: Terminal Server__

```
   HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\Terminal Server\Sysprocs
   Value name: OneOffixx.exe
   Data type: REG_DWORD 
   Base: Hex
```   
Caution! The terminal server needs to be restarted after this setting.
