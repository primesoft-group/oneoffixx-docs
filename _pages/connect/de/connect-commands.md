---
layout: page
title: Connect Commands
permalink: "connect/de/connect-commands/"
language: de
---
Mithilfe der Commands (Befehle) innerhalb eines Connect-Entries kann das Dokument weiterverarbeitet werden. Die Befehle werden ausgeführt nachdem das Dokument generiert wurde. Einige Befehle sind nur clientseitig, d.h. über die OneOffixx Desktopanwendung verfügbar.

Es gibt einen Sonderfall für den "Merge"-Befehl ("zusammenführen"):
Befehle kann man auf Connect-Entry Ebene nutzen oder für den gesamten Batch. Das ist interessant, wenn mehrere Dokumente auf einmal generiert werden und dann zusammengeführt werden sollen. Dann kann der "Merge" Befehl benutzt werden. Das zusammengeführte Dokument verhält sich anschliessend wieder wie ein einzelnes, folglich können danach auch andere Befehle aufgerufen werden. Mehr dazu unter dieser Seite: [Zusammenführen von Dokumenten]({{ site.baseurl }}/connect/de/usecases/merge-documents/)

Befehle können im __OneOffixxConnectBatch__

```xml
    <OneOffixxConnectBatch>
    	<Commands>
   		<Command Name="..." />
    	</Commands>
		...
    </OneOffixxConnectBatch>
```

...oder im __OneOffixxConnect__ verwendet werden:

```xml
    <OneOffixxConnect>
		<Arguments>
			...
		</Arguments>
		<Commands>
			<Command Name="..." />
		</Commands>
		...
    </OneOffixxConnect>
```

## Verfügbare Commands

