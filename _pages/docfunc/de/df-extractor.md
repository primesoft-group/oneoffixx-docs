---
layout: page
title: Data Extractor
permalink: "docfunc/de/df/extractor"
language: de
---

Die Dokumentfunktion **Data Extractor** extrahiert Daten aus dem aktuellen Word Dokument und speichert diese in ein beliebiges Datenfile. Diese Dokumentfunktion wird üblicherweise von DMS Systeme wie ua. LoboDMS verwendet um das Word Dokument nach dem Speichervorgang korrekt indizieren zu können. 

Die Konfiguration des Data Extractors entählt ein XSLT Script um ein XML-Outputdokument zu generieren. Das XML-Outputdokument enthält Anweisungen wie das Datenfile gespeichert werden soll und den Inhalt des Datenfile. 

Das XML-Outputdokument ist wie folgt aufgebaut:
```xml
<Extractor>
    <!-- Anweisungen wie und wo das Datenfile gespeichert werden soll -->
	<GlobalSettings>
		<Settings>

			<Active> true | false </Active>
            <!-- Relativer Pfad zum Speicherort des Word Dokument -->
			<Path>.</Path>
            <!-- File Extension des Datenfiles -->
			<Extension>xml | csv | oocx | oneoffixx </Extension>
            <!-- Soll das Datenfile versteckt im Filesystem abgelegt werden, ist diese Option true -->
			<Hidden> true | false </Hidden>
		</Settings>
	</GlobalSettings>
	<FileContent>
        <!-- Inhalte des Datenfiles -->
	</FileContent>
</Extractor
```

Als Input in die XSLT Transformation wird das Word OpenXML Dokument inkl. aller CustomXML Daten übergeben.

Eine Konfiguration des **Data Extractors** könnte wie folgt aussehen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0" 
xmlns:xsl="http://www.w3.org/1999/XSL/Transform" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns:oopart="http://schema.oneoffixx.com/OneOffixxContactsPart/1" xmlns:properties="http://schemas.openxmlformats.org/officeDocument/2006/custom-properties" xmlns:cp="http://schemas.openxmlformats.org/package/2006/metadata/core-properties" xmlns:extendedproperties="http://schemas.openxmlformats.org/officeDocument/2006/extended-properties">
  <xsl:output method="xml" version="1.0" encoding="utf-8" />

  <!-- Haupt-Template -->
  <xsl:template match="/">
    <xsl:element name="Extractor">
      <xsl:call-template name="GlobalSettings"/>
      <xsl:call-template name="FileContent"/>
    </xsl:element>
  </xsl:template>

  <!-- Einstellungen zur Steuerung des Datenfiles -->
  <xsl:template name="GlobalSettings">
    <xsl:element name="Settings">
      <xsl:element name="Active">true</xsl:element>
      <xsl:element name="Path">.</xsl:element>
      <xsl:element name="Extension">xml</xsl:element>
      <xsl:element name="Hidden">false</xsl:element>
    </xsl:element>
  </xsl:template>

  <!-- FileContent des Datenfiles -->
  <xsl:template name="FileContent">
    <xsl:element name="FileContent">
      <xsl:call-template name="MyExtractorFile"/>
    </xsl:element>
  </xsl:template>

  <!-- Alle Dokumentparameter ausgeben -->
  <xsl:template name="MyExtractorFile">
    <xsl:element name="ExtractorData">      
      <xsl:call-template name="DocumentParameter"/>      
    </xsl:element>
  </xsl:template>
  
  <!-- Dokument Parameter Dokumentfunktion-->
  <xsl:template name="DocumentParameter">
    <xsl:if test="//Parameter">
        <xsl:for-each select="//Parameter/*">
            <xsl:if test="normalize-space(.)">
                <xsl:call-template name="Content">
                    <xsl:with-param name="node" select="."/>
                </xsl:call-template>
            </xsl:if>
        </xsl:for-each>
    </xsl:if>
  </xsl:template>
  
   <xsl:template name="Content">
        <xsl:param name="node"/>
        <xsl:variable name="name" select="$node/@id"/>
        <xsl:element name="{$name}">
            <xsl:apply-templates select="node()" />
        </xsl:element>
  </xsl:template>

</xsl:stylesheet>
```
