---
layout: page
title: Extended Binding
permalink: "docfunc/de/df/extendedbinding"
language: de
---

Die Dokumentfunktion Extended Binding ermöglicht es über XSLT den Dokumentaufbau zu beeinflussen. Verglichen mit der Dokumentfunktion Skripts ist das Extended Binding in der Lage nebst dem Textinhalt noch weitere Attribute, wie Textfarbe, Grösse angwenadter Style etc. zu verändern.<br><br>
Das Extended Binding bietet viele neue Möglichkeiten, hat aber auch einige Tücken. Dokumente mit Extended Binding haben zum Beispiel eine viel höhere Ladezeit als Dokumente ohne Extended Binding. Des Weiteren ist das Pflegen von Dokumenten mit Extended Binding sehr aufwändig. - Man kann zusammenfassend sagen, wenn möglich sollte man Extended Binding nicht verwenden.

## Übersicht

- [Übersicht](#übersicht)
- [Tags](#tags)
- [Operatoren](#operatoren)
- [Zugriff auf Daten](#zugriffaufdaten)
- [Beispiele](#beispiele)

### Tags

__Allgemeine Tags:__

{:.table .table-striped}
| Tag | Funktion |
| --- | ---- |
| ``` <w:sdtContent></w:sdtContent> ``` | Diese Tags umschliessen das gesamte Extended Binding im Word-Dokument |
| ``` <xsl:stylesheet></xsl:stylesheet> ``` | Diese Tags umschliessen alle Templates |
| ``` <xsl:template></xsl:template> ``` | Diese Tags umschliessen ein Template |
| ``` <xsl:param></xsl:param> ``` | Diese Tags umschliessen einen Parameter |
| ``` <xsl:variable></xsl:variable> ``` | Diese Tags umschliessen eine Variable |
| ``` <xsl:value-of></xsl:value-of> ``` | Diese Tags umschliessen eine Variable, welche ausgegeben wird |
| ``` <xsl:call-template></xsl:call-template> ``` | Diese Tags umschliessen einen Templateaufruf |
| ``` <xsl:with-param></xsl:with-param> ``` | Diese Tags umschliessen einen Parameter, welcher beim Templateaufruf mitgegeben wird |
| ``` <w:p></w:p> ``` | Diese Tags umschliessen einen Paragraphen |
| ``` <w:r></w:r> ``` | Diese Tags umschliessen ein Set von WordprocessingML-Komponenten |
| ``` <w:t></w:t> ``` | Diese Tags umschliessen reinen Text |
| ``` <w:tbl></w:tbl> ``` | Diese Tags umschliessen eine gesamte Tabelle |
| ``` <w:tr></w:tr> ``` | Diese Tags umschliessene eine Tabellenzeile |
| ``` <w:tc></w:tc> ``` | Diese Tags umschliessene eine Tabellenzelle |


{:.table .table-striped}
|:--:|
| *Diese Aufzählung ist nicht abschliessend* |


__Formatierungs-Container Tags:__

{:.table .table-striped}
| Tag | Funktion | Link zu Attributen |
| --- | ---- |
| ```<w:pPr></w:pPr> ``` | Innerhalb dieser Tags wird die Formatierung für Paragraphen definiert | [Paragraph Properties](http://officeopenxml.com/WPparagraphProperties.php){:target="_blank"} |
| ```<w:rPr></w:rPr> ``` | Innerhalb dieser Tags wird die Formatierung für Runs definiert | [Run Properties](http://officeopenxml.com/WPtextFormatting.php) |
| ```<w:tblPr></w:tblPr> ``` | Innerhalb dieser Tags wird die Formatierung für gesamte Tabellen definiert | [Table Properties](http://officeopenxml.com/WPtableProperties.php) |
| ```<w:trPr></w:trPr> ``` | Innerhalb dieser Tags wird die Formatierung für Tabellenzeilen definiert | [TableRow Properties](http://officeopenxml.com/WPtableRowProperties.php) |
| ```<w:tcPr></w:tcPr> ``` | Innerhalb dieser Tags wird die Formatierung für Tabellenzellen definiert | [TableCell Properties](http://officeopenxml.com/WPtableCellProperties.php) |
| ```<w:t></w:t> ``` | Reiner Text hat keine Property-Tags, Text wird in den Run-Property-Tags definiert | [Text/Run Properties](http://officeopenxml.com/WPtextFormatting.php) |


#### Beispiele

__Empfänger mit Versandart:__

Die Versandart und der Empfänger haben unterschiedliche Style-Informationen, zudemm ist die Versandart eine optionale Eingabe. Wird gewünscht, dass der Empfänger eine Zeile nachrückt wenn die Versandart nicht ausgefüllt ist muss dies mit Extended Binding gelöst werden. Die üblichen Skripts können nicht verschiedene Style-Informationen in einem Skript verwenden.

{:.table .table-striped}
|:--:|
| ![x]({{ site.baseurl }}/assets/content-images/docfunc/de/ExtendedBindingTransmission.PNG){:   style="border:2px solid black;"} |
|:--:|
| *Beispiel eines Empfänger mit und ohne Versandart* |

```xml
<!-- Template für Empfänger mit optionaler Versandart. -->
<xsl:template name="OptionalTransmission">
    <!-- Variable mit Inhalt der Versandart. -->
    <xsl:variable name="Transmission" select="//Text[@id='CustomElements.Versandart']" />
    <!-- Variable mit Inhalt des Empfängers. -->
    <xsl:variable name="Anschrift" select="//Text[@id='CustomElements.Anschrift']" />
    <!-- Condition bei welcher geprüft wird of die Variable für die Versandart Inhalt hat. -->
    <xsl:if test="normalize-space($Transmission) = ''">
    <!-- Aufruf des Templates, welches Spaces durch Umbrüche ersetzt, damit die Empfängerinformationen untereinander angezeigt werden. -->
      <xsl:call-template name="StringToList">
        <xsl:with-param name="string" select="//Text[@id='CustomElements.Anschrift']" />
      </xsl:call-template>
    </xsl:if>
    <xsl:if test="normalize-space($Transmission) != ''">
      <w:p>
        <w:pPr>
          <w:pStyle w:val="Transmission" />
        </w:pPr>
        <w:r>
          <w:t>
            <xsl:value-of select="$Transmission" />
          </w:t>
        </w:r>
      </w:p>
    <!-- Aufruf des Templates, welches Spaces durch Umbrüche ersetzt, damit die Empfängerinformationen untereinander angezeigt werden. -->
        <xsl:call-template name="StringToList">
          <xsl:with-param name="string" select="//Text[@id='CustomElements.Anschrift']" />
        </xsl:call-template>
    </xsl:if>
  </xsl:template>
```

__Dynamische Tabellen:__

Tabellen mit statischer Anzahl Zeilen und Spalten aber optionaler Anzeige der Zeilen und Spalten sind ein weiteres Beispiel für den Einsatz von Extended Binding. Ob eine Zeile oder Spalte angezeigt wird, kann man im Dokumenten-Parameter via CheckBox definieren.

{:.table .table-striped}
|:--:|
| ![x]({{ site.baseurl }}/assets/content-images/docfunc/de/DynamicTable.PNG){:   style="border:2px solid black;"} |
|:--:|
| *Beispiel einer Tabelle mit dynamisch angezeigten Zeilen / Spalten* |

```xml
<!-- Template für dynamisch angezeigte Tabelle -->
<xsl:template name="DynamicTable">
    <w:p />
    <w:tbl>
      <w:tblPr>
        <w:tblStyle w:val="Tabellenraster" />
        <w:tblW w:w="0" w:type="auto" />
        <w:tblLook w:val="04A0" w:firstRow="1" w:lastRow="0" w:firstColumn="1" w:lastColumn="0" w:noHBand="0" w:noVBand="1" />
      </w:tblPr>
      <w:tblGrid>
        <w:gridCol w:w="1701" />
        <w:gridCol w:w="1701" />
      </w:tblGrid>
      <!-- Condition bei welcher geprüft wird ob die erste Zeile angezeigt werden soll [DocParam.Row1 = Erste Zeile anzeigen] -->
      <xsl:if test="//CheckBox[@id='DocParam.Row1'] = 'true'">
        <w:tr>
          <!-- Condition bei welcher geprüft wird ob die erste Spalte angezeigt werden soll [DocParam.Column1 = Erste Spalte anzeigen] -->
          <xsl:if test="//CheckBox[@id='DocParam.Column1'] = 'true'">
            <w:tc>
              <w:tcPr>
                <w:tcW w:w="1701" w:type="dxa" />
              </w:tcPr>
              <w:p>
                <w:r>
                  <w:t>
                  Zeile 1 Spalte 1
                  </w:t>
                </w:r>
              </w:p>
            </w:tc>
          </xsl:if>
          <!-- Condition bei welcher geprüft wird ob die zweite Spalte angezeigt werden soll [DocParam.Column2 = Zweite Spalte anzeigen] -->
          <xsl:if test="//CheckBox[@id='DocParam.Column2'] = 'true'">
            <w:tc>
              <w:tcPr>
                <w:tcW w:w="1701" w:type="dxa" />
              </w:tcPr>
              <w:p>
                <w:r>
                  <w:t>
                  Zeile 1 Spalte 2
                  </w:t>
                </w:r>
              </w:p>
            </w:tc>
          </xsl:if>
        </w:tr>
      </xsl:if>
      <!-- Condition bei welcher geprüft wird ob die zweite Zeile angezeigt werden soll [DocParam.Row2 = Zweite Zeile anzeigen] -->
      <xsl:if test="//CheckBox[@id='DocParam.Row2'] = 'true'">
        <w:tr>
          <!-- Condition bei welcher geprüft wird ob die erste Spalte angezeigt werden soll [DocParam.Column1 = Erste Spalte anzeigen] -->
          <xsl:if test="//CheckBox[@id='DocParam.Column1'] = 'true'">
            <w:tc>
              <w:tcPr>
                <w:tcW w:w="1701" w:type="dxa" />
              </w:tcPr>
              <w:p>
                <w:r>
                  <w:t>
                  Zeile 2 Spalte 1
                  </w:t>
                </w:r>
              </w:p>
            </w:tc>
          </xsl:if> 
          <!-- Condition bei welcher geprüft wird ob die zweite Spalte angezeigt werden soll [DocParam.Column2 = Zweite Spalte anzeigen] -->
          <xsl:if test="//CheckBox[@id='DocParam.Column2'] = 'true'">
            <w:tc>
              <w:tcPr>
                <w:tcW w:w="1701" w:type="dxa" />
              </w:tcPr>
              <w:p>
                <w:r>
                  <w:t>
                  Zeile 2 Spalte 2
                  </w:t>
                </w:r>
              </w:p>
            </w:tc>
          </xsl:if> 
        </w:tr>
      </xsl:if>
    </w:tbl>
    <w:p />
  </xsl:template>

```