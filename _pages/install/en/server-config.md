---
layout: page
title: OneOffixx Basic Configuration
permalink: "install/en/server-config/"
language: en
---

The configuration contains three main steps and the Admin web application will help guide you through these steps. You could start with the __"Rampup Guide"__ by opening the Admin page in your browser.

The Admin dashboard will help you with the Installation or the operation of OneOffixx, but is only indirectly required for the productive operation.

This instruction convers OneOffixx version 3 or higher. For version 2 you can find the instructions [here](#version2x).

## Version 3

{% include new-badge.html version="3" %}

__Step 1: OneOffixx.config__

The first step is to check if the __central configuration file "OneOffixx.config"__ is containing configuration parameters.

The "Rampup Guide" will be displayed immediately if this is not the case. Please take a configuration example from the "Rampup Guide" and edit the file "OneOffixx.config" manually or make use of the "Config-Editor".

__Editing OneOffixx.config manually:__

OneOffixx.config is located in the OneOffixx folder, which contains all needed OneOffixx installation files.

Default folder structure:

```
    - OneOffixx
        - Admin
	- Hub
	- Service
	- JobHost
	- Web
	- ...
	- OneOffixx.config
``` 

The most important configuration item is ConnectionString, which leads to the OneOffixx production database later on, and has to be addressed as follows:

    Data Source=localhost;InitialCatalog=oneoffixx;UserID=[user];Password=[PW];MultipleActiveResultSets=True

If windows authentication is enabled ConnectionString will take the following form:

    Data Source=localhost;InitialCatalog=oneoffixx;Integrated Security=true;MultipleActiveResultSets=True

__Step 2: Data Source Management__
	
Open the starting page of the Admin web application now if the configuration was saved in "OneOffixx.config" (manually or with the config editor). 

Click __"Init"__ if the SQL user has __"dbcreator" permissions__ and no database has been created yet.

This will create a database including tables.

__Click the checkbox__ if you have __already created an empty database__.

The database should be created in both cases.

__Step 3: Securing Admin__

Server components are now installed successfully and configured. It is recommended to follow the instructions of the configuration wizard and unlock the OneOffixx Admin only for specific users via the corresponding web.config-file. You can find several examples about this in the "Rampup Guide".


## Version 2 {% include anchor.html name="version2x" %}

__Step 1: OneOffixxAdmin.config__

The first step is to check if the file "OneOffixxAdmin.config" is containing configuration parameters.

The "Rampup Guide" will be displayed immediately if this is not the case. Please take a configuration example from the "Rampup Guide" and edit the file "OneOffixxAdmin.config" manually or make use of the "Config-Editor".

__Editing OneOffixxAdmin.config manually:__

OneOffixxAdmin.config is located in the Admin file of your OneOffixx installation.

The most important configuration item is ConnectionString, which leads to the OneOffixx production database later on, and has to be addressed as follows:

    Data Source=localhost;InitialCatalog=oneoffixx;UserID=[user];Password=[PW];MultipleActiveResultSets=True

If windows authentication is enabled ConnectionString will take the following form:

    Data Source=localhost;InitialCatalog=oneoffixx;Integrated Security=true;MultipleActiveResultSets=True

__Step 2: Data Source Management__
	
Open the starting page of the Admin web application now if the configuration was saved in "OneOffixxAdmin.config" (manually or with the config editor). 

Click __"Init"__ if the SQL user has __"dbcreator" permissions__ and no database has been created yet.

This will create a database including tables.

__Click the checkbox__ if you have __already created an empty database__.

The database should be created in both cases.

__Step 3: OneOffixx.config__

The actual OneOffixx applications, i.e. Service, Connect or web application, and their included "OneOffixx.config" file have to be configured in the last step. Please enter the ConnectionString for the OneOffixx production database.

__Securing Admin__

Server components are now installed successfully and configured. It is recommended to follow the instructions of the configuration wizard and unlock the OneOffixx Admin only for specific users. You can find several examples about this in the "Rampup Guide".
