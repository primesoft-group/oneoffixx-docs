---
layout: page
title: "Functions: ProfileData"
subtitle: Profildaten aus Fachapplikation übernehmen
permalink: "connect/de/functions/profiledata/"
language: de
---

Wie bereits unter [Connect Arguments: ProfileId]({{ site.baseurl }}/connect/de/connect-arguments#profileid) erwähnt, nutzt OneOffixx das aktuelle Profil, wenn nichts spezifiziert wird. Das Profil könnte über die Profil-Id bzw. den Profilnamen explizit genannt werden. 

Bei allen Varianten können über diese Funktion Profilfelder übersteuert werden. Dabei werden die Felder mit dem selektierten Profil zusammengelegt. Bilder können base64-kodiert ebenfalls übergeben werden.

__Aktuelles Profil, mit überschriebenen Feldern:__ 

Ohne Angabe eines expliziten Profiles wird das aktuelle Profil aus dem OneOffixx Client selektiert. Dazu können noch einzelne Profil-Felder überschrieben werden.

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
    				<LanguageLcid>2055</LanguageLcid>
    			</Arguments>
    		    <Function name="ProfileData" id="5C8B5321-E02D-4A1C-80E3-627D40AEABAF">
    				<Arguments>
    					<Value key="Profile.User.FirstName">Max</Value>
    					<Value key="Profile.User.LastName">Musterman</Value>
    				</Arguments>
    		    </Function>
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

__Profilwahl über Profil-ID:__

Ein Profil kann auch über die Id ausgewählt werden. Das ist mit oder ohne überschriebenen Feldern möglich.

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
    				<ProfileId>25558547-a6fb-4fad-908b-63118dcee5c9</ProfileId>
    				<LanguageLcid>2055</LanguageLcid>
    			</Arguments>			
    		    <Function name="ProfileData" id="5C8B5321-E02D-4A1C-80E3-627D40AEABAF">
    				<Arguments>
    					<Value key="Profile.User.FirstName">Max</Value>
    					<Value key="Profile.User.LastName">Musterman</Value>
    				</Arguments>
    		    </Function>
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

__Profilwahl über Name:__

Ein Profil kann auch über dessen Name ausgewählt werden. Das ist mit oder ohne überschriebenen Feldern möglich. 

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
    				<ProfileId>Profile Name</ProfileId>
    				<LanguageLcid>2055</LanguageLcid>
    			</Arguments>			
    		    <Function name="ProfileData" id="5C8B5321-E02D-4A1C-80E3-627D40AEABAF">
    				<Arguments>
    					<Value key="Profile.User.FirstName">Max</Value>
    					<Value key="Profile.User.LastName">Musterman</Value>
    				</Arguments>
    		    </Function>
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

Hinweis zu den Unterschreibenden (Signer):
Bei allen Profilen stehen nur diejenigen Signer zur Verfügung, die im Unterschriftenprofil, des jeweiligen Profiles, enthalten sind. Bei einem anonymen Profil werden automatisch 10 leere Signer erzeugt.
