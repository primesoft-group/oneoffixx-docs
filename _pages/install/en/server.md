---
layout: page
title: Server Installation
permalink: "install/en/server/"
language: en
---

System requirements and step-by-step instructions for the installation of OneOffixx Server components can be found here.

## <i class="fa fa-wrench" aria-hidden="true"></i> System requirements {% include anchor.html name="system-requirements" %}

__Operating system & components__

OneOffixx Server can be installed on the following operating systems:

* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

The following components are required for running OneOffixx Server applications:

* Internet Information Server Version 7 or higher
* SQL Server from Version 2008 (Express or higher). In case of a large number of users it is not recommended to use *Express*.
* Microsoft .NET Framework 4.5.2 or higher

*A PowerShell Script is included in the product package to ease installation on the Server. Windows PowerShell 2.0 has to be installed (automatically included on Windows Server 2008 R2 and higher) to run the Script correctly.*

*The PowerShell "ExecutionPolicy" has to be set to allow the execution of PowerShell scripts. Please execute the command "Set-ExecutionPolicy Unrestricted" in PowerShell if the script is not loaded properly.*

__Memory & CPU Cores__

OneOffixx Server is operated within the Internet Information Server. We recommend meeting the requirements of Microsoft.

Advisable are at least 4 GB memory and 2 cores. More advanced CPUs and larger memory are recommended if additional software is running on the web server.

__Hard disk space__

The software requires about 100 MB of hard drive space. The software requires about 100 MB of hard drive space. All OneOffixx Server applications are set in their standard configuration to log in their respective application directory.

Log files are created every day and can reach a size of several hundred Mb. Log files are stored for maximum 7 preceding days.

__Active Directory__

The server hosting OneOffixx must be part of the Active Directory. Permissions for the organizational units are set in the Active Directory.

Ensure that the company network is integrated in the Active Directory.

__DNS__

OneOffixx clients communicate through HTTP/HTTPS with the OneOffixx Server. It is recommended to assign a designated CNAME to the OneOffixx server in the local DNS server. This is employed multiple times in the client configuration and the server.

The following exemplary DNS CNAME is used from here on:

    oneoffixx.company.com

__Usage of antivirus programs on the Windows Server__

If a virus scanner is employed on the same system that is used to execute OneOffixx server applications, it should be configured to avoid restrictions in their functionality.

The following is recommended:

* The virus scanner should not analyze the installation directory of OneOffixx (standard "C:\inetpub\wwwroot\OneOffixx") on the server. Log files are frequently written in this directory if set in standard configuration.
* The directory IIS Logs should also not be analyzed ("C:\inetpub\logs").
* Exceptions should be added for OneOffixx if the virus scanner is analyzing HTTP/HTTPS connections.

Operating OneOffixx and a virus scanner on the server at the same time may lead to performance issues without application of the aforementioned changes.

## <i class="fa fa-cogs" aria-hidden="true"></i> Installation Scenarios {% include anchor.html name="install" %}

__Installing a OneOffixx Server & Database on new servers__

![x]({{ site.baseurl }}/assets/content-images/install/en/server-install-overview-single.png "New Windows Server for IIS & SQL Server")

{:.table .table-striped}
|     | Installation and configuration step | 
|:---:| --- |
| 1.  | Supply Microsoft Windows Server |
| 2.  | [Install SQL Server]({{ site.baseurl }}/install/en/server-sql-install) |
| 3.  | [Create a SQL Server OneOffixx user]({{ site.baseurl }}/install/en/server-sql-user) |
| 4.  | [Execute basic installation with PowerShell and follow instructions]({{ site.baseurl }}/install/en/server-install) |
| 5.  | [Follow the configuration wizard on the administrator page]({{ site.baseurl }}/install/en/server-config) |
| 6.  | [Functional test]({{ site.baseurl }}/install/en/server-test) |

__Installing an OneOffixx Server on a new server. The database is installed on an already existing server.__

![x]({{ site.baseurl }}/assets/content-images/install/en/server-install-overview-externalsql.png "New Windows Server for IIS & existing SQL Server")

{:.table .table-striped}
|     | Installation and configuration step | 
|:---:| --- |
| 1.  | Supply Microsoft Windows Servern | 
| 2.  | [Create a SQL Server OneOffixx user]({{ site.baseurl }}/install/en/server-sql-user) |
| 3.  | [Execute basic installation with PowerShell and follow instructions]({{ site.baseurl }}/install/en/server-install) |
| 4.  | [Follow the configuration wizard on the administrator page]({{ site.baseurl }}/install/en/server-config) |
| 5.  | [Functional test]({{ site.baseurl }}/install/en/server-test) |

__IIS and SQL Server already exist. Installing OneOffixx Server and database.__

![x]({{ site.baseurl }}/assets/content-images/install/en/server-install-overview-existinginfra.png "Existing Windows Server for IIS & existing SQL Server")

{:.table .table-striped}
|     | Installation and configuration step | 
|:---:| --- |
| 1.  | [Create a SQL Server OneOffixx user]({{ site.baseurl }}/install/en/server-sql-user) |
| 2.  | [Execute basic installation with PowerShell and follow instructions]({{ site.baseurl }}/install/en/server-install) |
| 3.  | [Follow the configuration wizard on the administrator page]({{ site.baseurl }}/install/en/server-config) |
| 4.  | [Functional test]({{ site.baseurl }}/install/en/server-test) |

## <i class="fa fa-refresh" aria-hidden="true"></i> Server Application Updates {% include anchor.html name="update" %}

{% include new-badge.html version="3.0" %}

{% include alert.html type="info" text="<b>Please note with Version 3</b><br/>A central configuration file for all server app has been introduced with version 3." %}

The PowerShell installation script can be called up again for an update. It is recommended to make a backup beforehand. You should make sure that the already existent files "OneOffixx.config" are kept during the installation. The script will take care of that for you.

Please note with Version 2.x: The admin application has it's own configuration file called "OneOffixxAdmin.config". 

Exception: We will supply you with separate instructions if changes affect the structure of "web.config".

Whether the update requires changes in the database will be displayed in the OneOffixx Admin and you will be able to implement these changes directly in the Admin web application.

{% include alert.html type="warning" text="Please do not hesitate to contact us if you have any questions or encounter any problems." %}
