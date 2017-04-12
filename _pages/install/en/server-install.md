---
layout: page
title: OneOffixx Basic Installation
permalink: "install/en/server-install/"
language: en
---

The supplied OneOffixx installation package contains a PowerShell script __"install.ps1"__ takes care of the basic installation.

The script needs to be executed with __administrator rights__, since missing Windows features will be enabled. Furthermore, the execution of PowerShell scripts needs to be enabled.

__ExecutionPolicy:__

ExecutionPolicy needs to be set to "RemoteSigned" at least, in order to start the script.

     Set-ExecutionPolicy RemoteSigned

![x]({{ site.baseurl }}/assets/content-images/install/de/server-install-ps.png "Powershell Set-ExecutionPolicy")

__Version 1: Starting through a new PowerShell Session__

Generate a new PowerShell session and call up "Install.ps1" from the installation package.

__Version 2: Run with PowerShell__

Windows Explorer can be used to start "Install.ps1". However, permission by ExecutionPolicy is also required:

![x]({{ site.baseurl }}/assets/content-images/install/de/server-install-explorer.png "Start via Windows Explorer")

## Script Procedure

__1.	Check required Windows features__

First of all, it should be verified that all necessary Windows features are installed. This includes the Internet Information Service with ASP.NET as well as WDF Services among others.

__2.	"OneOffixx" website registration in ISS__

The next step is checking whether there is already a "OneOffixx" website registered in the IIS. Please proceed with the next step if this is the case.

You will be asked to register a website and specify the installation path and a port in case there was no website found. The standard settings are displayed in the installation script.

__3.	"OneOffixx" applications__

In the final step the actual web applications are set up on the OneOffixx website.

In case applications are installed already, one will be asked if they should be updated. Here, "web.config" or OneOffixx configuration files can be kept or replaced.

For a normal update it is recommended to keep the configuration files.

__Finalizing the basic installation__

 After the first installation ISS as well as web applications should be installed now.

{% include alert.html type="info" text="The standard installation process creates a website that listens to port 80. This could potentially lead to conflicts with other websites.<br/><b>In this case the OneOffixx website will not be started.</b>" %}

