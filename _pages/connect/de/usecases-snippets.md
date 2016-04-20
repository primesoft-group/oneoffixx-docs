---
layout: page
title: Anwendungsfälle
subtitle: Textbausteine in Dokument einbauen
permalink: "connect/de/usecases/snippets/"
---

Es soll ein neues Dokument erstellt werden und mit Textbausteinen (Snippets) befüllt werden. Die Anzahl der Textbausteine ist beliebig. Die Textbausteine werden in die Bookmarks eingepflegt. Falls bereits Inhalte in den Bookmarks vorhanden sind, werden diese gelöscht. Die ID des Textbausteins kann mit Hilfe des Textbaustein Editors ausgelesen werden. Jede ID ist eineindeutig und ändert sich nach dem Anlegen nicht mehr. 

Die Sprache wird über die Dokumentensprache festgelegt.
    
```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
    				<LanguageLcid>2055</LanguageLcid>
    			</Arguments>
    			<Function name="SnippetsResolver" id="dd752747-733e-4175-9fc7-028ab7472742">
    				<Arguments>
    				<Snippet id="A7835D23-E945-4A39-81B9-3CEC067E26C0" bookmark="Bookmark1" />
    				<Snippet id="B8235D23-D945-5A39-31B9-23EC067E2120" bookmark="Bookmark1" />
    				<Snippet id="43535D23-45D5-6A39-81B9-DE1C067E2112" bookmark="Bookmark2" />
    				<Snippet id="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX" bookmark="Bookmark3" />
    				</Arguments>
    			</Function>
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

Mehrere Textbausteine können in einem Bookmark (z.Bsp. Bookmark1) gruppiert werden indem im Attribute Bookmark der gleiche Name steht. Die Textbausteine werden in der gleichen Reihenfolgen eingebaut wie sie im XML stehen.
Es ist ebenfalls möglich, den „_OneOffixxOpenAt“ Bookmark zu verwenden. 
Dadurch wird der Text an der Cursor-Plazierung, welche in der OneOffixx Vorlage definiert ist, eingefügt.

## Eigene Textbausteine in Dokument einbauen

Über die Textbausteine können auch eigene Inhalte / Texte übergeben werden. Dies im Text oder HTML Format.

### Beispiel Textbausteininhalt übermitteln:

Sofern die ID weggelassen wird, kann im Element ein Text übergeben werden der anstelle des Bookmarks ersetzt wird.

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    	<Entries>
    		<OneOffixxConnect>
    			<Arguments>
    				<TemplateId>6bb49520-1ebd-4f68-bb5f-02f46a9e1ec8</TemplateId>
    				<LanguageLcid>2055</LanguageLcid>
    			</Arguments>
    			<Function name="SnippetsResolver" id="dd752747-733e-4175-9fc7-028ab7472742">
    				<Arguments>
    	               <Snippet bookmark="Bookmark3">
					       Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Maecenas porttitor congue massa. Fusce posuere, magna sed pulvinar ultricies, purus lectus malesuada libero, sit amet commodo magna eros quis urna.
                           Nunc viverra imperdiet enim. Fusce est. Vivamus a tellus.
                           Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Proin pharetra nonummy pede. Mauris et orci.
                           Aenean nec lorem. In porttitor. Donec laoreet nonummy augue.
                           Suspendisse dui purus, scelerisque at, vulputate vitae, pretium mattis, nunc. Mauris eget neque at sem venenatis eleifend. Ut nonummy.
    				   </Snippet>
    				</Arguments>
    			</Function>
    		</OneOffixxConnect>
    	</Entries>
    </OneOffixxConnectBatch>
```

### Beispiel HTML-Bausteininhalt übermitteln:

Bei der Übermittlung von HTML Inhalten, ist der „type“ Html anzugeben. Es können generell alle von Office zugelassenen HTML Inhalte übermittelt werden (https://msdn.microsoft.com/en-us/library/aa338201%28v=office.12%29.asp)

```xml
    <Snippet bookmark="_OneOffixxOpenAt" type="Html">
       <![CDTA[
               <p>Demo</p>
       ]]>
    </Snippet>
```

__Text in definiertem Word-Style:__

Überschriften wie H1-H4 sowie die normalen Formatierung (bspw. fett resp. <strong>) werden automatisch in den ensprechenden Überschriftsstyle (bspw. <h1> = Überschrift1) dargestellt.

```xml
          <Snippet bookmark="_OneOffixxOpenAt" type="Html"><![CDATA[
            <h1>Grosser Titel</h1>
            <strong>fetter Text</strong>
          ]]></Snippet>
```

Texte können in durch die Angabe von „mso-style-name:“ einem bestimmten Word-Style zugeordnet werden.

```xml
          <Snippet bookmark="_OneOffixxOpenAt" type="Html"><![CDATA[
            <p style="mso-style-name:oneoffixxStyleName">Demo</p>
          ]]></Snippet>
```

__Tabelle:__

Als HTML können auch Tabellen übermittelt werden.

```xml
          <Snippet bookmark="_OneOffixxOpenAt" type="Html"><![CDATA[
            <table width="100%">
              <tr>
                <td>erste Spalte</td>
                <td>zweite Spalte</td>
              </tr>
            </table>
          ]]></Snippet>
```

