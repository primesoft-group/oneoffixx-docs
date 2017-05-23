---
layout: page
title: DocumentProtection / Dokumentenschutz
permalink: "docfunc/de/df/documentprotection"
language: de
---

In Word gibt es eine Funktion „Bearbeitung einschränken“.<br>
Bei OneOffixx-Vorlagen sollte diese **nicht im Editor** verwendet werden. Diese Einschränkungen müssen stattdessen **über diese Dokument-Funktion** konfiguriert werden.

Grund: Wenn eine Word-Vorlage im Editor gesperrt wird, kann es vorkommen, dass OneOffixx die nötigen Anpassungen zur Einhaltung des Corporate Designs oder für das Abfüllen der korrekten Profil-Daten nicht vornehmen kann.

## Word-Funktion „Bearbeitung einschränken“

Gemeint ist die Funktion, die in Word über den folgenden Button aufgerufen werden kann (im Ribbon „Überprüfen“ wie auch „Entwicklertools“):

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/documentProtectionWordButton.png)

Im Anschluss öffnet sich dieses Panel, das einige Optionen zur Einschränkung der Bearbeitung bietet:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/documentProtectionWordPanel.png)

## Simple Konfiguration

Hier eine Beispiel-Konfiguration:

```xml
<Type>AllowOnlyFormFields</Type>
<Password></Password>
<NoReset>True</NoReset>
<UseIRM>False</UseIRM>
<EnforceStyleLock>False</EnforceStyleLock>
```

### Type

Hier werden dieselben Einstellungsmöglichkeiten wie im Word-Panel geboten:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/documentProtectionWordPanelWithSelection.png)

Zwischen `<Type>` und `</Type>` kann einer dieser Ausdrücke reingeschrieben werden:

* `AllowOnlyRevisions` – entspricht „Überarbeitungen“
* `AllowOnlyComments` – entspricht „Kommentare“
* `AllowOnlyFormFields` – entspricht „Ausfüllen von Formularen“
* `AllowOnlyReading` – entspricht „Keine Änderungen (Schreibgeschützt)“

### Password

Zwischen `<Password>` und `</Password>` kann Optional ein Passwort festgelegt werden.<br>
Dies entspricht diesem Dialog, der in Word erscheint, nachdem im Panel der Button „Ja, Schutz jetzt anwenden“ gewählt wurde:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/documentProtectionWordSetPasswordDialog.png)

### NoReset

Zwischen `<NoReset>` und `</NoReset>` kann `True` oder `False` geschrieben werden.<br>
`True` stellt sicher, dass Formularfelder ihren Inhalt behalten, wenn das Dokument geschützt ist.<br>
Diese Einstellung kommt nur zur Anwendung, wenn Type auf AllowOnlyFormFields gesetzt ist (wird ansonsten ignoriert).<br>
(Standard: `False`)

### UseIRM

Zwischen `<UseIRM>` und `</UseIRM>` kann `True` oder `False` geschrieben werden.<br>
`True` bedeutet, dass „Information Rights Management“ (IRM) für den Dokumentenschutz verwendet wird.

### EnforceStyleLock

Zwischen `<EnforceStyleLock>` und `</EnforceStyleLock>` kann `True` oder `False` geschrieben werden.<br>
`True` bedeutet, dass das Formatieren von Text eingeschränkt wird.

## Triggers – Dokumentenschutz abhängig von Dokument-Parametern konfigurieren

Die Dokumentenschutz-Konfiguration kann auch von Einstellungen im Dokument-Parameter abhängig gemacht werden.<br>
Dies geschieht über sogenannte Triggers.

Hier ein Beispiel:

```xml
<Triggers>
  <Trigger>
    <XPath>//CheckBox[@id='DocParam.TrackRevisions'] = 'true'</XPath>
    <Type>AllowOnlyRevisions</Type>
    <Password></Password>
    <NoReset>True</NoReset>
    <UseIRM>False</UseIRM>
    <EnforceStyleLock>False</EnforceStyleLock>
  </Trigger>
  <Trigger>
    <XPath>//CheckBox[@id='DocParam.TrackRevisions'] = 'false'</XPath>
    <Type>NoProtection</Type>
    <Password></Password>
    <NoReset>True</NoReset>
    <UseIRM>False</UseIRM>
    <EnforceStyleLock>False</EnforceStyleLock>
  </Trigger>
</Triggers>
```

Im Element `XPath` muss ein XPath-Ausdruck angegeben werden, der wahr oder falsch (true/false) sein kann (siehe Beispiel). Dabei wird auf denselben XML-Baum zugegriffen wie bei den Extended Bindings – siehe ExtendedBinding („Bibliothek für erweitertes Binding“).

Im obigen Beispiel wird auf die Dokument-Parameter-Checkbox DocParam.TrackRevisions zugegriffen.
* Wenn diese angewählt ist, ist der Modus „Überarbeitungen“ aktiv.
* Wenn diese nicht angewählt ist, ist kein Dokumentenschutz vorhanden.


