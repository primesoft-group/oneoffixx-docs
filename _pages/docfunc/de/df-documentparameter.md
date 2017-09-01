---
layout: page
title: Dokumentenparameter
permalink: "docfunc/de/df/documentparameter"
language: de
---

## Übersicht
<!-- TOC -->

- [Übersicht](#übersicht)
- [Die DataNodes und deren Attribute](#die-datanodes-und-deren-attribute)
- [Views](#views)
- [Bindings](#bindings)
- [Calc-Erweiterung für Bindings](#calc-erweiterung-für-bindings)
- [DataSources](#datasources)
- [Beispiele](#beispiele)

<!-- /TOC -->

In der Dokumentfunktion ‘Dokument Parameter’ kann die Eingabemaske konfiguriert werden, die beim Anwählen einer Vorlage erscheint. Die Konfiguration kann grob in drei Teile unterteilt werden: oben bei den ‘DataNodes’ werden die Nodes definiert, auf die in der ‘View’ im unteren Teil zugegriffen wird. In der View wird das Aussehen des Dokumentparameters festgelegt. Im DataSources-Part können Datenbank Abfragen definiert werden, und die Werte aus der Abfrage auf die unter DataNodes definierten CustomElements geschrieben werden.

Grundgerüst __mit__ Verwendung von __Views__:
```xml
<Configuration>	<!-- Dies ist der Root Node der Konfiguration -->
	<!-- Zwingende Komponente, ohne DataNodes kann keine View aufgebaut werden	-->
	<CustomContentSection>
		<DataNodes>
    <!-- ↓ Bewirkt, dass der DocParam-Button in Word angewählt werden kann (nur bei Verwendung von Views nötig). -->
    <CustomDataNode xsi:type="TextNode" Id="DocParam.EnableDocParamButton" Visible="true"  LCID="2055" />
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

Grundgerüst __ohne__ Verwendung von __Views__:
```xml
<Configuration>	<!-- Dies ist der Root Node der Konfiguration -->
	<!-- Zwingende Komponente, ohne DataNodes kann keine View aufgebaut werden	-->
	<CustomContentSection>
		<DataNodes>
			<!-- CustomDataNodes und das Aussehen des Dialoges werden hier Definiert -->
		</DataNodes>
	</CustomContentSection>	
	<!-- Optionale Komponente -->
	<DataSources>
		<SqlDataSource>
		
		</SqlDataSource>
	</DataSources>
</Configuration>
```

Am Ende dieser Seite befinden sich einige Beispiele, um die Verwendung der DataNodes mit und ohne Views zu veranschaulichen.

__Attribute von CustomContentSection__  

Beispiel:
```xml
<CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
```

{:.table .table-striped}
|  __Name__  |  __Beschreibung__  |
|  ----  | ----  |
|   Name (Fenstername)        |    Über das Attribut "Name" kann der Name des Dokument-Parameter-Dialog-Fensters definiert werden.  |  
| WindowWidth (Fensterbreite) |  Über das Attribut "WindowWidth" kann die Fensterbreite in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. |
| WindowHeight (Fensterhöhe)  |  Über das Attribut "WindowHeight" kann die Fensterhöhe in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. Der Wert für WindowHeigth muss zwingend gesetzt sein. (Gilt für Verwendung mit und Ohne Views). Wenn der Inhalt die definierte WindowHeight überschreitet, wird automatisch eine Scrollleiste eingefügt. |

## Die DataNodes und deren Attribute

  In diesem Abschnitt geht es um die Konfiguration zwischen `<DataNodes>` und `</DataNodes>`.
  Jedes CustomDataNode definiert ein Dokument-Parameter-Feld, auf das im Editor, in Skripts
  oder über Extended Bindings zugegriffen werden kann.
  Für jedes Feld in den Views (siehe [Views](#views)) muss für die Weiterverwendung der Eingabe ein
  CustomDataNode angelegt werden.

__Grundgerüst eines CustomDataNodes:__

```xml
  <CustomDataNode xsi:type="" Id="" LCID=""></CustomDataNode>
```

Diese drei Attribute müssen unabhängig vom Typ auf jeden Fall vorhanden sein, ansonsten wird der DataNode nicht richtig funktionieren.

__CustomDataNode-Basisattribute (gelten für Verwendung mit und ohne Views)__  

{:.table .table-striped}  
|  __Name__                     		 |  __Beschreibung__  |
|    ----								 |        ----        |
| Type (xsi:type)						 | __TextNode__<br>Wird in Word zu einem Nur-Text-Inhaltssteuerelement (Plain Text Content Control), für ein- oder mehrzeilige Text-Eingabe, Überprüfung via Regex möglich<br><br>__CheckBoxNode__<br>Wird in Word zu einem Kontrollkästchensteuerelement (Check Box Content Control), für ja/nein-Auswahl<br><br>__DateTimeNode__<br>Wird in Word zu einem Datumsauswahl-Inhaltssteuerelement (Date Picker Content Control), für Datumsfeld mit Kalenderauswahl<br><br>__ComboBoxNode__ <br> Wird in Word zu einem Kombinationsfeld-Inhaltssteuerelement (Combo Box Content Control), für die Auswahl zwischen vorgegebenen Werten (beliebige Eingaben in Word zulässig)<br><br>__LabelNode__ <br> Überschrift im Dokument-Parameter-Dialog wenn Views nicht verwendet werden, nicht für die Verwendung im Editor, in Skripts und in Extended Bindings geeignet <br><br> __*RadioButton*__ <br>Es gibt keinen RadioButton-Typ. Der Grund ist, dass es in Word keine RadioButton-Inhaltssteuerelemente gibt. Trotzdem benötigen RadioButtons ein CustomDataNode, damit die Auswahl in der View gespeichert werden kann für die Verwendung im Editor, in Skripts und in Extended Bindings. <br><br> __Mögliche CustomDataNode-Typen für das Speichern der Auswahl von RadioButtons:__ <br><br>__Als Textnode__ <br> In diesem Fall wird der Value des in der View ausgewählten RadioButtons im TextNode gespeichert. Dies ist für Dokument-Parameter geeignet, die nicht in Word eingefügt werden sondern nur für den Zugriff via Skript oder Extended Binding erstellt wurden. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons als Standard-Text konfiguriert werden, also: <br> `<CustomDataNode xsi:type="TextNode" Id="DocParam.RadioButtonGender" LCID="2055">ValueDesEntsprechendenRadioButtons</CustomDataNode>`{:.language-xml} <br><br> __Als ComboBoxNode__ <br> In diesem Fall wird der ComboBoxNode-Eintrag ausgewählt, bei dem der Key genau dem Value des RadioButtons entspricht. Dies ist auch für Dokument-Parameter geeignet, welche in Word eingefügt werden, da die Anzeige im Dokument über den Value des ComboBoxNode-Eintrags gesteuert wird. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons im SelectedValue-Attribut der ComboBoxNode konfiguriert werden, also: <br> `<CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.RadioButtonGender" LCID="2055" SelectedValue="ValueDesEntsprechendenRadioButtons">...</CustomDataNode>`{:.language-xml} <br><br> Wie die RadioButtons dann in der View definiert werden, wird im entsprechenden Kapitel beschrieben. <br><br>__Ohne Views können keine RadioButtons definiert werden__  |  
|  Label (Beschriftung)        			 |  Beschriftung des Elements im Quick Check-Panel, wenn es sich um einen Tracked-Dokument-Parameter handelt.  |
|  Required (benötigtes Feld)  			 |   Attribut nur für Elemente des Typs Textfelder zulässig. Definiert ob das Feld leer gelassen werden kann (Required="false" oder nicht gesetzt) oder ob das Feld ausgefüllt werden muss (Required="true"). Wird von der Validierung (Regex-Attribut) übersteuert, falls eine gesetzt wird.  |  
|  Regex (Validierung)         			 |  Attribut nur für Elemente des Typs Textfelder zulässig. Erlaubt es einen Regex (.NET Syntax) zu definieren, welcher im eingegeben Text min. einen Match finden muss. Achtung: Falls der ganze Text 'gematcht' werden soll oder nur genau ein 'Match' vorhanden sein muss, muss dies vom Regex-Ausdruck definiert werden.<br><br>__Beispiele__<br>Regex="[0-9]+" erzwingt, dass min. ein Zeichen des Eingabetexts eine Ziffer sein muss. "Hallo 205" ist so z. B. eine gültige Eingabe. <br><br> Regex="^[0-9]+$" erzwingt, dass alle Zeichen des Eingabetexts Ziffern sein müssen (und dass min. 1 Ziffer vorhanden sein muss). (^ matcht den Anfang des Eingabetextes und $ das Ende) <br> [Online Tool zum erstellen von Regex](http://regexr.com/) | 
|    ValidationMessage (Fehlermeldung)   |  Attribut nur für Elemente des Typs Textfelder zulässig. Falls Required="true" oder ein Validierungs-Regex gesetzt wurde, erlaubt ValidationMessage eine benutzerdefinierte Fehlermeldung anzuzeigen, falls die Validierung fehlschlägt. Falls ValidationMessage nicht gesetzt ist, wird im Fehlerfall eine Standardmeldung angezeigt.  |
| Tracked (Überwachung mit "Quick Check")|	 Die OneOffixx-Funktion Quick Check (Inhaltssteuerelemente prüfen) wird mit dem Attribut Tracked aktiviert. Ist der Wert auf true gesetzt, wird dem Benutzer im separaten Panel das Feld angezeigt. Sofern der Inhalt des Elementes leer ist, wird das Feld im Panel rot und nach Bearbeitung grün angezeigt.	 |
|   Id (Identifikation)					 |  Textuelle Id, welche eindeutig sein muss. Diese wird im Editormodus angezeigt und danach für die Verwendung im Editor, in Skripts oder in Extended Bindings benötigt. Die Id darf keine Leerzeichen enthalten. <br>__Wenn eine Id Doppelt vorhanden ist (NICHT in der View, sondern in den CustomDataNodes), dann kann der Dokumente-Parameter-Dialog nicht geöffnet werden.__ |
| SelectedValue (Ausgewählter Eintrag)   |  Attribut nur für Elemente des Typs Kombinationsfeld (ComboBoxNode) zulässig. Über diese Option wird bestimmt, welcher Eintrag in der Liste standardmässig selektiert werden soll. |
| IsChecked (Standard-Selektion)		 |   Attribut nur für Elemente des Typs Kontrollkästchen (CheckBoxNode) zulässig. Über diese Option wird bestimmt, ob die Checkbox standardmässig selektiert oder unselektiert sein soll.  |
|  Locked (Sperrung)  					 |  Hat keine Wirkung. War ursprünglich dafür vorgesehen, dass das Inhaltssteuerelements (Content Control) in Word nicht gelöscht werden kann.  |
|    ReadOnly (nur Leserecht) 			 |	 Hat keine Wirkung. War ursprünglich dafür vorgesehen, dass das der Inhalt des Inhaltssteuerelements (Content Control) in Word nicht bearbeitet werden kann.
|    DateFormat    |    Nur für Nodes des Typen "DateTimeNode", definition des Datumsformates z.B. "dd MM yyyy" für "02.06.2016". [Liste mit Datumsformaten](https://msdn.microsoft.com/de-de/library/8kb3ddd4(v=vs.110).aspx)  |
|    IsNowDefault  |    Nur für Nodes des Typen "DateTimeNode", setzt das initiale Datum auf das aktuelle Tagesdatum.  |
|   Calendar       |    Nur für Nodes des Typen "DateTimeNode", setzt das format des Kalenders. Default ist "Gregor", muss nicht gesetzt werden. | 
|    LCID          |    Die LCID (locale identifiers) definieren die Sprachkultur des entsprechenden DataNodes. Wenn die LCID nicht gesetzt ist, funktioniert der DataNode nicht. [Liste mit den LCID-Codes](https://msdn.microsoft.com/en-us/library/ms912047(v=winembedded.10).aspx)  |  

__CustomDataNode-Zusatzattribute bei Nichtverwendung von Views__

{:.table .table-striped}  
|  __Name__                     		 	 					|  __Beschreibung__  |
|    ----								 	 					|        ----        |
| Row (Zeile) 			  					 					|  Zeile, in welcher das Element im Dokument-Parameter-Dialog angezeigt werden soll. |
| Column (Spalte)   	  				 	 					| Spalte, in welcher das Element im Dokument-Parameter-Dialog angezeigt werden soll (Startpunkt). Es sind mit der Label-Spalte 4 Spalten vorhanden. |
| ColumnSpan (Länge)      					 					|  Länge resp. Anzahl Spalten über welche sich das Element erstrecken soll.  |
|  Label (Beschriftung)   					 					| Beschriftung des Elements im Dokument-Parameter-Dialog, gilt auch für Überschriften des Typs LabelNode. Sofern mehrere Elemente in einer Zeile dargestellt werden, wird die Beschriftung des ersten Elements übernommen. Die Beschriftung erscheint immer in der Spalte ganz links. Wenn Tracked auf true gesetzt ist fungiert das Label zusätzlich als Beschriftung des Elements im Quick Check-Panel. |
|  Visible (Sichtbarkeit) 	 				 					| Wenn die Sichtbarkeit auf false gesetzt ist, wird der Dokument-Parameter im Dialog nicht angezeigt. |
|  Tooltip (Hinweis)      					 					| Hinweis, welcher angezeigt wird, wenn der Benutzer mit der Maus darüber fährt. Wird von ValidationMessage überschrieben, falls diese gesetzt ist (bei Textfeldern). |
|  IsInputEnabled (Beschriftung editierbar)  					| Attribut nur für Elemente des Typs Kontrollkästchen (CheckBoxNode) zulässig. Wenn diese Option auf true gesetzt ist, werden im Dokument-Parameter-Dialog Kontrollkästchen angezeigt, bei welchen der User die Beschriftung editieren resp. frei wählen kann.  |
|  MultiLine (Mehrzeiligkeit)				 					| Attribut nur für Elemente des Typs Textfelder (TextNode) zulässig. Erstellt mehrzeilige Textfelder wenn auf true gesetzt. |
| MultilineRows (Anzahl angezeigter Zeilen bei Mehrzeiligkeit)	| Attribut nur für Elemente des Typs Textfelder (TextNode inkl. Multiline="true") zulässig. Definiert die Anzahl angezeigter Zeilen in mehrzeiligen Textfelder (standardmässig auf 3). |
| IsSearchEnabled (Suche für Kombinationsfelder aktivieren)	 	| Attribut nur für Elemente des Typs Kombinationsfeld (ComboBoxNode) zulässig. Über diese Option wird bestimmt ob Mittels Tastatureingabe im Kombinationsfeld nach vorhandenen Einträgen gesucht werden kann. |
| IsEditable (bei Kombinationsfeld beliebige Eingabe zulassen)  | Attribut nur für Elemente des Typs Kombinationsfeld (ComboBoxNode) zulässig. Über diese Option wird bestimmt, ob der Benutzer eine beliebige Eingabe tätigen kann. Wenn dieses Attribut nicht auf true gesetzt ist kann der Benutzer nur zwischen den vorhandenen Einträgen auswählen. |


## Views  

__Grundaufbau__  

- Es kann n View Elemente geben.  
- Eine View kann n Row Elemente haben.  
- Ein View hat 4 Spalten (Columns).  

```xml
<Views IsDebug="false">
  <View Id="main" Label="Startseite">
    <Row />
    <Row />
    ...
    <Button Type="Submit" Label="OK" />
    <Button Type="Cancel" Label="Abbrechen" />
  </View>
</Views>
```

Spezial-IDs:  

- View mit "main" ==> Start-Ansicht  
- Button Type="Submit" ==> Dokument-Parameter-Dialog verlassen, weiter im Prozess  
- Button Type="Cancel" ==> Dokument-Parameter-Dialog verlassen, Abbruch des Prozesses  

__Navigations-Controls__  

- Buttons  

```xml
<Button TargetView="Final" IsDefault="true" Label="Abschluss" />
```  
  TargetView = Id des Ziel-View  
  Label = Text des Buttons  
  IsDefault = "true"/"false" - Standard-Aktion bei Enter  

Falls kein TargetView gefunden wird, sieht man nur eine weisse Fläche.

__Struktur-Controls innerhalb von Rows__  

{:.table .table-striped}  
|  __Name__                     		 	 					|  __Beschreibung__  |
|    ----								 	 					|        ----        |
|  TextBlock: Zum Darstellen von formatierten Text 				|  `<TextBlock Style="h1" Alignment="left">Hello World!</TextBlock>`{:.language-xml}<br>Style = "h1"/"h2"/"small"/""<br>Alignment = "left" (default) /"right"/"center"/"justify"  |
| 	Image: Bildanzeige											|  `<Image Height="50" Alignment="left">Base64Encoded-Image</Image>`{:.language-xml}<br>Alignment = "left"/"right"/"center" (default)<br>Height = Pixelhöhe<br>Bilddaten können auch innerhalb eines CDATA Block stehen  |
|  Separator: Trennlinie										|  `<Separator />`{:.language-xml}}  |
|  Label: Einfacher Text										|	`<Label Content="Eingabefeld" />`{:.language-xml}<br>Content = Text des Labels |

__Wert-Controls innerhalb von Rows__

Grundregel: Wenn es eine CustomDataNode mit derselben Id gibt, wird versucht dies als Datenquelle zu nutzen.
Diese Controls besitzen alle ein "Value"-Attribut, welches als initialer Wert genutzt wird.

{:.table .table-striped}  
|  __Name__                     		 	 					|  __Beschreibung__  |
|    ----								 	 					|        ----        |
|  TextBox: Einzeilige oder mehrzeilige Texteingabe				|  `<TextBox Value="Text" Id="DocParam.Subject" Lines="2" />`{:.language-xml}<br>Value = Vordefiniert, wird aber ignoriert wenn es eine CustomDataNode mit der Id gibt.<br>Lines = Anzahl an Zeilen - Standard ist 1.<br> Validierung: Verbindet man das TextBox Control an eine CustomDataNode vom Typ Text werden die Validierungsoptionen von dort übernommen.  |
|  CheckBox: Auswahlkasten - oder halt CheckBox					|  `<CheckBox Id="DocParam.Erweitert" Label="Notizen" />`{:.language-xml}<br>Label = Beschreibung, erscheint rechts von der CheckBox  |
|  ComboBox: Auswahlliste										|  `<ComboBox Value="0" IsInvalidWhenValue="0" Id="DocParam.Typ">`{:.language-xml}<br>&nbsp;`<Item Label="Bitte wählen" Value="0" />`{:.language-xml}<br>&nbsp;`<Item Label="Stufe 1" Value="1" />`{:.language-xml}`</ComboBox>`{:.language-xml} <br> Die Werte für die ComboBox können entweder im CustomDataNode definiert werden, oder in der View. Die Liste der Werte wird aus dem CustomDataNode übernommen, auch wenn in der View eine Liste definiert wurde. Wenn die Liste in der View definiert wird, dann muss der CustomDataNode ein TextNode sein, damit die Liste aus der View verwendet werden kann. Beispiele dazu finden sie am Ende dieser Seite. Wenn der CustomDataNode ein ComboBoxNode ist, dann wird das Feld bei Verwendung im Word als Auswahlbox dargestellt, wenn der CustomDataNode ein TextNode ist und die Liste der Werte in der View definiert werden, so wird bei Verwendung des Feldes im Word nur der Text der ausgewählten Option als Text abgefüllt.<br><br> Value = Ausgewähltes Element (muss als Item beschrieben sein)<br>IsInvalidWhenValue = Wenn das ausgewählte Element diesen Wert hat, ist das Control nicht "valide", d.h. man kann das Dokument nicht erzeugen<br>Item.Label = Text, welcher angezeigt wird<br>Item.Value = Wert, wenn ausgewählt<br> IsEditable = true/false - wenn true, kann selbst ein Text eingegeben werden
|  DatePicker: Datumsauswahl									|  `<DatePicker Id="DocParam.ErstellDatum" />`{:.language-xml}  |
|  RadioButton: Gruppierter Auswahlknopf 						|  `<RadioButton Id="DocParam.Level" Label="Stufe 1" Value="level1" />`{:.language-xml}<br><br>Eine RadioButton Auswahl basiert auf einen CustomDataNode. Pro Anwählbarer Option muss ein einzelnes solches RadioButton Element definiert werden. Die Id Bleibt dabei gleich, nur Label und Value sind anders<br><br>Label = Beschreibungstext, welcher rechts des Knopfs erscheint<br>Value=Wert<br><br>__Definition eines RedioButtons mit einem TextNode__<br>In diesem Fall wird der Value des in der View ausgewählten RadioButtons im TextNode gespeichert. Dies ist für Dokument-Parameter geeignet, die nicht in Word eingefügt werden sondern nur für den Zugriff via Skript oder Extended Binding erstellt wurden. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons als Standard-Text konfiguriert werden, also: <br><br>`<CustomDataNode xsi:type="TextNode" Id="DocParam.RadioButtonGender" LCID="2055">M</CustomDataNode>`{:.language-xml} <br><br> __Definition eines RadioButtons mit einem ComboBoxNode__<br>In diesem Fall wird der ComboBoxNode-Eintrag ausgewählt, bei dem der Key genau dem Value des RadioButtons entspricht. Dies ist auch für Dokument-Parameter geeignet, welche in Word eingefügt werden, da die Anzeige im Dokument über den Value des ComboBoxNode-Eintrags gesteuert wird. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons im SelectedValue-Attribut der ComboBoxNode konfiguriert werden, also:<br><br>`<CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.RadioButtonGender" LCID="2055" SelectedValue="M">`{:.language-xml}<br>&nbsp;`<ListItems>`{:.language-xml}<br>&nbsp;&nbsp;`<Item>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;`<Key><string>M</string></Key>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;`<Value><string>Männlich</string></Value>`{:.language-xml}<br>&nbsp;&nbsp;`</Item>`{:.language-xml}<br>&nbsp;&nbsp;`<Item>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;`<Key><string>W</string></Key>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;`<Value><string>Weiblich</string></Value>`{:.language-xml}<br>&nbsp;&nbsp;`</Item>`{:.language-xml}<br>&nbsp;`</ListItems>`{:.language-xml}<br>`</CustomDataNode>`{:.language-xml}<br><br>Die dazugehörige View Konfiguration der Radiobuttons (für beide Fälle) Würde dann so Aussehen:<br>`<Row>`{:.language-xml}<br>&nbsp;`<RadioButton Id="DocParam.RadioButtonGender" Value="M" Label="Männlich"></RadioButton>`{:.language-xml}<br>&nbsp;`<RadioButton Id="DocParam.RadioButtonGender" Value="W" Label="Weiblich"></RadioButton>`{:.language-xml}<br>`</Row>`{:.language-xml}<br><br>

Die Wert und Struktur-Controls können alle noch mit folgenden Attributen erweitert werden:

{:.table .table-striped}  
|  __Name__         |  __Beschreibung__  |
|    ----			|        ----        |
|   ColumnSpan		|	Gibt an wieviele Spalten das Control beansprucht (Mindestens 1, Maximal 4)  |
|  	ColumnOffset	|	Gibt an wieviele Spalten vor dem Control übersprungen werden sollen (Sogesehen der Einzug)  |
|	IsEnabled		| 	Aktiviert / Deaktiviert ("true"/"false", "1"/"0")	 			 	 	 |
|	IsVisible		|	Sichtbar / Unsichtbar ("true"/"false", "1"/"0")   |
|	Tooltip			|	Angezeigter Text wenn der Cursor über diesem Element ist  |

## Bindings 

Über "Bindings" können folgende Attribute gesteuert werden:  

- IsEnabled (gilt für alle Elemente)
- IsVisible (gilt für alle Elemente und kann ebenfalls auf eine Row angewandt werden.)
- Value (gilt für Elemente die ein "Wert" haben, TextBox/TextBlock - aber keine Buttons)
- TargetView (gilt nur für Buttons)

Bindings beziehen sich damit auf andere Werte und können diese als "Wert-Grundlage" oder abfrage nutzen.

__Bindings können nur bei Verwendung von Views eingefügt werden__

__IsEnabled/IsVisible Beispiel:__

```xml
<Button Bind="IsVisible: $('DocParam.Erweitert') != 'true'" TargetView="Final" Label=">" />
<Button Bind="IsVisible: $('DocParam.Erweitert') == 'true'" TargetView="Notizen" Label="Notizen >" />
```

Button mit Label "Notizen >" wird nur angezeigt, wenn es einen Wert "DocParam.Erweitert" mit "true" gibt. 
IsEnabled funktioniert genauso.

__TargetView Beispiel:__

```xml
<Button Bind="TargetView: $('DocParam.Type')" />
```
__Row Beispiel:__

```xml
<Row Bind="IsVisible: $('DocParam.Erweitert') == 'true'">
	<TextBlock>Nur Sichtbar wenn DocParam.Erweitert gleich true ist</TextBlock>
</Row>
```

__Vergleichsoperatoren der Bindings__

{:.table .table-striped}  
|  __Operator__         |  __Beschreibung__  |
|    ----			|        ----        |
|  != 	| 	ungleich, gilt für Text und Zahlen. |
|  ==   |	gleich, gilt für Text und Zahlen  |
| `&gt;`  für > |  grösser als. (XML-Attribute erlauben keine < oder >, daher muss `&lt;` oder `&gt;` verwendet werden)  
| `&gt;=` für >= | grösser oder gleich |
| `&lt;` für <   | kleiner als  |
| `&lt;=` für <= | kleiner oder gleich  |

Mehrere Bedingungen können mit UND oder ODER verknüpft werden.  
|| für ODER  
`&amp;&amp;` für UND (steht für &&) (XML-Attribute erlauben keine &, daher muss &amp; verwendet werden)  

Es können auch mehrere Bindings mit einem "," separiert angegeben werden:  

```xml
<TextBlock ColumnSpan="4" Bind="Value: $('DocParam.Notizen'), IsEnabled: 'false'" />
```

__Value-Bind Beispiel:__  
Werte können auch an Controls gebunden werden um z.B. bei der letzten Seite eine Übersicht der eingegeben Daten anzuzeigen:

```xml
<Row>
<Label Content="Notizen aktiv:" />
  <CheckBox IsEnabled="false" ColumnSpan="3" Bind="Value: $('DocParam.Erweitert')" />
</Row>
<Row>
 <Label Content="Notizen:" />
 <TextBlock IsEnabled="false" ColumnSpan="3" Bind="Value: $('DocParam.Notizen')" />
</Row>
<Row>
 <TextBlock>Number Input:</TextBlock>
 <TextBox Id="NumberTest" />
 <TextBlock>Number Output:</TextBlock>
 <TextBlock Bind="IsVisible: $('NumberTest') &gt;= 100">EQUAL OR OVER 100!</TextBlock>
 <TextBlock Bind="IsVisible: $('NumberTest') &lt; 100">BELOW 100!</TextBlock>
</Row>
<Row>
 <TextBlock>Number with Combine:</TextBlock>
 <TextBox Id="NumberTestA" />
 <TextBox Id="NumberTestB" />
</Row>
<Row>
 <TextBlock>Output:</TextBlock>
 <TextBlock Bind="IsVisible: $('NumberTestA') &gt; 100 &amp;&amp; $('NumberTestB') &gt; 100">Both are over 100!</TextBlock>
 <TextBlock Bind="IsVisible: $('NumberTestA') &gt; 100 || $('NumberTestB') &gt; 100">One Is over 100!</TextBlock>
</Row>
```   
  
## Calc-Erweiterung für Bindings   
<span class="label label-info">NEU ab 3.1.1</span> 

Die Wertgrundlagen für die Bindings können mit mathematischen Funktionen erweitert werden.
Das Ansprechen der Felder bleibt dabei gleich, $('DocParam.xy'). Um die Felder mathematisch miteinander zu verknüpfen, können die normalen Basisoperatorn (+-/*) verwendet werden.  

Übersicht über alle möglichen Operatoren und wie sie verwendet werden:  
 
{:.table .table-striped}  
|  __Operatoren__         |  __Beschreibung__  |  
|    ----			|        ----        |  
|  Basis-Operatoren wie +,-,*,/      |                      [Basis Operatoren](https://github.com/pieterderycke/Jace/wiki/Basic-Operations)  |
|  Standard funktionen wie Quadratwurzel, sin,tan,cos etc  | [Standard Funktionen](https://github.com/pieterderycke/Jace/wiki/Standard-Functions) | 
|  ==/!=/<= etc Operationen     |       [Boolsche Operatoren](https://github.com/pieterderycke/Jace/wiki/Boolean-Operations) 

Jeder Calc-Aufruf enthält als abschliessendes Argument den Formatierungsstring, vom Term separiert durch ein ";". Dieser wert kann weggelassen werden, das ";" ist aber zwingend.

Formatierung:   
F2 -> Zahl mit 2 Nachkommastellen (Standard)  
C2 -> Währungsformat entsprechend der CurrenThreadCulture (Ländereinstellung des PC's) mit 2 Nachkommastellen  

Komplette Liste mit Formatierungscodes: [https://msdn.microsoft.com/de-de/library/dwhawy9k(v=vs.110).aspx](https://msdn.microsoft.com/de-de/library/dwhawy9k(v=vs.110).aspx)

Syntax:

Calc(Term;Format)  
Calc($('DocParam.Field1') + $('DocParam.Field2');)  
Calc($('DocParam.Field1') + ($('DocParam.Field2') * $('DocParam.Field2'));C2)  

__WICHTIG:__   
Nach dem ";" muss entweder ein Wert, oder gar nichts stehen. Calc(Term; ) führt zu einem Fehler, richtig ist Calc(Term;)/Calc(Term;Format)  
Wird in der Calc Funktion ein Boolscher vergleich durchgeführt (Calc(DocParam.Node1 == DocParamNode2;F0)), dann muss unbedingt beachtet werden, dass die Formatierung auf "F0" gsetzt ist, denn der Rückgabewert muss 0 oder 1 sein (für true/false) und wenn als Formatierung nicht F0 angegeben ist, wird der Wert zu 1.00 formatiert, was nicht als Boolsches true erkannt wird.    
Wird der Vergleich so aufgebaut; Calc(Term;Format) == 'Value', dann muss darauf geachtet werden, dass der entsprechende Value mit dem Richtigen Format angegeben wird (Standard xx.yy), ansonsten schlägt der Vergleich fehl; 10.00 == 10 wird als false ausgewertet.  

Die verwendete Library ist fähig, Exponent-vor-Punkt-vor-Strich zu rechnen.  -> ( a + b * c) == (a + (b * c)) != ((a + b ) * c)

Das Calc-Schlüsselwort ist Case-Insensitive

Die Calc-Funktion kann auf die Attribute
 
Value  
IsEnabled  
IsVisible  

angewendet werden.  

__Beispiele__

Value-Bind:  
```xml
<Row>
 <Label Content="Addition" />
 <TextBox Id="DocParam.OutputAdd" ColumnSpan="3" Bind="Value: Calc($('DocParam.Field1') + $('DocParam.Field2');C2)" />
</Row>  
```
      
IsVisible/IsEnabled-Bind:  

```xml
<Row>
 <Label Content="IsVisible" />
 <TextBox Id="DocParam.OutputSubtract" ColumnSpan="3" Bind="IsVisible: Calc($('DocParam.Field1') - $('DocParam.Field2');C2) == 'CHF 20.00'" />
</Row>
<Row>  
 <Label Content="IsVisible" />
 <TextBox Id="DocParam.OutputSubtract" ColumnSpan="3" Bind="IsVisible: Calc($('DocParam.Field1') - $('DocParam.Field2');) == '20'" />
</Row>  
```  

Weiter bietet die Calc-Funktion die Möglichkeit, angewählte Checkboxen zu "zählen":

```xml
  <Row Bind="IsVisible: Calc($('Checkbox1') + $('Checkbox2') + $('Checkbox3') + $('Checkbox4');F0) == '2'">
    <Label Content="Label">
  </Row>
```
Der Boolsche "Checked"-Value der Checkbox wird von der Calc-Funktion in einen Integer mit Wert 0 für false(= nicht angewählt) und 1 für true(= angewählt) umgewandelt, so das die Werte zusammengerechnet werden können. Das Obige Beispiel steht für: "Wenn Zwei der Checkboxen 1-4 (welche egal) angewählt sind, dann zeige die Row mit dem Label an." Dabei muss ebenfalls auf den Formatierungswert geachtet werden: Zwingend ohne kommastellen, denn 1.00 ist nicht gleich 1, und kann dementsprechend nicht in einen Boolschen Wert zurückgewandelt werden. 

Sofern keine Standardwerte in den CustomDataNodes vorgegeben sind, werden alle Calc-Binding Werte mit 0 initialisiert.   
Insbesondere bei "IsEnabled" / "IsVisible" Bindings mit "Calc"-Bedingungen sollte man auf valide Standardwerte achten, ansonsten ist die Bedingung initial immer erfüllt.      


##  DataSources  
<span class="label label-info">NEU ab 3.1.1</span>  

Allgemein:  

Mit den DataSources kann eine Datenbankabfrage in den Dokumenteparameter eingeschleust werden. Diese Abfragen werden beim Öffnen des DokumenteParameter Dialogs,
jeh nach definiertem "Loadbehavior" (siehe Selector), aufgerufen. Die Daten aus der Abfrage können dann über das Mapping des Selectors auf CustomDataNodes gemappt werden  

Die Grundstruktur für eine DataSource-Anbindung sieht folgendermassen aus:

```xml
<DataSources>
 <DataSource>
  <ConnectionProvider />
  <ConnectionString />
  <Selector LoadBehavior="Value">
   <Query />
   <Result>
    <Map Source="ColumnName1" Target="CustomDataNode1" />
    <Map Source="ColumnName2" Target="CustomDataNode2" />
   </Result>
  </Selector>
 </DataSource>
</DataSources>
```

__DataSource__  

Der DataSource-Node kann verschieden Typen annehmen. Der Name ist im XML identisch mit den hier aufgelisteten DataSource Typen.      

__Attribute und Elemente für jeden Typ DataSource:__  

{:.table .table-striped}  
|  __Name__         |  __Beschreibung__  |  
|    ----			|        ----        |  
|  Id (Optional, Attribut)					| Gibt der DataSource eine Eindeutige Id | 
|  ConnectionProvider (Zwingend, Element) 	| Definiert den ConnectionProvider für den entsprechenden Datenbank Typ. Über diesen Provider wird die Verbindung auf die Datebank hergestellt. <br>  [Übersicht über die ConnectionProvider des .NET Frameworks :](https://msdn.microsoft.com/en-us/library/a6cd7c08(v=vs.110).aspx) |
|  ConnectionString (Zwingend, Element)		| Der Connectionstring bietet die nötigen Informationen zum Herstellen der Verbindung auf die Datenbank. jede Datenbank definiert ihr eigenes Format für den ConnectionString |
|  Selector	 (Zwingend, Element)			| Definiert die Datenbankabfrage (Query) und das entsprechende Mapping auf die DataNodes  |
	
__Datenbanktypen und ihre typenspezifische Attribute__     

{:.table .table-striped}  
|  __Typ__         |  __Attribute__  |  
|    ----			|        ----        |  
| SqlDataSource  |  __SafeQuery__ <br> Wenn der Wert auf true gesetzt ist (standard), dann werden etwaige Parameter (siehe Selector--> Query) in der Query nicht mit den aktuellen Werten ersetzt, sondern es wird eine Parameter Liste mit dem Key Value paar an die Datenbank gesendet, und diese ersetzt dann die Werte in der Query. Dadurch entsteht eine erhöhte Sicherheit betreffend SQL-Injection


__Selector__    

Der Selector definiert den Ausführzeitpunkt, die auszuführende Datenbankabfrage und das Enstprechende Mapping auf die CustomDataNodes. Eine DataSource kann beliebig viele Selectoren enthalten  

{:.table .table-striped}  
|  __Name__         |  __Beschreibung__  |  
|    ----			|        ----        |  
|  Id (Optional, Attribut)					| Innerhalb einer DataSource eineindeutig | 
| LoadBehavior (Zwingend, Attribut) 		| Definiert bei welcher Art von Aufruf des DP die abfrage ausgelöst werden soll. Die möglichen LoadBehaviors sind: <br>OnlyOnce (bei erster initierung des DP) <br> Always (immer wenn das DocParam Modul aufgerufen wird).
|  Query (Zwingend, Element)				| Die Abfrage welche auf der Datenbank ausgeführt wird. Mit {} können Platzhalter eingesetzt werden, und so z.B. auf den Wert eines CustomElements verweisen => {DocParam.ValueToInject}. Wenn Platzhalter eingesetzt werden, muss beachtet werden, dass die CustomElements welche angesprochen werden einen Validen Standardwert haben, ansonsten kann es sein, dass die Abfrage Fehlschlägt, was dazu führen kann, dass das Öffnen des Dokumenteparameter Dialoges fehlschlägt. Wenn in der Query ein < oder ein > verwendet wird, dann muss diese in einem `<![CDATA[InsertQueryHere]]>` tag stehen.|
|  Result (Zwingend, Element) 		 		| Das Result Element des Selectors enthält die Informationen, wie die Werte aus der Datenbank auf die CustomElements gemappt werden sollen. Für jedes `<Map Source="DBColName" Target="CustomDataNodeName">`{:.language-xml} wird der Wert aus der angegbenen Spalte der Abfrage (Source) in den entsprechenden CustomDataNode (Target) geschrieben.<br><br>Der Wert aus der Query kann auf Jeden Typ von CustomDataNode gemappt werden. Bei Abfragen mit mehreren Datensätzen als resultat, kann auch auf eine Liste (z.B. ComboBox) gemappt werden. Wird eine Liste zurückgegeben und versucht auf z.B. einen Textnode zu mappen, wird nur der Erste Wert aus der Query gemappt, der Rest wird ignoriert.  |

__Beispiel mit einer SqlDataSource__  

```xml
<DataSources> 
  <SqlDataSource Id="DataSource1">
    <ConnectionProvider>System.Data.SqlClient</ConnectionProvider>    
    <ConnectionString>server=DbServer\SqlServerInstance;database=DbName;Trusted_Connection=True;</ConnectionString>
    <Selector LoadBehavior="OnlyOnce">
      <Query><![CDATA[SELECT Name, LastName, Nr, BirthDate, IsAdult, Gender FROM dbo.Users WHERE Id = 2]]></Query>
      <Result>
        <Map Source="Name" Target="DocParam.NameFromDB" />
        <Map Source="LastName" Target="DocParam.LastNameFromDB" />
        <Map Source="Nr" Target="DocParam.NrFromDB" />
        <Map Source="BirthDate" Target="DocParam.CreationTime" />
        <Map Source="IsAdult" Target="DocParam.IsAdultFromDB" />
        <Map Source="Gender" Target="DocParam.GenderFromDB" />         
      </Result>
    </Selector>    
  </SqlDataSource>    
</DataSources>
```

## Beispiele

__Konfiguration eines einfachen DokumentParameter mit Verwendung von Views__

```xml
<Configuration>
  <CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
    <DataNodes>
      <!-- ↓ Bewirkt, dass der DocParam-Button in Word angewählt werden kann (nur bei Verwendung von Views nötig). -->
      <CustomDataNode xsi:type="TextNode" Id="DocParam.EnableDocParamButton" Visible="true" LCID="2055" />
      <CustomDataNode xsi:type="TextNode" Id="DocParam.Subject" LCID="2055" />
      <CustomDataNode xsi:type="DateTimeNode" Id="DocParam.CreationTime" LCID="2055" IsNowDefault="true" DateFormat="d. MMMM yyyy" Calendar="Gregor" />
      <CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.CheckBox1" LCID="2055" IsChecked="false" />
      <CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.ComboBox1" LCID="2055" SelectedValue="default">
        <ListItems>
          <Item>
            <Key><string>opt1</string></Key>
            <Value><string>Option 1</string></Value>
          </Item>
          <Item>
            <Key><string>opt2</string></Key>
            <Value><string>Option 2</string></Value>
          </Item>
          <Item>
            <Key><string>opt3</string></Key>
            <Value><string>Option 3</string></Value>
          </Item>
        </ListItems>
      </CustomDataNode>
      <CustomDataNode xsi:type="TextNode" Id="DocParam.TextNodeForRadio" LCID="2055" />
      <CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.ComboBoxForRadio" LCID="2055">
        <ListItems>
          <Item>
            <Key><string>opt1</string></Key>
            <Value><string>Option 1</string></Value>
          </Item>
          <Item>
            <Key><string>opt2</string></Key>
            <Value><string>Option 2</string></Value>
          </Item>
          <Item>
            <Key><string>opt3</string></Key>
            <Value><string>Option 3</string></Value>
          </Item>
        </ListItems>
      </CustomDataNode>
    </DataNodes>
  </CustomContentSection>
  <Views IsDebug="false">
    <View Id="main" Label="Startseite">
      <Row>
        <TextBlock Style="h1" ColumnSpan="4">Titel</TextBlock>
      </Row>
      <Row>
        <Separator ColumnSpan="4" />
      </Row>
      <Row>
        <Label Content="Betreff" />
        <TextBox Id="DocParam.Subject" ColumnSpan="3" />
      </Row>
      <Row>
        <Label Content="Datum" />
        <DatePicker Id="DocParam.CreationTime" ColumnSpan="3" />
      </Row>
      <Row>
        <CheckBox Id="DocParam.CheckBox1" Label="CheckBox mit ColumnOffset=1" ColumnOffset="1" ColumnSpan="2"></CheckBox>
      </Row>
      <Row>
        <Label Content="das ist eine Combobox" ColumnSpan="1"></Label>
        <ComboBox Id="DocParam.ComboBox1" ColumnSpan="2"></ComboBox>
      </Row>
      <Row>
        <Label Content="RadioButton Basierend auf einem TextNode" ColumnSpan="4"></Label>
      </Row>
      <Row>
        <Separator ColumnSpan="4" />
      </Row>
      <Row>
        <!-- Konfiguration eines RadioButton über einen TextNode. Wenn der TextNode im Dokuement verwendet wird, dann wird der Value der Ausgewählten Option eingefügt. Die anderen Optionen können im Dokument nicht mehr angewählt werden, nur über den Dokumenteparameterdialog -->
        <RadioButton Id="DocParam.TextNodeForRadio" Value="opt1" Label="Option 1"></RadioButton>
        <RadioButton Id="DocParam.TextNodeForRadio" Value="opt2" Label="Option 2"></RadioButton>
        <RadioButton Id="DocParam.TextNodeForRadio" Value="opt3" Label="Option 3"></RadioButton>
      </Row>
      <Row>
        <!-- Fügt eine Leere Row ein, kann so verwendet werden um Elemente optisch besser zu trennen -->
        <TextBlock></TextBlock>
      </Row>
      <Row>
        <Label Content="RadioButton basierend auf einem ComboBoxNode" ColumnSpan="4"></Label>
      </Row>
      <Row>
        <Separator ColumnSpan="4" />
      </Row>
      <Row>
         <!-- Konfiguration eines RedioButton über einen ComboBoxNode. Wenn der ComboBoxNode im Dokument verwendet wird, wird das Label der ausgewählten Option angezeigt. Die anderen Optionen können über die ComboBox von Word weiterhin angewählt werden -->
        <RadioButton Id="DocParam.ComboBoxForRadio" Value="opt1" Label="Option 1"></RadioButton>
        <RadioButton Id="DocParam.ComboBoxForRadio" Value="opt2" Label="Option 2"></RadioButton>
        <RadioButton Id="DocParam.ComboBoxForRadio" Value="opt3" Label="Option 3"></RadioButton>
      </Row>
      <Button Type="Submit" Label="OK" IsDefault="true" />
      <Button Type="Cancel" Label="Abbrechen" />
    </View>
  </Views>
</Configuration>
```
Der dazugehörige Dialog:  

![DocumentParameterDialog]({{ site.baseurl }}/assets/content-images/docfunc/de/ExampleDocParamWithView.png)  


__Konfiguration eines einfachen DokumenteParameter ohne Verwendung von Views__

```xml
<Configuration>
  <CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
    <DataNodes>      
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.Subject"      LCID="2055" Row="1" Column="1" Label="Das ist ein TextNode"/>
      <CustomDataNode xsi:type="DateTimeNode" Id="DocParam.CreationTime" LCID="2055" Row="2" Column="1" IsNowDefault="true" DateFormat="d. MMMM yyyy" Calendar="Gregor" Label="Datumsauswahl"/>
      <CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.ComboBox"     LCID="2055" Row="3" Column="1" ColumnSpan="1"  Label="Dies ist eine Combobox" SelectedValue="default">
        <ListItems>
          <Item>
            <Key><string>default</string></Key>
            <Value><string>default</string></Value>
          </Item>
          <Item>
            <Key><string>opt1</string></Key>
            <Value><string>Option 1</string></Value>
          </Item>
          <Item>
            <Key><string>opt2</string></Key>
            <Value><string>Option 2</string></Value>
          </Item>
        </ListItems>
      </CustomDataNode>
      <!-- ColumnOffset wird nur mit Views verwendet, ohne Views wird direkt die Column angegeben, in welcher das Element platziert werden soll -->
      <CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.CheckBox"  LCID="2055" Row="3" Column="2" Label="Eine Checkbox" IsChecked="false" ></CustomDataNode>            
    </DataNodes>
  </CustomContentSection>  
</Configuration>
```

Der dazugehörige Dialog:  

![DocumentParameterDialog]({{ site.baseurl }}/assets/content-images/docfunc/de/ExampleDocParamWithoutView.png)  

__Validierung__

```xml
<Configuration>
  <CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
    <DataNodes>      
      <!-- ↓ Bewirkt, dass der DocParam-Button in Word angewählt werden kann (nur bei Verwendung von Views nötig). -->
      <CustomDataNode xsi:type="TextNode" Id="DocParam.EnableDocParamButton" Visible="true" Row="0" Column="1" LCID="2055" />      
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.Subject"      LCID="2055"  Required="true" ValidationMessage="Bitte geben sie einen Betreff ein"/>
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.4NumbersMax"      LCID="2055"   Regex="^[0-9]{1,4}$" ValidationMessage="Die Zahl darf maximal aus vier Ziffern bestehen und muss natürlich sein"/>      
    </DataNodes>
  </CustomContentSection>
  <Views IsDebug="false">
    <View Id="main" Label="Startseite">
      <Row>
        <TextBlock Style="h1" ColumnSpan="4">Titel</TextBlock>
      </Row>
      <Row>
        <Separator ColumnSpan="4"/>
      </Row>
      <Row>
        <Label Content="Betreff" />
        <TextBox Id="DocParam.Subject" ColumnSpan="3" />
      </Row>
       <Row>
        <Label Content="Maximal Vierstellige, natürlich Zahl" />
        <TextBox Id="DocParam.4NumbersMax" ColumnSpan="3" />
      </Row>
      <Button Type="Submit" Label="OK" IsDefault="true" />
      <Button Type="Cancel" Label="Abbrechen" />
    </View>
  </Views>
</Configuration>
```  
Verhalten des Dialoges  

![DocumentParameterDialog]({{ site.baseurl }}/assets/content-images/docfunc/de/Validation.gif)  

__Binding Beispiele__  
___Standard Bindings___  
```xml
<Configuration>
  <CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
    <DataNodes>    
      <!-- ↓ Bewirkt, dass der DocParam-Button in Word angewählt werden kann (nur bei Verwendung von Views nötig). -->
      <CustomDataNode xsi:type="TextNode" Id="DocParam.EnableDocParamButton" Visible="true" Row="0" Column="1" LCID="2055" />      
      <CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.Checkbox1" LCID="2055"  IsChecked="false" ></CustomDataNode>
      <CustomDataNode xsi:type="TextNode" Id="DocParam.TextNode1" LCID="2055"> </CustomDataNode>            
    </DataNodes>
  </CustomContentSection>
  <Views IsDebug="false">
    <View Id="main" Label="Startseite">
      <Row>
        <TextBlock Style="h1" ColumnSpan="4">Titel</TextBlock>
      </Row>
      <Row>
        <Separator ColumnSpan="4"/>
      </Row>      
      <Row>
        <Label Content="Name für CustomLabel"></Label>
        <TextBox Id="DocParam.TextNode1"></TextBox>
      </Row>
      <Row>
        <CheckBox Id="DocParam.Checkbox1" Label="Zeige CustomLabel"></CheckBox>
      </Row>
      <Row>
       <Label Content="CustomLabel: " Bind="IsVisible: $('DocParam.Checkbox1')"></Label>
        <!-- Einfaches, Doppeltes Binding mit einer Bedingung pro gebindetem Attrbut (isVisible, Value) -->
        <TextBlock Bind="IsVisible: $('DocParam.Checkbox1'), Value: $('DocParam.TextNode1')"></TextBlock>
      </Row>
      <!-- Einfaches Value Binding -->
        <Row Bind="IsVisible: $('DocParam.TextNode1') == 'Hello'">
        <TextBlock>CustomLabel hat den Wert 'hello'</TextBlock>
      </Row>
      <!-- IsVisible-Binding mit einer UND Bedingung (&& --> &amp;&amp; ) -->
      <Row Bind="IsVisible: $('DocParam.Checkbox1') &amp;&amp; $('DocParam.TextNode1') == 'Hello'">
        <TextBlock Value="">CustomLabel ist sichtbar UND hat den Wert 'Hello'</TextBlock>
      </Row>  
      <!-- IsVisible-Binding mit einer ODER Bedingung -->
      <Row Bind="IsVisible: $('DocParam.Checkbox1') || $('DocParam.TextNode1') == 'hello'">
        <TextBlock>CustomLabel ist sichtbar ODER hat den Wert 'hello'</TextBlock>
      </Row>
      <Button Type="Submit" Label="OK" IsDefault="true" />
      <Button Type="Cancel" Label="Abbrechen" />
    </View>
  </Views>
</Configuration>
```
Das Verhalten des Dialoges:    
  

![DocumentParameterDialog]({{ site.baseurl }}/assets/content-images/docfunc/de/Standard_Bindings.gif)  


___Calc-Bindings___

```xml
<Configuration>
  <CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
    <DataNodes>      
      <!-- ↓ Bewirkt, dass der DocParam-Button in Word angewählt werden kann (nur bei Verwendung von Views nötig). -->
      <CustomDataNode xsi:type="TextNode" Id="DocParam.EnableDocParamButton" Visible="true" Row="0" Column="1" LCID="2055" />
      
      <!-- EingabeFelder für die Mathematischen Funktionen, mit validen Standardwerten-->
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.Field1"              LCID="2055" >1</CustomDataNode>
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.Field2"              LCID="2055" >1</CustomDataNode>
            
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.TestNode2"           LCID="2055" />
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.OutputAdd"           LCID="2055" />
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.OutputSubtract"      LCID="2055" />
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.OutputDivide"        LCID="2055" />
      <CustomDataNode xsi:type="TextNode"     Id="DocParam.OutputMultiply"      LCID="2055" />
      <CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.CB1"                 LCID="2055" />
      <CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.CB2"                 LCID="2055" />
      <CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.CB3"                 LCID="2055" />
      <CustomDataNode xsi:type="CheckBoxNode" Id="DocParam.CB4"                 LCID="2055" />     
    </DataNodes>
  </CustomContentSection>
  <Views IsDebug="false">
    <View Id="main" Label="Startseite">      
      <Row>
        <TextBlock Style="h1" ColumnSpan="4">Titel</TextBlock>
      </Row>
      <Row>
        <Separator ColumnSpan="4"/>
      </Row>
      <Row>
        <Label Content="Wert 1" />
        <TextBox Id="DocParam.Field1" ColumnSpan="3"/>
      </Row>
      
       <Row>
        <Label Content="Wert 2" />
        <TextBox Id="DocParam.Field2" ColumnSpan="3" />
      </Row>    
      <Row Bind="IsVisible: calC($('DocParam.Field1') + $('DocParam.Field2') &gt; 1000;F0) ">
        <TextBlock>Wert1 + Wert2 Ergeben mehr als 1000</TextBlock>
      </Row>
       <Row>
        <Label Content="Ergebnis Addition" />
        <!-- Simples CalcBinding mit Addition und Formatierung auf zwei Nachkomastellen im Währungsformat -->
        <TextBox Id="DocParam.OutputAdd" ColumnSpan="3" Bind="Value: Calc($('DocParam.Field1') + $('DocParam.Field2');C2)" />
      </Row>
      <Row>
        <Label Content="Ergebnis Subtraktion" />
         <!-- Simples CalcBinding mit Subtraktion und Formatierung auf zwei Nachkomastellen im Währungsformat -->
        <TextBox Id="DocParam.OutputSubtract" ColumnSpan="3" Bind="Value: Calc($('DocParam.Field1') - $('DocParam.Field2');C2)" />
      </Row>
       <Row>
        <Label Content="Ergebnis Division" />
         <!-- Simples CalcBinding mit Divison und Formatierung auf drei Nachkomastellen im Dezimalformat -->
        <TextBox Id="DocParam.OutputDivide" ColumnSpan="3" Bind="Value: Calc($('DocParam.Field1') / $('DocParam.Field2');F3)" />
      </Row>
         <Row>
        <Label Content="Ergebnis Multiplikation" />
         <!-- Simples CalcBinding mit Multiplikation und Formatierung auf zwei Nachkomastellen im Währungsformat -->
        <TextBox Id="DocParam.Outputmultiply" ColumnSpan="3" Bind="Value: Calc($('DocParam.Field1') * $('DocParam.Field2');C2)" />
      </Row>     
      <Row>
       <CheckBox Id="DocParam.CB1" Label="CB1"></CheckBox>  
       <CheckBox Id="DocParam.CB2" Label="CB2"></CheckBox>
       <CheckBox Id="DocParam.CB3" Label="CB3"></CheckBox> 
       <CheckBox Id="DocParam.CB4" Label="CB4"></CheckBox>     
      </Row>  
      <!-- Calc Binding um angewählte Checkboxen zu "zählen" -->
      <Row Bind="IsVisible: calc($('DocParam.CB1') + $('DocParam.CB2') + $('DocParam.CB3') + $('DocParam.CB4');F0) == '1'">
        <Label Content="Eine Checkbox angewählt"></Label>
      </Row>       
      <Row Bind="IsVisible: calc($('DocParam.CB1') + $('DocParam.CB2') + $('DocParam.CB3') + $('DocParam.CB4');F0) == '2'">
        <Label Content="Zwei Checkboxen angewählt"></Label>
      </Row>      
      <Row Bind="IsVisible: calc($('DocParam.CB1') + $('DocParam.CB2') + $('DocParam.CB3') + $('DocParam.CB4');F0) == 3">
        <Label Content="Drei Checkboxen angewählt"></Label>
      </Row>       
      <Row Bind="IsVisible: calc($('DocParam.CB1') + $('DocParam.CB2') + $('DocParam.CB3') + $('DocParam.CB4');F0) == 4">
        <Label Content="Vier Checkboxen angewählt"></Label>
      </Row>     
      <Button Type="Submit" Label="OK" IsDefault="true" />
      <Button Type="Cancel" Label="Abbrechen" />
    </View>
  </Views>  
</Configuration>
```

Verhalten des Dialoges:  

![DocumentParameterDialog]({{ site.baseurl }}/assets/content-images/docfunc/de/CalcBindings.gif)  