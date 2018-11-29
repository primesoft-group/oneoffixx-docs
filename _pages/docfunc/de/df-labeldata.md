---
layout: page
title: Label Data
permalink: "docfunc/de/df/labeldata"
language: de
---

Diese Dokument-Funktion regelt Etikettenkonfigurationen.

__Konfiguration:__
```xml
<LabelDataConfiguration>
  <!-- Beispielkonfiguration Etikettenvorlage (nur direkt auf Etikettenvorlage notwendig!) -->
  <LabelTemplate>
    
    <!-- Anzahl Etiketten -->
    <Columns>2</Columns>
    <Rows>3</Rows>
    
    <!-- Konfiguration Vorschau -->
    <Preview>
      <DataNode id="CustomElements.LabelDefinition"/>
    </Preview>
    
    <!-- Scripts fuer data binding -->
    <Script>
      <CustomDataNode id="LabelDefinition" type="Text">
        <Line>
          <Element id="Recipient.Selected.Transmission"/>
        </Line>
        <Line>
          <Element id="Person.Anschrift"/>
        </Line>
      </CustomDataNode>
    </Script>
    
  </LabelTemplate>

  <!-- Beispielkonfiguration Etikettendialog -->
  <LabelDialog>
    
    <!-- Erlaubte Vorlagen (nur auf Vorlagen aus welchen Etiketten generiert werden können notwendig!) -->
    <LabelTemplates>
      <Template id=""/>
    </LabelTemplates>

    <!-- Salutation configuration -->
    {[Recipients.SalutationConfiguration]}

    <!-- Shipping method configuration -->
    {[Recipients.ShippingMethodConfiguration]}
    
  </LabelDialog>  
</LabelDataConfiguration>
```