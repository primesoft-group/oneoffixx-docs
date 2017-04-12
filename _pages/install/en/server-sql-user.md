---
layout: page
title: SQL Server – User Configuration
permalink: "install/en/server-sql-user/"
language: en
---

{% include alert.html type="info" text="OneOffixx can be operated with  <b>Windows Authentication as well as with SQL Authentication</b>. We recommend SQL Authentication due to an easier set up procedure in most cases. The following description is using <b>SQL Authentication</b>." %}

Data access requires a OneOffixx SQL User.

__SQL Script__

The following steps can be automated by employing this SQL script:

The __'PASSWORD'__ and possibly the corresponding login name (__oneoffixxuser__) have to be replaced.

    CREATE LOGIN [oneoffixxuser] WITH PASSWORD='PASSWORD', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF
    GO
    
    EXEC sys.sp_addsrvrolemember @loginame = N'oneoffixxuser', @rolename = N'dbcreator'
    GO

__About the UI__

First of all, a new login has to be created.

![x]({{ site.baseurl }}/assets/content-images/install/en/server-sql-user-new.png "New Login")

Make sure that SQL Server Authentication is selected and enter your password.

{% include alert.html type="warning" text="Depending on password policy it is possible for the account’s password to expire. Make sure that the SQL User is ready for use or deactivate 'Enforce Password Policy' and 'User must change password at next login'." %}

![x]({{ site.baseurl }}/assets/content-images/install/en/server-sql-user-new-dialog.png "Security-Settings")

__Server Roles / Permissions__

The new user requires at least a __'public' role__ in order to log in to the SQL server.

OneOffixx is able to create databases on his own. For this purpose the SQL User is required to be 'dbcreator'. This role is __optional__. An empty database needs to be created manually and the OneOffixx SQL user role has to be set to 'dbo' if you prefer not to use 'dbcreator'.

![x]({{ site.baseurl }}/assets/content-images/install/en/server-sql-user-new-roles.png "Standard assignment of roles for the OneOffixx SQL User")

New databases can be created and existing databases can be copied with the OneOffixx administrator interface. Therefore, it is recommended to keep the role ‘dbcreator’.


