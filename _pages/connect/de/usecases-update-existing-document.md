---
layout: page
title: Anwendungsfälle
subtitle: Bestehendes Dokument aktualisieren und/oder ergänzen
permalink: "connect/de/usecases/update-existing-documents/"
language: de
---

Ein Dokument soll generiert werden und die Daten innerhalb dieses Dokumentes sollen aktualisiert werden. Im Argument DocumentLocation wird der Pfad und Dateiname der Datei angegeben. OneOffixx lädt diese Datei, ermittelt daraus die TemplateId und die Dokumentsprache und aktualisiert anschliessend das Dokument.

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<DocumentLocation>c:\Documents\..\foobar.docx</DocumentLocation>
    			</Arguments>
    
    			<Function name="String" id="String">
    				… Zu aktualisierende Daten
    			</Function>
    
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

Der Dokumentenpipeline wird das Command „ConnectUpdate" gesendet (intern). Dadurch wird jede Dokumentfunktion angewiesen, ihre Daten im Dokument zu aktualisieren.
