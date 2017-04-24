---
layout: page
title: Skripte
permalink: "docfunc/de/df/scripts"
language: de
---

Die Skripte dienen vor Allem der Vereinfachung der Dokumente. Über sie können viele Informationen z.B. von den Empfängern oder Profildaten in ein Content-Control hineingepackt werden, anstatt die Felder einzeln ins Dokument einzufügen. Es besteht auch die Möglichkeit viel verwendete Skripte global abzulegen. In die Skripte können auch verschiedene Logiken eingebaut werden.

Jedes Skript wird vom Tag 'CustomDataNode' umarmt. Für alle Skripte muss eine Id angegeben werden. Diese ist frei wählbar, muss aber eindeutig sein. Um ein Skript über mehrere Zeilen zu machen muss mit den 'Line' Tags gearbeitet werden. Mit den 'Text' Tags kann ein fixer Text ausgegeben werden.


```xml 
<CustomDataNode id="Beispiel">
    <Line>
        <Text>Erste Zeile</Text>
    </Line>
    <Line>
        <Text>Zweite Zeile</Text>
    </Line>
</CustomDataNode>
```

Über die 'Element' Tags können Daten aus dem Profil oder externen Quellen angezogen werden. Damit die Daten aus dem Profil angezogen werden können wird die Feld-Id benötigt. Diese kann unter den Benutzereinstellungen gefunden werden.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/fieldid.png)

Damit ein Skript die Daten aus dem Profil anziehen kann muss vor die Feld-Id 'Profile.' geschrieben werden. Mit den Skripten es gibt die Möglichkeit die angezogenen Daten weiter zu verarbeiten oder zu ergänzen. Ein häufig verwendetes Attribut ist der 'separator'. Damit kann definiert werden, was die Trennung zum allfällig nachfolgenden Text sein soll. Folgt kein Text, so wird der definierte Separator nicht ausgegeben.


```xml
<CustomDataNode id="Beispiel">
    <Line>
        <Element id="Profile.User.Salutation" separator=" " />
        <Element id="Profile.User.FirstName" />
    </Line>
    <Line>
        <Element id="Profile.Org.Title" />
    </Line>
</CustomDataNode>
```

Mit 'Condition' Tags können Bedingungen in die Skripte eingebaut werden. Es gibt 'when' und 'notwhen' Bedingungen. Für 'oder'- Verknüpfungen kann das '|'- Zeichen verwendet werden. Für 'und'- Verknüpfungen ist es das '+'- Zeichen.


