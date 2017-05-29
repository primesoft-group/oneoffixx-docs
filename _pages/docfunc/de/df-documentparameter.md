---
layout: page
title: Dokumentenparameter
permalink: "docfunc/de/df/documentparameter"
language: de
---

In der Dokumentfunktion ‘Dokument Parameter’ kann die Eingabemaske konfiguriert werden, die beim Anwählen einer Vorlage erscheint. Die Konfiguration kann grob in drei Teile unterteilt werden: oben bei den ‘DataNodes’ werden die Nodes definiert, auf die in der ‘View’ im unteren Teil zugegriffen wird. In der View wird das Aussehen des Dokumentparameters festgelegt. Im DataSources-Part können Datenbank Abfragen definiert werden, und die Werte aus der Abfrage auf die unter DataNodes definierten CustomElements geschrieben werden.

Grundgerüst mit Verwendung von Views:
```xml
<Configuration>	<!-- Dies ist der Root Node der Konfiguration -->
	<!-- Zwingende Komponente, ohne DataNodes kann keine View aufgebaut werden	-->
	<CustomContentSection>
		<DataNodes>
			<!-- CustomDataNodes werden hier Definiert -->
		</DataNodes>
	</CustomContentSection>
	<!-- Zwingende Komponente, ohne View gibt es keinen Dialog -->
	<Views>
		<View>
			<!-- Hier wird das Aussehen des Dialoges Definiert -->
		</view>
	</Views>
	<!-- Optionale Komponente -->
	<DataSources>
		<SqlDataSource>
		
		</SqlDataSource>
	</DataSources>
</Configuration>
```

Grundgerüst ohne Verwendung von Views:
```xml
<Configuration>	<!-- Dies ist der Root Node der Konfiguration -->
	<!-- Zwingende Komponente, ohne DataNodes kann keine View aufgebaut werden	-->
	<CustomContentSection>
		<DataNodes>
			<!-- CustomDataNodes werden hier Definiert -->
		</DataNodes>
	</CustomContentSection>	
	<!-- Optionale Komponente -->
	<DataSources>
		<SqlDataSource>
		
		</SqlDataSource>
	</DataSources>
</Configuration>
```

__Attribute von CustomContentSection__  

Beispiel:
```xml
<CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
```

|  __Name__  |  Beschreibung  |
|  ----  | ----  |
|   Name (Fenstername)  |    Über das Attribut "WindowWidth" kann die der Name des Dokument-Parameter-Dialog-Fensters definiert werden.  |  
| WindowWidth (Fensterbreite) |  Über das Attribut "WindowWidth" kann die Fensterbreite in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. |
| WindowHeight (Fensterhöhe) |  Über das Attribut "WindowHeight" kann die Fensterhöhe in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. |

## Die DataNodes

In der folgenden Tabelle werden die verschiedenen Arten von CustomDataNodes erklärt.

{:.table .table-striped}
|  Typ     |  Grundstruktur  |             
|  --- 	|  ---	|    
|  Textfeld (TextNode) | `<CustomDataNode xsi:type="TextNode" Id="DocParam.TextNode" LCID="2055">Standardtext</CustomDataNode>`{:.language-xml}    |   
|  CheckBox (CheckBoxNode) | `<CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.Checkbox"  IsChecked="false"  LCID="2055" />`{:.language-xml}  |    
|  ComboBox	(ComboBoxNode)	| `<CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.ComboBoxNode"  LCID="2055" SelectedValue="default">`{:.language-xml}<br>&nbsp;&nbsp;`<ListItems>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;&nbsp;`<Item>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<Key><string>empty</string></Key>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<Value><string>default</string></Value>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;&nbsp;`</Item>`{:.language-xml}<br>&nbsp;&nbsp;`</ListItems>`{:.language-xml}<br>`</CustomDataNode>`{:.language-xml}   |    
|  |  `<CustomDataNode xsi:type="TextNode" Id="DocParam.Betreff" Regex="^[0-9]+$" ValidationMessage="Geben Sie eine gültige Zahl an" LCID="2055">42</CustomDataNode>`{:.language-xml}  |   
|  |  Pflichfeld und validiert |  
|  |  `<CustomDataNode xsi:type="TextNode" Id="DocParam.Zahl" Required="true" ValidationMessage="Das Betreff-Feld darf nicht leer sein." LCID="2055" />`{:.language-xml}  |
|  |  Pflichtfeld mit bestimmten Format und validiert |
|  |  `<CustomDataNode xsi:type="TextNode" Id="DocParam.Zahl" Required="true" Regex="^[0-9]+$" ValidationMessage="Das Betreff-Feld darf nicht leer sein." LCID="2055" />`{:.language-xml}  |
|  |  Über Quickcheck aufrufbar (Tracked-Dokument-Parameter) |
|  |  `<CustomDataNode xsi:type="TextNode" Id="DocParam.Tracked.Kosten" Tracked="true" Label="Gesamtkosten" LCID="2055" />`{:.langauge-xml}  |
