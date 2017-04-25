---
layout: page
title: Skripte
permalink: "docfunc/de/df/scripts"
language: de
---

Die Skripte dienen vor Allem der Vereinfachung der Dokumente. Über sie können viele Informationen z.B. von den Empfängern oder Profildaten in ein Content-Control hineingepackt werden, anstatt die Felder einzeln ins Dokument einzufügen. Es besteht auch die Möglichkeit viel verwendete Skripte global abzulegen. In die Skripte können auch verschiedene Logiken eingebaut werden.

Jedes Skript wird vom Tag 'CustomDataNode' umarmt. Für alle Skripte muss eine Id angegeben werden. Diese ist frei wählbar, muss aber eindeutig sein. Um ein Skript über mehrere Zeilen zu machen muss mit den 'Line' Tags gearbeitet werden. Mit den 'Text' Tags kann ein fixer Text ausgegeben werden.


```xml 
<CustomDataNode id="Example">
    <Line>
        <Text>First row</Text>
    </Line>
    <Line>
        <Text>Second row</Text>
    </Line>
</CustomDataNode>
```

Über die 'Element' Tags können Daten aus dem Profil oder externen Quellen angezogen werden. Damit die Daten aus dem Profil angezogen werden können wird die Feld-Id benötigt. Diese kann unter den Benutzereinstellungen gefunden werden.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/fieldid.png)

Damit ein Skript die Daten aus dem Profil anziehen kann muss vor die Feld-Id 'Profile.' geschrieben werden. Mit den Skripten es gibt die Möglichkeit die angezogenen Daten weiter zu verarbeiten oder zu ergänzen. Ein häufig verwendetes Attribut ist der 'separator'. Damit kann definiert werden, was die Trennung zum allfällig nachfolgenden Text sein soll. Folgt kein Text, so wird der definierte Separator nicht ausgegeben.


```xml
<CustomDataNode id="Example">
    <Line>
        <Element id="Profile.User.Salutation" separator=" " />
        <Element id="Profile.User.FirstName" />
    </Line>
    <Line>
        <Element id="Profile.Org.Title" />
    </Line>
</CustomDataNode>
```

Mit 'Condition' Tags können Bedingungen in die Skripte eingebaut werden. Es gibt 'when' und 'notwhen' Bedingungen. Für 'oder'- Verknüpfungen kann das '`|`'- Zeichen verwendet werden. Für 'und'- Verknüpfungen ist es das '`+`'- Zeichen.

```xml
<CustomDataNode id="Example">
    <Line>
        <Element id="Profile.User.Salutation" separator=" " />
        <Condition when="ShowFirstName = 'true' + DontShowFirstName = 'false'">
            <Element id="Profile.User.FirstName" />
        </Condition>
    </Line>
    <Condition notwhen="ShowTitle = 'false'">
        <Line>
            <Element id="Profile.Org.Title" />
        </Line>
    </Condition>
</CustomDataNode>
```

Via dem 'Snippet' Tag können OneOffixx Textbausteine angezogen werden. Dabei gilt es zu beachten, dass keine anderen daten-anziehenden Tags wie z.B. 'Element' im selben Skript verwendet werden dürfen. Dem 'CustomDataNode' Tag um das Snippet-Skript kann das Attribut 'update' gegeben werden. Es kann mit 'true oder 'false' angegeben werden, ob sich das Skirpt aktualisieren und bei geänderten Eingaben einen anderen Textbaustein anziehen darf.

```xml
<CustomDataNode id="BeispielSnippetSkript" update="true">
    <Condition when="RedCircle = 'true'">
        <Snippet id="05da9095-de60-4b78-bcd8-692639e8d377" />
    </Condition>
    <Condition notwhen="RedCircle = 'true' | BlueCircle = 'false'">
        <Snippet id="5bc2d759-431f-41e0-a18c-d577b240e612" />
    </Condition>
</CustomDataNode>
```

Nachfolgend werden die drei verschiedenen Arten von Skripts beschrieben.
{:.table .table-striped}
Skript Art          | Beschreibung
-------             | -------
__Text-Skript__     | Das Resultat ist ein Text als Binding-Element. Es dürfen alle Tags verwendet werden ausser "Image" und "Snippet".
__Snippet-Skript__  | Das Resultat ist eine Zusammensetzung von Textbausteinen. In Snippet-Skripts dürfen nur "Snippet" und "Condition" verwendet werden.
__Image-Skript__    | Das Resultat ist ein Bild. In Image-Skripts dürfen nur "Image" und "Condition" verwendet werden.

Folgende Script Elemente stehen zur Verfügung:
<!-- TOC -->

