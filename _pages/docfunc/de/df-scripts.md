---
layout: page
title: Skripte
permalink: "docfunc/de/df/scripts"
language: de
---

Die Skripte dienen vor Allem der Vereinfachung der Dokumente. Über sie können viele Informationen z.B. von den Empfängern oder Profildaten in ein Content-Control hineingepackt werden, anstatt die Felder einzeln ins Dokument einzufügen. Es besteht auch die Möglichkeit viel v
erwendete Skripte global abzulegen. In die Skripte können auch verschiedene Logiken eingebaut werden.

Jedes Skript wird vom 'CustomDataNode' umarmt. Alle Skripte müssen eine frei wählbare und eindeutige Id haben. Wenn ein Skript im Dokument  über mehrere Zeilen gehen soll braucht es die Lines. 

```xml 
    <CustomDataNode id="Beispiel">
      <Line>
        ...
      </Line>
    </CustomDataNode>
```

