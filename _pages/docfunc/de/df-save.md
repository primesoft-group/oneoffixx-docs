---
layout: page
title: Save / Speicherpfad Definition
permalink: "docfunc/de/df/save"
language: de
---

„Speicherpfad Definition“ wird verwendet, um beim Speichervorgang des Dokuments einen Namen und einen Dateispeicherort vorzuschlagen.

Bei Bedarf kann man anhand von Elementen wie z. B. einem Dokument-Parameter, einem Profil-Nachnamen oder einem Empfänger-Firmennamen den vorgeschlagene Dateinamen und/oder Speicherpfad automatisch zusammenstellen.<br>
Dies geschieht in der Konfiguration mittels Zugriff über XSLT und XPath auf Elemente aus dem CustomXMLPart.

## Beispiel 1: Simple Konfiguration

Hier eine Beispiel-Konfiguration, die möglichst schlank gehalten ist:

```xml
<SavePathConfiguration>
  <SaveNewDocumentOnOpen>false</SaveNewDocumentOnOpen>
  
  <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:output method="xml" version="1.0" encoding="utf-8" />
    
    <!-- parameters from outside this stylesheet
         can be passed by an interface
         they are not used in this configuration -->
    <xsl:param name="filename" />
    <xsl:param name="path" />
    <xsl:param name="pathAndFilename" />
    <xsl:param name="targetFolderFileList" />
    
    <xsl:template match="/">
      
      <xsl:variable name="Path" select="'C:\temp\'" />
      <xsl:variable name="Filename" select="'Test_FileName'" />
      
      <xsl:element name="DocumentFunction" namespace="">
        <xsl:attribute name="name">SavePathDefinition</xsl:attribute>
        <xsl:element name="Path" namespace="">
          <xsl:value-of select="concat($Path, $Filename,'.docx')" />
        </xsl:element>
        <xsl:element name="CreateFolder" namespace="">false</xsl:element>
      </xsl:element>
      
    </xsl:template>
  </xsl:stylesheet>
</SavePathConfiguration>
```

### Resultat

Dies bewirkt, dass durch das XSLT-Stylseheet das folgende XML-Dokument erzeugt wird:

```xml
<DocumentFunction name="SavePathDefinition">
  <Path>C:\temp\Test_FileName.docx</Path>
  <CreateFolder>false</CreateFolder>
</DocumentFunction>
```

Dieses wird von OneOffixx so interpretiert, dass im Speichern-Dialog der Pfad „C:\temp\“ und der Dateinamen „Test_FileName.docx“ vorgeschlagen werden soll.<br>
Wenn der Ordner „C:\temp\“ nicht existiert soll der Ordner in diesem Beispiel *nicht* erstellt werden, da `CreateFolder` auf `false` gesetzt ist.

Speichern-Dialog:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/saveDialog.png)

Mit der Option `SaveNewDocumentOnOpen` kann definiert werden, ob der Benutzer nach dem Generieren eines Dokuments zum Speichern aufgefordert werden soll, indem ihm der Speichern-Dialog angezeigt wird.

### Bestehende Speicherpfade und Dateinamen

Unschön bei dieser Konfiguration: Wenn bei Dokumenten, welche bereits gespeichert wurden (z. B. TestDok.docx auf dem Desktop), der Speichern-Dialog aufgerufen wird, so wird erneut „Test_FileName“ unter C:\temp\ vorgeschlagen und nicht wie gewohnt der bestehende Name am bestehenden Speicherort („TestDok“ auf dem Desktop).


## Beispiel 2: Umfassendere Konfiguration

Hier ein Beispiel einer Konfiguration mit deutlich mehr Funktionalität:

