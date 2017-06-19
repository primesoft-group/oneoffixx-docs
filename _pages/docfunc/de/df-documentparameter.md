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
| WindowHeight (Fensterhöhe)  |  Über das Attribut "WindowHeight" kann die Fensterhöhe in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. Der Wert für WindowHeigth muss zwingend gesetzt sein. (Gilt für Verwendung mit und Ohne Views) |

## Die DataNodes und deren Attribute

  In diesem Abschnitt geht es um die Konfiguration zwischen `<DataNodes>` und `</DataNodes>`.
  Jedes CustomDataNode definiert ein Dokument-Parameter-Feld, auf das im Editor, in Skripts
  oder über Extended Bindings zugegriffen werden kann.
  Für jedes Feld in den Views (siehe 4. Views) muss für die Weiterverwendung der Eingabe ein
  CustomDataNode angelegt werden.

__CustomDataNode-Basisattribute (gelten für Verwendung mit und ohne Views)__  

{:.table .table-striped}  
|  __Name__                     		 |  __Beschreibung__  |
|    ----								 |        ----        |
| Type (xsi:type)						 | __TextNode__<br>Wird in Word zu einem Nur-Text-Inhaltssteuerelement (Plain Text Content Control), für ein- oder mehrzeilige Text-Eingabe, Überprüfung via Regex möglich<br><br>__CheckBoxNode__<br>Wird in Word zu einem Kontrollkästchensteuerelement (Check Box Content Control), für ja/nein-Auswahl<br><br>__DateTimeNode__<br>Wird in Word zu einem Datumsauswahl-Inhaltssteuerelement (Date Picker Content Control), für Datumsfeld mit Kalenderauswahl<br><br>__ComboBoxNode__ <br> Wird in Word zu einem Kombinationsfeld-Inhaltssteuerelement (Combo Box Content Control), für die Auswahl zwischen vorgegebenen Werten (beliebige Eingaben in Word zulässig)<br><br>__LabelNode__ <br> Überschrift im Dokument-Parameter-Dialog wenn Views nicht verwendet werden, nicht für die Verwendung im Editor, in Skripts und in Extended Bindings geeignet <br><br> __*RadioButton*__ <br>Es gibt keinen RadioButton-Typ. Der Grund ist, dass es in Word keine RadioButton-Inhaltssteuerelemente gibt. Trotzdem benötigen RadioButtons ein CustomDataNode, damit die Auswahl in der View gespeichert werden kann für die Verwendung im Editor, in Skripts und in Extended Bindings. <br><br> __Mögliche CustomDataNode-Typen für das Speichern der Auswahl von RadioButtons:__ <br><br>__Als Textnode__ <br> In diesem Fall wird der Value des in der View ausgewählten RadioButtons im TextNode gespeichert. Dies ist für Dokument-Parameter geeignet, die nicht in Word eingefügt werden sondern nur für den Zugriff via Skript oder Extended Binding erstellt wurden. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons als Standard-Text konfiguriert werden, also: <br> `<CustomDataNode xsi:type="TextNode" Id="DocParam.RadioButtonGender" LCID="2055">ValueDesEntsprechendenRadioButtons</CustomDataNode>`{:.language-xml} <br><br> __Als ComboBoxNode__ <br> In diesem Fall wird der ComboBoxNode-Eintrag ausgewählt, bei dem der Key genau dem Value des RadioButtons entspricht. Dies ist auch für Dokument-Parameter geeignet, welche in Word eingefügt werden, da die Anzeige im Dokument über den Value des ComboBoxNode-Eintrags gesteuert wird. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons im SelectedValue-Attribut der ComboBoxNode konfiguriert werden, also: <br> `<CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.RadioButtonGender" LCID="2055" SelectedValue="ValueDesEntsprechendenRadioButtons">...</CustomDataNode>`{:.language-xml} <br><br> Wie die RadioButtons dann in der View definiert werden, wird im entsprechenden Kapitel beschrieben.  |  
|  Label (Beschriftung)        			 |  Beschriftung des Elements im Quick Check-Panel, wenn es sich um einen Tracked-Dokument-Parameter handelt.  |
|  Required (benötigtes Feld)  			 |   Attribut nur für Elemente des Typs Textfelder zulässig. Definiert ob das Feld leer gelassen werden kann (Required="false" oder nicht gesetzt) oder ob das Feld ausgefüllt werden muss (Required="true"). Wird von der Validierung (Regex-Attribut) übersteuert, falls eine gesetzt wird.  |  
|  Regex (Validierung)         			 |  Attribut nur für Elemente des Typs Textfelder zulässig. Erlaubt es einen Regex (.NET Syntax) zu definieren, welcher im eingegeben Text min. einen Match finden muss. Achtung: Falls der ganze Text 'gematcht' werden soll oder nur genau ein 'Match' vorhanden sein muss, muss dies vom Regex-Ausdruck definiert werden.<br><br>__Beispiele__<br>Regex="[0-9]+" erzwingt, dass min. ein Zeichen des Eingabetexts eine Ziffer sein muss. "Hallo 205" ist so z. B. eine gültige Eingabe. <br><br> Regex="^[0-9]+$" erzwingt, dass alle Zeichen des Eingabetexts Ziffern sein müssen (und dass min. 1 Ziffer vorhanden sein muss). (^ matcht den Anfang des Eingabetextes und $ das Ende)  | 
|    ValidationMessage (Fehlermeldung)   |  Attribut nur für Elemente des Typs Textfelder zulässig. Falls Required="true" oder ein Validierungs-Regex gesetzt wurde, erlaubt ValidationMessage eine benutzerdefinierte Fehlermeldung anzuzeigen, falls die Validierung fehlschlägt. Falls ValidationMessage nicht gesetzt ist, wird im Fehlerfall eine Standardmeldung angezeigt.  |
| Tracked (Überwachung mit "Quick Check")|	 Die OneOffixx-Funktion Quick Check (Inhaltssteuerelemente prüfen) wird mit dem Attribut Tracked aktiviert. Ist der Wert auf true gesetzt, wird dem Benutzer im separaten Panel das Feld angezeigt. Sofern der Inhalt des Elementes leer ist, wird das Feld im Panel rot und nach Bearbeitung grün angezeigt.	 |
|   Id (Identifikation)					 |  Textuelle ID, welche eindeutig sein muss. Diese wird im Editormodus angezeigt und danach für die Verwendung im Editor, in Skripts oder in Extended Bindings benötigt. Die Id darf keine Leerzeichen enthalten. |
| SelectedValue (Ausgewählter Eintrag)   |  Attribut nur für Elemente des Typs Kombinationsfeld (ComboBoxNode) zulässig. Über diese Option wird bestimmt, welcher Eintrag in der Liste standardmässig selektiert werden soll. |
| IsChecked (Standard-Selektion)		 |   Attribut nur für Elemente des Typs Kontrollkästchen (CheckBoxNode) zulässig. Über diese Option wird bestimmt, ob die Checkbox standardmässig selektiert oder unselektiert sein soll.  |
|  Locked (Sperrung)  					 |  Hat keine Wirkung. War ursprünglich dafür vorgesehen, dass das Inhaltssteuerelements (Content Control) in Word nicht gelöscht werden kann.  |
|    ReadOnly (nur Leserecht) 			 |	 Hat keine Wirkung. War ursprünglich dafür vorgesehen, dass das der Inhalt des Inhaltssteuerelements (Content Control) in Word nicht bearbeitet werden kann.

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
|  TextBox: Einzeilige oder mehrzeilige Texteingabe				|  `<TextBox Value="Text" Id="DocParam.Subject" Lines="2" />`{:.language-xml}<br>Value = Vordefiniert, wird aber ignoriert wenn es eine CustomDataNode mit der ID gibt.<br>Lines = Anzahl an Zeilen - Standard ist 1.<br> Validierung: Verbindet man das TextBox Control an eine CustomDataNode vom Typ Text werden die Validierungsoptionen von dort übernommen.  |
|  CheckBox: Auswahlkasten - oder halt CheckBox					|  `<CheckBox Id="DocParam.Erweitert" Label="Notizen" />`{:.language-xml}<br>Label = Beschreibung, erscheint rechts von der CheckBox  |
|  ComboBox: Auswahlliste										|  `<ComboBox Value="0" IsInvalidWhenValue="0" Id="DocParam.Typ">`{:.language-xml}<br>&nbsp;`<Item Label="Bitte wählen" Value="0" />`{:.language-xml}<br>&nbsp;`<Item Label="Stufe 1" Value="1" />`{:.language-xml}`</ComboBox>`{:.language-xml} <br> Die Werte für die ComboBox können entweder im CustomDataNode definiert werden (die Liste der Werte wird aus dem CustomDataNode übernommen, auch wenn in der View eine Liste definiert wurde. Wenn die Liste in der View Definiert wird, dann muss der CustomDataNode ein TextNode sein. Beispiele dazu finden Sie am Ende dieser Seite). Wenn der CustomDataNode ein CheckBoxNode ist, dann wird das Feld bei Verwendung im Word als Auswahlbox dargestellt, wenn der CustomDataNode ein TextNode ist und die Liste der Werte in der View definiert werden, so wird bei Verwendung des Feldes im Word nur der Text der ausgewählten Option als Text abgefüllt.<br><br> Value = Ausgewähltes Element (muss als Item beschrieben sein)<br>IsInvalidWhenValue = Wenn das ausgewählte Element diesen Wert hat, ist das Control nicht "valide", d.h. man kann das Dokument nicht erzeugen<br>Item.Label = Text, welcher angezeigt wird<br>Item.Value = Wert, wenn ausgewählt<br> IsEditable = true/false - wenn true, kann selbst ein Text eingegeben werden
|  DatePicker: Datumsauswahl									|  `<DatePicker Id="DocParam.ErstellDatum" />`{:.language-xml}  |
|  RadioButton: Gruppierter Auswahlknopf 						|  `<RadioButton Id="DocParam.Level" Label="Stufe 1" Value="level1" />`{:.language-xml}<br><br>Eine RadioButton Auswahl basiert auf einen CustomDataNode. Pro Anwählbarer Option muss ein einzelnes solches RadioButton Element definiert werden. Die ID Bleibt dabei gleich, nur Label und Value sind anders<br><br>Label = Beschreibungstext, welcher rechts des Knopfs erscheint<br>Value=Wert<br><br>__Definition eines RedioButtons mit einem TextNode__<br>In diesem Fall wird der Value des in der View ausgewählten RadioButtons im TextNode gespeichert. Dies ist für Dokument-Parameter geeignet, die nicht in Word eingefügt werden sondern nur für den Zugriff via Skript oder Extended Binding erstellt wurden. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons als Standard-Text konfiguriert werden, also: <br><br>`<CustomDataNode xsi:type="TextNode" Id="DocParam.RadioButtonGender" LCID="2055">M</CustomDataNode>`{:.language-xml} <br><br> __Definition eines RadioButtons mit einem ComboBoxNode__<br>In diesem Fall wird der ComboBoxNode-Eintrag ausgewählt, bei dem der Key genau dem Value des RadioButtons entspricht. Dies ist auch für Dokument-Parameter geeignet, welche in Word eingefügt werden, da die Anzeige im Dokument über den Value des ComboBoxNode-Eintrags gesteuert wird. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons im SelectedValue-Attribut der ComboBoxNode konfiguriert werden, also:<br>`<CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.RadioButtonGender" LCID="2055" SelectedValue="M">`{:.language-xml}<br>&nbsp;`<ListItems>`{:.language-xml}<br>&nbsp;&nbsp;`<Item>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;`<Key><string>M</string></Key>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;`<Value><string>Männlich</string></Value>`{:.language-xml}<br>&nbsp;&nbsp;`</Item>`{:.language-xml}<br>&nbsp;&nbsp;`<Item>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;`<Key><string>W</string></Key>`{:.language-xml}<br>&nbsp;&nbsp;&nbsp;`<Value><string>Weiblich</string></Value>`{:.language-xml}<br>&nbsp;&nbsp;`</Item>`{:.language-xml}<br>&nbsp;`</ListItems>`{:.language-xml}<br>`</CustomDataNode>`{:.language-xml}<br><br>Die dazugehörige View Konfiguration der Radiobuttons (für beide Fälle) Würde dann so Aussehen:<br>`<Row>`{:.language-xml}<br>&nbsp;`<RadioButton Id="DocParam.RadioButtonGender" Value="M" Label="Männlich"></RadioButton>`{:.language-xml}<br>&nbsp;`<RadioButton Id="DocParam.RadioButtonGender" Value="W" Label="Weiblich"></RadioButton>`{:.language-xml}<br>`</Row>`{:.language-xml}<br><br>

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
| <pre>&gt;</pre>  für > |  grösser als. (XML-Attribute erlauben keine < oder >, daher muss <pre>&lt;</pre> oder <pre>&gt;</pre> verwendet werden)  
| <pre>&gt;=</pre> für >= | grösser oder gleich |
| <pre>&lt;</pre> für <   | kleiner als  |
| <pre>&lt;=</pre> für <= | kleiner oder gleich

Mehrere Bedingungen können mit UND oder ODER verknüpft werden.  
|| für ODER  
&amp;&amp; für UND (steht für &&) (XML-Attribute erlauben keine &, daher muss &amp; verwendet werden)  

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

Die Wertgrundlagen für die Bindings können mit mathematischen Funktionen erweitert werden.
Das Ansprechen der Felder bleibt dabei gleich, $('DocParam.xy'). Um die Felder mathematisch miteinander zu verknüpfen, können die normalen Basisoperatorn (+-/*) verwendet werden.  

Übersicht über alle möglichen Operatoren und wie sie verwendet werden:   
Basis-Operatoren wie +,-,*,/                            https://github.com/pieterderycke/Jace/wiki/Basic-Operations  
Standard funktionen wie Quadratwruzel, sin,tan,cos etc  https://github.com/pieterderycke/Jace/wiki/Standard-Functions  
==/!=/<= etc Operationen                                https://github.com/pieterderycke/Jace/wiki/Boolean-Operations  

Jeder Calc-Aufruf enthält als abschliessendes Argument den Formatierungsstring, vom Term separiert durch ein ";". Dieser wert kann weggelassen werden, das ";" ist aber zwingend.

Formatierung: 
G2 -> Zahl mit 2 Nachkommastellen
C2 -> Währungsformat entsprechend der CurrenThreadCulture mit 2 Nachkommastellen

Komplette Liste mit Formatierungscodes: https://msdn.microsoft.com/de-de/library/dwhawy9k(v=vs.110).aspx

Syntax:

calc($('DocParam.Field1') + $('DocParam.Field2');)
calc($('DocParam.Field1') + ($('DocParam.Field2') * $('DocParam.Field2'));)

WICHTIG: 
Nach dem ";" muss entweder ein Wert, oder gar nichts stehen. Calc(...; ) führt zu einem Fehler, richtig ist Calc(...;)/Calc(...;Wert)

Die verwendete Library ist fähig, Exponent-vor-Punkt-vor-Strich zu Rechnen.  -> ( a + b * c) == (a + (b * c)) != ((a + b ) * c)

Das Calc-schlüsselwort ist Case-insensitive

Die Calc-funktion kann auf die Attribute

Value
IsEnabled
IsVisible

angewendet werden.