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

Das Berechtigungskonzept von OneOffixx basiert auf Rollen, Benutzer, Benutzergruppen und Objekten. Rollen, und damit Rechte, werden den Objekten durch AD-Gruppen, AD-Benutzer, OneOffixx-Gruppen oder OneOffixx-User verknüpft.

![x]({{ site.baseurl }}/assets/content-images/concepts/de/system-authorization.png "Berechtigung")

OneOffixx-Gruppen und OneOffixx-User sind eigenständige Authorisierungsklassen. Einer OneOffixx Gruppe kann AD Gruppen bzw AD-User oder auch OneOffixx User enthalten.

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

1. Sofern der Templateadmin das explizite Änderungsecht auf der Vorlage besitzt.
2. Sofern auf dem Textbaustein explizit der User Änderungsrecht besitzt.

Folgende Rollen sind in OneOffixx vorgesehen:

### Rolle OneOffixx-System
Höchste Berechtigung. Der Systemadministrator kann Benutzer, AD-Gruppen und OneOffixx-Gruppen erstellen und Zugriffe auf das Dashboard erteilen. Zudem kann er alle Vorlagen bearbeiten (auch jene, auf die der Benutzer kein explizites Änderungsrecht besitzt.) sowie Organisationen, Textbausteine, Benutzer und Felder.
>>>>>>> b37d89910e81b8a34cefe120fc03692ae79d4776
 
### Rolle OneOffixx-Organisation
Berechtigung für die Modifikation von Organisationseinheiten in OneOffixx (bspw. Logo-Wechsel, Adressänderungen, ….)
 
### Rolle OneOffixx-Benutzeradministration
Berechtigung für die Administration aller User und Profile in OneOffixx (also auch fremde Personen). Das ist für alle diejenigen sinnvoll, die Support für eine OneOffixx Umgebung leisten.
 
### Rolle OneOffixx-Template
Berechtigung, um Vorlagen zu bearbeiten und zu erstellen.<br />
Vorlagen können aber nur bearbeitet werden, wenn der Benutzer das explizite Änderungsrecht auf der Vorlage bzw. Vorlagengruppe besitzt. <br />
Der Vorlagenadministrator kann zudem alle Vorlagen-Textbausteine bearbeiten und neue erstellen.

### Rolle OneOffixx-Kampagne
Berechtigung, um Kampagnen zu bearbeiten und zu erstellen
 
### Rolle OneOffixx-Snippet
Berechtigung, um gemeinsam genutzte Textbausteine zu bearbeiten und zu erstellen<br />
Der Textbausteinadministrator benötigt kein explizites Änderungsrecht auf die zu bearbeitenden Textbausteine. Er kann immer alle Textbausteine bearbeiten.

### Gruppe pro Abteilung/Amt/Organisation
Es ist empfehlenswert, eine Vorlagengruppe pro Amt zu erstellen, damit die Sichtbarkeit der Vorlagen eingeschränkt werden kann, was insbesondere im Bereich der Usability (schnelles Finden der gewünschten Vorlage) hilfreich und sinnvoll ist.
>>>>>>> b37d89910e81b8a34cefe120fc03692ae79d4776

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
