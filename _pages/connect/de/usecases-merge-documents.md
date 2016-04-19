---
layout: page
title: Anwendungsfälle - Verbinden von Dokumenten
permalink: "connect/de/usecases/merge-documents/"
---

OneOffixx ist in der Lage, verschiedene Dokumente desselben Typs miteinander zu verbinden. Jedes einzelne Dokument wird als OneOffixx Connect Entry übergeben. Als globales Kommando muss „Merge“ oder „AltChunkMerge“ angegeben werden.

    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Commands>
    		<Command Name="Merge">
    			<Parameters>
    				<Add key="PageNumberStart">123</Add>
    				<Add key="Filename">c:\Temp\MergedDocument.docx</Add>
    			</Parameters>
    		</Command>
    		<Command Name="DefaultProcess">
    			<Parameters>
    				<Add key="Start">true</Add>
    			</Parameters>
    		</Command>
    	</Commands>
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<DocumentLocation>c:\Temp\Dok1.docx</DocumentLocation>
    			</Arguments>
    		</OneOffixxConnect>
    		<OneOffixxConnect>
    			<Arguments>
    				<DocumentLocation>c:\Temp\Dok2.docx</DocumentLocation>
    			</Arguments>
    		</OneOffixxConnect>
    		<OneOffixxConnect>
    			<Arguments>
    				<DocumentLocation>c:\Temp\Dok3.docx</DocumentLocation>
    			</Arguments>
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>

Merge verbindet Dokumente mit Header und Footer; AltChunkMerge nur den Dokumenteninhalt.