- [Script](#script)
- [CustomDataNode](#customdatanode)
- [Line](#line)
- [Element](#element)
- [Text](#text)
- [Image](#image)
- [Link](#link)
- [Condition](#condition)
- [Textvergleichoperatoren](#textvergleichoperatoren)
- [List](#list)
- [Snippet](#snippet)

<!-- /TOC -->

Column A | Column B | Column C
---------|----------|---------
 A1 | B1 | C1
 A2 | B2 | C2
 A3 | B3 | C3


### Script
{:.table .table-striped}
Tag/Attribut | Beschreibung
---------|----------
__Script__          | Via "Script" können dynamische Binding-Elemente (Scripts) in Vorlagen verwendet werden. Das Element Script kann beliebig viele solcher Elemente (CustomDataNode) zur Verfügung stellen.
Bsp.                | `<Script engine="XSL" version="2"><CustomDataNode>...</CustomDataNode></Script>`
engine              | Engine die für die Scriptinterpretation resp. -umsetzung zur Anwendung kommt (es steht aktuell nur "XSL" zur Verfügung)
version             | Scriptengine-Version die zur Anwendung kommt (Aktuell : 2, Standard : 1). Die Angabe dieser Version kann auf Ebene 'CustomDataNode' übersteuert werden. Die Angabe der Version ist in Bezug auf die Abwärtskompatibilität wichtig
depth               | Anzahl Berechnungen der Skript-Resultate. Wenn ein Skript auf das Resultat eines anderen Skripts zugreift, muss die depth 2 sein. Pro zusätzlichem verschachtelten Zugriff muss die depth um 1 erhöht werden. Standard: 2

### CustomDataNode
Via "CustomDataNode" kann ein neues Binding-Element erstellt werden in welchem der Skriptinhalt definiert wird.
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<CustomDataNode id="Demo" version="2"><Line>...</Line></CustomDataNode>`
id                  | ID des neuen Binding-Elements welches erzeugt werden soll (muss eindeutig sein). Für eine bessere Übersichtlichkeit im Vorlagen-Editor können durch Punkte "." in der ID Ordner erzeugt werden. OneOffixx setzt vor jede ID den Prefix "CustomElements." (z. B. CustomElements.Demo).
version             | Scriptengine-Version die zur Anwendung kommt (Aktuell: 2, Standard: 1). Die Angabe der Version auf Ebene 'CustomDataNode' übersteuert eine allfällige Versionsdekleration auf Ebene 'Script'.
bookmarkname        | Textmarke (Bookmark) in welchen die entsprechenden Bausteinen (Snippets) eingefügt resp. plaziert werden sollen. Wird nur berücksichtigt im Zusammenhang mit Bausteinen (siehe Snippet)
update              | Beim Einfügen von Bausteinen via Scripts (Snippets) kann über update definiert werden, ob die jeweiligen Bausteine nur beim Erstellen des Dokuments eingefügt werden oder ob sie im offenen Dokument aktualisiert werden sollen (Standard: false) Wird nur berücksichtigt im Zusammenhang mit Bausteinen (siehe Snippet)

### Line 
Via "Line" kann ein Zeilenumbruch generiert werden. Diese wird nur ausgegeben sofern auch ein Inhalt vorhanden ist (Ausnahme siehe Attribut 'fixoutput')
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<Line textbefore="prefix" textafter="suffix"/>`
textbefore          | Text welcher immer wenn die Zeile angezeigt wird vorgängig erscheint
textafter           | Text welcher immer wenn die Zeile angezeigt wird nachgestellt erscheint
fixoutput           | Wenn "fixoutput" auf "true" gesetzt ist, wird die Zeile auch ausgegeben wenn kein Inhalt vorhanden ist

### Element
Via "Element" können Texte aus OneOffixx angezogen werden.
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<Element id="Profile.User.FirstName" separator=" " textbefore="prefix" textafter="suffix" substring="3,2"/>`
id                  | ID des Binding-Elements welches verwendet werden soll
separator           | Trennzeichen zum nächsten Element oder Text der nur angezeigt wird, sofern nachfolgend ein weiteres Element einen Inhalt liefert
textbefore          | Text welcher immer wenn das Element angezeigt wird vorgängig erscheint
textafter           | Text welcher immer wenn das Element angezeigt wird nachgestellt erscheint
linePrefix          | Prefix-Zeichen für jede Zeile einer Liste resp. eines mehrzeiligen Text-Elements
showEmptyStartLines | Übernimmt alle vorhandenen vorangestellten Leerzeilen (erlaubte Werte: "true", "false" [Standard])
showEmptyEndLines   | Übernimmt alle vorhandenen nachgestellten Leerzeilen (erlaubte Werte: "true", "false" [Standard])
checkBoxActivatedSymbol     | Definition des Zeichens, welches bei einer angewählten Checkbox ausgegeben werden soll
checkBoxDeactivatedSymbol   | Definition des Zeichens, welches bei einer nicht angewählten Checkbox ausgegeben werden soll
when                | Siehe Condition-Attribute
notwhen             | Siehe Condition-Attribute
__Funktionen__      |
fSubstring          | Sofern nur ein Teil des Textes ausgegeben werden soll. <br/> Schema -> `fSubstring"[Startzeichen],[Anzahl Zeichen]"`
fSubstringBefore    | Sofern nur der Anfang (vor einer bestimmten Zeichenkette) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird der ganze Text ausgegeben. <br/> Schema -> `fSubstringBefore="[Zeichenkette]"`
fSubstringBeforeOrEmpty | Sofern nur der Anfang (vor einer bestimmten Zeichenkette) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird kein Text ausgegeben. <br/> Schema -> `fSubstringBeforeOrEmpty="[Zeichenkette]"`
fSubstringAfter         |  Sofern nur das Ende (nach einer bestimmten Zeichekette) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird der ganze Text ausgegeben. <br/> Schema -> `fSubstringAfter="[Zeichenkette]"`
fSubstringAfterOrEmpty  |  Sofern nur das Ende (nach einer bestimmten Zeichenkette) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird kein Text ausgegeben. <br/> Schema -> `fSubstringAfterOrEmpty="[Zeichenkette]"`
fCase               | Sofern der Textes gross ("upper") oder klein ("lower") geschrieben werden soll. Schema -> `fCase="[upper/lower]"` <br/> Für Unicode-Zeichen gibt es eine Erweiterung die ähnlich funktioniert: <br/> `upperUnicode/lowerUnicode`
fReplace            | Sofern ein Teil des Textes ersetzt werden soll. <br/> Schema -> `fReplace="[bestehende Zeichenkette],[neue Zeichenkette]"`
fTrim               | Sofern nur eine maximale Anzahl an Zeichen ausgegeben werden soll. <br/> Schema -> `fTrim="[maximale Anzahl Zeichen],[Modus],[Platzhalter]"`. <br/> [Modus] -> Ort an welchem bei Überlänge der Text abgeschnitten werden soll - erlaubte Werte: "left", "right" und "middle" <br/> [Platzhalter] -> Platzhaltertext der eingefügt wird, sofern eine Überlänge erreicht ist (bspw. "...")
fTrimURL            | Sofern nur ein Teil einer URL oder eines Filepfads ausgegeben werden soll (siehe auch fTrim). <br/> Schema -> `fTrim="[Art],[Modus],[Anzahl Ordner]"` <br/> [Art] -> File oder Folder, wobei File den Dateinamenselektiert und Folder den Pfad ohne Dateinamen. Aus diesem Grund stehen die nachfolgenden Optionen "Modus" und "Anzahl Ordern" nur bei "Folder" zur Verfügung. <br/> [Modus] -> Ort von welchem aus die Anzahl gewünschter Ordner angezeigt werden sollen - erlaubte Werte "left" und "right" <br/> [Anzahl Ordner] -> Anzahl der Ordner die Angezeigt werden soll
fSelectLine         | Sofern aus einem mehrzeiligen Text eine oder mehrere Zeilen selektiert werden sollen. <br/> Schema -> `fSelectLine="[Startzeile],[Endzeile]"`
fFormatingDate      | Sofern ein Datum in einem expliziten Format ausgegeben werden soll. <br/> Schema -> `fFormattingDate="[Datumsformat]", z. B. fFormattingDate="dddd, d. MMMM yyyy"`
fFormatingNumber    | Sofern eine Nummer in einem bestimmten Format (bspw. Tel.-Nummer) ausgegeben werden soll. <br/> Schema -> `fFormattingNumber="[Schema des Formats],[Vorwahl (optional)]"` <br/> Die angegebene Vorwahl wird hinzugefügt, wenn die Nummer des Elements mit '0' aber nicht mit '00' beginnt. <br/> Bsp. für eine internationale Tel.-Nummer: `fFormattingNumber="+## '(0)'## ### ## ##,41"` <br/> Literale (siehe auch http://openbook.galileocomputing.de/csharp/kap30.htm): <br/> # -> Stellenplatzhalter <br/> 0 -> Stellenplatzhalter (identisch mit # jedoch wird hier das Zeichen '0' ausgegeben wenn keine Zahl an dieser Stelle vorhanden ist) <br/> ' -> Text-Maskierung (Text, der in einfachen Anführungszeichen eingegeben wird, wird nicht interpretiert und als Text ausgegeben) <br/> \ -> Zeichen-Maskierung (Das nächste Zeichen wird nicht interpretiert und als Zeichen ausgegeben)

### Text
Via "Text" können Fix-Texte ausgegeben werden.
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<Text when="Profile.User.Phone | Profile.User.Phone2">Tel:</Text>`
when                | Siehe Condition-Attribute
notwhen             | Siehe Condition-Attribute

### Image
Via "Image" können Bilder aus OneOffixx angezogen werden. Durch das "when"-Attribut kann dieses bspw. anhand eines Dokument-Parameters ein- und ausgeblendet werden.
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<Image id="Profile.Org.Logo"/>`
id                  | ID des Binding-Elements welches verwendet werden soll
when                | Siehe Condition-Attribute
notwhen             | Siehe Condition-Attribute

### Link
Via "Link" kann ein HTML-Link erzeugt werden (nur in HTML-E-Mails und nicht in Kombination mit den normalen Textscripts verwendbar). In diesem können auch Daten aus OneOffixx verwendet werden. Sollten mehrere Link-Elemente auf verschiedenen Zeilen ausgegeben werden, muss das Zeilenende mit &#160; markiert werden (siehe Beispiel).
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<Link id="Profile.User.URL" text="Web"/>` <br/> `<Link id="Profile.Org.Web" bindingText="Profile.Org.Web" style="color:green;font:italic" />` <br/> `<Link imageURL="test-Dateien/tel-symbol.png" height="10">www.oneoffixx.com</Link>`
Bsp. mehrzeilig     | `<Line>` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`<Link id="Profile.Org.Web" bindingText="Profile.Org.Web" />` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`<Text>&#160;</Text>` <br/> `</Line>` <br/> `<Line>` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`<Link id="Profile.Org.Email" type="mailto" bindingText="Profile.Org.Email" />` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`<Text>&#160;</Text>` <br/> `</Line>`
id                  | ID des Binding-Elements welches als URI verwendet werden soll (alternativ kann auch ein fixer Link als Taginhalt - siehe Bsp. oben angegeben werden)
text                | Fixtext welcher (sofern abweichend von der URI) angezeigt werden soll (wird nur angezeigt, sofern kein Binding-Text vorhanden ist)
bindingText         | ID des Binding-Elements welches als Link-Text angezeigt werden soll
style               | CSS Styleangaben für die Formatierung des HTML-Links
imageName           | Bezeichnung des lokalen Bilds welches als Link angezeigt werden soll
imageURL            | URL eines Bildes (damit ein Bild verlinkt dargestellt wird) <br/> Falls ein Bild über das "FileExplorer"-Feature genutzt werden soll, um es z. B. via Scripting einzufügen: <br/> - Es muss der komplette Pfad angegeben werden, d. h. falls die Signature "test" heisst und auf einem DE-System erstellt wurde, muss der Pfad mit "test-Dateien/" beginnen <br/> - Ab Office 2013 werden Bilder nicht mehr automatisch "embedded" mitgeschickt, in diesem Fall muss explizit ein Registry-Schlüssel gesetzt werden: <br/> HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Outlook\Options\Mail (Office 2013) <br/> HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Outlook\Options\Mail (Office 2016) <br/> DWord: 'Send Pictures With Document' Value: '1'
imageWidth          | Grösse in Pixel oder Prozent für die Breite des Bilds
imageHeight         | Grösse in Pixel oder Prozent für die Höhe des Bilds
type                | Linktyp - Art des Links, erlaubt ist Mailto, XingProfile, TwitterProfile, LinkedInProfile, Google+Profile, FacebookProfile <br/> Bei einem so typisierten Link wird die generelle URL automatisch hinzugefügt und es muss nur der individuelle Profilname resp. die Profil-ID angegeben werden.
when                | Siehe Condition-Attribute
notwhen             | Siehe Condition-Attribute

### Condition
Via "Condition" können ganze Bereiche anhand von Bedingungen aktiviert oder deaktiviert werden. Es können Text-, CheckBox-, ComboBox- und Image-Elemente validiert werden.
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<Condition notwhen="Profile.User.Phone">...</Condition>`
when                | Bedingung damit die beinhalteten Elemente und Texte angezeigt werden. <br/> Bei der Angabe von IDs (ohne Textvergleichoperatoren, siehe unten) wird geprüft, ob das OneOffixx-Element mit der ID existiert und einen Inhalt hat. <br/> Für eine "oder"-Verknüpfung kann das "`|`"-Zeichen verwendet werden <br/> Für eine "und"-Verknüpfung kann das "`+`"-Zeichen verwendet werden <br/> Eine Mischung von "und" und "oder"-Bedingungen im selben when-Attribut ist nicht erlaubt. <br/> Bei Combobox-Elementen wird normalerweise der Wert (Anzeigetext) verwendet. Für den Zugriff auf den Key muss ein $-Zeichen vorangestellt werden (Bsp: `<Condition when="$DocParam.TestDropdown = 'key1'">`). <br/> <br/> Image Verhalten: <br/> `<Image when="Profile.Org.Logo" ... />` resultiert entweder in einem leeren Bild oder dem eigentlichen Bildinhalt, wenn es solch ein Binding-Element in OneOffixx gibt. <br/> Möchte man abfragen, ob bestimmte Bilddaten gesetzt oder "leer" sind und nur ein Bild "selektieren", muss man über eine direkte Condition gehen: <br/> `<CustomDataNode id="SelectImage">` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`<Condition when="Profile.User.Sign">` <br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<Image id="Profile.User.Sign" />` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`</Condition>` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`<Condition when="Signer_0.Org.Logo">` <br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<Image id="Signer_0.Org.Logo" />` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`</Condition>` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`<Condition when="Signer_1.Org.Logo">` <br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<Image id="Signer_1.Org.Logo" />` <br/> &nbsp;&nbsp;&nbsp;&nbsp;`</Condition>` <br/> `</CustomDataNode>` <br/>
notwhen             | Analog dem when-Attribut, jedoch invertiert.

### Textvergleichoperatoren
In einem when- oder notwhen-Attribut können auch Vergleichsoperatoren verwendet werden, wobei Fixtexte in einfachen Anführungszeichen (') stehen müssen:
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<Condition notwhen="Profile.User.Phone contains '044'"></Condition>` <br/> 
"="                 | Der Inhalt wird 1:1 verglichen
"~"                 | Der Inhalt wird ohne Berücksichtigung von Gross-/Kleinschreibung und Leerzeichen verglichen
"contains"          | Prüfung ob der Inhalt eine bestimmte Zeichenkette enthält (an beliebiger Position)
"startsWith"        | Prüfung ob der Inhalt mit bestimmten Zeichen beginnt
"length"            | Vergleich der Anzahl Zeichen
"lengthBiggerThan"  | Prüfung ob die Zeichenanzahl grösser ist
"lengthLowerThan"   | Prüfung ob die Zeichenanzahl kleiner ist

### List
Via "List" kann eine dynamische Liste von Elementen ausgegeben werden. Dies kommt primär für die Anzeige einer Empfängerliste (z. B. in einem Protokoll, ...) zur Anwendung. Innerhalb einer Liste können wieder "Line", "Element" und "Condition" verwendet werden. Die Adressierung der IDs wird nun relativ gemacht (bspw. Person.FirstName anstelle von Contact.Recipient.Selected.Person.FirstName).
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<List type="Recipient" separator="," filter="An">`
type                | Der Listentyp definiert die gewünschte Liste. Zur Zeit steht nur "Recipient" zur Verfügung.
separator           | Text welcher immer zwischen den einzelnen Einträgen angezeigt wird
filter              | Es gibt unterschiedliche Filterkriterien. Bspw. sofern nur alle "An" Empfänger angezeigt werden sollen, kann dies mit filter="An" geregelt werden
includeSelected     | Bestimmt ob der aktuell selektierte Kontakt auch in der Liste angezeigt wird oder nicht (Standard: true)

### Snippet
Via "Snippet" können Textbausteine aus OneOffixx verwendet oder fixe Inhalte abgefüllt werden.
{:.table .table-striped}
Tag/Attribut        | Beschreibung
-------             | -------
Bsp.                | `<Snippet id="b353eb86-ac5a-4db4-99bc-1847e31793bb" />` <br/> `<Snippet><![CDATA[Demotext]]></Snippet>` <br/> `<Snippet type="html"><![CDATA[<h1>Titel 1</h1>]]></Snippet>`
id                  | ID des Textbausteins welcher in die entsprechende Textmarke (siehe auch Attribut bookmarkname bei CustomDataNode) eingefügt werden soll
type                | "Text" oder "Html" für einen fixen Inhalt, wobei der Inhalt innhalb eines CDATA-Tags innerhalb des Snippet-Tags folgt
when                | Siehe Condition-Attribute
notwhen             | Siehe Condition-Attribute