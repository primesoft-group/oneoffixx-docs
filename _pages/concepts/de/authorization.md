---
layout: page
title: Berechtigungen
permalink: "concepts/de/authorization/"
language: de
---

Das OneOffixx Berechtigungskonzept verfolgt folgende Ziele: 

* Verringerung des administrativen Aufwandes
* Sicherstellung, dass nur benutzerrelevante Daten auf dem Computer der Benutzer synchronisiert werden
* Einbindung der Fachabteilungen zur Pflege der Textbausteine
* Einschränkung der Sichtbarkeit von Vorlagen und Textbausteinen aufgrund der Organisations- und Rollenzugehörigkeit
* Unterstützung von Active Directory und Windows Gruppen

Das Berechtigungskonzept von OneOffixx basiert auf Rollen, Benutzer, Benutzergruppen und Objekten. Rollen und damit Rechte werden den Objekten durch AD-Gruppen, AD-Benutzer, OneOffixx-Gruppen oder OneOffixx-Benutzer verknüpft.

![x]({{ site.baseurl }}/assets/content-images/concepts/de/system-authorization.png "Berechtigung")

OneOffixx-Gruppen und OneOffixx-User sind eigenständige Authorisierungsklassen. Einer OneOffixx Gruppe können AD Gruppen bzw. AD-Benutzer oder auch OneOffixx Benutzer enthalten.

{:.table .table-striped}
Berechtigung \ Rolle | Sys-Admin | Org-Admin | User-Admin | Template-Admin | Campaign-Admin | Snippet-Admin | Benutzer | 
---------|----------|---------|---------|---------|---------|---------|---------|
Organisationen verwalten | ☑ | ☑ | ☐ | ☐ | ☐ | ☐ | ☐
Logo verwalten | ☑ | ☑ | ☐ | ☐ | ☐ | ☐ | ☐
Vorlagen verwalten | ☑ | ☐ | ☐ | ☑ | ☐ | ☐ | ☐
Vorlagen ändern | ☑ | ☐ | ☐ | ☑ _1_ | ☐ | ☐ | ☐
Benutzer verwalten | ☑ | ☐ | ☑ | ☐  | ☐ |☐ | ☐
Berechtigungen verwalten | ☑ | ☐ | ☐ | ☐  | ☐ |☐ | ☐
Globale Textbausteine verwalten | ☑ | ☐ | ☐ | ☐ | ☐ | ☑ | ☑ _2_
Vorlagen-Textbausteine erstellen | ☑ | ☐ | ☐ | ☑ | ☐ | ☐ | ☐
Private Textbausteine verwalten | ☑ | ☑ | ☑ | ☑ | ☑ | ☑ | ☑
Felder verwalten | ☑ | ☐ | ☐ | ☑ | ☐ | ☐ | ☐
Kampagne verwalten | ☑ | ☐ | ☐ | ☐  | ☑ | ☐ | ☐
Signaturen verwalten | ☑ | ☐ | ☐ | ☑  | ☐ | ☐ | ☐

1. Sofern der Vorlagenadministrator das explizite Änderungsrecht auf der Vorlage besitzt.
2. Sofern der Benutzer das explizite Änderungsrecht auf dem Textbaustein besitzt.

## Rollen in OneOffixx
Folgende Rollen sind in OneOffixx vorgesehen:

### Rolle Systemadministrator
Systemadministrator sind berechtigt, alle anderen Administratoren zu definieren sowie festzulegen, wer Zugriff auf das OneOffixx Dashboard hat. Ein Systemadministrator wird folglich entweder via Dashboard oder durch einen anderen Systemadministrator definiert. Der Systemadministrator kann alle Vorlagen bearbeiten (auch jene, auf die er als Benutzer kein explizites Änderungsrecht besitzt). Auch Organisationen, Textbausteine, Benutzer und Felder können durch den Systemadministrator bearbeitet werden. 
 
### Rolle Organisationsadministrator 
Organisationsadministrator sind berechtigt, alle Organisationseinheiten zu pflegen. Zudem kann ein Benutzer mit dieser Berechtigung auch die Struktur der Organisationseinheiten anpassen.
 
### Rolle Benutzeradministrator
Benutzeradministratoren sind berechtigt, alle OneOffixx Benutzer und die entsprechenden Profile zu pflegen, d.h. neu zu erstellen, zu bearbeiten und zu löschen.
 
### Rolle Vorlagenadministrator
Vorlagenadministratoren sind berechtigt, alle Vorlagentypen (Hauptvorlagen, Untervorlagen und Format- und Stylevorlagen) zu pflegen, auf die sie ein explizites Änderungsrecht besitzen. Ist er also gleichzeitig Systemadministrator, hat er Zugriff auf alle Vorlagen. Mit dieser Berechtigung kann er alle Vorlagen-Textbausteine bearbeiten und neue erstellen.

### Rolle Kampagnenadministrator 
Kampagnenadministratoren können die Kampagnenverwaltung pflegen. Das gilt für Word-Kampagnen, sowie für Outlook-Kampagnen.
 
### Rolle Textbausteinadministrator 
Textbausteinadministratoren sind berechtigt, alle "Gemeinsam genutzten Textbausteine" sowie deren Kategorien zu pflegen, auf die sie ein explizites Änderungsrecht besitzen. 

## Gruppe pro Abteilung/Amt/Organisation
Es ist empfehlenswert, eine OneOffixx-Gruppe pro Organisationseinheit zu erstellen, damit die Sichtbarkeit der Vorlagen eingeschränkt werden kann. Das ist insbesondere hilfreich und sinnvoll, wenn schnell die gewünschte Vorlage gefunden werden muss.

## Unterschiede zwischen Textbausteinen und Vorlagen
Bei den Berechtigungskonzepten von Textbausteinen und Vorlagen muss darauf geachtet werden, dass diese nicht vermischt werden.

**Möglichkeit, einen Textbaustein zu bearbeiten:**

{:.table .table-striped}
&nbsp; | mit Änderungsrecht | ohne Änderungsrecht | 
---------|----------|---------|
Benutzer | ☑ | ☐ |
Textbausteinadministrator | ☑ | ☑ |
Systemadministrator | ☑ | ☑ |

**Möglichkeit, eine Vorlage zu bearbeiten:**

{:.table .table-striped}
&nbsp; | mit Änderungsrecht | ohne Änderungsrecht | 
---------|----------|---------|
Benutzer | ☐ | ☐ |
Vorlagenadministrator | ☑ | ☐ |
Systemadministrator | ☑ | ☑ |
