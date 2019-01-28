---
layout: page
title: Extended Binding
permalink: "docfunc/de/df/extendedbinding"
language: de
---

Die Dokumentfunktion Extended Binding ermöglicht es über XSLT den Dokumentaufbau zu beeinflussen. Verglichen mit der Dokumentfunktion Skripts ist das Extended Binding in der Lage nebst dem Textinhalt noch weitere Attribute, wie Textfarbe, Grösse angwenadter Style etc. zu verändern.<br><br>
Das Extended Binding bietet viele Möglichkeiten, hat aber auch einige Tücken. Dokumente mit Extended Binding haben zum Beispiel eine viel höhere Ladezeit als Dokumente ohne Extended Binding. Des Weiteren ist das Pflegen von Dokumenten mit Extended Binding sehr aufwändig. - Man kann zusammenfassend sagen, wenn möglich sollte man Extended Binding nicht verwenden.

## Übersicht

- [Übersicht](#übersicht)
- [Tags](#tags)
- [Operatoren](#operatoren)
- [Zugriff auf Daten](#zugriffaufdaten)
- [Funktionalitäten](#funktionalitäten)
- [Beispiele](#beispiele)

## Tags

__Allgemeine Tags:__

{:.table .table-striped}
| Tag | Funktion |
| --- | --- |
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
| <sub>**Diese Aufzählung ist nicht abschliessend*</sub> |


__Formatierungs-Container Tags:__

{:.table .table-striped}
| Tag | Funktion | Link zu Attributen |
| --- | ---- | --- |
| ```<w:pPr></w:pPr> ``` | Innerhalb dieser Tags wird die Formatierung für Paragraphen definiert | [Paragraph Properties](http://officeopenxml.com/WPparagraphProperties.php){:target="_blank"} |
| ```<w:rPr></w:rPr> ``` | Innerhalb dieser Tags wird die Formatierung für Runs definiert | [Run Properties](http://officeopenxml.com/WPtextFormatting.php){:target="_blank"} |
| ```<w:tblPr></w:tblPr> ``` | Innerhalb dieser Tags wird die Formatierung für gesamte Tabellen definiert | [Table Properties](http://officeopenxml.com/WPtableProperties.php){:target="_blank"} |
| ```<w:trPr></w:trPr> ``` | Innerhalb dieser Tags wird die Formatierung für Tabellenzeilen definiert | [TableRow Properties](http://officeopenxml.com/WPtableRowProperties.php){:target="_blank"} |
| ```<w:tcPr></w:tcPr> ``` | Innerhalb dieser Tags wird die Formatierung für Tabellenzellen definiert | [TableCell Properties](http://officeopenxml.com/WPtableCellProperties.php){:target="_blank"} |
| ```<w:t></w:t> ``` | Reiner Text hat keine Property-Tags, Text wird in den Run-Property-Tags definiert | [Text/Run Properties](http://officeopenxml.com/WPtextFormatting.php){:target="_blank"} |

## Operatoren

{:.table .table-striped}
| Operator | Funktion |
| --- | - |
| ``` + ``` | Addition |
| ``` - ``` | Subtraktion |
| ``` * ``` | Multiplikation |
| ``` div ``` | Division |
| ```=``` | Gleich |
| ``` != ``` | Ungleich |
| ``` < / &lt; ``` | Kleiner als |
| ``` > / &gt; ``` | Grösesr als |
| ``` <= / &gt;= ``` | Kleiner Gleich |
| ``` >= / &lt;= ``` | Grösser Gleich |
| ``` or ``` | Logisches Oder |
| ``` and ``` | Logisches Und |
| ``` Mod ``` | Modulus |
| ``` $ ``` | Wird verwendet um eine Variable anzusprechen |
| ``` // ``` | Der Doppel-Slash gibt einen Pfad an mit Root als Ausgangspunkt |
| ``` / ``` | Der Einfache-Slash gibt einen Pfad an mit der jetztigen Position als Ausgangspunkt |
| ``` . ``` | Der Einfache-Punkt spricht das aktuelle Element an |
| ``` .. ``` | Der Doppel-Punkt spricht das Elternelement des aktuellen Elemnts an |
| ``` @ ``` | Das @ spricht Attribute an |
| ``` | ``` | Das &#124;-Zeichen ist ein logisches Und, man kann mehrere Elemente miteinander logisch verbinden |
| ``` not() ``` | Das wird für eine Negation verwendet |

## Zugriff auf Daten

Mit dem Extended Binding kann man wie auch mit den Skripten auf Daten zugreifen und diese weiter verwenden. Die Daten werden dabei in einer Variable gespeichert.

__Beispiel für eine Variable:__
```xml
  <xsl:variable name="[NAME DER VARIABLE]" select="[REFERNZIERTES OBJEKT]" />
```

__Beispiel für den Zugriff auf ein Textfeld im Dokumenten-Parameter:__
```xml
  <xsl:variable name="Subject" select="//Text[@id='DocParam.Subject']" />
```
<sub>**Der Präfix 'DocParam' ist nicht zwingend nötig die OneOffixx-Konventionen schreiben jedoch vor, dass Felder im Dokumenten-Parameter mit diesem Präfix zu versehen sind.*</sub>

__Beispiel für den Zugriff auf eine CheckBox im Dokumenten-Parameter:__
```xml
  <xsl:variable name="CheckBox" select="//CheckBox[@id='DocParam.CheckBox']" />
```
<sub>**Der Präfix 'DocParam' ist nicht zwingend nötig die OneOffixx-Konventionen schreiben jedoch vor, dass Felder im Dokumenten-Parameter mit diesem Präfix zu versehen sind.*</sub>

__Beispiel für den Zugriff auf eine ComboBox:__
```xml
  <xsl:variable name="ComboBox" select="//ComboBox[@id='DocParam.Combo']/@selectedValue" />
```
<sub>**Der Präfix 'DocParam' ist nicht zwingend nötig die OneOffixx-Konventionen schreiben jedoch vor, dass Felder im Dokumenten-Parameter mit diesem Präfix zu versehen sind.*</sub>

__Beispiel für den Zugriff auf in Skript:__
```xml
  <xsl:variable name="ExampleSkript" select="//Text[@id='CustomElements.ExampleSkript']" />
```
<sub>**Anders als beim Zugriff auf den Dokumenten-Parameter ist hier der Präfix 'CustomElements' zwingend notwendig.*</sub>

## Funktionalitäten

__Normalize-Space:__

Die Funktion "Normalize-Space()" bereinigt Variablen, Eingabefelder, etc... Das heisst sollte in einem Feld versehentlicher Weise ein Leerschlag sein, wird dieses als leer betrachtet.
```xml
  <xsl:variable name="Subject" select="normalize-space(//Text[@id='DocParam.Subject'])" />
```
<sub>**Die obenstehende Variable enthält den Inhalt des Betrefffelds aus dem Dokumenten-Parameter bereinigt von überflüssigen Leerschlägen.*</sub>

__If:__

Die Funktion "If" bietet die Möglichkeit Aktionen von Bedingungen abhängig zu machen.

```xml
  <xsl:template name="ConditionedSubject">
    <xsl:variable name="Subject" select="//Text[@id='DocParam.Subject']">
    <xsl:if test="normalize-space($Subject) != ''">
      <w:p>
        <w:r>
          <w:t>
            <xsl:value-of select="$Subject" />
          </w:t>
        </w:r>
      </w:p>
    </xsl:if>
  </xsl:template>
```
<sub>**Das obenstehende Template prüft ob das Betrefffeld im Dokumenten-Parameter nicht leer ist, wenn das zutrifft wird der Wert ausgegeben, ansonsten geschieht nichts.*</sub>

__Choose:__

Die Funktion "Choose" ist eine Erweiterung der Funktion "IF" sie bietet zusätzlich die Möglichkeit eine Anweisung zu machen, wenn die Bedingung nicht zu trifft. Hierfür werden die Tags "When" und "Otherwise" verwendet. Das was zwischen den When-Tags steht wird ausgeführt, wenn die Bedingung zutrifft, das was zwischen den Otherwise-Tags steht wird ausgeführt, wenn die Bedingung nicht zutrifft.

```xml
  <xsl:template name="ConditionedSubject">
    <xsl:variable name="Subject" select="//Text[@id='DocParam.Subject']" />
    <w:p>
      <w:r>
        <w:t>
          <xsl:choose>
            <xsl:when test="normalize-space($Subject) != ''">
              <xsl:value-of select="$Subject" />
            </xsl:when>
            <xsl:otherwise>
              Subject is empty
            </xsl:otherwise>
          </xsl:choose>
        </w:t>
      </w:r>
    </w:p>
  </xsl:template>  
```
<sub>**Das obenstehende Template prüft ob das Betrefffeld im Dokumenten-Parameter nicht leer ist, wenn das zutrifft wird der Wert ausgegeben, falls der das Betrefffeld leer ist, wir der Informationstext 'Subject is empty' ausgegeben.*</sub>

__Substring:__

Die Funktion "Substring" wird in zwei Unterfunktionen unterteilt, es gibt __Substirng-before__ und __Substring-after__. Man übergibt dem Template einen String (Text) und ein Charakter (Zeichen) bei welchem der Text getrennt werden soll.
```xml
  <xsl:template name="SubstringBeforeEMail">
    <xsl:variable name="E-Mail" select="//Text[@id='DocParam.E-Mail']" />
    <xsl:variable name="Charakter">@</xsl:variable>
    <w:p>
      <w:r>
        <w:t>
          <xsl:value-of select="substring-before($E-Mail, $Charakter)" />
        </w:t>
      </w:r>
    </w:p>
  </xsl:template>

  <xsl:template name="SubstringAfterEMail">
    <xsl:variable name="E-Mail" select="//Text[@id='DocParam.E-Mail']" />
    <xsl:variable name="Charakter">@</xsl:variable>
    <w:p>
      <w:r>
        <w:t>
          <xsl:value-of select="substring-after($E-Mail, $Charakter)" />
        </w:t>
      </w:r>
    </w:p>
  </xsl:template>
```
<sub>**Das erste Template gibt alles aus was in der E-Mail vor dem "@" steht, das zweite Template gibt alles aus, was nach dem "@" steht.<br>
Achtung das Zeichen, welches als Ausgangspunkt verwendet wird in diesem Fall "@" wird nicht mitausgegeben.*</sub>

__Concat:__

Die Funktion "Concat" ist das Gegenteil der Funktion Substring, sie verbindet Zeichenketten.
```xml
  <xsl:template name="ConcatEMail">
    <xsl:variable name="FirstName" select="//Text[@id='DocParam.FirstName']" />
    <xsl:variable name="LastName" select="//Text[@id='DocParam.LastName']" />
    <w:p>
      <w:r>
        <w:t>
          <xsl:value-of select="concat($FirstName, '.', $LastName, '@beispiel.com')" />
        </w:t>
      </w:r>
    </w:p>
  </xsl:template>
```
<sub>**Das obenstehende Template erstellt aus dem Vornamen und Nachnamen eine E-Mail Adresse, zwischen Vornamen und Nachnamen wird ein Punkt gesetzt und nachdem Nachnamen wird noch "@beispiel.com" angehängt.*</sub>

## Beispiele

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
    </xsl:if>
    <!-- Aufruf des Templates, welches Spaces durch Umbrüche ersetzt, damit die Empfängerinformationen untereinander angezeigt werden. -->
    <xsl:call-template name="StringToList">
      <xsl:with-param name="string" select="$Anschrift" />
    </xsl:call-template>
  </xsl:template>
```

Verbesserungen:
* Variable `Anschrift` wurde vorher nicht benutzt
* `if-A if-!A` ersetzt mit `choose when-A otherwise`
* fixen Teil (Anschrift) aus Bedingung rausnehmen, da dieser _immer_ eingefügt werden muss
* `choose` entfernen, da nur noch in `otherwise` etwas vorhanden ist

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