---
layout: page
title: OneOffixx Basic Installation
permalink: "install/en/server-install/"
language: en
---

The supplied OneOffixx installation package contains a PowerShell script __"install.ps1"__, that takes care of the basic installation. The script needs to be executed with __administrator rights__, since missing Windows features will be enabled. Furthermore, the execution of PowerShell scripts needs to be enabled.

__ExecutionPolicy:__

ExecutionPolicy needs to be set to "Unrestricted", in order to start the script.

     Set-ExecutionPolicy Unrestricted

```ps
PS C:\Users\administrator> Set-ExecutionPolicy Unrestricted

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
http://go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): y
```

__Option 1: Starting through a new PowerShell Session__

Open a new PowerShell session and call up "Install.ps1" from the installation package.

__Option 2: Run with PowerShell__

Windows Explorer can be used to start "Install.ps1". However, permission set by ExecutionPolicy is also required:

![x]({{ site.baseurl }}/assets/content-images/install/en/server-install-explorer.png "Start via Windows Explorer")

## Script Procedure

__1.	Check required Windows features__

First of all, it should be verified that all necessary Windows features are installed. This includes the Internet Information Service (IIS) with ASP.NET as well as WDF Services among others.

__2.	"OneOffixx" website registration in IIS__

The next step is checking whether there is already a "OneOffixx" website registered in the IIS. Please proceed with the next step if this is the case. You will be asked to register a website and specify the installation path and a port in case there was no website found. The standard settings are displayed in the installation script.

__3.	"OneOffixx" applications__

In the final step the actual web applications are set up on the OneOffixx website. In case applications are installed already, one will be asked if they should be updated. Here, "web.config" or OneOffixx configuration files can be kept or replaced. For a normal update it is recommended to keep the configuration files.

__Finalizing the basic installation__

 After the first installation the IIS as well as the OneOffixx web applications should be installed now.

{% include alert.html type="info" text="The standard installation process creates a website that listens on port 80. This could potentially lead to conflicts with other websites.<br/><b>In this case the OneOffixx website will not be started.</b>" %}