{:.table .table-striped}
| Name | Beschreibung | Client | Server |                     
| ---- | --- | --- | --- |
| [DefaultProcess](#defaultprocess) | Startet den 'DefaultProcess', der im Windows für den Dateityp registriert ist. | ☑ | ☐ |
| [ConvertToDocument](#converttodocument) | Konvertiert Office-Vorlagen (.dotx etc.) in Dokumente (.docx). |  ☑ | ☑ | 
| [ConvertToPdf](#converttopdf) | Konvertiert Vorlagen oder Dokumente (.dotx/.docx) in PDF (.pdf) (ohne Microsoft Office). |  ☑ | ☑ |
| [Print](#print) | Sendet das Dokument zum Standarddrucker. | ☑ | ☐ |
| [SaveAs](#saveas) | Speichert das Dokument am angegebenen Zielort im angegebenen Format.  | ☑ | ☑ * |
| [UpdateFieldsOnOpen](#updatefieldsonopen) | Aktualisiert Felder und das Inhaltsverzeichnis (Fields / ToC) im Dokument - entweder über Microsoft Office oder direkt im Dokument. |  ☑ | ☑ | 
| [Merge](#merge) | Verbindet mehreren Office-Dokumente zu einem. |  ☑ | ☑ |
| [CreateConnectorResult](#createconnectorresult) | Erstellt eine OneOffixx-Connector-Result-Datei. | ☑ | ☐ |
| [BindCustomXML](#bindcustomxml) | Bindet alle CustomControls mit den jeweiligen Daten. | ☑ | ☑ |
| [InvokeProcess](#invokeprocess) | Ruft ein bestimmtes, im OneOffixx-System registriertes, Programm auf. | ☑ | ☐ |

\* = Mit Einschränkungen

## Command Beschreibung

__DefaultProcess (Client): {% include anchor.html name="defaultprocess" %}__

Dieser Befehl startet den DefaultProcess, der im Windows für den generierten Dateityp registriert ist. Dieser Aufruf funktioniert nur über den Client.

Möglicher Parameter:

* "Start": True/False, bei False wird der Process nicht gestartet.

```xml
    <Command Name="DefaultProcess">
    	<Parameters>
    		<Add key="Start">true</Add>
    	</Parameters>
    </Command>
```

__ConvertToDocument (Server & Client): {% include anchor.html name="converttodocument" %}__

Dieses Befehl gilt nur für Word-Dokumente. OneOffixx verwaltet und generiert Word-Vorlagen (.dotx). Um nach dem Generieren des Dokuments ein Word-Dokument (.docx) zu erhalten, wird dieser Befehl benötigt.

Fehlt diese Angabe und wird das Ergebnis als .docx-Datei gespeichert, zeigt Word eine Fehlermeldung an.


```xml
	<Command Name="ConvertToDocument" />
```

__ConvertToPdf: {% include anchor.html name="converttopdf" %}__

<span class="label label-info">ab 3.1.1</span> Dieser Befehl ist auch im Client verfügbar und gilt nur für Word-Dokumente. OneOffixx konvertiert das Dokument direkt in ein PDF. Dieser Befehl steht nur serverseitig zur Verfügung. Sollen PDFs im Client erzeugt werden, verwenden Sie bitte den [SaveAs](#saveas) Befehl.

```xml
	<Command Name="ConvertToPdf" />
```

Nicht alle OpenXML bzw. Word-Features sind bei der PDF-Konvertierung unterstützt. Folgende Einschränkungen bestehen:

* Es werden nur "TrueType Font" Schriftarten (TTF), die auf dem Server installiert sind, unterstützt. "OpenType Font" (OTF) wird aktuell nicht unterstützt.

__Print (Client):  {% include anchor.html name="print" %}__

Das Dokument wird an den Standard-Drucker gesendet.

```xml
	<Command Name="Print" />
```

__SaveAs (Client & Server*):  {% include anchor.html name="saveas" %}__

Speichert das Dokument am angegebenen Zielort. Der neue Dateispeicherort wird für alle folgenden Befehle berücksichtigt (z. B. im DefaultProcess).

Möglicher Parameter:

* "Filename": Absoluter Pfad mit Dateiendung
* "Overwrite": True/False, gibt an, ob eine bestehende Datei überschrieben werden soll
* "CreateFolder": True/False, gibt an, ob Ordner, die im Filename angegeben sind erstellt werden sollen
* "AllowUpdateDocumentPart": True/False, bei "True" wird der OneOffixx Document Part als "SavedDocument" anstatt "NewDocument" markiert
* "CopyOnly": True/False. Wenn diese Einstellung getroffen wird, werden das Dokument in dem aktuellen Stand als Kopie abgespeichert. Im Client-Anwendungsfall wird die Datei trotzdem z. B. weiterhin als "Vorlage (.dotx)" behandelt und im Temp-Ordner erstellt und von dieser Datei Microsoft Word geöffnet. {% include new-badge.html version="3.3" %}

Nur clientseitig verfügbar:

* "Type": Wenn hier "PDF" angegeben wird, wird das Dokument über Word als PDF gespeichert.

```xml
	<Command Name="SaveAs">
		<Parameters>
			<Add key="Filename">\\MyServer\share\organization\...\documentxyz.dotx</Add>
			<Add key="Overwrite">true</Add>
			<Add key="CreateFolder">true</Add>
			<Add key="CopyOnly">false</Add>  

			<Add key="Type">PDF</Add>  <!-- nur Client-Seitig verügbar. -->
			<Add key="AllowUpdateDocumentPart">false</Add>
		</Parameters>
	</Command>
```

{% include new-badge.html version="3.3" %}

Hinzugekommen ist zudem eine "Auto-Konvertierung", falls im Dateipfad ".docx" angegeben wird. In diesem Fall wird aus der ".dotx"-Datei eine ".docx"-Datei.

```xml
	<Command Name="SaveAs">
		<Parameters>
			<Add key="Filename">\\MyServer\share\organization\...\documentxyz.docx</Add>
			<Add key="CopyOnly">true</Add>  
			...
		</Parameters>
	</Command>
```

".pdf" würde Client-Seitig ebenfalls unterstützt werden.


__UpdateFieldsOnOpen (Client & Server): {% include anchor.html name="updatefieldsonopen" %}__

Dieser Befehl gilt nur für Word-Dokumente und speichert im Dokument die Information, dass Office die Felder, wie z. B. Inhaltsverzeichnisse oder Verknüpfungen, aktualisieren soll.

Hinweis: Standardmässig wird nur ein Flag im Dokument gesetzt, sodass Word beim Öffnen des Dokuments den Benutzer fragt, ob die Felder aktualisiert werden sollen.

```xml
	<Command Name="UpdateFieldsOnOpen" />
```

<span class="label label-info">ab 3.1.1</span>

Über einen Parameter kann OneOffixx auch angewiesen werden, Felder und Inhaltsverzeichnisse (Fields / ToC) direkt im Dokument zu aktualisieren. Das ist insbesondere im Zusammenhang mit dem "ConvertToPdf"-Befehl nötig.

Hinweis: Es wird empfohlen den Befehl im Zusammenhang mit "ConvertToDocument" (bzw. für den PDF-Output mit "ConvertToPdf") zu benutzen, da Word beim Öffnen einer ".dotx"-Datei ebenfalls das Inhaltsverzeichnis nicht richtig darstellt.

Mögliche Parameter:

* "Type": Mittels "OneOffixx" wird versucht, die Felder und Inhaltsverzeichnisse direkt im Dokument zu aktualisieren.

```xml
        <Command Name="ConvertToDocument" />
	<Command Name="UpdateFieldsOnOpen">
		<Parameters>
			<Add key="Type">OneOffixx</Add>
		</Parameters>
	</Command>
```


__Merge (Client & Server - ConnectBatch): {% include anchor.html name="merge" %}__

Der Merge-Befehl gilt nur für Word-Dokumente und kann zum Zusammenführen von mehreren Dokumenten verwendet werden. Das zusammengeführte Dokument kann anschliessend wieder als ein einzelnes verwendet werden. Der Befehl macht nur auf Connect-Batch Ebene Sinn.

Mögliche Parameter:

* "PageNumberStart": Gibt an, bei welcher Seite das neu generierte Dokument startet.

```xml
	<Command Name="Merge">
		<Parameters>
			<Add key="PageNumberStart">10</Add>
		</Parameters>
	</Command>
```

Das Ergebnis des Merge-Befehls ist immer ein Word Dokument (.docx).

__CreateConnectorResult (Client): {% include anchor.html name="createconnectorresult" %}__


Dieser Befehl speichert nach dem Durchlauf der Dokumentgenerierung und der Befehl-Pipeline eine Connector-Result-Datei. Diese wird im gleichen Ordner gespeichert, wie wo das Connectfile hinterlegt ist. Das Format der Datei ist dasselbe wie in den [Global Settings]({{ site.baseurl }}/connect/de/xml-schema/#oneoffixx-connect-batch-settings) angegeben. 

```xml
	<Command Name="CreateConnectorResult" />
```

__BindCustomXML (Client & Server): {% include anchor.html name="bindcustomxml" %}__

<span class="label label-info">ab 3.1.1</span>

Dieser Befehl gilt nur für Word-Dokumente. OneOffixx legt alle Daten als sogenannte "CustomXML-Daten" im Dokument ab und Office lädt beim Öffnen des Dokuments diese Daten und schreibt die Werte in die jeweiligen ContentControls.

Es gibt vereinzelt Fälle in welchen Office bzw. der Open XML-fähige Client nicht die richtigen Werte lädt oder die Felder leer bleiben, weil z. B. eine ältere Office Applikation genutzt wird oder weil der Open XML-Client diese Funktionalität nicht implementiert hat.

In diesem Fall kann dieser Befehl helfen, da OneOffixx bereits bei der Dokumentgenerierung die Daten nicht nur im CustomXML ablegt sondern weil es gleichzeitig die Daten in den ContentControls aktualisiert.

```xml
	<Command Name="BindCustomXML" />
```

__InvokeProcess (Client): {% include anchor.html name="invokeprocess" %}__

<span class="label label-info">ab 3.1.1</span>

Dieser Befehl ruft den dazugehörigen Prozess nach der Erstellung des Dokuments auf. Aus Sicherheitsgründen können nur im OneOffixx-System registrierte "Prozesse" aufgerufen werden. Die Einstellung können Sie im OneOffixx Dashboard vornehmen. Es können mehrere Prozesse definiert werden. Die Konfiguration sieht hierfür so aus:

```xml
    <CommandConfig>
	    <Process name="OurSystemNotepad" executablePath="%systemroot%/notepad.exe" />
	    <Process name="..." executablePath="..." />
    </CommandConfig>
```
Dieser Prozess kann nun über den Namen "OurSystemNotepad" im Befehl über "Name" angesteuert werden. Optional können Argumente mitangegeben werden:

```xml
	<Command Name="InvokeProcess">
		<Parameters>
			<Add key="Name">OurSystemNotepad</Add>
			<Add key="Arguments">/w test.txt</Add>
		</Parameters>
	</Command>
```
