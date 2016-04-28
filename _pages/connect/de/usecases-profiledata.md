---
layout: page
title: Anwendungsfälle
subtitle: Profildaten aus Fachapplikation übernehmen
permalink: "connect/de/usecases/profiledata/"
---

Profiledaten können an OneOffixx übergeben werden. Dabei muss die Kundenkonfiguration jeweils berücksichtigt werden, da jeder Kunde seine spezifische Feldkonfiguration hat.
Es gibt verschiedene Varianten wie man das Profil bestimmt. Felder werden mit dem selektierten Profile gemerged. Bilder können Base64 kodiert ebenfalls übergeben werden.

## Aktuelles Profil des Clients: 

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
    				<LanguageLcid>2055</LanguageLcid>
    			</Arguments>
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```
 
## Aktuelles Profil des Clients, mit überschriebenen Feldern: 

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

## Ein Profil über die ID auswählen (mit oder ohne überschriebenen Feldern möglich): 

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

## Ein Profil über dessen Namen auswählen (mit oder ohne überschriebenen Feldern möglich): 

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

Hinweis zu den Signern (Unterschreibenden):
Bei allen Profilen steht nur die Signer zur Verfügung die dem Profil auch angehängt sind. Bei einem anonymen Profil werden 10 leere Signer automatisch erzeugt.
