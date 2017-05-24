---
layout: page
title: E-Mail Versand
permalink: "docfunc/de/df/sendmail"
language: de
---

Dokumente die in Word erstellt wurden, können direkt via E-Mail versendet werden. Die Funktion steht im Word Ribbon mit dem Knopf «Senden» zur Verfügung.
![E-Mail Versand Icon]({{ site.baseurl }}/assets/content-images/docfunc/de/sendmail.png)

Dabei kennt OneOffixx, je nachdem die Dokumentfunktion SendMail an der Vorlage angehängt ist, zwei Modi:
1. Ohne Dokumentfunktion wird die Standardfunktion von Word aufgerufen. Der Mailclient wird via IMAPI Interface gestartet und eine Kopie des Worddokumentes angehängt. Weder Dokumentinhalt noch Inhalt der Mail lassen sich beeinflussen. Je nach Mailclient ist die Mail nach dem Öffnen leer.
1. Mit Dokumentfunktion hat der Benutzer die Möglichkeit eine Mailvorlage auszuwählen und ob Logo, Faxstempel etc. ein bzw. ausgeblendet werden sollen. Zusätzlich kann ausgewählt werden, ob das Dokument als PDF, XPS oder als Word versendet werden soll. Innerhalb eines Unternehmens macht es auch Sinn, das Dokument zuerst auf einen gemeinsamen Laufwerk zu speichern und nur den Link zu versenden. ACHTUNG: Es wird auch in diesem Fall ein Link auf eine Kopie und nie das Originaldokument versendet. Der Grund liegt darin, dass auch in diesem Dokument Logo etc anders behandelt werden können als im Orginaldokument.

![SendMail]({{ site.baseurl }}/assets/content-images/docfunc/de/sendmaildlg.gif)

## Konfiguration

```xml
<Configuration>
  
  ↓ Empfängergruppe (erlaubt ist "*" für alle und einzelne Domains - bei mehreren mit Semikolon getrennt (z. B. "sevitec.ch;oneoffixx.com") :
  <RecipientGroup domains="*">
    
    <DefaultOptions>
      
      ↓ Dateiformat, in welchem standardmässig versendet wird (erlaubt: '.pdf', '.xps' und '.docx'-9
      <Extension>.pdf</Extension>
      
      ↓ Art, wie die Datei standardmässig versendet werden soll (erlaubt: 'Attachement' = als Anhang und 'Link' = als Link auf ein Dateipfad)
      <EmbeddedType>Attachment</EmbeddedType>
      
      ↓ Konfiguration für den Dateiversand als Anhang
      <Attachment>
        ↓ Name des Anhangs, erlaubt: saved="true" (greift, wenn Dok. bereits gespeichert wurde), saved="false" (greift, wenn Dok. noch nicht gespeichert wurde), 'saved' kann auch weggelassen werden
        <Text saved="true">
          [Binding oder Fixtext] → kann <Binding><![CDATA[//*[@id = 'DocParam.Subject']]]></Binding> enthalten oder direkt <![CDATA[FIXTEXT]]>
        </Text>
        <Text saved="false">
          [Binding oder Fixtext]
        </Text>
        
        ↓ Zusatztext des Anhangs, sofern der Entwurfsmodus aktiv ist, erlaubt: type="prefix" für vorangestellt oder type="suffix" für nachgestellt
        <DraftAddition type="suffix"> [Binding oder Fixtext] </DraftAddition>
      </Attachment>
      
      ↓ Konfiguration für den Dateiversand als Link
      <Link>
        
        ↓ Vorgeschlagener Dateiname, erlaubt: saved="true" (greift, wenn Dok. bereits gespeichert wurde), saved="false" (greift, wenn Dok. noch nicht gespeichert wurde), 'saved' kann auch weggelassen werden
        <Text> [Binding oder Fixtext] </Text>
        
        ↓ siehe oben
        <DraftAddition type="suffix"> [Binding oder Fixtext] </DraftAddition>
        
      </Link>
      
      ↓ Konfiguration des E-Mail-Betreffs
      <Subject>
        
        ↓ Vorgeschlagener Betreff, erlaubt: saved="true" (greift, wenn Dok. bereits gespeichert wurde), saved="false" (greift, wenn Dok. noch nicht gespeichert wurde), 'saved' kann auch weggelassen werden
        <Text> [Binding oder Fixtext] </Text>
        
        ↓ siehe oben
        <DraftAddition type="suffix"> [Binding oder Fixtext] </DraftAddition>
        
      </Subject>
      
      ↓ Konfiguration, welche Mailvorlage verwendet wird
      <MailTemplate>5bf2d50e-202d-4c79-bd76-d1bbf5af9046</MailTemplate>
      
    </DefaultOptions>
    
    ↓ Konfiguration der Standardwerte für Logo (logo), Faxstempel (fax), Entwurfsstempel (draft), Vektorsignatur (vectorSignature) und Kampagne (campaign) ein / aus. (erlaubt: 'On' für immer ein, 'Off' für immer aus oder 'FormDocument' für Übernahme des Zustands aus Dokument
    <Content logo="On" fax="Off" draft="FromDocument" vectorSignature="FromDocument" campaign="FromDocument" />
  
  </RecipientGroup>
  
  ↓ Beispielkonfiguration für weitere RecipientGroup
  <RecipientGroup domains="sevitec.ch;oneoffixx.ch;sevitec.com;oneoffixx.com">
    <DefaultOptions>
      <Extension>.docx</Extension>
      <EmbeddedType>Link</EmbeddedType>
      <Attachment>
        <Text saved="true">
          <Binding><![CDATA[//*[@id = 'DocParam.Subject']]]></Binding>
        </Text>
        <Text saved="false"><![CDATA[MyUnsavedDocument]]></Text>
        <DraftAddition type="suffix"><![CDATA[ [Entwurf]]]></DraftAddition>
      </Attachment>
      <Link>
        <Path saved="true"><![CDATA[U:\Transfer]]></Path>
        <Path saved="false"><![CDATA[U:\Transfer]]></Path>
        <Text saved="true">
          <Binding><![CDATA[//*[@id = 'DocParam.Subject']]]></Binding>
        </Text>
        <Text saved="false"><![CDATA[MyUnsavedDocument]]></Text>
        <DraftAddition type="suffix"><![CDATA[ [Entwurf]]]></DraftAddition>
      </Link>
      <Subject>
        <Text>
          <Binding><![CDATA[//*[@id = 'DocParam.Subject']]]></Binding>
        </Text>
        <DraftAddition type="suffix"><![CDATA[ [Entwurf]]]></DraftAddition>
      </Subject>
      <MailTemplate>5bf2d50e-202d-4c79-bd76-d1bbf5af9046</MailTemplate>
    </DefaultOptions>
    <Content logo="On" fax="Off" draft="FromDocument" vectorSignature="FromDocument" campaign="FromDocument" />
  </RecipientGroup>
</Configuration>
                
```