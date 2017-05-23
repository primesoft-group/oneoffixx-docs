---
layout: page
title: PeoplePicker / Personenauswahl
permalink: "docfunc/de/df/peoplepicker"
language: de
---

Beim Hinzufügen der Personenauswahl erscheint beim Erstellen eines Dokuments ein Dialog, bei dem eine andere Person als Profil ausgewählt werden kann:

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/peoplePickerDialog.png)

Momentan wird als Quelle einzig das AD (Active Directory) unterstützt.<br>
Die Authentifizierung erfolgt über den aktuellen Windows-Benutzer.


## Einschränkungen

Bei der Verwendung der Personenauswahl müssen folgende Punkte bedacht werden:

* Die Personenauswahl funktioniert ausserhalb des bestehenden Freigabe-Konzepts von OneOffixx-Profilen. Alle AD-Benutzer können gewählt werden, nicht nur die OneOffixx-Profile, für die man berechtigt ist.
* Es besteht keine Möglichkeit, auf die Daten von OneOffixx-Benutzern oder OneOffixx-Profilen zuzugreifen. Wenn die Vektorunterschriften z. B. in den OneOffixx-Benutzern gepflegt werden, kann mit der Personenauswahl nicht auf diese Daten zugegriffen werden.
* Es werden lediglich diejenigen Felder überschrieben, die explizit angegeben werden. Beim FieldMapping die Felder Profile.Id, Profile.User.FirstName und Signer_0.User.Sign nicht angegeben werden, so befinden sich darin die Daten des aktuellen Profils (und nicht die Daten der im Personenauswahl-Dialog gewählten Person).
* Die Möglichkeit, eine Person im Personenauswahl-Dialog auszuwählen, bietet sich nur beim Erstellen des Dokuments. Bei bestehenden Dokumenten kann die Personenauswahl nicht erneut aufgerufen werden.<br>Profilwechsel funktionieren, bewirken aber, dass die Daten, welche durch die Personenauswahl abgefüllt wurden, überschrieben werden.

Grundsätzlich wird empfohlen, die Profil-Freigaben zu verwenden. In gewissen Fällen kann die Personenauswahl jedoch durchaus Sinn machen.


## Konfiguration

Hier eine Beispiel-Konfiguration:

```xml
<Config>
  <Provider>
    <Ldap>
      <PropertiesToLoad>sn,givenName,description,department,mail</PropertiesToLoad>
    </Ldap>
  </Provider>
  <FieldMapping>
    <MapFieldNames>*</MapFieldNames>
    <Element id="departmentEdited" when="department = 'Sales'">"Verkauf"</Element>
    <Element id="departmentEdited" notwhen="department = 'Sales'">department</Element>
    <Element id="mailLowerCase" fCase="lower">mail</Element>
    <Element id="emptyImage">""</Element>
  </FieldMapping>
  <FieldsToProfileMapping>
    <Map source="sn" target="Profile.User.LastName" />
    <Map source="givenName" target="Profile.User.Firstname" />
    <Map source="description" target="Profile.User.Function" />
    <Map source="departmentEdited" target="Profile.Org.Unit" />
    <Map source="mailLowerCase" target="Profile.User.Email" />
    <Map source="emptyImage" target="Profile.User.Sign" />
    <Map source="emptyImage" target="Signer_0.User.Sign" />
  </FieldsToProfileMapping>
</Config>
```

Zwischen `<PropertiesToLoad>` und `</PropertiesToLoad>` können die AD-User-Attribute angegeben werden, welche vom AD angefordert werden sollen und welche dann im Mapping verwendet werden können.

In `<FieldMapping>` können zusätzliche Elemente erstellt werden, welche dann in `<FieldsToProfileMapping>` verwendet werden können. Dabei können bei `<Element ... />` dieselben Attribute verwendet werden wie in der [Scripts]({{ site.baseurl }}/docfunc/de/df/scripts)-Dokument-Funktion.

In `<FieldsToProfileMapping>` müssen alle Felder, welche durch AD-Daten überschrieben werden sollen, angegeben werden.

