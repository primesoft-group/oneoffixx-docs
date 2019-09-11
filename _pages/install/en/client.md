---
layout: page
title: Client Installation
permalink: "install/en/client/"
language: en
---

System requirements and instructions for the installation of OneOffixx client components are presented here.

## <i class="fa fa-wrench" aria-hidden="true"></i> System requirements {% include anchor.html name="system-requirements" %}

__Operation System__

The OneOffixx client can be installed on the following operating systems:

* Windows Vista SP2 or higher (32-bit as well as 64-bit)
* Windows Server 2008 or higher (32-bit as well as 64-bit)
* [Citrix XenApp/TS or Windows Terminal Server (compatible for versions from Vista SP2 onwards, 32bit and 64bit)]({{ site.baseurl }}/install/en/client-citrix-ts)

__Supported Microsoft Office Versions__

OneOffixx supports all Microsoft Office versions later than __Office 2010, 32-bit as well as 64-bit versions. __[OneOffixx supports earlier versions of Microsoft Windows and Microsoft Office until they are no longer supported by Microsoft ("extended support period by an API Service").](http://oneoffixx.com/lifecycle/)__

__.NET Framework__

 {% include new-badge.html version="3.0" %} The OneOffixx client with Release 2019 requires at least __[.NET Framework 4.7.2 ](https://https://dotnet.microsoft.com/download/thank-you/net472)__.
 
The OneOffixx client with version 3.0 requires at least __[.NET Framework 4.5.2](https://www.microsoft.com/en-US/download/details.aspx?id=42642)__.

__Hard disk space__

The software itself needs approximately 200 MB of hard disk space. In addition, log files and settings are stored by the OneOffixx client. A local cache for offline usage is also created. Cache size varies with number and size of templates.

__Active Directory__

The server applications and the OneOffixx client need to be located in the same domain or in a domain authorized by system trusts.

## <i class="fa fa-power-off" aria-hidden="true"></i> 32bit or 64bit Installation {% include anchor.html name="bitness" %}

The OneOffixx installer is available in a 32-bit and a 64-bit version. The required version __depends on the installed Microsoft Office version__.

The 64-bit OneOffixx version __needs to be__ installed if a 64-bit version of Microsoft office is used. 

## <i class="fa fa-plug" aria-hidden="true"></i> Ports & Server-Connections {% include anchor.html name="ports" %}

The OneOffixx client communicates exclusively __by HTTP/HTTPS__ with the OneOffixx server. Therefore, only port 80 or port 443 is required.

## <i class="fa fa-windows" aria-hidden="true"></i> MSI Parameters {% include anchor.html name="msi" %}

The OneOffixx MSI package contains the OneOffixx client and various Microsoft Office add-ins.

__OneOffixx’ specific parameters:__

* APPLICATIONFOLDER = install folder (default C:\Program Files (x86)\OneOffixx)
* INSTALLDESKTOPSHORTCUT = 1 / 0 for yes or no
* AUTOSTART = 1 / 0 for yes or no
* SERVICEENDPOINTURL = Service Endpoint (\*can be overwritten via registry)
* {% include new-badge.html version="3.3" %} SERVICESPN = SPN for the user, which runs the Service (advanced setting, might only be needed when the Service runs under a Service-Account and SQL Integrated Authentication is used. \* can be overwritten via registry) 
* ADDLOCAL = Features
     * WordAddInFeature = Word Add-In
     * OutlookAddInFeature = Outlook Add-In
     * ExcelAddInFeature = Excel Add-In
     * PowerPointAddInFeature = PowerPoint Add-In

The following parameters are only necessary for certain installation versions (e.g. installation on Terminal Servers) and are therefore optional:

* DATAINLOCALAPPDATAFOLDER = False/True (must be True on Network Share)
* CACHEFOLDER = Path e.g. \\Share\... (with Placeholders like %username% from environment-variables etc.)
* SETTINGFOLDER = Path e.g. \\Share\... (with Placeholders like %username% from environment-variables etc.)
* SHUTDOWNONDISCONNECT = true / false (Allows to configure OneOffixx to shutdown when a disconnect happens (such as disconnecting from an RDP Session) )
* LOGFOLDER = Path for storing logfiles e.g. \\Share\... (with Placeholders supported by [NLog](https://github.com/NLog/NLog/wiki/Layout-Renderers))

Apart from this, common __[MSIEXEC command-line options](https://msdn.microsoft.com/en-us/library/windows/desktop/aa367988%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)__ apply.

Example: 

    msiexec /qb /i "OneOffixx.Install(x86).msi" APPLICATIONFOLDER="C:\Program Files (x86)\OneOffixx" SERVICEENDPOINTURL="http://appurl/OneOffixxService.svc" INSTALLDESKTOPSHORTCUT=1 AUTOSTART=1 /l*v OneOffixxInstall.log AddLocal=WordAddInFeature,OutlookAddInFeature

__ServiceEndpointUrl via Registry:__

OneOffixx searches the registry for a string value "ServiceAddress" with the keys (HKCU &HKLM):

    [HKEY_CURRENT_USER\Software\Sevitec Informatik AG\OneOffixx]
    "ServiceAddress"="http..."

or 

    [HKEY_LOCAL_MACHINE\Software\Sevitec Informatik AG\OneOffixx]
    "ServiceAddress"="http..."

or (suitable for __group policies__)

    [HKEY_CURRENT_USER\Software\Policies\Sevitec Informatik AG\OneOffixx]
    "ServiceAddress"="http..."
  
This value will be used instead of ServiceAddress from the OneOffixx.exe.config file, if found. 

__[OneOffixx ADMX templates]({{ site.baseurl }}/assets/content-files/OneOffixxGroupPoliciesTemplate.zip)__ are available to control these settings via group policies.


## <i class="fa fa-cogs" aria-hidden="true"></i> Installation Scenarios {% include anchor.html name="install" %}

OneOffixx installer’s default settings are aiming for a "normal" installation on a system that can be started by one or multiple Windows users. Here, cache and settings are stored in %AppData%.

Every OneOffixx client entity needs to have exclusive access to ensure full functionality. A new cache location needs to be declared, if this is not the case (e.g. for some Citrix/Terminal Server configurations).

### <i class="fa fa-cog" aria-hidden="true"></i> OneOffixx Client: Default Installation

No further parameters are necessary. Cache and settings are stored in %AppData%.

__Recommended for:__

☑ No roaming profiles stored on server side

### <i class="fa fa-cog" aria-hidden="true"></i> OneOffixx Client: Cache & Settings location

Cache as well as settings can be stored in %AppDataLocal%, if the following parameter is set:

    DATAINLOCALAPPDATAFOLDER = True

__Recommended for:__

☑ Roaming profiles stored on server side

☑ *%AppDataLocal%* folder is not being deleted

☑ User is always logged in on the same machine

### <i class="fa fa-cog" aria-hidden="true"></i> OneOffixx Client: Cache located in a specific folder

The following setting can specify the cache location, if %AppData% as well as %AppDataLocal% is not an option, or it is possible that multiple OneOffixx entities are open for one user.

    CACHEFOLDER = Path e.g. //Share/... (with Placeholders like %username% etc.)

__Recommended for:__

☑ Terminal server installation with multiple open sessions per user

__Requirements:__

☑ Specified network drive is present and always available

### <i class="fa fa-cog" aria-hidden="true"></i> OneOffixx Client: Settings located in a specific folder

It is also possible to store the settings in a dedicated folder:

    SETTINGFOLDER = Path e.g. //Share/... (with Placeholders like %username% etc.)

## <i class="fa fa-life-ring" aria-hidden="true"></i> Troubleshooting {% include anchor.html name="troubleshooting" %}

__OneOffixx AddIns in Microsoft Office do not start {% include anchor.html name="troubleshooting-vcredist" %}__

OneOffixx add-ins cannot be started, i.e. no Office icon is visible in the Office ribbon. This may have several causes:

* The OneOffixx add-in is not installed: 
    * If the OneOffixx add-in does not appear under "File – Options – Add-Ins" it might not be installed. Please check if the corresponding add-in was selected during the installation.
* A 64-bit Office version was installed with a 32-bit OneOffixx installer.
    * If a 64-bit Office version is used, it needs to be installed with a 64-bit OneOffixx installer.
* OneOffixx Version 2.0: Visual C++ Redistributable 2015 Package is missing or not installed properly.
    * OneOffixx versions above 2.3.40140 include the Redistributable 2015 Package, but it is possible that a corrupt system installation prevents the add-in from being executed. The [VC++ Redistributable 2015 Package](https://www.microsoft.com/de-ch/download/details.aspx?id=48145) should be re-installed if this is the case.

__Starting Microsoft Office is significantly delayed since the OneOffixx add-in was installed {% include anchor.html name="troubleshooting-ngen" %}__

Slowly starting Office can be caused by an incomplete execution of the "Native Image Generator (ngen)" process. This process is triggered automatically after the installation and is part of the .NET framework. Executing "Native Image Generator" (ngen):

The process ngen.exe is located in the following path: c:\windows\microsoft.net\framework\v4.0.30319\ngen.exe. The current status can be checked with "display". This should look like this:

    C:\Windows\Microsoft.NET\Framework\v4.0.30319\ngen.exe display "C:\Program Files (x86)\OneOffixx\OneOffixx.exe"
    Microsoft (R) CLR Native Image Generator - Version 4.6.1087.0
    Copyright (c) Microsoft Corporation.  All rights reserved.

    NGEN Roots:

    C:\Program Files (x86)\OneOffixx\OneOffixx.exe

    NGEN Roots that depend on "c:\Program Files (x86)\OneOffixx\OneOffixx.exe

    C:\Program Files (x86)\OneOffixx\OneOffixx.exe

    Native Images:

    OneOffixx, Version=2.3.40190.0, Culture=neutral, PublicKeyToken=null

The compilation process should be re-started by "update", if OneOffixx is displayed as "pending".

    c:\Windows\Microsoft.NET\Framework\v4.0.30319\ngen.exe update

This should significantly accelerate the loading process for add-ins. 

{% include alert.html type="warning" text="Please do not hesitate to contact us if you have any questions or encounter any problems. " %}
