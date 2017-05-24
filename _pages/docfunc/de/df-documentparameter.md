---
layout: page
title: Dokumentenparameter
permalink: "docfunc/de/df/documentparameter"
language: de
---

In der Dokumentfunktion ‘Dokument Parameter’ kann die Eingabemaske konfiguriert werden, die beim Anwählen einer Vorlage erscheint. Die Konfiguration kann grob in drei Teile unterteilt werden: oben bei den ‘DataNodes’ werden die Nodes definiert, auf die in der ‘View’ im unteren Teil zugegriffen wird. In der View wird das Aussehen des Dokumentparameters festgelegt. Im DataSources-Part können Datenbank Abfragen definiert werden, und die Werte aus der Abfrage auf die unter DataNodes definierten CustomElements geschrieben werden.

Grundgerüst:
```xml
<Configuration>	<!-- Dies ist der Root Node der Konfiguration -->
	<!--
		Zwingende Komponente, ohne DataNodes kann keine View aufgebaut werden
	-->
	<CustomContentSection>
		<DataNodes>
			<!-- CustomDataNodes werden hier Definiert -->
		</DataNodes>
	</CustomContentSection>
	<!--
		Zwingende Komponente, ohne View gibt es keinen Dialog
	-->
	<Views>
		<View>
			<!-- Hier wird das Aussehen des Dialoges Definiert -->
		</view>
	</Views>
	<!-- 
		Optionale Komponente
	-->
	<DataSources>
		<SqlDataSource>
		
		</SqlDataSource>
	</DataSources>
</Configuration>
```

Eine der ersten Zeilen ist die CustomContentSection. Darin können die Grösse und Name des Dokument Parameters festgelegt werden. Über das 'Name' Attribut kann der Fenstername gewählt werden. Mit 'WindowWidth' und 'WindowHeight' können die Breite, resp. die Höhe des Fensters angepasst werden.
Das Attribut "WindowHeight" muss zwingend gesetzt sein, ansonsten wird der Dialog nicht richtig angezeigt.

Beispiel:
```xml
<CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
```

## Die DataNodes

In der folgenden Tabelle werden die verschiedenen Arten von CustomDataNodes erklärt.

{:.table .table-striped}
|  Typ     |  Beschreibung  |             
|  --- 	|  ---	|    
|  Textfeld (TextNode) | `<CustomDataNode xsi:type="TextNode" Id="DocParam.Subject" LCID="2055">Standardtext</CustomDataNode>`{:.language-xml}    |   
|  CheckBox (CheckBoxNode) | `<CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.IsAdultFromDB"  IsChecked="false"  LCID="2055" />`{:.language-xml}  |    
|  ComboBox	(ComboBoxNode)	| ` <CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.NameListFromDB"    LCID="2055" SelectedValue="default">`<br>`<ListItems>`<br>`<Item>`<br>`<Key><string>empty</string></Key>`<br>`<Value><string>default</string></Value>`<br>`</Item>`<br>`</ListItems>`<br>`</CustomDataNode>`{:.language-xml}   |    
|  |  `<CustomDataNode xsi:type="TextNode" Id="DocParam.Betreff" Regex="^[0-9]+$" ValidationMessage="Geben Sie eine gültige Zahl an" LCID="2055">42</CustomDataNode>`{:.language-xml}  |   
|  |  Pflichfeld und validiert |  
|  |  `<CustomDataNode xsi:type="TextNode" Id="DocParam.Zahl" Required="true" ValidationMessage="Das Betreff-Feld darf nicht leer sein." LCID="2055" />`{:.language-xml}  |
|  |  Pflichtfeld mit bestimmten Format und validiert |
|  |  `<CustomDataNode xsi:type="TextNode" Id="DocParam.Zahl" Required="true" Regex="^[0-9]+$" ValidationMessage="Das Betreff-Feld darf nicht leer sein." LCID="2055" />`{:.language-xml}  |
|  |  Über Quickcheck aufrufbar (Tracked-Dokument-Parameter) |
|  |  `<CustomDataNode xsi:type="TextNode" Id="DocParam.Tracked.Kosten" Tracked="true" Label="Gesamtkosten" LCID="2055" />`{:.langauge-xml}  |
