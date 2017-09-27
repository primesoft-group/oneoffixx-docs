---
layout: page
title: Berechtigungen
permalink: "concepts/de/authorization/"
language: de
---

Das OneOffixx Berechtigungskonzeptes verfolgt folgende Ziele: 

* Verringerung des administrativen Aufwandes
* Sicherstellung, dass nur benutzerrelevante Daten auf dem Rechner der User synchronisiert werden
* Einbindung der Fachabteilungen zur Pflege der Inhaltsdaten von Textbausteinen
* Einschränkung der Sichtbarkeit von Vorlagen und Textbausteinen aufgrund der Organisations und Rollenzugehörigkeit
* Unterstützung von Active Directory und Windows Gruppen

Das Berechtigungskonzept von OneOffixx basiert auf Rollen, Benutzer, Benutzergruppen und Objekten. Rollen und damit Rechte werden den Objekten durch AD-Gruppen, AD-Benutzer, OneOffixx-Gruppen oder OneOffixx-User verknüpft.

![x]({{ site.baseurl }}/assets/content-images/concepts/de/system-authorization.png "Berechtigung")

OneOffixx-Gruppen und OneOffixx-User sind eigenständige Authorisierungsklasse. Einer OneOffixx Gruppe kann AD Gruppen bzw AD-User oder auch OneOffix User enthalten.

### Rolle OneOffixx-System
Höchste Berechtigung. Mit dieser können sowohl die User, AD-Gruppen und OneOffixx-Gruppen aller anderen Administrationsbereiche gesetzt werden und der Zugriff auf’s Web-Backend (bspw. mit der Statistik, Servereinstellungen, …) gewährt werden. 
 
### OneOffixx-Organisation
Berechtigung für die Modifikation von Organisationseinheiten in OneOffixx (bspw. Logo-Wechsel, Adressänderungen, ….)
 
### OneOffixx-Useradministration
Berechtigung für die Administration aller User und Profile in OneOffixx (also auch fremder Personen). Dies ist für alle welche Support für eine OneOffixx Umgebung leisten, sinnvoll.
 
### OneOffixx-Template-Dev
Berechtigung um Vorlagen auf der Entwicklungs- / Test-Umgebung zu Bearbeiten, Erstellen, …
 
### OneOffixx-Template-Prod 
Berechtigung um Vorlagen auf der Produktiv-Umgebung zu Bearbeiten, Erstellen, …
 
### OneOffixx-Snippet-Dev 
Berechtigung um Textbausteine auf der Entwicklungs- / Test-Umgebung zu Bearbeiten, Erstellen, …
 
### OneOffixx-Snippet-Prod
Berechtigung um Textbausteine auf der Produktiv-Umgebung zu Bearbeiten, Erstellen, …
 
### Gruppe pro Abteilung/Amt/Organisation
Eine Gruppe pro Amt, damit die Sichtbarkeit der Vorlagen eingeschränkt Werden kann, was insbesondere im Bereich der Usability (schnelles finden der gewünschten Vorlage) hilfreich und sinnvoll wäre.
