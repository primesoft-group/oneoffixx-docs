---
layout: page
title: Aktenverzeichnis
permalink: "docfunc/de/df/fileindex"
language: de
---

Mit dieser Dokumentfunktion können Titelblätter für Aktenmappen erstellt werden. In der Konfiguration wird ein Fenster konfiguriert, das beim Öffnen des Dokuments erscheint. Das gesamte resultierende Dokument besteht aus einem extended Binding, das anhand der im Dialog eingegebenen Informationen das gesamte Dokument erstellt.

So sieht der Aufbau der Konfiguration aus:

```xml
<Folders>
    <Folder DisplayName="Mappe weiss" Description="Beilagen zum Antrag an den Regierungsrat" />
    <Folder DisplayName="Mappe rot" Description="Geheime Dokumente" />
    <Folder DisplayName="Mappe gelb" Description="Antrag an den Stadtpräsidenten" />
    <Folder DisplayName="Benutzerdefiniert" IsDescriptionChangeable="true" />
  </Folders>
  <FolderProperties>
    <Property DisplayName="Geschäftsbezeichnung" />
    <Property DisplayName="Sachverhalt/Vorhaben/Titel" />
    <Property DisplayName="Geschäftsnummern" />
  </FolderProperties>
  <DefaultFileNames>
    <FileName DisplayText="Baugesuch - Grundriss" />
    <FileName DisplayText="Grundstücksschätzung" />
    <FileName DisplayText="Report Brandschutzkontrolle" />
  </DefaultFileNames>
```

Diese Konfiguration resultiert in folgendem Fenster:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/fileIndex.png)

Im OneOffixxDocumentPart (bei entpackten docx-Dateien unter /customXml/itemX.xml) wird nun der DocumentPart "FileIndexData" hinzugefügt.
Dieser kann z.B. so aussehen:

