---
layout: page
title: SQL Server - User Konfiguration
permalink: "install/de/server-sql-user/"
language: de
---

{% include alert.html type="info" text="OneOffixx kann <b>sowohl mit Windows Authentication als auch mit SQL Authentication</b> betrieben werden. Wir empfehlen die SQL-Authentifizierung, da diese in den meisten Fällen ein einfachereres Setup darstellt." %}

Für den Datenzugriff wird ein OneOffixx SQL-Benutzer benötigt. 

__SQL-Skript__

Die folgenden Schritte können auch über dieses SQL-Skript automatisiert werden:

Ausgetauscht werden, muss das __'PASSWORD'__ und eventuell der entsprechende Loginname; im Beispiel __oneoffixxuser__.

    CREATE LOGIN [oneoffixxuser] WITH PASSWORD='PASSWORD', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF
    GO
    
    EXEC sys.sp_addsrvrolemember @loginame = N'oneoffixxuser', @rolename = N'dbcreator'
    GO

__Über die UI__

Legen Sie als erstes ein neues Login an. 

![x]({{ site.baseurl }}/assets/content-images/install/en/server-sql-user-new.png "Neuer Login")

Stellen Sie sicher, dass SQL Server Authentication ausgewählt ist und geben Sie das Passwort ein. 

{% include alert.html type="warning" text="Je nach Password-Policy kann das Passwort des Accounts ablaufen. Stellen Sie sicher, dass der SQL-Benutzer stets betriebsbereit ist oder deaktivieren Sie 'Enforce Password Policy' und 'User must change password at next login'." %}

![x]({{ site.baseurl }}/assets/content-images/install/en/server-sql-user-new-dialog.png "Security-Settings")

__Server Roles / Berechtigungen__

Der neue Benutzer bentöigt mindestens die __"public" Rolle__, um sich am SQL Server anzumelden.

OneOffixx kann selbst die Datenbank erstellen - Voraussetzung dafür ist, dass der SQL-Benutzer ebenfalls noch "dbcreator" ist. Diese Rolle ist __optional__. Falls Sie den Weg ohne "dbcreator" bevorzugen, müssen Sie selbst eine leere Datenbank anlegen und den OneOffixx SQL User die "dbo"-Rolle zuweisen.

![x]({{ site.baseurl }}/assets/content-images/install/en/server-sql-user-new-roles.png "Standard Rollen Zuweisung für den OneOffixx SQL User")

Die OneOffixx Administrationsoberfläche erlaubt es, auch neue Datenbanken anzulegen bzw. bestehende zu kopieren, daher empfiehlt es sich, die Rolle "dbcreator" beizubehalten.


