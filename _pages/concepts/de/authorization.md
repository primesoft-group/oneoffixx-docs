---
layout: page
title: Berechtigungen
permalink: "concepts/de/authorization/"
language: de
---

Das OneOffixx Berechtigungskonzept verfolgt folgende Ziele: 

* Verringerung des administrativen Aufwandes
* Sicherstellung, dass nur benutzerrelevante Daten auf dem Rechner der User synchronisiert werden
* Einbindung der Fachabteilungen zur Pflege der Inhaltsdaten von Textbausteinen
* Einschränkung der Sichtbarkeit von Vorlagen und Textbausteinen aufgrund der Organisations- und Rollenzugehörigkeit
* Unterstützung von Active Directory und Windows Gruppen

Das Berechtigungskonzept von OneOffixx basiert auf Rollen, Benutzer, Benutzergruppen und Objekten. Rollen und damit Rechte werden den Objekten durch AD-Gruppen, AD-Benutzer, OneOffixx-Gruppen oder OneOffixx-User verknüpft.

![x]({{ site.baseurl }}/assets/content-images/concepts/de/system-authorization.png "Berechtigung")

OneOffixx-Gruppen und OneOffixx-User sind eigenständige Authorisierungsklasse. Einer OneOffixx Gruppe kann AD Gruppen bzw AD-User oder auch OneOffixx User enthalten.

{:.table .table-striped}
Berechtigung \ Rolle | Sys-Admin | Org-Admin | User-Admin | Template-Admin | Campaign-Admin | Snippet-Admin | Benutzer | 
---------|----------|---------|---------|---------|---------|---------|---------|
Organisationen verwalten | ☑ | ☑ | ☐ | ☐ | ☐ | ☐ | ☐
Logo verwalten | ☑ | ☑ | ☐ | ☐ | ☐ | ☐ | ☐
Vorlagen verwalten | ☑ | ☐ | ☐ | ☑ | ☐ | ☐ | ☐
Vorlagen ändern | ☑ | ☐ | ☐ | ☑_1_ | ☐ | ☐ | ☐
Benutzer verwalten | ☑ | ☐ | ☑ | ☐  | ☐ |☐ | ☐
Berechtigungen verwalten | ☑ | ☐ | ☐ | ☐  | ☐ |☐ | ☐
Globale Textbausteine verwalten | ☑ | ☐ | ☐ | ☐ | ☐ | ☑ | ☑_2_
Vorlagen-Textbausteine erstellen | ☑ | ☐ | ☐ | ☑ | ☐ | ☐ | ☐
Private Textbausteine verwalten | ☑ | ☑ | ☑ | ☑ | ☑ | ☑ | ☑
Felder verwalten | ☑ | ☐ | ☐ | ☑ | ☐ | ☐ | ☐
Kampagne verwalten | ☑ | ☐ | ☐ | ☐  | ☑ | ☐ | ☐
Signaturen verwalten | ☑ | ☐ | ☐ | ☑  | ☐ | ☐ | ☐

1. Sofern der Template-Admin das explizite Änderungsecht auf der Vorlage besitzt.
2. Sofern der User das explizite Änderungsrecht auf dem Textbaustein besitzt.

## Rollen in OneOffixx
Folgende Rollen sind in OneOffixx vorgesehen:

### Rolle OneOffixx-System
Höchste Berechtigung. Mit dieser können sowohl die User, AD-Gruppen und OneOffixx-Gruppen aller anderen Administrationsbereiche gesetzt werden und der Zugriff auf’s Web-Backend (bspw. mit der Statistik, Servereinstellungen, …) gewährt werden. <br />
Zudem kann der Sys-Admin alle Vorlagen bearbeitet (auch jene, auf die der Benutzer kein explizites Änderungsrecht besitzt). Auch Organisationen, Textbausteine, Benutzer und Felder können durch den Sys-Admin bearbeitet werden.
 
### Rolle OneOffixx-Organisation
Berechtigung für die Modifikation von Organisationseinheiten in OneOffixx (bspw. Logo-Wechsel, Adressänderungen, ….)
 
### Rolle OneOffixx-Useradministration
Berechtigung für die Administration aller User und Profile in OneOffixx (also auch fremder Personen). Dies ist für Personen, welche Support für eine OneOffixx-Umgebung leisten, sinnvoll.
 
### Rolle OneOffixx-Template
Berechtigung um Vorlagen zu bearbeiten und zu erstellen. <br />
Vorlagen können aber nur bearbeitet werden, wenn der User das explizite Änderungsrecht auf der Vorlage besitzt. <br />
Der Template-Admin kann zudem alle Vorlagen-Textbausteine bearbeiten und neue erstellen.

### Rolle OneOffixx-Kampagne
Berechtigung um Kampagnen zu bearbeiten, erstellen
 
### Rolle OneOffixx-Snippet
Berechtigung um gemeinsam genutzte Textbausteine zu bearbeiten, erstellen <br />
Der Snippet-Admin benötigt kein explizites Änderungsrecht auf die zu bearbeitenden Textbausteine. Er kann immer alle Textbausteine bearbeiten.

## Gruppe pro Abteilung/Amt/Organisation
Es ist empfehlenswert, eine OneOffixx-Gruppe pro Amt zu erstellen, damit die Sichtbarkeit der Vorlagen eingeschränkt werden kann, was insbesondere im Bereich der Usability (schnelles Finden der gewünschten Vorlage) hilfreich und sinnvoll ist.

## Unterschiede zwischen Textbausteinen und Vorlagen

Bei den Berechtigungskonzepten von Textbausteinen (Snippets) und Vorlagen (Templates) muss darauf geachtet werden, dass diese nicht vermischt werden.

**Möglichkeit, einen Textbaustein zu bearbeiten:**

{:.table .table-striped}
&nbsp; | mit Änderungsrecht | ohne Änderungsrecht | 
---------|----------|---------|
User | ☑ | ☐ |
Snippet-Admin | ☑ | ☑ |
Sys-Admin | ☑ | ☑ |

**Möglichkeit, eine Vorlage zu bearbeiten:**

{:.table .table-striped}
&nbsp; | mit Änderungsrecht | ohne Änderungsrecht | 
---------|----------|---------|
User | ☐ | ☐ |
Template-Admin | ☑ | ☐ |
Sys-Admin | ☑ | ☑ |
