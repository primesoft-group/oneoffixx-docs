---
layout: page
title: Versionierung
permalink: "docengine/de/versioncontrol/"
language: de
---

## Document Engine - Versionierung: Vorlagen Abhängigkeiten & Status {% include anchor.html name="versioning-overview" %}

<span class="label label-info">NEU ab 3.0</span>

Die Versionierung im OneOffixx erlaubt es, auch komplexere Änderungen in den Vorlagen vorzunehmen und zu testen, ohne die "Produktiven"-Vorlagen zu gefährden. 

Generell gilt, dass eine Vorlage mehrere Versionen besitzen kann, wobei alle Versionen einer Vorlage über die eindeutige "TemplateId" verbunden sind. Erstellt man eine neue Version einer vorhanden Vorlage, werden alle Daten kopiert. Eine Version muss manuell angelegt werden.

__"Published" & "Draft":__

Um die richtige Vorlagenversion während der Dokumenterzeugung zu wählen, muss eine Version entsprechend markiert werden:

* "Published": Diese Vorlagenversion ist die öffentlich sichtbare Version.
* "Draft": Diese Vorlagenversion wird zum Testen benutzt.
* "Unspecified": Die Vorlage ist weder als "Draft" noch "Published" gesetzt.

"Published" und "Draft" können gleichzeitig gesetzt sein. "Published" & "Draft" zusammen verhalten sich wie "Published" alleine.

__Erzeugungsarten:__

Für die "Document Engine" im OneOffixx gibt es drei verschiedene Arten eine Vorlage zu öffnen bzw. zu verwenden:

* "Document": Die Vorlage wird benutzt, um ein neues Dokument zu erstellen, z.B. im Client wird direkt eine Vorlage ausgewählt und ein neues Dokument erzeugen.
* "Editor": Die Vorlage wird aus dem Vorlageneditor im entsprechenden Editor (z.B. Microsoft Word o.Ä.) geöffnet.
* "Test": Die Vorlage wird aus dem Vorlageneditor via "Vorlage testen" benutzt, um ein neues Dokument zu testen.

__Vererbung und Unterdokumente:__

Je nach Erzeugungsart (Document/Editor/Test) und Veröffentlichungsstatus (Published/Draft/Unspecified) wird die Vererbung oder die Unterdokumentrelation unterschiedlich aufgelöst.

{:.table .table-striped}
| Erzeugungsart | Version der ausgewählen Vorlage | Aufgelöste Version der Abhängigkeiten |                      
| --- | ---- | --- |
| Document | Published | Published |
| Document | Draft| (nicht möglich) |
| Document | Unspecified | (nicht möglich) |
| Editor | Published | Published |
| Editor | Draft | Draft |
| Editor | Unspecified | Draft |
| Test | Published | Draft |
| Test | Draft | Draft |
| Test | Unspecified | Draft |

__Nutzungsszenarien:__

_Normale Dokumentenerzeugung - "Document":_

Erzeugt man als Nutzer ein Dokument (= Erzeugungsart "Document"), wird die als "Published" markierte Version der Vorlage genommen und etwaige Abhängigkeiten, z.B. Formatvorlagen oder Stylevorlagen, werden auch als "Published" aufgelöst. Die Erzeugungsart "Document" ist nur mit "Published" markierten Vorlagen erlaubt. Möchte man Änderungen testen, gibt es den "Test"-Modus. 

_Änderung an einer aktuell freigegebenen Vorlage - "Editor" & "Published":_

Editiert ein berechtigter Nutzer eine bereits freigegebene Vorlagenversion (= "Published") werden alle Abhängigkeiten ebenfalls als "Published" aufgelöst. Die Variante hier ist nur für überschaubare Änderungen empfohlen. Bei grösseren Änderungen sollte stets eine neue Version angelegt werden.

_Änderung an einem Style und Testen der Auswirkungen:_

Ein berechtigter Nutzer kann eine neue Version eines Styles anlegen. Diese Version wird automatisch als "Draft" markiert. Um die Änderungen in einer Hauptvorlage zu prüfen, kann der Vorlagenbauer nun über "Dokument testen" ein Testdokument erzeugen. Durch die Dokumenterzeugungsart "Dokument testen" wird der "Draft"-Style als Abhängigkeit aufgelöst.

_Hinzufügen eines neuen Styles und nutzen des Styles in einer neuen Formatvorlagenversion:_

Möchte man einen neuen Style zu einer bestehenden Stylevorlage hinzufügen und den Style auch in einer übergeordneten Formatvorlage nutzen, kann sowohl vom Style als auch von der Formatvorlage jeweils eine neue Version angelegt werden. Beide neuen Versionen sind automatisch als "Draft" gekennzeichnet. Wird nun der "Editor" von der Formatvorlage gestartet wird der ebenfalls im "Draft"-Modus befindliche Style geladen. Wenn die Änderungen abgeschlossen sind, können beide Versionen gemeinsam als "Published" gekennzeichnet werden. 