---
layout: page
title: Installation of SQL Server
permalink: "install/en/server-sql-install/"
language: en
---

This document describes the installation of a SQL server for OneOffixx.

The OneOffixx server can in principle also be used with a [SQL Express Edition](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/sql-server-express.aspx) without any issues. This alternative is only recommended as a test environment or for small companies.

Please install the SQL server with the installation package provided by Microsoft.

{% include alert.html type="info" text="OneOffixx can be operated with <b>Windows Authentication as well as with SQL Authentication</b>. We recommend SQL Authentication due to the easier set up procedure." %}

__Collation:__

__Case-insensitive__ collation should be employed for the operation of OneOffixx. It is recommended to use __SQL_Latin1_General_CP1_CI_AS__ and on older SQL servers __SQL_Latin1_General_CI_AS__ respectively.

* CI: Case-Insensitive ('ABC' == 'abc')
* AS: Accent sensitive ('ü' != 'u')

OneOffixx is automatically using the SQL server’s Collation during the database generation. It is required to explicitly set up an empty, case-insensitive database manually if the server is set to using a case-sensitive Collation by default.

__Authentication Mode: Mixed Mode__

Make sure that the Authentication Mode is set to Mixed Mode during installation.

![x]({{ site.baseurl }}/assets/content-images/install/en/server-sql-install-mixedmode.png "Mixed-Mode Auth in SQL Server")

This setting can be changed subsequently in the Security tab.

![x]({{ site.baseurl }}/assets/content-images/install/en/server-sql-install-mixedmode-change.png "Change Mixed-Mode Auth in SQL Server")

__Authentication Mode: Windows Only__

The default installation utilizes a SQL user to connect to the database. The following steps should be considered when using a Windows user instead:

The ConnectionStrings in the OneOffixx.config file and OneOffixxAdmin.config respectively for the database need to be adapted:

    "Integrated Security=true" instead of "User ID=...;Password=..."

The Windows User needs to be lodged as User in AppPool in the IIS. This Pool has to be employed by every application:

    IIS -> Application Pools -> Advanced Settings -> Identity -> Custom account

Additionally, this Windows User needs to be lodged in the "Log on as service" policy.

    Administrative Tools -> Local Security Policy -> Local Policies -> User Rights Assignment ->"Log on as a service"
  
The OneOffixx web application should be running with the corresponding Windows User after these steps have been completed.
