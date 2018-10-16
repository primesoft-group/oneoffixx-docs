---
layout: page
title: Anwendungsfälle
subtitle: Vorlagen filtern mittels Tags
permalink: "connect/de/usecases/templatepicker/"
language: de
---

Anstelle der Id der zu öffnenden Vorlage, können im Connect mithilfe von Tags auch Filterkriterien angegeben werden:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<TemplateFilter>
    					<Tag>Tag1</Tag>
    					<Tag>Tag2;Tag3;Tag4</Tag>
    				</TemplateFilter>
    			</Arguments>
    			<Commands>
    				<Command Name="DefaultProcess">
    					<Parameters>
    						<Add Key="Start">true</Add>
    					</Parameters>
    				</Command>
    			</Commands>
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

AND-Verknüpfungen werden innerhalb eines Tag-Elements durch Semikolons getrennt definiert, OR-Verknüpfungen durch mehrere Tag-Elemente. Das obige Beispiel zeigt alle Vorlagen, die mit Tag1 oder Tag2, Tag3 und Tag4 markiert sind. Gibt es mehrere Vorlagen, die den Filterkriterien entsprechen, öffnet sich ein Auswahldialog, der Template-Picker. Hier kann der Benutzer die gewünschte Vorlage auswählen:

![x]({{ site.baseurl }}/assets/content-images/connect/de/templatepicker.png "TemplatePicker")

