---
layout: page
title: Versionierung
permalink: "docengine/de/versioncontrol/"
language: de
---

## Document Engine - Versionierung: Vorlagen Abhängigkeiten & Status {% include anchor.html name="versioning-overview" %}

<span class="label label-info">ab 3.0</span>

Die Versionierung in OneOffixx erlaubt es, auch komplexere Änderungen in den Vorlagen vorzunehmen und zu testen, ohne die Vorlagen, die in Betrieb bzw. produktiv sind, zu gefährden. 

Generell gilt, dass eine Vorlage mehrere Versionen besitzen kann, wobei alle Versionen einer Vorlage über die eindeutige "TemplateId" verbunden sind. Erstellt man eine neue Version einer vorhanden Vorlage, werden alle Daten kopiert. Eine Version muss manuell angelegt werden.

__"Published" & "Draft":__

Um die richtige Vorlagenversion während der Dokumenterzeugung zu wählen, muss eine Version entsprechend markiert werden:

* "Veröffentlicht/Published": Diese Vorlagenversion ist die öffentlich sichtbare Version.
* "Entwurf/Draft": Diese Vorlagenversion wird zum Testen benutzt.
* "Unspecified": Die Vorlage ist weder als "Draft" noch "Published" gesetzt.

"Published" und "Draft" können gleichzeitig gesetzt sein. "Published" und "Draft" zusammen verhalten sich wie Published alleine.

__Erzeugungsarten:__

Für die [Document Engine]({{ site.baseurl }}/docengine/de/pipeline/) in OneOffixx gibt es drei verschiedene Arten, eine Vorlage zu öffnen bzw. die Vorlage zu verwenden:

* "Dokument": Die Vorlage wird benutzt, um ein neues Dokument zu erstellen, z.&nbsp;B. im Client wird direkt eine Vorlage ausgewählt und ein neues Dokument erzeugt.
* "Editor": Die Vorlage wird aus dem Vorlageneditor im entsprechenden Editor (z.&nbsp;B. Microsoft Word) geöffnet.
* "Dokument testen": Die Vorlage wird aus dem Vorlageneditor via "Vorlage testen" generiert, um ein neues Dokument zu testen.

__Vererbung und Unterdokumente:__

Je nach Erzeugungsart (Dokument/Editor/Dokument testen) und Veröffentlichungsstatus (Veröffentlicht/Entwurf/Unspecified) wird die Vererbung oder die Unterdokument-Relation unterschiedlich aufgelöst. 

{:.table .table-striped}
| Erzeugungsart | Version der ausgewählen Vorlage | Aufgelöste Version der Abhängigkeiten |                      
| --- | ---- | --- |
| Dokument | Veröffentlicht | Veröffentlicht |
| Dokument | Entwurf | (nicht möglich) |
| Dokument | Unspecified | (nicht möglich) |
| Editor | Veröffentlicht | Veröffentlicht |
| Editor | Entwurf | Entwurf |
| Editor | Unspecified | Entwurf |
| Dokument testen | Veröffentlicht | Entwurf |
| Dokument testen | Entwurf | Entwurf |
| Dokument testen | Unspecified | Entwurf |

__Nutzungsszenarien:__

_Normale Dokumentenerzeugung - "Dokument":_

Generiert man als Benutzer ein Dokument (= Erzeugungsart "Dokument") wird die als "Veröffentlicht" markierte Version der Vorlage genommen und etwaige Abhängigkeiten, z.&nbsp;B. Formatvorlagen oder Style-Vorlagen, werden auch als "Veröffentlicht" aufgelöst.
Die Erzeugungsart "Dokument" ist nur mit "Veröffentlicht" markierten Vorlagen erlaubt. Möchte man Änderungen testen, gibt es den "Dokument testen"-Button. 

_Änderung an einer aktuell freigegebenen Vorlage - "Editor" & "Veröffentlicht":_

Editiert ein berechtigter Benutzer eine bereits freigegebene Vorlagenversion (= "Veröffentlicht") werden alle Abhängigkeiten ebenfalls als "Veröffentlicht" aufgelöst. Die Variante hier ist nur für überschaubare Änderungen empfohlen. Bei grösseren Änderungen sollte stets eine neue Version angelegt werden.

_Änderung an einem Style und Testen der Auswirkungen:_

Ein berechtigter Benutzer kann eine neue Version eines Styles anlegen. Diese Version wird automatisch als "Entwurf" markiert. Um die Änderungen in einer Hauptvorlage zu prüfen, kann der Vorlagenbauer nun über "Dokument testen" ein Testdokument erzeugen. Dadurch wird der "Entwurf"-Style als Abhängigkeit aufgelöst.

_Hinzufügen eines neuen Styles und nutzen des Styles in einer neuen Formatvorlagenversion:_

Möchte man einen neuen Style zu einer bestehenden Style-Vorlage hinzufügen und den Style auch in einer übergeordneten Formatvorlage nutzen, kann vom Style als auch von der Formatvorlage jeweils eine neue Version angelegt werden. Beide neuen Versionen sind automatisch als "Entwurf" gekennzeichnet. Wird nun der "Editor" von der Formatvorlage gestartet, wird der ebenfalls im "Entwurf"-Modus befindliche Style geladen. Wenn die Änderungen abgeschlossen sind, können beide Versionen gemeinsam als "Veröffentlicht" gekennzeichnet werden. 