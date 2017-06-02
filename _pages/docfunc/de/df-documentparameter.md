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


{:.table .table-striped}
|  __Name__  |  Beschreibung  |
|  ----  | ----  |
|   Name (Fenstername)  |    Über das Attribut "Name" kann der Name des Dokument-Parameter-Dialog-Fensters definiert werden.  |  
| WindowWidth (Fensterbreite) |  Über das Attribut "WindowWidth" kann die Fensterbreite in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. |
| WindowHeight (Fensterhöhe) |  Über das Attribut "WindowHeight" kann die Fensterhöhe in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. |

### Die DataNodes und deren Attribute

  In diesem Abschnitt geht es um die Konfiguration zwischen <DataNodes> und </DataNodes>.
  Jedes CustomDataNode definiert ein Dokument-Parameter-Feld, auf das im Editor, in Skripts
  oder über Extended Bindings zugegriffen werden kann.
  Für jedes Feld in den Views (siehe 4. Views) muss für die Weiterverwendung der Eingabe ein
  CustomDataNode angelegt werden.

In der folgenden Tabelle werden die verschiedenen Arten von CustomDataNodes aufgelistet.

{:.table .table-striped}
|  __Typ__     |  __Grundstruktur__  |             
|  --- 	|  ---	|    
|  Textfeld (TextNode) | `<CustomDataNode xsi:type="TextNode" Id="DocParam.TextNode" LCID="2055">Standardtext</CustomDataNode>`{:.language-xml}    |   
|  Kontrollkästchen (CheckBoxNode) | `<CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.Checkbox"  IsChecked="false"  LCID="2055" />`{:.language-xml}  |    
|  Kombinationsfeld	(ComboBoxNode)	| `<CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.ComboBoxNode"  LCID="2055" SelectedValue="default">`{:.language-xml}<br>&nbsp;&nbsp;`<ListItems>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;&nbsp;`<Item>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<Key><string>empty</string></Key>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<Value><string>default</string></Value>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;&nbsp;`</Item>`{:.language-xml}<br>&nbsp;&nbsp;`</ListItems>`{:.language-xml}<br>`</CustomDataNode>`{:.language-xml}   |    
|  Datumsfeld (DateTimeNode)  |  '<CustomDataNode xsi:type="DateTimeNode" Id="DocParam.DefinitionTime" LCID="2055" DateFormat="d. MMMM yyyy" Calendar="Gregor">'{:.language-xml}<br>`<DateTime>2015-02-15</DateTime>`{:.language-xml}<br>`</CustomDataNode>`{:.language-xml}  |
|  Mit heutigem Datum als standardwert |  '<CustomDataNode xsi:type="DateTimeNode" Id="DocParam.DefinitionTime" LCID="2055" DateFormat="d. MMMM yyyy" Calendar="Gregor" IsNowDefault="true"></CustomDataNode>`{:.language-xml}  |

###CustomDataNode-Attribute (bei Verwendung von Views)
 