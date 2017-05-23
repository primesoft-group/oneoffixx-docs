---
layout: page
title: GlobalOOConnectInterfaceProvider / Schnittstellen Konverter für OneOffixx Connect
permalink: "docfunc/de/df/globalooconnectinterfaceprovider"
language: de
---

In seltenen Fällen kann es Sinn machen, dass eine Fremdapplikation beim Aufruf von OneOffixx keine sauberen Connect-Files übermittelt, sondern XML-Files mit einer beliebigen Struktur.

Dabei muss beim Aufruf von OneOffixx zusätzlich der Name des Interfaces mitgegeben werden.
Beim Client sieht ein solcher Aufruf so aus:<br>
`OneOffixx.exe /connector "C:\temp\testfile.xml" /interfaceType "myDefinedInterface"`

In dieser Dokument-Funktion werden nun mit XSLT die „Regeln“ für das „myDefinedInterface“ definiert, wie das erhaltene XML-File (hier testfile.xml) zu einem korrekten Connect-File umgeformt wird. Wir machen dies anhand eines Beispiels.

## testfile.xml

In unserem Beispiel hat „testfile.xml“ folgenden Inhalt:

```xml
<root>
  <anElement>
    <hereItIs>Test Content from XML file</hereItIs>
  </anElement>
  <anotherElement>don't care about this one</anotherElement>
</root>
```

## Beispiel-Szenario: CustomInterfaceConnector-Feld abfüllen

Bei diesem Szenario wollen wir mit obigem testfile.xml ein Feld des [CustomInterfaceConnector]({{ site.baseurl }}/docfunc/de/df/custominterfaceconnector)s abfüllen. Hierfür erstellen wir im CustomInterfaceConnector eine Konfiguration für das Feld „TestCustomInterface.Field01“ im Interface „TestCustomInterface“.

Diese Konfiguration sieht so aus:

```xml
<CustomInterfaces>
  
  <!-- TestCustomInterface -->
  <InterfaceDescription Name="TestCustomInterface" Description="Test Interface...">
    <Node Id="TestCustomInterface.Field01">[default text]</Node>
  </InterfaceDescription>
    
</CustomInterfaces>
```

Dieses Feld kann nun im Word-Editor in die Vorlage eingefügt werden:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/globalOOConnectInterfaceProviderContentControlDefaultText.png)

**Achtung**: Es gibt sowohl im GlobalOOConnectInterfaceProvider wie auch im [CustomInterfaceConnector]({{ site.baseurl }}/docfunc/de/df/custominterfaceconnector) sogenannte „Interfaces“. Diese dürfen nicht verwechselt werden.

## Ziel: OneOffixx-Connect-file

Das Ziel ist es nun, das „myDefinedInterface“ (siehe Aufruf) im GlobalOOConnectInterfaceProvider so zu definieren, dass OneOffixx beim obigen Aufruf eine Umformung vornimmt, sodass dieses Connect-File entsteht und ausgeführt wird:

```xml
<OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Settings />
  <Entries>
    <OneOffixxConnect>
      <Arguments>
        <TemplateId>804ea87d-37a4-4307-99d7-23d16032f426</TemplateId>
        <LanguageLcid>2055</LanguageLcid>
      </Arguments>
      <Function name="CustomInterfaceConnector" id="70E94788-CE84-4460-9698-5663878A295B">
        <Arguments>
          <Interface Name="TestCustomInterface">
            <Node Id="TestCustomInterface.Field01">
              [Inhalt von "hereItIs"-Element: «Test Content from XML file»]
            </Node>
          </Interface>
        </Arguments>
      </Function>
    </OneOffixxConnect>
  </Entries>
</OneOffixxConnectBatch>
```

## GlobalOOConnectInterfaceProvider-Konfiguration

Die Konfiguration vom GlobalOOConnectInterfaceProvider muss wie folgt lauten:

```xml
<Configuration>
  <Interfaces>
    
    <!-- myTestInterface -->
    <Interface name="myTestInterface" version="1.0">
      <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
        <xsl:template match="/">
          <OneOffixxConnectBatch xmlns="http://schema.oneoffixx.com/OneOffixxConnectBatch/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
            <Settings />
            <Entries>
              <OneOffixxConnect>
                <Arguments>
                  <TemplateId>804ea87d-37a4-4307-99d7-23d16032f426</TemplateId>
                  <LanguageLcid>2055</LanguageLcid>
                </Arguments>
                <Function name="CustomInterfaceConnector" id="70E94788-CE84-4460-9698-5663878A295B">
                  <Arguments>
                    <Interface Name="TestCustomInterface">
                      <Node Id="TestCustomInterface.Field01">
                        <xsl:value-of select="/root/anElement/hereItIs" />
                      </Node>
                    </Interface>
                  </Arguments>
                </Function>
              </OneOffixxConnect>
            </Entries>
          </OneOffixxConnectBatch>
        </xsl:template>
      </xsl:stylesheet>
    </Interface>
    
  </Interfaces>
</Configuration>
```

Beim Nachbauen dieses Beispiels muss darauf geachtet werden, dass sich zwischen `<TemplateId>` und `</TemplateId>` die korrekte Template-ID befindet.

Fertig.<br>
Der Aufruf von oben<br>
`OneOffixx.exe /connector "C:\temp\testfile.xml" /interfaceType "myDefinedInterface"`<br>
erzeugt nun ein Dokument, bei dem das Feld `TestCustomInterface.Field01` den Inhalt „Test Content from XML file“ (stammt aus testfile.xml) hat:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/globalOOConnectInterfaceProviderContentControlXMLContent.png)