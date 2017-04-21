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

Mit 'Condition' Tags können Bedingungen in die Skripte eingebaut werden. Für 'oder'-Verknüpfungen kann das '|'-Zeichen verwendet. Für 'und'-Verknüpfungen ist es das '+'-Zeichen.