```xml
<CustomDataNode id="Beispiel">
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

{:.table .table-striped}
Typ | Beschreibung
------- | -------
__Script__ | Via "Script" können dynamische Binding-Elemente (Scripts) in Vorlagen verwendet werden. Das Element Script kann beliebig viele solcher Elemente (CustomDataNodes) zur Verfügung stellen
engine | Engine die für die Scriptinterpretation resp. -umsetzung zur Anwenung kommt (es steht aktuell nur "XSL" zur Verfügung)
version | Scriptengine-Version die zur Anwendung kommt (Aktuell = 2, Standard = 1). Die Angabe dieser Version können auf Ebene 'CustomDataNode' übersteuert werden. Die Angabe der Version ist in Bezug auf die Abwärtskompatibilität wichtig
__CustomDataNode__ | Via "CustomDataNode" kann ein neues Binding-Element generiert werden in welchem der eigentliche Scriptinhalt definiert wird
id | ID des neuen Binding-Elements welches erzeugt werden soll (muss eindeutig sein). Für eine bessere Übersichtlichkeit im Vorlagen-Editor, können durch Punkte in der ID, Ordner erzeugt werden
version | Scriptengine-Version die zur Anwendung kommt (Aktuell = 2, Standard = 1). Die Angabe der Version auf Ebene 'CustomDataNode' übersteuert eine allfällige Versionsdekleration auf Ebene 'Script'
bookmarkname | Textmarke (Bookmark) in welchen die entsprechenden Bausteinen (Snippets) eingefügt resp. plaziert werden sollen. Wird nur berücksichtigt im Zusammenhang mit Bausteinen (siehe Snippet)
update | Beim Einfügen von Bausteinen via Scripts (Snippets), kann über update definiert werden, ob die jeweiligen Bausteine nur initial aktuell eingefügt werden, oder im offenen Dokument aktualisiert werden sollen (Standard = false). Wird nur berücksichtigt im Zusammenhang mit Bausteinen (siehe Snippet)
__Line__ | Via "Line" kann ein Zeilenumbruch generiert werden. Diese wird nur ausgegeben sofern auch ein Inhalt vorhanden ist (Ausnahme siehe Attribut 'fixoutput')
textbefore | Text welcher immer wenn die Zeile angezeigt wird, vorgängig erscheint (Achtung: Dokumentsprachunabhängig - alternativ "Text"-Funktion verwenden)
textafter | Text welcher immer wenn die Zeile angezeigt wird, nachgestellt erscheinet (Achtung: Dokumentsprachunabhängig - alternativ "Text"-Funktion verwenden)
fixoutput | Sofern "fixoutput" auf "true" gesetzt wird, wird die Linie auch ausgegeben wenn kein Inhalt vorhanden ist
__Element__ | Via "Element" können Texte aus dem OO-Binding angezogen werden. Diese werde nur ausgegeben sofern auch ein Inhalt vorhanden ist.
id | ID des Binding-Elements welches verwendet werden soll
separator | Trennzeichen zum nächsten Element oder Text der nur angezeigt wird, sofern achfolgend noch weitere Element einen Inhalt liefern
textbefore | Text welcher immer wenn das Element angezeigt wird, vorgängig erscheint (Achtung: Dokumentsprachunabhängig - alternativ "Text"-Funktion verwenden)
textafter | Text welcher immer wenn das Element angezeigt wird, nachgestellt erscheinet (Achtung: Dokumentsprachunabhängig - alternativ "Text"-Funktion verwenden)
linePrefix | Prefix Zeichen für jede Zeile einer Liste resp. eines mehrzeiligen Text-Elements
showEmptyStartLines | Übernimmt alle vorhandenen vorangestellten Leerzeilen (erlaubte Werte: "true", "false" [Default])
showEmptyEndLines | Übernimmt alle vorhandenen nachgestellten Leerzeilen (erlaubte Werte: "true", "false" [Default])
checkBoxActivatedSymbol | Definition des Zeichens, welches bei einer angewählten Checkbox ausgegeben werden soll
checkBoxDeactivatedSymbol | Definition des Zeichens, welches bei einer nicht angewählten Checkbox ausgegeben werden soll
when | Siehe Condition-Attribute
notwhen | Siehe Condition-Attribute
Funktionen |
fSubstring | Sofern nur ein Teil des Textes ausgegeben werden soll. Schema -> fSubstring([Startzeichen],[Anzahl Zeichen])
fSubstringBefore | Sofern nur der Anfang (vor einem bestimmten Zeichen) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird der ganze Text ausgegeben. Schema -> fSubstringBefore([Zeichenkette])
fSubstringBeforeOrEmpty | Sofern nur der Anfang (vor einem bestimmten Zeichen) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird kein Text ausgegeben. Schema -> fSubstringBeforeOrEmpty([Zeichenkette])
fSubstringAfter | Sofern nur das Ende (nach einem bestimmten Zeichen) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird der ganze Text ausgegeben. Schema -> fSubstringAfter([Zeichenkette])
fSubstringAfterOrEmpty | Sofern nur das Ende (nach einem bestimmten Zeichen) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird kein Text ausgegeben. Schema -> fSubstringAfterOrEmpty([Zeichenkette])
fCase | Sofern der Textes gross ("upper") oder klein ("lower") geschrieben werden soll. Schema -> fCase([upper/lower])
fReplace | Sofern ein Teil des Textes ersetzt werden soll. Schema -> fReplace([bestehende Zeichenkette],[neue Zeichenkette])
fTrim |  Sofern nur eine maximale Anzahl an Zeichen ausgegeben werden soll. Schema -> fTrim([maximale Anzahl Zeichen],[Modus],[Platzhalter]). [Modus] -> Ort an welchem bei Überlänge der Text abgeschnitten werden soll - erlaubte Werte "left","right" und "middle". [Platzhalter] -> Platzhaltertext der eingefügt wird, sofern eine Überlänge erreicht ist (bspw. "...")
fTrimURL | Sofern nur ein Teil einer URL oder eines Filepfads ausgegeben werden soll (siehe auch fTrim). Schema -> fTrim([Art],[Modus],[Anzahl Ordner]) [Art] -> File oder Folder, wobei File den Dateinamenselektiert und Folder den Pfad ohne Dateinamen. Aus diesem Grund stehen die nachfolgenden Optionen "Modus" und "Anzahl Ordern" nur bei "Folder" zur Verfügung. [Modus] -> Ort von welchem aus die Anzahl gewünschter Ordner angezeigt werden sollen - erlaubte Werte "left" und "right" [Anzahl Ordner] -> Anzahl der Ordner die Angezeigt werden soll
fSelectLine | Sofern aus einem mehrzeiligen Text eine oder mehrere Zeilen extrahiert werden sollen Schema -> fSelectLine([Startzeile],[Endzeile])
fFormatingDate | Sofern ein Datum in einem expliziten Format ausgegeben werden soll. Schema -> fFormatingDate([Datumsformat])
fFormatingNumber |  Sofern eine Nummer in einem bestimmten Format (bspw. Tel. Nummer) ausgegeben werden soll. Schema -> fFormatingNumber([Schema des Formats],[true oder false ob die +41 Vorwahl ausgegeben werden soll]) Bsp. für eine internationale Tel. Nummer -> fFormatingNumber("+##\\''(0)'##\\'###\\'##\\'##,true") Literale (siehe auch http://openbook.galileocomputing.de/csharp/kap30.htm): # -> Stellenplatzhalter inkl. Leerstellenausgabe 0 -> Stellenplatzhalter (identisch mit # jedoch wird hier kein Leerzeichen ausgegeben sofern keine Zahl an dieser Stelle vorhanden ist) ' -> Text-Maskierung (Text der in einfachen Anführungszeichen eingegeben wird, wird nicht interpretiert und als Text ausgegeben) \\-> Zeichen-Maskierung (Das nächste Zeichen wird nicht interpretiert und als Zeichen ausgegeben)
__Text__ | Via "Text" können Fix-Texte ausgegeben werden. Dies auch in Abhängigkeit der Dokumentsprache
when | Siehe Condition-Attribute
notwhen | Siehe Condition-Attribute
lcid | Definition der Dokumentsprache anhand der LCID -> http://msdn.microsoft.com/en-us/library/ms912047%28WinEmbedded.10%29.aspx
__Image__ | Via "Image" können Bilder aus dem OO-Binding angezogen werden. Via dem "when" Attribut kann dieses bspw. anhand eines Dokument-Parameters ein/ausgeblendet werden. (Achtung: hier darf kein "Line"-Tag verwendet werden)
id | ID des Binding-Elements welches verwendet werden soll
when | Siehe Condition-Attribute
notwhen | Siehe Condition-Attribute
__Link__ | Via "Link" kann ein HTML Link erzeugt werden (nur in HTML Emails und nicht in Kombination mit den normalen Textscripts verwendbar). In diesem können auch Daten aus dem OO-Binding verwendet werden werden. Via dem "when" Attribut kann dieses analog den anderen Elementen ein/ausgeblendet werden.
id | ID des Binding-Elements welches als URI verwendet werden soll (alternativ kann auch ein fixer Link als Taginhalt - siehe Bsp. oben angegeben werden)
text | Fixtext welcher (sofern abweichend von der URI) angezeigt werden soll (wird nur angezeigt, sofern kein Binding-Text vorhanden ist)
bindingText | ID des Binding-Elements welches als Link-Text angezeigt werden soll
style | CSS Styleangaben für die Formatierung eines HTML-Links
imageName | Bezeichnung des lokalen Bilds welches als Link angezeigt werden soll
imageURL | URL eines Bildes (damit ein Bild verlinkt dargestellt wird)
imageWidth | Grösse in Pixel oder Prozent für die Breite des Bilds
imageHeight | Grösse in Pixel oder Prozent für die Höhe des Bilds
type | Linktyp - Art des Links, erlaubt ist Mailto, XingProfile, TwitterProfile, LinkedInProfile, Google+Profile, FacebookProfile. Bei einem so typisierten Link wird die generelle URL automatisch hinzugefügt und es muss nur der individuelle Profilname resp. Profilid angegeben werden.
when | Siehe Condition-Attribute
notwhen | Siehe Condition-Attribute
__Condition__ Via "Condition" können ganze Bereich anhand von Bedingungen ein- oder ausgegeben werden. Es können Text-, Checkbox und ComboBox-Elemente validiert werden.
when | Bedingung welche Binding-IDs vorhanden resp. gefüllt sein müssen damit die beinhalteten Elemente und Texte angezeigt werden. Für eine "oder"-Verknüpfung kann das "|"-Zeichen verwendet werden. Für eine "und"-Verknüpfung kann das "+"-Zeichen verwendet werden. Eine Mischung von "und" und "oder"-Bedingungen im selben when-Attribut ist nicht erlaubt. Bei Combobox-Elementen wird normalerweise der Wert (DisplayText) verwendet. Für den Zugriff auf den Key muss ein $-Zeichen vorangestellt werden (Bsp: <Condition when="$DocParam.TestDropdown = 'key1'">).
                        
                        Image Verhalten:
                        <Image when="Profile.Org.Logo" ... /> resultiert entweder in einem leeren Bild oder dem eigentlichen Bildinhalt, wenn es solch ein Binding-Element im CustomXML gibt.
                        Möchte man abfragen, ob bestimmte Bilddaten gesetzt sind oder "leer" sind und nur ein Bild "selektieren", muss man über eine direkte Condition gehen:
                        
                          <CustomDataNode id="SelectImage">
                            <Condition when="Profile.User.Sign">
                               <Image id="Profile.User.Sign" />
                            </Condition>
                            <Condition when="Signer_0.Org.Logo">
                                <Image id="Signer_0.Org.Logo" />
                            </Condition>
                            <Condition when="Signer_1.Org.Logo">
                                <Image id="Signer_1.Org.Logo" />
                            </Condition>
                          </CustomDataNode>

notwhen | Analog dem when-Attribut, jedoch invertiert.
__Textvergleichoptionen__ | In einem when oder notwhen Tag können auch Vergleichsoperatoren verwendet werden, wobei Fixtexte in einfachen Anführungszeichen (') stehen müssen:
"=":                  Der Inhalt wird 1:1 verglichen
"~":                  Der Inhalt wird ohne Berücksichtigung von Gross-/Kleinschreibung und Leerzeichen verglichen
"contains":           Prüfung ob der Inhalt einen Anderen an einer beliebigen Stelle beinhaltet
"startsWith":         Prüfung ob der Inhalt mit bestimmten Zeichen beginnt
"length":             Vergleich der Anzahl Zeichen
"lengthBiggerThan":   Prüfung ob die Zeichenanzahl grösser ist
"lengthLowerThan":    Prüfung ob die Zeichenanzahl kleiner ist

__List__ | Via "List" kann eine dynamische Liste von Elementen ausgegeben werden. Dies kommt primär für die Anzeige einer Empfängerliste (Protokoll, ...) zur Anwendung. Innerhalb einer Liste können wieder "Line", "Element" und "Condition" verwendet werden. Die Adressierung der Ids wird nun relativ gemacht (bspw. Person.FirstName anstelle von Contact.Recipient.Selected.Person.FirstName).
type | Der Listentyp definiert die gewünschte Liste. Zur Zeit steht nur "Recipient" zur Verfügung.
separator | Text welcher immer zwischen den einzelnen Einträgen angezeigt wird
filter | Es gibt unterschiedliche Filterkriterien. Bspw. sofern nur alle "An" Empfänger angezeigt werden sollen, kann dies mit filter="An" geregelt werden
includeSelected | Bestimmt ob der aktuell selektierte Kontakt auch in der Liste angezeigt wird oder nicht (Defaultmässig auf true)