```xml
<?xml version="1.0" encoding="utf-16"?><OneOffixxDocumentPart xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" id="c29b638e-a25c-489d-8884-023954c9b110" tId="b19e5174-c038-410d-9d6f-3bb4f6095a18" mtId="275af32e-bc40-45c2-85b7-afb1c0382653" tname="sdfaasdf ohne rsids" revision="1" createdmajorversion="2" createdminorversion="0" created="2017-05-23T13:49:03.3182032+02:00" modifiedmajorversion="2" modifiedminorversion="3" modified="2017-05-23T13:49:03.3182032+02:00" profile="00000000-0000-0000-0000-000000000000" mode="SavedDocument" colormode="None" lcid="2055" xmlns="http://schema.oneoffixx.com/OneOffixxDocumentPart/1">
  <Content>
    <DataModel xmlns="">
      <FileIndexData windowwidth="0" windowheight="0" minwindowwidth="0" maxwindowwidth="0" minwindowheight="0" maxwindowheight="0">
        <RawText id="FileIndex">
          <![CDATA[<?xml version="1.0" encoding="utf-16"?>
          <FileIndexCxmlPart xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schema.oneoffixx.com/OneOffixxDocumentPart/FileIndex">
            <FolderData>
              <FolderData Id="07226303-6d82-4c69-be5d-4fce7996c02e" Description="Beilagen zum Antrag an den Regierungsrat" DisplayName="Mappe weiss" IsDefault="false" IsDescriptionChangeable="false" />
              <FolderData Id="f3fa4e32-cadc-49b0-8b83-04cd122b0f6b" Description="Geheime Dokumente" DisplayName="Mappe rot" IsDefault="false" IsDescriptionChangeable="false" />
              <FolderData Id="6fb17343-5cb5-437f-adf4-f4b4b5ae6fdc" Description="Antrag an den Stadtpräsidenten" DisplayName="Mappe gelb" IsDefault="false" IsDescriptionChangeable="false" />
              <FolderData Id="3eb6d1db-2e1f-40f8-abc9-835dac8398ce" Description="Benutzerdefinierte Mappe" DisplayName="Benutzerdefiniert" IsDefault="false" IsDescriptionChangeable="true" />
            </FolderData>
            <FileData>
              <FileData Id="ac0d8208-6ec9-40f1-b761-f2523b36a9af" Name="Baugesuch - Grundriss">
                <SelectedFolders>
                  <boolean>true</boolean>
                  <boolean>false</boolean>
                  <boolean>true</boolean>
                  <boolean>false</boolean>
                </SelectedFolders>
              </FileData>
              <FileData Id="ac646e48-7466-4ccd-89b8-6b7f16ed37b8" Name="Report Brandschutzkontrolle">
                <SelectedFolders>
                  <boolean>false</boolean>
                  <boolean>true</boolean>
                  <boolean>true</boolean>
                  <boolean>false</boolean>
                </SelectedFolders>
              </FileData>
              <FileData Id="6d0c6642-c5ae-43e5-9e55-2374587be6d0" Name="Report Brandschutzkontrolle">
                <SelectedFolders>
                  <boolean>true</boolean>
                  <boolean>false</boolean>
                  <boolean>true</boolean>
                  <boolean>true</boolean>
                </SelectedFolders>
              </FileData>
            </FileData>
            <PropertyData>
              <PropertyData Id="00000000-0000-0000-0000-000000000000" Value="Abc" DisplayName="Geschäftsbezeichnung" />
              <PropertyData Id="00000000-0000-0000-0000-000000000000" Value="Def" DisplayName="Sachverhalt/Vorhaben/Titel" />
              <PropertyData Id="00000000-0000-0000-0000-000000000000" Value="Ghi" DisplayName="Geschäftsnummern" />
            </PropertyData>
            <DefaultFileNames>
              <string>Baugesuch - Grundriss</string>
              <string>Grundstücksschätzung</string>
              <string>Report Brandschutzkontrolle</string>
            </DefaultFileNames>
          </FileIndexCxmlPart>
          ]]>
          </RawText>
        <NodeGroup id="FileIndex.Properties" row="0" column="0" columnspan="0" label="" visible="True">
          <Text id="Property0" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="Geschäftsbezeichnung" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Abc]]></Text>
          <Text id="Property1" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="Sachverhalt/Vorhaben/Titel" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Def]]></Text>
          <Text id="Property2" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="Geschäftsnummern" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Ghi]]></Text>
        </NodeGroup>
        <NodeGroup id="FileIndex.Folder0" row="0" column="0" columnspan="0" label="" visible="True">
          <Text id="Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Mappe weiss]]></Text>
          <Text id="Description" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Beilagen zum Antrag an den Regierungsrat]]></Text>
          <Text id="File0Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Baugesuch - Grundriss]]></Text>
          <Text id="File1Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Report Brandschutzkontrolle]]></Text>
        </NodeGroup>
        <NodeGroup id="FileIndex.Folder1" row="0" column="0" columnspan="0" label="" visible="True">
          <Text id="Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Mappe rot]]></Text>
          <Text id="Description" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Geheime Dokumente]]></Text>
          <Text id="File0Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Report Brandschutzkontrolle]]></Text>
        </NodeGroup>
        <NodeGroup id="FileIndex.Folder2" row="0" column="0" columnspan="0" label="" visible="True">
          <Text id="Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Mappe gelb]]></Text>
          <Text id="Description" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Antrag an den Stadtpräsidenten]]></Text>
          <Text id="File0Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Baugesuch - Grundriss]]></Text>
          <Text id="File1Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Report Brandschutzkontrolle]]></Text>
          <Text id="File2Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Report Brandschutzkontrolle]]></Text>
        </NodeGroup>
        <NodeGroup id="FileIndex.Folder3" row="0" column="0" columnspan="0" label="" visible="True">
          <Text id="Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Benutzerdefiniert]]></Text>
          <Text id="Description" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Benutzerdefinierte Mappe]]></Text>
          <Text id="File0Name" row="0" column="0" columnspan="0" multiline="False" multilinerows="3" locked="False" label="" readonly="False" visible="True" required="False" regex="" validationmessage="" tooltip="" tracked="False"><![CDATA[Report Brandschutzkontrolle]]></Text>
        </NodeGroup>
      </FileIndexData>
    </DataModel>
  </Content>
</OneOffixxDocumentPart>
```

Dieser Inhalt kann z. B. über folgendes Extended Binding in einem Dokument ausgegeben werden:

