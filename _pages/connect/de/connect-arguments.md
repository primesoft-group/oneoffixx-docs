---
layout: page
title: Connect Arguments
permalink: "connect/de/connect-arguments/"
subtitle: "//OneOffixxConnectBatch/Entries/OneOffixxConnect/Arguments"
language: de
---

Über die Connect Argumente kann die Vorlage, die Sprache, das Profil, die OE und andere Parameter genau definiert werden.


## TemplateId - Vorlage definieren {% include anchor.html name="templateid" %}
	
Über die __TemplateId__ wird die Vorlage für die Dokumentverarbeitung gewählt. Als Angabe dafür muss die genaue GUID der Vorlage übergeben werden.

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				...
    				<TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
``` 

## TemplateTags - Vorlage definieren {% include anchor.html name="templatetags" %}
	
Anstelle der Id der zu öffnenden Vorlage können über __TemplateFilter__ auch in der Vorlage hinterlegte Tags angegeben werden:

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<TemplateFilter>
    					<Tag>Tag1</Tag>
    					<Tag>Tag2;Tag3;Tag4</Tag>
    				</TemplateFilter>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
``` 

AND-Verknüpfungen werden innerhalb eines Tag-Elements durch Semikolons getrennt definiert, OR-Verknüpfungen durch mehrere Tag-Elemente. 
Das obige Beispiel zeigt alle Vorlagen, welche mit Tag1 oder Tag2, Tag3 und Tag4 markiert sind. 
Gibt es mehrere Vorlagen, welche den Filterkriterien entsprechen, öffnet sich ein Auswahldialog, durch den der Benutzer die gewünschte Vorlage auswählen kann:

![x]({{ site.baseurl }}/assets/content-images/connect/de/templatepicker.png "TemplatePicker")

<span class="label label-info">NEU ab 2.3.40160</span>

TemplateTags können auch serverseitig genutzt werden. Falls es mehrere Vorlagen gibt, die dem Filterkriterium entsprechen, wird stets der erste Eintrag genommen. Die Reihenfolge ist dabei nicht garantiert!

## LanguageLcid - Sprache definieren {% include anchor.html name="languagelcid" %}

Über __LanguageLcid__ wird die Dokumentsprache für die Verarbeitung gesetzt. Es muss eine genaue LCID angegeben werden. Meistgenutzte LCIDs:

{:.table .table-striped}
| __LCID__ | __Sprache__ 
| --- | ---- | --- 
| 2055 | Deutsch - Schweiz 
| 1031 | Deutsch - Deutschland 
| 4108 | Französisch - Schweiz 
| 2064 | Italienisch - Schweiz 
| 1033 | Englisch - USA 
| 2057 | Englisch - UK 

Alle anderen LCIDs finden sie [__hier__](https://msdn.microsoft.com/de-ch/goglobal/bb964664.aspx).

Die Sprache hat z. B. Auswirkungen auf die gewählten Textbausteine oder die Funktionsweise von Dokumentfunktionen.

{% include alert.html type="info" text="Bei der Angabe einer TemplateId muss sichergestellt werden, dass diese Vorlage auch für diese Sprache freigegeben ist. Über TemplateTags gibts es einen indirekten Mechanismus, welcher die richtige Vorlage für die angegebene Sprache sucht." %}

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				...
    				<LanguageLcid>2055</LanguageLcid>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

## DocumentLocation - Bestehendes Dokument aktualisieren {% include anchor.html name="documentlocation" %}

Über die __DocumentLocation__ können [bestehende Dokumente aktualisiert]({{ site.baseurl }}/connect/de/usecases/update-existing-documents/) oder [zwei bestehende Dokumente verbunden]({{ site.baseurl }}/connect/de/usecases/merge-documents/) werden.

{% include alert.html type="info" text="Für den vollen Funktionsumfang müssen die Dokumente von OneOffixx generiert wurden sein." %}

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<DocumentLocation>c:\Temp\Doc1.docx</DocumentLocation>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
``` 

## ProfileId - Profilwahl {% include anchor.html name="profileid" %}

Über das __ProfileId__-Element kann ein bestimmtes Profil angegeben werden. Dafür wird entweder die __Id des Profiles__ oder der __Profilname__ benötigt. Ohne Angabe eines expliziten Profiles, wird das aktuelle Profile vom OneOffixx Client genommen bzw. auf Serverseite das erste Profil des jeweiligen Users. 

Mittels ProfileId:
```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<ProfileId>25558547-a6fb-4fad-908b-63118dcee5c9</ProfileId>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
``` 

...oder über den Profilnamen:

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<ProfileId>Profil Name</ProfileId>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
``` 

## OrganizationId - Profilwahl {% include anchor.html name="profile" %}

<span class="label label-info">NEU ab 2.3.40160</span>

Diese Option erlaubt es, eine beliebige (freigegebene) Organisation in der  [__ProfileData-Dokumentfunktion__]({{ site.baseurl }}/connect/de/functions/profiledata/) zu nutzen.
Wird die angegebene Organisation gefunden, werden für den Aufruf die entsprechenden Organisationsdaten genutzt. 

Die Organisation kann dabei über die interne Id gesucht werden:

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<Profile>
					<OrganizationId>25558547-a6fb-4fad-908b-63118dcee5c9</OrganizationId>
				</Profile>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
``` 

...oder über eine Abfrage: 

Abfragesyntax:

    { *Feldname* = *Wert* }

Im Feldnamen können alle konfigurierten Felder für Organisationseinheiten genutzt werden. Werden mehrere Organisationen gefunden, wird die erste genommen, wobei keine Reihenfolge garantiert ist.

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<Profile>
					<OrganizationId>{Org.Name = IT}</OrganizationId>
				</Profile>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
``` 

## Version {% include anchor.html name="version" %}

{% include new-badge.html version="3.3.1" %}

Neu kann über das Version-Element eine bestimmte Version der Vorlage ausgewählt werden:

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<Version>Draft</Version>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```
Dabei stehen folgende Werte zur Verfügung:

{:.table .table-striped}
| Wert | Id-Typ | Version der ausgewählen Vorlage | Aufgelöste Version der Abhängigkeiten | Template-Picker
| ---  | ---- 	| --- 							 | --- 									 | --- 				|
| Published 	| Template-Id 					| Published 							| Published | Ja
| PublishedDraft | Template-Id 					| Published 							| Draft | Ja
| Draft 		| Template-Id 					| Draft 								| Draft | Ja
| SpecificDraft | Versions-Template-Id 			| Specific 								| Draft | Nein
| SpecificPublished | Versions-Template-Id 		| Specific 								| Published | Nein

## Editor {% include anchor.html name="editor" %}

{% include new-badge.html version="3.3.1" %}

Das Editor-Element erlaubt es, die Vorlage via Connect im Editor zu öffnen:

```xml
    <OneOffixxConnectBatch>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<Editor>true</Editor>
    			</Arguments>
    			...
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

Mittels der Version-Angabe kann exakt gesteuert werden, welche Version der Vorlage dabei im Editor geöffnet wird. Wenn mit Filter oder ohne TemplateId aufgerufen, kann dazu auch der TemplatePicker benutzt werden.