```xml
<SavePathConfiguration>
  <SaveNewDocumentOnOpen>false</SaveNewDocumentOnOpen>
  
  <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:output method="xml" version="1.0" encoding="utf-8" />
    
    <!-- parameters from outside this stylesheet
         can be passed by an interface
         they are not used in this configuration -->
    <xsl:param name="filename" />
    <xsl:param name="path" />
    <xsl:param name="pathAndFilename" />
    <xsl:param name="targetFolderFileList" />
    
    <xsl:template match="/">
      
      <!-- add OneOffixx data -->
      <xsl:variable name="CustomElements.SavePathConfig.FileName" select="//Text[@id='CustomElements.SavePathConfig.FileName']" />
      <xsl:variable name="CustomElements.SavePathConfig.Path" select="//Text[@id='CustomElements.SavePathConfig.Path']" />
      <xsl:variable name="CustomElements.SavePathConfig.UpdateFileName" select="//Text[@id='CustomElements.SavePathConfig.UpdateFileName']" />
      <xsl:variable name="DocumentProperties.SavePath" select="//Text[@id='DocumentProperties.SavePath']" />
      <xsl:variable name="DocumentProperties.DocumentName" select="//Text[@id='DocumentProperties.DocumentName']" />
      
      <!-- evaluate boolean variables -->
      <xsl:variable name="documentWasSaved" select="boolean(normalize-space($DocumentProperties.SavePath) != '')" />
      <xsl:variable name="updateFileName" select="boolean($CustomElements.SavePathConfig.UpdateFileName = 'true')" />
      <xsl:variable name="keepExistingPath" select="boolean($documentWasSaved)" />
      <xsl:variable name="keepExistingName" select="boolean($documentWasSaved and not($updateFileName))" />
      
      <!-- set Path and Filename -->
      <xsl:variable name="Path">
        <xsl:choose>
          <xsl:when test="$keepExistingPath">
            <xsl:value-of select="$DocumentProperties.SavePath" />
          </xsl:when>
          <xsl:otherwise>
            <xsl:value-of select="$CustomElements.SavePathConfig.Path" />
          </xsl:otherwise>
        </xsl:choose>
      </xsl:variable>
      <xsl:variable name="Filename">
        <xsl:choose>
          <xsl:when test="$keepExistingName">
            <xsl:value-of select="$DocumentProperties.DocumentName" />
          </xsl:when>
          <xsl:otherwise>
            <xsl:value-of select="translate($CustomElements.SavePathConfig.FileName, ' ', '_')" />
          </xsl:otherwise>
        </xsl:choose>
      </xsl:variable>
      
      <!-- generate output XML -->
      <xsl:call-template name="generateOutputXML">
        <xsl:with-param name="path" select="concat($Path, $Filename,'.docx')" />
      </xsl:call-template>
      
    </xsl:template>
        
    <xsl:template name="generateOutputXML">
      <xsl:param name="path" />
      <xsl:param name="createFolder" />
      <xsl:element name="DocumentFunction" namespace="">
        <xsl:attribute name="name">SavePathDefinition</xsl:attribute>
        <xsl:element name="Path" namespace="">
          <xsl:value-of select="$path" />
        </xsl:element>
        <xsl:element name="CreateFolder" namespace="">
          <xsl:choose>
            <xsl:when test="$createFolder">
              <xsl:value-of select="$createFolder" />
            </xsl:when>
            <xsl:otherwise>false</xsl:otherwise>
          </xsl:choose>
        </xsl:element>
      </xsl:element>
    </xsl:template>
    
  </xsl:stylesheet>
  
</SavePathConfiguration>
```

Mit der Funktion `translate(...)` werden in diesem Beispiel alle Spaces zu Underscores („_“) ersetzt.

### Einbindung von Skripts

Hier wird auf folgende Skripts zugegriffen:

```xml
<CustomDataNode id="SavePathConfig.FileName">
  <Element id="DocParam.DateOfChange" fFormatingDate="yyMMdd" textafter=" " />
  <Text>Einverständniserklärung </Text>
  <Element id="Profile.User.LastName" separator=" " />
  <Element id="Profile.User.FirstName" />
</CustomDataNode>

<CustomDataNode id="SavePathConfig.Path">
  <Text>S:\Personaldossier\</Text>
</CustomDataNode>

<CustomDataNode id="SavePathConfig.UpdateFileName">
  <Text>false</Text>
</CustomDataNode>
```

Die Funktion der einzelnen Skripts sollte anhand des Namens selbsterklärend sein.<br>
Diese Skripts müssen auf jeder Vorlage verfügbar sein, bei der „Speicherpfad Definition“ mit dieser Konfiguration angehängt ist.

### Zugriff auf ToolboxData

Zudem wird auf diese OneOffixx-Inhalte zugegriffen:

* DocumentProperties.SavePath
* DocumentProperties.DocumentName

Damit diese Inhalte zur Verfügung stehen muss die Dokument-Funktion [ToolboxData]({{ site.baseurl }}/docfunc/de/df/toolboxdata) („Toolboxen im Editormodus“) angehängt sein.

### Bestehende Speicherpfade und Dateinamen

Mit dem obigen einbeziehen des bestehenden Speicherpfads und Dokumentnamens wird bei bereits gespeicherten Dokumenten bewirkt, dass der bestehende Speicherpfad und Dateinamen verwendet wird (siehe „Bestehende Speicherpfade und Dateinamen“ beim Beispiel 1 oben).

Ein Problem, welches hier aber bleibt: Wenn eine Word-Datei verschoben oder umbenannt wird werden die Felder `DocumentProperties.SavePath` und `DocumentProperties.DocumentName` nicht aktualisiert. In diesem Fall wird der alte Speicherpfad und Dateinamen vorgeschlagen, der bei der letzten Speicherung noch aktuell war.