```xml
<w:sdtContent xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">
  <xsl:for-each select="//*//FileIndexData/NodeGroup">
    <w:p w:rsidR="00D3266E" w:rsidRPr="00C12586" w:rsidRDefault="00D3266E" w:rsidP="00D3266E">
      <w:pPr>
        <w:pStyle w:val="BDVTitel" />
        <w:tabs>
          <w:tab w:val="right" w:pos="10348" />
        </w:tabs>
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
      </w:pPr>
      <w:r w:rsidRPr="00C12586">
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
        <w:t>Aktenverzeichnis </w:t>
      </w:r>
      <w:r>
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
        <w:t>
          <xsl:value-of select="./Text[@id='Name']" />
        </w:t>
      </w:r>
    </w:p>
    <w:p w:rsidR="00D3266E" w:rsidRDefault="00D3266E" w:rsidP="00D3266E">
      <w:pPr>
        <w:pStyle w:val="BDVStandard" />
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
      </w:pPr>
    </w:p>
    <xsl:for-each select="./Text[starts-with(@id,'Property')]">
      <w:p w:rsidR="00D3266E" w:rsidRPr="008C62F8" w:rsidRDefault="00D3266E" w:rsidP="00D3266E">
        <w:pPr>
          <w:pStyle w:val="BDVStandard" />
          <w:tabs>
            <w:tab w:val="left" w:pos="3402" />
          </w:tabs>
          <w:ind w:left="3402" w:hanging="3402" />
          <w:rPr>
            <w:rFonts w:eastAsia="Arial Unicode MS" />
          </w:rPr>
        </w:pPr>
        <w:r w:rsidRPr="00E00404">
          <w:rPr>
            <w:rFonts w:eastAsia="Arial Unicode MS" />
            <w:b />
          </w:rPr>
          <w:t>
            <xsl:value-of select="./@label" />
          </w:t>
        </w:r>
        <w:r w:rsidRPr="008C62F8">
          <w:rPr>
            <w:rFonts w:eastAsia="Arial Unicode MS" />
          </w:rPr>
          <w:tab />
          <w:t>
            <xsl:value-of select="." />
          </w:t>
        </w:r>
      </w:p>
    </xsl:for-each>
    <w:p w:rsidR="00D3266E" w:rsidRDefault="00D3266E" w:rsidP="00D3266E">
      <w:pPr>
        <w:pStyle w:val="BDVStandard" />
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
      </w:pPr>
    </w:p>
    <w:p w:rsidR="00D3266E" w:rsidRDefault="00D3266E" w:rsidP="00D3266E">
      <w:pPr>
        <w:pStyle w:val="BDVStandard" />
        <w:pBdr>
          <w:top w:val="single" w:sz="4" w:space="1" w:color="auto" />
        </w:pBdr>
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
      </w:pPr>
    </w:p>
    <w:p w:rsidR="00D3266E" w:rsidRDefault="00D3266E" w:rsidP="00D3266E">
      <w:pPr>
        <w:pStyle w:val="BDVStandard" />
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
      </w:pPr>
      <w:r>
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
        <w:t>
          <xsl:value-of select="./Text[@id='Description']" />
        </w:t>
      </w:r>
    </w:p>
    <w:p w:rsidR="00D3266E" w:rsidRPr="00C12586" w:rsidRDefault="00D3266E" w:rsidP="00D3266E">
      <w:pPr>
        <w:pStyle w:val="BDVStandard" />
        <w:rPr>
          <w:rFonts w:eastAsia="Arial Unicode MS" />
        </w:rPr>
      </w:pPr>
    </w:p>
    <w:tbl>
      <w:tblPr>
        <w:tblW w:w="0" w:type="auto" />
        <w:tblBorders>
          <w:bottom w:val="single" w:sz="4" w:space="0" w:color="auto" />
          <w:insideH w:val="single" w:sz="4" w:space="0" w:color="auto" />
        </w:tblBorders>
        <w:tblCellMar>
          <w:left w:w="0" w:type="dxa" />
          <w:right w:w="0" w:type="dxa" />
        </w:tblCellMar>
        <w:tblLook w:val="04A0" w:firstRow="1" w:lastRow="0" w:firstColumn="1" w:lastColumn="0" w:noHBand="0" w:noVBand="1" />
      </w:tblPr>
      <w:tblGrid>
        <w:gridCol w:w="622" />
        <w:gridCol w:w="8450" />
      </w:tblGrid>
      <w:tr w:rsidR="00D3266E" w:rsidRPr="00C12586" w:rsidTr="00B13147">
        <w:tc>
          <w:tcPr>
            <w:tcW w:w="671" w:type="dxa" />
          </w:tcPr>
          <w:p w:rsidR="00D3266E" w:rsidRPr="00C12586" w:rsidRDefault="00D3266E" w:rsidP="00B13147">
            <w:pPr>
              <w:pStyle w:val="BDVStandardTitel" />
              <w:jc w:val="center" />
              <w:rPr>
                <w:rFonts w:eastAsia="Arial Unicode MS" />
              </w:rPr>
            </w:pPr>
            <w:r w:rsidRPr="00C12586">
              <w:rPr>
                <w:rFonts w:eastAsia="Arial Unicode MS" />
              </w:rPr>
              <w:t>Nr.</w:t>
            </w:r>
          </w:p>
        </w:tc>
        <w:tc>
          <w:tcPr>
            <w:tcW w:w="9687" w:type="dxa" />
          </w:tcPr>
          <w:p w:rsidR="00D3266E" w:rsidRPr="00C12586" w:rsidRDefault="00D3266E" w:rsidP="00B13147">
            <w:pPr>
              <w:pStyle w:val="BDVStandardTitel" />
              <w:rPr>
                <w:rFonts w:eastAsia="Arial Unicode MS" />
              </w:rPr>
            </w:pPr>
            <w:r w:rsidRPr="00C12586">
              <w:rPr>
                <w:rFonts w:eastAsia="Arial Unicode MS" />
              </w:rPr>
              <w:t>Bezeichnung des Aktenstücks</w:t>
            </w:r>
          </w:p>
        </w:tc>
      </w:tr>
      <xsl:for-each select="./Text[starts-with(@id,'File')]">
        <w:tr w:rsidR="00D3266E" w:rsidRPr="0010445B" w:rsidTr="00B13147">
          <w:tc>
            <w:tcPr>
              <w:tcW w:w="671" w:type="dxa" />
            </w:tcPr>
            <w:p w:rsidR="00D3266E" w:rsidRPr="0010445B" w:rsidRDefault="00D3266E" w:rsidP="00B13147">
              <w:pPr>
                <w:pStyle w:val="BDVStandard" />
                <w:spacing w:before="60" w:after="60" />
                <w:jc w:val="center" />
                <w:rPr>
                  <w:rFonts w:eastAsia="Arial Unicode MS" />
                </w:rPr>
              </w:pPr>
              <w:r>
                <w:rPr>
                  <w:rFonts w:eastAsia="Arial Unicode MS" />
                </w:rPr>
                <w:t>
                  <xsl:value-of select="position()" />.</w:t>
              </w:r>
            </w:p>
          </w:tc>
          <w:tc>
            <w:tcPr>
              <w:tcW w:w="9687" w:type="dxa" />
            </w:tcPr>
            <w:p w:rsidR="00D3266E" w:rsidRPr="0010445B" w:rsidRDefault="00D3266E" w:rsidP="00B13147">
              <w:pPr>
                <w:pStyle w:val="BDVStandard" />
                <w:spacing w:before="60" w:after="60" />
                <w:rPr>
                  <w:rFonts w:eastAsia="Arial Unicode MS" />
                </w:rPr>
              </w:pPr>
              <w:r>
                <w:rPr>
                  <w:rFonts w:eastAsia="Arial Unicode MS" />
                </w:rPr>
                <w:t>
                  <xsl:value-of select="." />
                </w:t>
              </w:r>
              <w:r>
                <w:rPr>
                  <w:rFonts w:eastAsia="Arial Unicode MS" />
                </w:rPr>
                <w:tab />
              </w:r>
            </w:p>
          </w:tc>
        </w:tr>
      </xsl:for-each>
    </w:tbl>
    <w:p w:rsidR="00D3266E" w:rsidRDefault="00D3266E">
      <w:pPr>
        <w:rPr>
          <w:rFonts w:ascii="Times New Roman" w:eastAsia="Times New Roman" w:hAnsi="Times New Roman" w:cs="Times New Roman" />
          <w:sz w:val="24" />
          <w:szCs w:val="20" />
          <w:lang w:val="fr-CH" w:eastAsia="de-DE" />
        </w:rPr>
      </w:pPr>
      <w:r>
        <w:rPr>
          <w:lang w:val="fr-CH" />
        </w:rPr>
        <w:br w:type="page" />
      </w:r>
    </w:p>
  </xsl:for-each>
</w:sdtContent>
```